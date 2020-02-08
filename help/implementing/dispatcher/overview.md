---
title: 云中的调度程序
description: '云中的调度程序 '
translation-type: tm+mt
source-git-commit: 64475ec492863f713a7cefaedc4c0782014682ae

---


# 云中的调度程序 {#Dispatcher-in-the-cloud}

## Apache和Dispatcher配置和测试 {#apache-and-dispatcher-configuration-and-testing}

本节介绍如何将AEM构建为云服务Apache和Dispatcher配置，以及如何在部署到云环境之前在本地验证并运行它。 它还介绍在云环境中进行调试。 有关Dispatcher的其他信息，请参阅 [AEM Dispatcher文档](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html)。

>[!NOTE]
>Windows用户需要使用Windows 10 Professional或支持Docker的其他分发版本。 这是在本地计算机上运行和调试Dispatcher的先决条件。 以下各节包括使用Mac或Linux版本的SDK的命令，但Windows SDK也可以以类似方式使用。

## 调度程序工具 {#dispatcher-sdk}

调度程序工具作为云服务SDK是整个AEM的一部分，它提供：

* 包含要包含在调度程序的主项目中的配置文件的vanila文件结构；
* 客户在本地验证调度程序配置的工具；
* 在本地调度程序启动的Docker映像。

## 下载和提取工具 {#extracting-the-sdk}

Dispatcher Tools可从软件分发门户的zip文件 [下载](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) 。 请注意，对SDK列表的访问权限仅限于将AEM Managed services或AEM作为云服务环境的用户。 该新调度程序工具版本中可用的任何新配置均可用于部署到在Cloud或更高版本中运行该版本AEM的云环境。

**对于macOS和Linux**，将shell脚本下载到计算机上的文件夹，使其可执行并运行它。 它将自解压缩存储在其目录下的Dispatcher Tools文件(其中 `version` 是Dispatcher Tools的版本)。

```bash
$ chmod +x DispatcherSDKv<version>.sh
$ ./DispatcherSDKv<version>.sh
Verifying archive integrity...  100%   All good.
Uncompressing DispatcherSDKv<version>  100% 
```

**对于Windows**，请下载zip存档并解压缩它。

## 文件结构 {#file-structure}

项目的调度程序子文件夹的结构如下所述，应将其复制到主项目调度程序文件夹中：

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── default.vhost -> ../available_vhosts/default.vhost
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
└── conf.dispatcher.d
    ├── available_farms
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── default.farm -> ../available_farms/default.farm
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
        ├── default_virtualhosts.any
        └── virtualhosts.any
```

以下是可修改的显着文件说明：

**可自定义的文件**

以下文件可自定义，并将在部署时传输到您的云实例：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以拥有一个或多个这些文件。 它们包 `<VirtualHost>` 含与主机名匹配的条目，并允许Apache使用不同的规则处理每个域流量。 文件在目录中创建， `available_vhosts` 并在目录中启用符号链 `enabled_vhosts` 接。 从文件 `.vhost` 中，将包括重写和变量等其他文件。

* `conf.d/rewrites/rewrite.rules`

此文件包含在文件 `.vhost` 中。 它有一套重写规则 `mod_rewrite`。

>[!NOTE]
>
>此时，必须使用单个重写文件，而不是站点特定的文件。 该文件大小必须小于1MB。

* `conf.d/variables/custom.vars`

此文件包含在文件 `.vhost` 中。 您可以在此位置为Apache变量添加定义。

* `conf.d/variables/global.vars`

此文件包含在文件 `dispatcher_vhost.conf` 中。 您可以更改调度程序并重写此文件中的日志级别。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以拥有一个或多个这些文件，它们包含的群与主机名匹配并允许调度程序模块使用不同的规则处理每个群。 文件在目录中创建， `available_farms` 并在目录中启用符号链 `enabled_farms` 接。 文件中 `.farm` 将包括过滤器、缓存规则等其他文件。

* `conf.dispatcher.d/cache/rules.any`

此文件包含在文件 `.farm` 中。 它指定缓存首选项。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此文件包含在文件 `.farm` 中。 它指定应将哪些请求标头转发到后端。

* `conf.dispatcher.d/filters/filters.any`

此文件包含在文件 `.farm` 中。 它有一组规则，这些规则更改了应过滤掉的流量，而不是将流量发送到后端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此文件包含在文件 `.farm` 中。 它包含要由全局匹配匹配的主机名或URI路径列表。 这决定了用于提供请求的后端。

上述文件引用下面列出的不可改变的配置文件。 云环境中的调度程序不会处理对不可变文件所做的更改。

**不可变的配置文件**

这些文件是基本框架的一部分，并实施标准和最佳做法。 这些文件被视为不可变的，因为在本地修改或删除它们不会影响您的部署，因为它们不会被传输到您的云实例。

建议上述文件引用下面列出的不可改变的文件，后面跟有任何其他语句或覆盖。 将调度程序配置部署到云环境时，将使用不可改变文件的最新版本，而不管本地开发中使用的版本如何。

* `conf.d/available_vhosts/default.vhost`

包含示例虚拟主机。 对于您自己的虚拟主机，请创建此文件的副本，对其进行自定义，转到并创 `conf.d/enabled_vhosts` 建指向自定义副本的符号链接。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用于说明如何包括虚拟主机和全局变量。

* `conf.d/rewrites/default_rewrite.rules`

适用于标准项目的默认重写规则。 如果需要自定义，请修改 `rewrite.rules`。 在自定义中，如果默认规则符合您的需求，您仍可以先包含这些规则。

* `conf.dispatcher.d/available_farms/default.farm`

包含一个调度程序群示例。 对于您自己的农场，请创建此文件的副本，对其进行自定义，转到并创 `conf.d/enabled_farms` 建到自定义副本的符号链接。

* `conf.dispatcher.d/cache/default_invalidate.any`

基本框架的一部分，在启动时生成。 您必须 **在** “部分”中定义的每个农场中包含此 `cache/allowedClients` 文件。

* `conf.dispatcher.d/cache/default_rules.any`

适用于标准项目的默认缓存规则。 如果需要自定义，请修改 `conf.dispatcher.d/cache/rules.any`。 在自定义中，如果默认规则符合您的需求，您仍可以先包含这些规则。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

默认请求标头可转发到后端，适用于标准项目。 如果需要自定义，请修改 `clientheaders.any`。 在自定义中，您仍可以首先包含默认的请求标头（如果它们符合您的需求）。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用于说明如何包括调度程序群。

* `conf.dispatcher.d/filters/default_filters.any`

适用于标准项目的默认过滤器。 如果需要自定义，请修改 `filters.any`。 在自定义中，如果默认过滤器符合您的需要，您仍可以先包含这些过滤器。

* `conf.dispatcher.d/renders/default_renders.any`

作为基本框架的一部分，此文件在启动时生成。 您必须 **在** “部分”中定义的每个农场中包含此 `renders` 文件。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

适用于标准项目的默认主机回声。 如果需要自定义，请修改 `virtualhosts.any`。 在自定义中，您不应包括默认主机globbing，因为它匹配每个传入 **的请** 求。

>[!NOTE]
>AEM作为云服务主原型将生成相同的调度程序配置文件结构。

以下各节介绍如何在本地验证配置，以便在部署内部版本时在Cloud manager中传递关联的质量门。

## 调度程序配置的本地验证 {#local-validation-of-dispatcher-configuration}

验证工具在SDK中以Mac OS、Linux或 `bin/validator` Windows二进制形式提供，允许客户运行与Cloud manager在构建和部署发行版时执行的验证相同的验证。

它被调用为： `validator full [-d folder] [-w whitelist] zip-file | src folder`

该工具可验证Apache和调度程序配置。 它使用模式扫描所有文 `conf.d/enabled_vhosts/*.vhost` 件，并检查是否只使用列入白名单的指令。 通过运行validator的whitelist命令，可以列出Apache配置文件中允许的指令：

```
$ validator whitelist
Cloud manager validator 2.0.4
 
Whitelisted directives:
  <Directory>
  ...
  
```

下表显示了支持的apache模块：

| 模块名称 | 参考页 |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
| `mod_auth_basic` | [https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html](https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html) |
| `mod_authn_core` | [https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html) |
| `mod_authn_file` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_file.html) |
| `mod_authz_core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html) |
| `mod_authz_groupfile` | [https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html) |
| `mod_deflate` | [https://httpd.apache.org/docs/2.4/mod/mod_deflate.html](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html) |
| `mod_dir` | [https://httpd.apache.org/docs/2.4/mod/mod_dir.html](https://httpd.apache.org/docs/2.4/mod/mod_dir.html) |
| `mod_env` | [https://httpd.apache.org/docs/2.4/mod/mod_env.html](https://httpd.apache.org/docs/2.4/mod/mod_env.html) |
| `mod_filter` | [https://httpd.apache.org/docs/2.4/mod/mod_filter.html](https://httpd.apache.org/docs/2.4/mod/mod_filter.html) |
| `mod_headers` | [https://httpd.apache.org/docs/2.4/mod/mod_headers.html](https://httpd.apache.org/docs/2.4/mod/mod_headers.html) |
| `mod_mime` | [https://httpd.apache.org/docs/2.4/mod/mod_mime.html](https://httpd.apache.org/docs/2.4/mod/mod_mime.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |

客户无法添加任意模块，但将来可能会考虑将其他模块包含在产品中。 如Dispatcher Tools文档中所述，客户可以通过在SDK中执行“validator whitelist”来查找指定Dispatcher版本可用的指令列表。

白名单中包含客户配置中允许的Apache指令列表。 如果指令未列入白名单，则该工具将记录一个错误并返回非零的退出代码。 如果命令行上没有提供白名单（这是应调用该白名单的方式），则该工具会使用默认白名单，Cloud manager将在部署到云环境之前使用该白名单进行验证。

此外，它还使用模式扫描所有文 `conf.dispatcher.d/enabled_farms/*.farm` 件并检查：

* 不存在允许通过的过滤器规 `/glob` 则(请参 [阅CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) )
* 不公开任何管理功能。 例如，访问路径，如 `/crx/de or /system/console`。

当针对主对象或子目录运行时， `dispatcher/src` 它将报告验证失败：

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-whitelisted directives:
 conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
 conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

请注意，验证工具仅报告未列入白名单的禁止使用Apache指令。 它不会报告Apache配置的语法或语义问题，因为此信息仅适用于运行环境中的Apache模块。

未报告验证失败时，您的配置已准备好进行部署。

以下是调试工具输出的常见验证错误的疑难解答技巧：

**在存档中找`conf.dispatcher.d`不到子文件夹**

您的存档应包含文件夹 `conf.d` 和 `conf.dispatcher.d`。 请注意，您不应 **在**&#x200B;存档 `etc/httpd` 中使用前缀。

**找不到`conf.dispatcher.d/enabled_farms`**

已启用的农场应位于提及的子文件夹中。

**包含的文件(...)必须命名：...**

您的农场配置中有两个部分必须 **包含** 特定文件： `/renders` 和 `/allowedClients` 部分 `/cache` 中。 这些部分必须如下：

```
/renders {
    $include "../renders/default_renders.any"
}
```

和:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**文件包含在未知位置：...**

您的农场配置中有四个部分，允许您在其中包含您自己的文件： `/clientheaders`, `filters`在部 `/rules` 分和 `/cache``/virtualhosts`中 所包含的文件需要命名如下：

| 区域 | 包括文件名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包 **含这些文件的默认版本** ，其名称前面加有单词 `default_`，如 `../filters/default_filters.any`.

**包含位于(...)的语句，位于任何已知位置之外：...**

除了上述段落中提到的六个部分之外，您不得使用该 `$include` 语句，例如，以下内容会生成此错误：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允许的客户端／渲染器不包括自：...**

当您未在部分中为和指定包含时，会 `/renders` 生 `/allowedClients` 成此错误 `/cache` 。 **请参阅**&#x200B;包含的文件(...)必须命名：...的下界。

**过滤器不得使用全局模式允许请求**

不安全地允许具有样式规则的请 `/glob` 求，该样式规则与完整的请求行匹配，例如，

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此语句旨在允许对文件的请 `css` 求，但也允许对任何资源的请 **求** ，后跟查询字符串 `?a=.css`。 因此，禁止使用此类过滤器（另请参阅CVE-2016-0957）。

**包含的文件(...)与任何已知文件均不匹配**

Apache虚拟主机配置中有两种类型的文件可指定为包括：重写和变量。
所包含的文件需要命名如下：

| 类型 | 包括文件名 |
|-----------|---------------------------------|
| 重写 | `conf.d/rewrites/rewrite.rules` |
| 变量 | `conf.d/variables/custom.vars` |

或者，您也可以包含 **重写规则** （名称为）的默认版本 `conf.d/rewrites/default_rewrite.rules`。
请注意，变量文件没有默认版本。

**检测到已弃用的配置布局，启用兼容性模式**

此消息表示您的配置具有已弃用的版本1布局，其中包含完整的Apache配置和带前缀的 `ams_` 文件。 虽然后向兼容性仍支持此功能，但您应切换到新布局。

## 在本地测试Apache和Dispatcher配置 {#testing-apache-and-dispatcher-configuration-locally}

还可以在本地测试Apache和Dispatcher配置。 它要求本地安装Docker，并且您的配置要通过上述验证。

通过使用“`-d`”参数，验证程序输出一个文件夹，其中包含调度程序所需的所有配置文件。

然后，脚本 `docker_run.sh` 可以指向该文件夹，从您的配置开始创建容器。

```
$ validator full -d out src/dispatcher
2019/06/19 16:02:55 No issues found
$ docker_run.sh out docker.for.mac.localhost:4503 8080
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
Starting httpd server
...
```

这将在容器中启动调度程序，其后端指向在本地Mac OS计算机上运行的AEM实例（端口4503）。

## 调试Apache和Dispatcher配置 {#debugging-apache-and-dispatcher-configuration}

以下策略可用于增加调度程序模块的日志输出并查看本地和云环 `RewriteRule` 境中的评估结果。

这些模块的日志级别由变量和定 `DISP_LOG_LEVEL` 义 `REWRITE_LOG_LEVEL`。 可在文件中设置它们 `conf.d/variables/global.vars`。 其相关部分如下：

```
# Log level for the dispatcher
#
# Possible values are: Error, Warn, Info, Debug and Trace1
# Default value: Warn
#
# Define DISP_LOG_LEVEL Warn
 
# Log level for mod_rewrite
#
# Possible values are: Error, Warn, Info, Debug and Trace1 - Trace8
# Default value: Warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to Trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL Warn
```

在本地运行调度程序时，日志也直接打印到终端输出。 大多数情况下，这些日志应位于DEBUG中，这可以通过在运行Docker时作为参数传入调试级别来实现。 例如：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

云环境的日志将通过Cloud manager中提供的日志记录服务公开。

## 每个环境的不同调度程序配置 {#different-dispatcher-configurations-per-environment}

此时，同一调度程序配置将作为云服务环境应用于所有AEM。 运行时将有一个环境变量， `ENVIRONMENT_TYPE` 其中包含当前的运行模式（dev、stage或prod）以及定义。 定义可以 `ENVIRONMENT_DEV`是 `ENVIRONMENT_STAGE` 或 `ENVIRONMENT_PROD`。 在Apache配置中，变量可以直接在表达式中使用。 或者，可以使用定义构建逻辑：

```
# Simple usage of the environment variable
ServerName ${ENVIRONMENT_TYPE}.company.com
 
# When more logic is required
<IfDefine ENVIRONMENT_STAGE>
  # These statements are for stage
  Define VIRTUALHOST stage.example.com
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  # These statements are for production
  Define VIRTUALHOST prod.example.com
</IfDefine>
```

在调度程序配置中，可以使用相同的环境变量。 如果需要更多逻辑，请如上例所示定义变量，然后在调度程序配置部分中使用这些变量：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

在本地测试配置时，可以通过将变量直接传递给脚本来模拟不 `DISP_RUN_MODE` 同的 `docker_run.sh` 环境类型：

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

未传递DISP_RUN_MODE值时的默认运行模式为“dev”。
有关可用选项和变量的完整列表，请运行不带参数 `docker_run.sh` 的脚本。

## 查看Docker容器正在使用的调度程序配置 {#viewing-dispatcher-configuration-in-use-by-docker-container}

使用特定于环境的配置，可能难以确定实际的Dispatcher配置的外观。 启动您的码头容器后，可 `docker_run.sh` 以按如下方式倾弃它：

* 确定正在使用的Docker容器ID:

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* 使用该容器ID执行以下命令行：

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## AMS Dispatcher与AEM作为云服务的主要区别 {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

如上所述，AEM中作为云服务的Apache和Dispatcher配置与AMS配置非常相似。 主要区别是：

* 在AEM中，某些Apache指令不能被使用(例如 `Listen` 或 `LogLevel`)
* 在AEM中，作为云服务，只能将部分调度程序配置放入包含文件中，其命名很重要。 例如，要在不同主机之间重复使用的过滤器规则必须放入一个名为的文件中 `filters/filters.any`。 有关详细信息，请参阅参考页面。
* 在AEM云服务中，存在额外的验证以禁止使用编写的过滤器规则以防 `/glob` 止安全问题。 由于 `deny *` 将使用而不是 `allow *` （无法使用），客户将从本地运行Dispatcher以及执行试用和错误中受益，查看日志以准确了解Dispatcher过滤器为了添加这些过滤器而阻止的路径。

## 将调度程序配置从AMS迁移到AEM作为云服务的准则

调度程序配置结构在Managed services和AEM（作为云服务）之间存在差异。 下面是有关如何将AMS Dispatcher配置版本2作为云服务迁移到AEM的分步指南。

## 如何将AMS转换为AEM作为云服务调度程序配置

下节提供有关如何转换AMS配置的分步说明。 假定您有一个存档，其结构与 [Cloud Manager调度程序配置中描述的类似](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### 提取存档并删除最终的前缀

将存档解压缩到文件夹，并确保立即使用子文件夹以 `conf`、 `conf.d`和`conf.dispatcher.d` 开头 `conf.modules.d`。 如果不这样做，就在层次中上移。

### 删除未取消使用的子文件夹和文件

删除子 `conf` 文件夹 `conf.modules.d`和，以及匹配的文件 `conf.d/*.conf`。

### 删除所有非发布虚拟主机

删除名称中包 `conf.d/enabled_vhosts` 含、 `author`、 `unhealthy``health``lc` 或 `flush` 的任何虚拟主机文件。 中未链接的所 `conf.d/available_vhosts` 有虚拟主机文件也可以删除。

### 删除或注释不引用端口80的虚拟主机部分

如果您的虚拟主机文件中仍有部分专门引用端口80以外的其他端口，例如

```
<VirtualHost *:443>
...
</VirtualHost>
```

删除或添加注释。 这些部分中的语句将不会得到处理，但是，如果保留这些语句，您最终可能仍然会编辑它们，而不会产生任何效果，这令人混淆。

### 检查重写

Enter directory `conf.d/rewrites`.

删除名为和的任 `base_rewrite.rules` 何文 `xforwarded_forcessl_rewrite.rules` 件，并记住删除 `Include` 虚拟主机文件中引用它们的语句。

如果 `conf.d/rewrites` 现在包含单个文件，则应将其重命名为 `rewrite.rules` ，并且不要忘记在虚拟主机文件 `Include` 中调整引用该文件的语句。

但是，如果文件夹包含多个特定于虚拟主机的文件，则其内容应当被添加到虚拟主 `Include` 机文件中引用这些文件的语句中。

### 检查变量

Enter directory `conf.d/variables`.

删除任何名为的文 `ams_default.vars` 件，并记住删除虚拟 `Include` 主机文件中引用它们的语句。

如果 `conf.d/variables` 现在包含单个文件，则应将其重命名为 `custom.vars` ，并且不要忘记在虚拟主机文件 `Include` 中调整引用该文件的语句。

但是，如果文件夹包含多个特定于虚拟主机的文件，则其内容应当被添加到虚拟主 `Include` 机文件中引用这些文件的语句中。

### 删除白名单

删除文件夹 `conf.d/whitelists` 并删除 `Include` 虚拟主机文件中引用该子文件夹中某个文件的语句。

### 替换任何不再可用的变量

在所有虚拟主机文件中：

重命名 `PUBLISH_DOCROOT` 为删 `DOCROOT`除引用名为、或 `DISP_ID``PUBLISH_FORCE_SSL` 者 `PUBLISH_WHITELIST_ENABLED`

### 通过运行验证程序检查您的状态

使用子命令在目录中运行调度程序 `httpd` 验证程序：

```
$ validator httpd .
```

如果您看到有关缺少包含文件的错误，请检查您是否正确重命名了这些文件。

如果看到未列入白名单的Apache指令，请删除它们。

### 删除所有非发布农场

删除名称中 `conf.dispatcher.d/enabled_farms` 包含、 `author`、 `unhealthy``health``lc` 或 `flush` 的任何农场文件。 也可以删除 `conf.dispatcher.d/available_farms` 所有未链接的农场文件。

### 重命名农场文件

必须重命名 `conf.d/enabled_farms` 中的所有农场以匹配该模 `*.farm`式，因此应重命名名为afarm `customerX_farm.any` 的文件 `customerX.farm`。

### 检查缓存

Enter directory `conf.dispatcher.d/cache`.

删除任何前缀的文件 `ams_`。

如果 `conf.dispatcher.d/cache` 现在为空，请将文件从标 `conf.dispatcher.d/cache/rules.any`准调度程序配置复制到此文件夹。 此SDK的文件夹中可找到标准调度 `src` 程序配置。 不要忘记也要调整引用`$include` 农场文件中 `ams_*_cache.any` 的规则文件的语句。

如果现 `conf.dispatcher.d/cache` 在包含带后缀的单个文件，则应将其重命名为 `_cache.any`，并且不要忘记在农场文件中改编 `rules.any``$include` 引用该文件的语句。

但是，如果文件夹包含多个具有该模式的特定农场文件，则应将其内容复制到引用该群 `$include` 体文件中这些文件的语句中。

删除任何具有后缀的文件 `_invalidate_allowed.any`。

将Cloud调度程 `conf.dispatcher.d/cache/default_invalidate_any` 序配置中的默认AEM文件复制到该位置。

在每个农场文件中，删除该部分中的所 `cache/allowedClients` 有内容，并将其替换为：

```
$include "../cache/default_invalidate.any"
```

### 检查客户端标题

Enter directory `conf.dispatcher.d/clientheaders`.

删除任何前缀的文件 `ams_`。

如果 `conf.dispatcher.d/clientheaders` 现在包含带后缀的单个文件 `_clientheaders.any`，则应将其重命名为 `clientheaders.any` ，并且不要忘记在农场文件中改编 `$include` 引用该文件的语句。

但是，如果文件夹包含多个具有该模式的特定农场文件，则应将其内容复制到引用该群 `$include` 体文件中这些文件的语句中。

将文件从默 `conf.dispatcher/clientheaders/default_clientheaders.any` 认AEM复制为Cloud service调度程序配置，复制到该位置。

在每个农场文件中，替换任何clientheader包含如下所示的语句：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

和语句：

```
$include "../clientheaders/default_clientheaders.any"
```

### 检查过滤器

Enter directory `conf.dispatcher.d/filters`.

删除任何前缀的文件 `ams_`。

如果 `conf.dispatcher.d/filters` 现在包含单个文件，则应将其重命名为`filters.any` ，并且不要忘记在农场文件 `$include` 中改编引用该文件的语句。

但是，如果文件夹包含多个具有该模式的特定农场文件，则应将其内容复制到引用该群 `$include` 体文件中这些文件的语句中。

将文件从默 `conf.dispatcher/filters/default_filters.any` 认AEM复制为Cloud service调度程序配置，复制到该位置。

在每个农场文件中，替换任何过滤器包含如下所示的语句：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

和语句：

```
$include "../filters/default_filters.any"
```

### 检查渲染

Enter directory `conf.dispatcher.d/renders`.

删除该文件夹中的所有文件。

将文件从默 `conf.dispatcher.d/renders/default_renders.any` 认AEM复制为Cloud service调度程序配置，复制到该位置。

在每个农场文件中，删除该部分中的所 `renders` 有内容并将其替换为：

```
$include "../renders/default_renders.any"
```

### 检查虚拟主机

将目录重命 `conf.dispatcher.d/vhosts` 名为 `conf.dispatcher.d/virtualhosts` 并输入它。

删除任何前缀的文件 `ams_`。

如果 `conf.dispatcher.d/virtualhosts` 现在包含单个文件，则应将其重命名为`virtualhosts.any` ，并且不要忘记在农场文件 `$include` 中改编引用该文件的语句。

但是，如果文件夹包含多个具有该模式的特定农场文件，则应将其内容复制到引用该群 `$include` 体文件中这些文件的语句中。

将文件从默 `conf.dispatcher/virtualhosts/default_virtualhosts.any` 认AEM复制为Cloud service调度程序配置，复制到该位置。

在每个农场文件中，替换任何过滤器包含如下所示的语句：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

和语句：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 通过运行验证程序检查您的状态

使用子命令将AEM作为Cloud Service Dispatcher validator运行在您的目录 `dispatcher` 中：

```
$ validator dispatcher .
```

如果您看到有关缺少包含文件的错误，请检查您是否正确重命名了这些文件。

如果您看到与未定义变量相关的 `PUBLISH_DOCROOT`错误，请将其重命名为 `DOCROOT`。

有关所有其他错误，请参阅验证程序工具文档的“疑难解答”部分。

### 使用本地部署测试配置（需要安装Docker）

使用AEM中 `docker_run.sh` 的脚本作为云服务调度程序工具，您可以测试您的配置是否不包含任何只会显示部署的其他错误：

### 第1步：使用验证程序生成部署信息

```
validator full -d out .
```

这将验证完整配置并在 `out`

### 第2步：使用该部署信息在文档处理器映像中启动调度程序

在macOS计算机上运行AEM发布服务器，监听端口4503时，您可以在该服务器前运行调度程序，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

这将启动容器并公开本地端口8080上的Apache。

### 使用新的调度程序配置

恭喜！ 如果验证程序不再报告任何问题，并且docker容器启动时没有出现任何故障或警告，您就可以将配置移到git存储库的 `dispatcher/src` 子目录。

**使用AMS Dispatcher配置版本1的客户应联系客户支持以帮助他们从版本1迁移到版本2，以便遵循上述说明。**

## Dispatcher和CDN {#dispatcher-cdn}

数据流如下：

1. 放入浏览器的URL
2. 向DNS中映射到该域的CDN发出请求
3. 如果内容已在CDN上完全缓存，则CDN会将其提供给浏览器
4. 如果内容未完全缓存，CDN将向调度程序发出（反向代理）
5. 如果内容已完全缓存在调度程序上，则调度程序会将其提供给CDN
6. 如果内容未完全缓存，调度程序将调用（反向代理）到AEM发布
7. 浏览器呈现的内容

### CDN {#cdn}

AEM提供两个选项：

1. 受管CDN - AEM现成的CDN。
2. 非托管CDN —— 客户自带CDN并完全负责管理它。

强烈建议使用第一个选项，Adobe不对使用第二个选项时任何配置错误的结果负责。

#### 受管CDN {#managed-cdn}

在Adobe配置CDN后，您应创建CNAME，将应用程序的域映射到托管的CDN域上托管的Adobe控制域。

CDN充当第7层Web应用程序防火墙，它需要SSL终止，因此它需要经过客户签名的SSL证书。 在预发布阶段，您必须通过手动流程向Adobe提供证书。

在GA时，您应将证书上传到Cloud Manager，然后Cloud Manager再将其上传到CDN。 当SSL证书即将过期时，您将收到通知，以便在Cloud manager中刷新证书。

#### 非托管CDN {#unmanaged-cdn}

您可以管理您自己的CDN，前提是：

1. 您已有CDN。
2. 你会管的。
3. 您的应用程序不会向CDN发出AEM架构中尚未包含的大量API调用。
4. AEM作为云服务能够确保端到端系统正常工作。
5. 您需要向Adobe提供要允许的CDN URL白名单。

Adobe将提供一个AEM cloudURL，用作您的CDN源。


#### CDN缓存失效 {#CDN-cache-invalidation}

缓存失效遵循以下规则：

* 通常，HTML内容会根据调度程序发出的缓存控制头在CDN中缓存5分钟。
* 对于不尊重不可变值的旧版浏览器，使用设置为不可变或30天的缓存控件可无限期地缓存客户端库（JavaScript和CSS）。 请注意，客户端库以唯一路径提供，如果客户端库发生更改，则该路径会发生更改。 换句话说，将根据需要生成引用客户端库的HTML，以便在发布新内容时体验新内容。
* 默认情况下，不缓存图像。

## 显式调度程序缓存失效 {#explicit-invalidation}

在将AEM作为云服务之前，有两种方法可以使调度程序缓存失效。

1. 调用复制API，指定发布调度程序刷新代理
2. 直接调用 `invalidate.cache` API(例如，POST /dispatcher/invalidate.cache)

此方 `invalidate.cache` 法将不再受支持，因为它只针对特定的调度程序节点。
AEM作为云服务，在服务级别运行，而不是在单个节点级别运行，因此 [](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) Dispatcher帮助文档中的失效说明不再准确。
而应使用复制API方法。 [API文档可用](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) ，有关刷新缓存的示例，请参阅 [API示例页](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) ，特别是向所有可用代理发出ACTIVATE类型的复制操作的CustomStep示例。

下图说明了这一点。

<!-- [CDN](assets/cdn.png "CDN") -->

<!-- See [Apache and Dispatcher Configuration and Testing](../developing/introduction/developer-experience.md#apache-and-dispatcher-configuration-and-testing) for instructions on how a developer can configure apache and the dispatcher module. -->

### 激活／取消激活期间调度程序缓存失效 {#cache-activation-deactivation}

此发布触发的失效与快速启动相同：当发布实例从作者处（通过复制和管道队列）收到页面或资产的新版本时，它使用刷新代理使其调度程序上的相应路径无效。 更新的路径将从调度程序缓存及其父缓存中删除，最高可以使用statfilelevel配置 [的级别](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)。

### 内容新鲜度和版本一致性 {#content-consistency}

* 页面由HTML、Javascript、CSS和图像组成。
* 我们鼓励您利用clientlibs框架将Javascript和CSS资源导入HTML页面，同时考虑到JS库之间的依赖关系。
* 提供了自动版本管理，这意味着开发人员可以在源代码控制中登记对JS库的更改，并在推送版本时提供最新版本。 如果没有此选项，开发人员需要手动更改对新版本库的引用的HTML，如果许多HTML模板共享同一库，这尤其繁琐。
* 将新版本的库发布到生产版本后，引用的HTML页面会更新，其中包含指向这些更新的库版本的新链接。 在给定HTML页面的浏览器缓存过期后，不会担心旧库会从浏览器缓存中加载，因为刷新的页面（从AEM）现在可保证引用新版本的库。 换句话说，刷新的HTML页面将包括所有最新的库版本。
