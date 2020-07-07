---
title: 云中的调度程序
description: '云中的调度程序 '
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '3914'
ht-degree: 9%

---


# 云中的调度程序 {#Dispatcher-in-the-cloud}

## Apache and Dispatcher configuration and testing {#apache-and-dispatcher-configuration-and-testing}

本节介绍如何将AEM构建为Cloud ServiceApache和Dispatcher配置，以及如何在部署到云环境之前在本地验证和运行它。 还描述了在云环境中进行调试。 有关Dispatcher的其他信息，请参阅 [AEMDispatcher文档](https://docs.adobe.com/content/help/zh-Hans/experience-manager-dispatcher/using/dispatcher.html)。

>[!NOTE]
>
>Windows用户需要使用Windows 10 Professional或支持Docker的其他分发版。 这是在本地计算机上运行和调试Dispatcher的先决条件。 以下各节包括使用Mac或Linux版本的SDK的命令，但Windows SDK也可以采用类似的方式使用。

>[!WARNING]
>
>Windows用户： 当前版本的AEM作为Cloud Service本地Dispatcher工具(v2.0.20)与Windows不兼容。 请联系 [Adobe支持](https://daycare.day.com/home.html) ，获取Windows兼容性更新。

## Dispatcher工具 {#dispatcher-sdk}

Dispatcher工具作为Cloud ServiceSDK是整个AEM的一部分，它提供：

* 一种香草文件结构，包含要包含在调度程序的主项目中的配置文件；
* 客户在本地验证调度程序配置的工具；
* 在本地调度程序启动的Docker映像。

## 下载和提取工具 {#extracting-the-sdk}

Dispatcher工具可从软件分发门户的zip文 [件下载](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) 。 请注意，对SDK列表的访问权限仅限于将AEM Managed Services或AEM作为Cloud Service环境的用户。 该新调度程序工具版本中提供的任何新配置均可用于部署到云环境，在云或更高版本中运行该版本的AEM。

**对于macOS和Linux**，请将shell脚本下载到计算机上的文件夹，使其可执行并运行它。 它将自解压存储到的目录下的Dispatcher工具文件(其中 `version` 是调度程序工具的版本)。

```bash
$ chmod +x DispatcherSDKv<version>.sh
$ ./DispatcherSDKv<version>.sh
Verifying archive integrity...  100%   All good.
Uncompressing DispatcherSDKv<version>  100% 
```

**对于Windows**，请下载zip存档并解压。

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

以下是可修改的值得注意的文件的说明：

**可自定义的文件**

以下文件可自定义，并将在部署时传输到您的云实例：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以拥有一个或多个这些文件。 它们包 `<VirtualHost>` 含与主机名匹配的条目，并允许Apache使用不同的规则处理每个域通信。 文件在目录中创 `available_vhosts` 建，并在目录中启用符号链 `enabled_vhosts` 接。 从文件 `.vhost` 中，将包括重写和变量等其他文件。

* `conf.d/rewrites/rewrite.rules`

此文件包含在您的文 `.vhost` 件中。 它有一套重写规则 `mod_rewrite`。

>[!NOTE]
>
>此时，必须使用单个重写文件，而不是站点特定的文件。 该文件大小必须小于1MB。

* `conf.d/variables/custom.vars`

此文件包含在您的文 `.vhost` 件中。 您可以在此位置放入Apache变量的定义。

* `conf.d/variables/global.vars`

此文件包含在文件 `dispatcher_vhost.conf` 中。 您可以更改此文件中的调度程序和重写日志级别。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以有一个或多个这些文件，它们包含与主机名匹配的场，并允许调度程序模块使用不同的规则处理每个场。 文件在目录中创 `available_farms` 建，并在目录中启用符号链 `enabled_farms` 接。 从文件 `.farm` 中，将包括过滤器、缓存规则等其他文件。

* `conf.dispatcher.d/cache/rules.any`

此文件包含在您的文 `.farm` 件中。 它指定缓存首选项。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此文件包含在您的文 `.farm` 件中。 它指定应将哪些请求标头转发到后端。

* `conf.dispatcher.d/filters/filters.any`

此文件包含在您的文 `.farm` 件中。 它有一组规则，这些规则会更改应过滤掉的流量，而不会将流量发送到后端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此文件包含在您的文 `.farm` 件中。 它具有列表主机名或URI路径，要通过全局匹配进行匹配。 这决定了使用什么后端来服务请求。

上述文件引用下面列出的不可改变的配置文件。 云环境中的调度程序将不会处理对不可变文件所做的更改。

**不可变的配置文件**

这些文件是基本框架的一部分，并实施标准和最佳实践。 这些文件被视为不可变，因为在本地修改或删除它们不会影响您的部署，因为它们不会被传输到您的云实例。

建议上述文件引用下面列出的不可改变文件，后跟任何附加语句或覆盖。 将调度程序配置部署到云环境时，将使用不可变文件的最新版本，而不管本地开发中使用的版本如何。

* `conf.d/available_vhosts/default.vhost`

包含示例虚拟主机。 对于您自己的虚拟主机，请创建此文件的副本，对其进行自定义，转 `conf.d/enabled_vhosts` 到并创建指向自定义副本的符号链接。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用于说明如何包含虚拟主机和全局变量。

* `conf.d/rewrites/default_rewrite.rules`

适用于标准项目的默认重写规则。 如果需要自定义，请修改 `rewrite.rules`。 在自定义中，如果默认规则符合您的需求，您仍可以先包含这些规则。

* `conf.dispatcher.d/available_farms/default.farm`

包含一个调度程序群示例。 对于您自己的场，请创建此文件的副本，对其进行自定义，转 `conf.d/enabled_farms` 到并创建到自定义副本的符号链接。

* `conf.dispatcher.d/cache/default_invalidate.any`

作为基本框架的一部分，在启动时生成。 您必 **须在** “ ”部分中定义的每个场中包含此 `cache/allowedClients` 文件。

* `conf.dispatcher.d/cache/default_rules.any`

适用于标准项目的默认缓存规则。 如果需要自定义，请修改 `conf.dispatcher.d/cache/rules.any`。 在自定义中，如果默认规则符合您的需求，您仍可以先包含这些规则。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

默认请求标头可转发到后端，适用于标准项目。 如果需要自定义，请修改 `clientheaders.any`。 在自定义中，您仍可以首先包含默认请求标头（如果它们符合您的需求）。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用于说明如何包含调度程序群。

* `conf.dispatcher.d/filters/default_filters.any`

适用于标准项目的默认过滤器。 如果需要自定义，请修改 `filters.any`。 在自定义中，您仍可以先包含默认过滤器（如果它们符合您的需求）。

* `conf.dispatcher.d/renders/default_renders.any`

作为基本框架的一部分，此文件在启动时生成。 您必 **须在** “ ”部分中定义的每个场中包含此 `renders` 文件。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

适用于标准项目的默认主机全局匹配。 如果需要自定义，请修改 `virtualhosts.any`。 在自定义中，您不应包括默认主机全局覆盖，因为它匹配每 **个传** 入请求。

>[!NOTE]
>AEM作为Cloud Service主原型将生成相同的调度程序配置文件结构。

以下各节介绍如何在本地验证配置，以便在部署内部版本时在Cloud Manager中通过相关的质量门。

## Dispatcher配置的本地验证 {#local-validation-of-dispatcher-configuration}

验证工具在SDK中以Mac OS、 `bin/validator` Linux或Windows二进制形式提供，允许客户运行与Cloud Manager在构建和部署版本时将执行的验证相同的验证。

它被调用为： `validator full [-d folder] [-w whitelist] zip-file | src folder`

该工具可验证Apache和调度程序配置。 它使用模式扫描所 `conf.d/enabled_vhosts/*.vhost` 有文件并检查是否只使用已列入允许列表的指令。 通过运行validator的命令，可以列出Apache配置文件中允许的指允许列表令：

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

客户无法添加任意模块，但将来可能会考虑将其他模块包含在产品中。 如上所述，客户可以通过在SDK中执行validator的列表命令来找允许列表到指令的，该指令可用于给定Dispatcher版本。

该允许列表程序包含列表客户配置中允许的Apache指令。 如果指令未已列入允许列表，该工具将记录错误并返回非零退出代码。 如果允许列表命令行上未提供任何(即应调用该环境的方式)，则该工具将使用Cloud Manager在部署到Cloud之前将用于验证的默认。

此外，它还使用模式扫描所有文 `conf.dispatcher.d/enabled_farms/*.farm` 件并检查：

* 不存在使用允许的筛选 `/glob` 规则( [有关详细信息，请参阅](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) CVE-2016-0957)
* 不公开管理功能。 例如，对路径的访问 `/crx/de or /system/console`。

当针对主对象或子目录运 `dispatcher/src` 行时，将报告验证失败：

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-whitelisted directives:
 conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
 conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

请注意，验证工具仅报告未已列入允许列表的禁止使用Apache指令。 它不会报告Apache配置的语法或语义问题，因为此信息仅对正在运行的环境中的Apache模块可用。

未报告验证失败时，您的配置已准备好进行部署。

以下是调试工具输出的常见验证错误的疑难解答技术：

**在存档中找`conf.dispatcher.d`不到子文件夹**

您的存档应包含文件夹 `conf.d` 和 `conf.dispatcher.d`。 请注意，您不应 **在**&#x200B;存档 `etc/httpd` 中使用前缀。

**在`conf.dispatcher.d/enabled_farms`**

启用的场应位于所述子文件夹中。

**包含的文件(...)必须命名： ...**

您的场配置中有两个部分必须 **包含** 特定文件： `/renders` 和 `/allowedClients` 部分 `/cache` 中。 这些部分必须如下：

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

**文件包含在未知位置： ...**

您的场配置中有四个部分，允许您包含您自己的文件： `/clientheaders`、 `filters`, `/rules` 章节 `/cache` 和 `/virtualhosts`。 所包含的文件需要命名如下：

| 区域 | 包含文件名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包 **含这些文件的默认版本** ，其名称前面加有单词 `default_`，如 `../filters/default_filters.any`.

**包含位于(...)的语句，位于任何已知位置之外： ...**

除了上述段落中提到的六个部分之外，您不允许使 `$include` 用该语句，例如，以下内容会生成此错误：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允许的客户端／渲染不包括自： ...**

当您未在部分中为和指定包含时， `/renders` 会 `/allowedClients` 生成此 `/cache` 错误。 请参阅&#x200B;**包含的文件(...)必须命名： ...部分** ，以了解更多信息。

**过滤器不能使用glob模式允许请求**

允许使用样式规则的请求是不安 `/glob` 全的，该规则与完整的请求行匹配，例如，

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此语句用于允许对文件 `css` 进行请求，但也允许对任何资 **源** (后跟查询字符串)发出请求 `?a=.css`。 因此，禁止使用此类过滤器（另请参阅CVE-2016-0957）。

**包含的文件(...)与任何已知文件不匹配**

Apache虚拟主机配置中有两种类型的文件可指定为包括： 重写和变量。
所包含的文件需要命名如下：

| 类型 | 包含文件名 |
|-----------|---------------------------------|
| 重写 | `conf.d/rewrites/rewrite.rules` |
| 变量 | `conf.d/variables/custom.vars` |

或者，您也可以包 **含** rewrite规则的默认版本，其名称为 `conf.d/rewrites/default_rewrite.rules`。
请注意，不存在变量文件的默认版本。

**检测到已弃用的配置布局，启用兼容性模式**

此消息表示您的配置具有已弃用的版本1布局，包含完整的Apache配置和带有前缀的 `ams_` 文件。 虽然后向兼容性仍支持此功能，但您应切换到新布局。

## 在本地测试Apache和Dispatcher配置 {#testing-apache-and-dispatcher-configuration-locally}

还可以在本地测试Apache和Dispatcher配置。 它需要在本地安装Docker，并且您的配置要通过验证，如上所述。

通过使用“`-d`”参数，验证程序输出一个文件夹，其中包含调度程序所需的所有配置文件。

然后，脚本 `docker_run.sh` 可以指向该文件夹，从您的配置开始容器。

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

这将在容器中开始调度程序，其后端指向在本地Mac OS计算机上运行的AEM实例（端口4503）。

## 调试Apache和Dispatcher配置 {#debugging-apache-and-dispatcher-configuration}

以下策略可用于增加调度程序模块的日志输出并查看本地和云环境 `RewriteRule` 中评估结果。

这些模块的日志级别由变量和 `DISP_LOG_LEVEL` 定义 `REWRITE_LOG_LEVEL`。 可在文件中设置它们 `conf.d/variables/global.vars`。 其相关部分如下：

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

在本地运行Dispatcher时，日志也直接打印到终端输出。 大多数时间，这些日志应位于DEBUG中，这可以通过在运行Docker时以参数的形式传递到调试级别来完成。 例如：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

云环境的日志将通过云管理器中提供的日志记录服务公开。

## 每个Dispatcher的不同环境配置 {#different-dispatcher-configurations-per-environment}

此时，同一调度程序配置将作为Cloud Service环境应用于所有AEM。 运行时将具有一个环境 `ENVIRONMENT_TYPE` 变量，该变量包含当前运行模式（开发、舞台或生产）以及定义。 定义可以 `ENVIRONMENT_DEV`是 `ENVIRONMENT_STAGE` 或 `ENVIRONMENT_PROD`。 在Apache配置中，变量可以直接在表达式中使用。 或者，可以使用定义来构建逻辑：

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

在Dispatcher配置中，可以使用相同的环境变量。 如果需要更多逻辑，请如上例所示定义变量，然后在Dispatcher配置部分使用它们：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

在本地测试配置时，可以通过将变量直接传递到脚本来模拟 `DISP_RUN_MODE` 不同的 `docker_run.sh` 环境类型：

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

不传递DISP_RUN_MODE值时的默认运行模式为“dev”。
要获得可用选项和变量的完整列表，请运行不带参 `docker_run.sh` 数的脚本。

## 查看DockerDispatcher容器正在使用的配置 {#viewing-dispatcher-configuration-in-use-by-docker-container}

对于环境特定配置，可能很难确定实际Dispatcher配置的外观。 在启动您的码头容器之后， `docker_run.sh` 可以按如下方式丢弃它：

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

## AMSDispatcher与AEM作为Cloud Service的主要区别 {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

如以上参考页所述，AEM中作为Dispatcher的Apache和Cloud Service配置与AMS配置非常相似。 主要区别是：

* 在AEM中，某些Apache指令不能被使用(例如 `Listen` 或 `LogLevel`)
* 在AEM中，作为Cloud Service，只能将部分Dispatcher配置放入包含文件中，其命名很重要。 例如，要在不同主机之间重复使用的筛选器规则必须放入一个名为的文件中 `filters/filters.any`。 有关详细信息，请参阅参考页面。
* 在AEM中，作为Cloud Service，存在额外的验证以禁止使用编写的筛选器规则 `/glob` 来防止安全问题。 由于 `deny *` 将使用Dispatcher，而 `allow *` 非（不能使用）Dispatcher，因此客户将从本地运行以及执行试用和错误中受益，查看日志以准确了解过滤器为了添加这些路径而阻止的路径。

## 将调度程序配置从AMS迁移到AEM作为Cloud Service的准则

作为Cloud Service，调度程序配置结构在Managed Services和AEM之间有差异。 下面是一个分步指南，介绍如何将AMSDispatcher配置版本2作为Cloud Service迁移到AEM。

## 如何将AMS转换为AEM作为云服务调度程序配置

下节提供有关如何转换AMS配置的分步说明。 It assumes
that you have an archive with a structure similar to the one described in [Cloud Manager dispatcher configuration](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### 提取存档并删除最后的前缀

将存档解压到文件夹中，并确保包含、和的直接子文 `conf`件夹 `conf.d`开始`conf.dispatcher.d``conf.modules.d`。 如果他们不这样做，就在层级中向上移动。

### 删除未使用的子文件夹和文件

Remove subfolders `conf` and `conf.modules.d`, as well as files matching `conf.d/*.conf`.

### 删除所有未发布的虚拟主机

删除名称中 `conf.d/enabled_vhosts` 、 `author`、或 `unhealthy`名 `health`称中`lc` 的任何虚 `flush` 拟主机文件。 All virtual host files in `conf.d/available_vhosts` that are not
linked to can be removed as well.

### 移除或注释未引用端口 80 的虚拟主机部分

如果您的虚拟主机文件中仍然有部分内容专门引用端口 80 以外的其他端口，例如

```
<VirtualHost *:443>
...
</VirtualHost>
```

，
则请移除或注释该部分。这些部分中的语句将不会得到处理，但是如果保留它们，您可能最终仍会对其进行编辑，并且不会有任何效果，这可能会造成混淆。

### 检查 rewrites

Enter directory `conf.d/rewrites`.

Remove any file named `base_rewrite.rules` and `xforwarded_forcessl_rewrite.rules` and remember to
remove `Include` statements in the virtual host files referring to them.

If `conf.d/rewrites` now contains a single file, it should be renamed to `rewrite.rules` and don&#39;t
forget to adapt the `Include` statements referring to that file in the virtual host files as well.

If the folder however contains multiple, virtual host specific files, their contents should be
copied to the `Include` statement referring to them in the virtual host files.

### 检查 variables

Enter directory `conf.d/variables`.

Remove any file named `ams_default.vars` and remember to remove `Include` statements in the virtual
host files referring to them.

If `conf.d/variables` now contains a single file, it should be renamed to `custom.vars` and don&#39;t
forget to adapt the `Include` statements referring to that file in the virtual host files as well.

If the folder however contains multiple, virtual host specific files, their contents should be
copied to the `Include` statement referring to them in the virtual host files.

### 删除允许列表

Remove the folder `conf.d/whitelists` and remove `Include` statements in the virtual host files referring to
some file in that subfolder.

### 替换任何不再可用的变量

在所有虚拟主机文件中：

重命 `PUBLISH_DOCROOT` 名为 `DOCROOT`删除引用名为或名为的变量 `DISP_ID`的节 `PUBLISH_FORCE_SSL` 。 `PUBLISH_WHITELIST_ENABLED`

### 通过运行验证器检查状态

Run the dispatcher validator in your directory, with the `httpd` subcommand:

```
$ validator httpd .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到未已列入允许列表的Apache指令，请删除它们。

### 删除所有未发布的场

Remove any farm file in `conf.dispatcher.d/enabled_farms` that has `author`, `unhealthy`, `health`,
`lc` or `flush` in its name. All farm files in `conf.dispatcher.d/available_farms` that are not
linked to can be removed as well.

### 重命名场文件

All farms in `conf.d/enabled_farms` must be renamed to match the pattern `*.farm`, so e.g. a
farm file called `customerX_farm.any` should be renamed `customerX.farm`.

### 检查 cache

Enter directory `conf.dispatcher.d/cache`.

移除所有前缀为 `ams_` 的文件。

If `conf.dispatcher.d/cache` is now empty, copy the file `conf.dispatcher.d/cache/rules.any`
from the standard dispatcher configuration to this folder. The standard dispatcher
configuration can be found in the folder `src` of this SDK. Don&#39;t forget to adapt the
`$include` statements referring to the `ams_*_cache.any` rule files  in the farm files
as well.

If instead `conf.dispatcher.d/cache` now contains a single file with suffix `_cache.any`,
it should be renamed to `rules.any` and don&#39;t forget to adapt the `$include` statements
referring to that file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Remove any file that has the suffix `_invalidate_allowed.any`.

将文件从 `conf.dispatcher.d/cache/default_invalidate_any` 云调度程序配置中的默认AEM复制到该位置。

In each farm file, remove any contents in the `cache/allowedClients` section and replace it
with:

```
$include "../cache/default_invalidate.any"
```

### 检查 client headers

Enter directory `conf.dispatcher.d/clientheaders`.

移除所有前缀为 `ams_` 的文件。

If `conf.dispatcher.d/clientheaders` now contains a single file with suffix `_clientheaders.any`,
it should be renamed to `clientheaders.any` and don&#39;t forget to adapt the `$include` statements
referring to that file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

将文件从 `conf.dispatcher/clientheaders/default_clientheaders.any` 默认AEM复制为Cloud Service调度程序配置到该位置。

在每个场文件中，将如下所示的所有 clientheader include 语句：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

替换为语句：

```
$include "../clientheaders/default_clientheaders.any"
```

### 检查 filter

Enter directory `conf.dispatcher.d/filters`.

移除所有前缀为 `ams_` 的文件。

If `conf.dispatcher.d/filters` now contains a single file it should be renamed to
`filters.any` and don&#39;t forget to adapt the `$include` statements referring to that
file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

将文件从 `conf.dispatcher/filters/default_filters.any` 默认AEM复制为Cloud Service调度程序配置到该位置。

在每个场文件中，将如下所示的所有 filter include 语句：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

替换为语句：

```
$include "../filters/default_filters.any"
```

### 检查 renders

Enter directory `conf.dispatcher.d/renders`.

移除该文件夹中的所有文件。

将文件从 `conf.dispatcher.d/renders/default_renders.any` 默认AEM复制为Cloud Service调度程序配置到该位置。

In each farm file, remove any contents in the `renders` section and replace it
with:

```
$include "../renders/default_renders.any"
```

### 检查 virtualhosts

Rename the directory `conf.dispatcher.d/vhosts` to `conf.dispatcher.d/virtualhosts` and enter it.

移除所有前缀为 `ams_` 的文件。

If `conf.dispatcher.d/virtualhosts` now contains a single file it should be renamed to
`virtualhosts.any` and don&#39;t forget to adapt the `$include` statements referring to that
file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

将文件从 `conf.dispatcher/virtualhosts/default_virtualhosts.any` 默认AEM复制为Cloud Service调度程序配置到该位置。

在每个场文件中，将如下所示的所有 filter include 语句：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

替换为语句：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 通过运行验证器检查状态

使用子命令将AEM作为Cloud Service调度程序validator运行在您的目 `dispatcher` 录中：

```
$ validator dispatcher .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到有关未定义变量 `PUBLISH_DOCROOT` 的错误，请将该变量重命名为 `DOCROOT`。

有关其他每个错误，请参阅验证器工具文档的“疑难解答”部分。

### 使用本地部署测试配置（需要安装Docker）

Using the script `docker_run.sh` in the AEM as a Cloud Service Dispatcher Tools, you can test that
your configuration does not contain any other error that would only show up in
deployment:

### 第1步： 使用验证程序生成部署信息

```
validator full -d out .
```


这将验证完整配置并在 中生成部署信息`out`

### 第2步： 将调度程序与该部署信息开始到docker映像中

在 macOS 计算机上运行 AEM 发布服务器，并监听端口 4503 时，您可以在该服务器前面运行启动 Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

这将启动容器并在本地端口 8080 上公开 Apache。

### 使用新的调度程序配置

恭喜！ If the validator no longer reports any issue and the
docker container starts up without any failures or warnings, you&#39;re
ready to move your configuration to a `dispatcher/src` subdirectory
of your git repository.

**使用AMSDispatcher配置版本1的客户应联系客户支持，帮助他们从版本1迁移到版本2，以便遵循上述说明。**
