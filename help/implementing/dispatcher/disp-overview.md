---
title: 云中的调度程序
description: '云中的调度程序 '
translation-type: tm+mt
source-git-commit: aae587109d1f8764ac535b316a2a7d05fd7179fe
workflow-type: tm+mt
source-wordcount: '4059'
ht-degree: 9%

---


# 云中的调度程序 {#Dispatcher-in-the-cloud}

## Apache和Dispatcher配置和测试{#apache-and-dispatcher-configuration-and-testing}

本节介绍如何将AEM构造为Cloud ServiceApache和Dispatcher配置，以及如何在部署到云环境之前在本地验证和运行它。 还描述了在云环境中进行调试。 有关Dispatcher的其他信息，请参阅[AEM Dispatcher文档](https://docs.adobe.com/content/help/zh-Hans/experience-manager-dispatcher/using/dispatcher.html)。

>[!NOTE]
>
>Windows用户需要使用Windows 10 Professional或支持Docker的其他分发版。 这是在本地计算机上运行和调试Dispatcher的先决条件。 以下各节包括使用Mac或Linux版本的SDK的命令，但Windows SDK也可以采用类似的方式使用。

>[!WARNING]
>
>Windows用户：当前版本的AEM作为Cloud Service本地调度程序工具(v2.0.20)与Windows不兼容。 请联系[Adobe支持](https://daycare.day.com/home.html)以接收Windows兼容性的更新。

## 调度程序工具{#dispatcher-sdk}

调度程序工具作为Cloud ServiceSDK是整个AEM的一部分，它提供：

* 一种香草文件结构，包含要包含在调度程序的主项目中的配置文件。
* 客户验证调度程序配置是否仅包含AEM作为Cloud Service支持的指令的工具。        此外，工具还验证语法是否正确，以便apache能够成功开始。
* 在本地调度程序启动的Docker映像。

## 下载并解压工具{#extracting-the-sdk}

作为Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)的[AEM的一部分，调度程序工具可从[软件分发](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)门户的zip文件下载。 该新调度程序工具版本中提供的任何新配置均可用于部署到云环境，在云或更高版本中运行该版本的AEM。

解压缩SDK，它捆绑适用于macOS/Linux和Windows的Dispatcher Tools。

**对于macOS/Linux**，使调度程序工具对象可执行并运行它。它将自解压存储到的目录下的调度程序工具文件（其中`version`是调度程序工具的版本）。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**对于Windows**，解压Dispatcher Toolbingzip存档。

## 文件结构{#file-structure}

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

您可以拥有一个或多个这些文件。 它们包含与主机名匹配的`<VirtualHost>`条目，并允许Apache使用不同的规则处理每个域通信。 文件在`available_vhosts`目录中创建，并在`enabled_vhosts`目录中启用符号链接。 从`.vhost`文件中，将包括其他文件，如重写和变量。

* `conf.d/rewrites/rewrite.rules`

此文件包含在`.vhost`文件中。 它有一组用于`mod_rewrite`的重写规则。

>[!NOTE]
>
>此时，必须使用单个重写文件，而不是站点特定的文件。 该文件大小必须小于1MB。

* `conf.d/variables/custom.vars`

此文件包含在`.vhost`文件中。 您可以在此位置放入Apache变量的定义。

* `conf.d/variables/global.vars`

此文件包含在`dispatcher_vhost.conf`文件中。 您可以更改此文件中的调度程序和重写日志级别。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以有一个或多个这些文件，它们包含与主机名匹配的场，并允许调度程序模块使用不同的规则处理每个场。 文件在`available_farms`目录中创建，并在`enabled_farms`目录中启用符号链接。 从`.farm`文件中，将包括过滤器、缓存规则等其他文件。

* `conf.dispatcher.d/cache/rules.any`

此文件包含在`.farm`文件中。 它指定缓存首选项。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此文件包含在`.farm`文件中。 它指定应将哪些请求标头转发到后端。

* `conf.dispatcher.d/filters/filters.any`

此文件包含在`.farm`文件中。 它有一组规则，这些规则会更改应过滤掉的流量，而不会将流量发送到后端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此文件包含在`.farm`文件中。 它具有列表主机名或URI路径，要通过全局匹配进行匹配。 这决定了使用什么后端来服务请求。

上述文件引用下面列出的不可改变的配置文件。 云环境中的调度程序将不会处理对不可变文件所做的更改。

**不可变的配置文件**

这些文件是基本框架的一部分，并实施标准和最佳实践。 这些文件被视为不可变，因为在本地修改或删除它们不会影响您的部署，因为它们不会被传输到您的云实例。

建议上述文件引用下面列出的不可改变文件，后跟任何附加语句或覆盖。 将调度程序配置部署到云环境时，将使用不可变文件的最新版本，而不管本地开发中使用的版本如何。

* `conf.d/available_vhosts/default.vhost`

包含示例虚拟主机。 对于您自己的虚拟主机，请创建此文件的副本，对其进行自定义，转到`conf.d/enabled_vhosts`并创建一个指向自定义副本的符号链接。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用于说明如何包含虚拟主机和全局变量。

* `conf.d/rewrites/default_rewrite.rules`

适用于标准项目的默认重写规则。 如果需要自定义，请修改`rewrite.rules`。 在自定义中，如果默认规则符合您的需求，您仍可以先包含这些规则。

* `conf.dispatcher.d/available_farms/default.farm`

包含一个调度程序群示例。 对于您自己的场，请创建此文件的副本，对其进行自定义，转到`conf.d/enabled_farms`并创建一个指向自定义副本的符号链接。

* `conf.dispatcher.d/cache/default_invalidate.any`

作为基本框架的一部分，在启动时生成。 您是&#x200B;**必需**&#x200B;的`cache/allowedClients`部分，要在您定义的每个场中包含此文件。

* `conf.dispatcher.d/cache/default_rules.any`

适用于标准项目的默认缓存规则。 如果需要自定义，请修改`conf.dispatcher.d/cache/rules.any`。 在自定义中，如果默认规则符合您的需求，您仍可以先包含这些规则。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

默认请求标头可转发到后端，适用于标准项目。 如果需要自定义，请修改`clientheaders.any`。 在自定义中，您仍可以首先包含默认请求标头（如果它们符合您的需求）。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用于说明如何包含调度程序群。

* `conf.dispatcher.d/filters/default_filters.any`

适用于标准项目的默认过滤器。 如果需要自定义，请修改`filters.any`。 在自定义中，您仍可以先包含默认过滤器（如果它们符合您的需求）。

* `conf.dispatcher.d/renders/default_renders.any`

作为基本框架的一部分，此文件在启动时生成。 您是&#x200B;**必需**&#x200B;的`renders`部分，要在您定义的每个场中包含此文件。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

适用于标准项目的默认主机全局匹配。 如果需要自定义，请修改`virtualhosts.any`。 在自定义中，您不应包含默认主机全局覆盖，因为它与&#x200B;**每**&#x200B;传入请求匹配。

>[!NOTE]
>
>AEM作为Cloud Service主原型将生成相同的调度程序配置文件结构。

以下各节介绍如何在本地验证配置，以便在部署内部版本时在Cloud Manager中通过相关的质量门。

## 调度程序配置{#local-validation-of-dispatcher-configuration}中支持的指令的本地验证

此验证工具在SDK中以Mac OS、Linux或Windows二进制形式提供，允许客户运行与Cloud Manager在构建和部署发行版时执行的验证相同的验证。`bin/validator`

它被调用为：`validator full [-d folder] [-w whitelist] zip-file | src folder`

该工具通过扫描模式为`conf.d/enabled_vhosts/*.vhost`的所有文件来验证调度程序配置是否使用AEM支持的适当指令作为云服务。 通过运行validator的命令，可以列出Apache配置文件中允许的指允许列表令：

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

客户无法添加任意模块，但将来可能会考虑将其他模块包含在产品中。 如上所述，客户可以通过在SDK中执行validator的列表命令，找允许列表到特定Dispatcher版本可用的指令。

该允许列表程序包含列表客户配置中允许的Apache指令。 如果未指列入允许列表令，该工具将记录错误并返回非零退出代码。 如果允许列表命令行上未提供任何(即应调用该环境的方式)，则该工具将使用Cloud Manager在部署到Cloud之前将用于验证的默认。

此外，它还使用模式`conf.dispatcher.d/enabled_farms/*.farm`扫描所有文件并检查：

* 不存在通过`/glob`允许使用的筛选器规则（有关更多详细信息，请参阅[CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)）
* 不公开管理功能。 例如，对路径（如`/crx/de or /system/console`）的访问。

当针对主对象或`dispatcher/src`子目录运行时，它将报告验证失败：

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-whitelisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

请注意，验证工具仅报告未的禁止使用Apache指列入允许列表令。 它不会报告Apache配置的语法或语义问题，因为此信息仅对正在运行的环境中的Apache模块可用。

以下是调试工具输出的常见验证错误的疑难解答技术：

**在存档中找 `conf.dispatcher.d` 不到子文件夹**

您的存档应包含文件夹 `conf.d` 和 `conf.dispatcher.d`。 请注意，您不应 **在**&#x200B;存档 `etc/httpd` 中使用前缀。

**在`conf.dispatcher.d/enabled_farms`**

启用的场应位于所述子文件夹中。

**包含的文件(...)必须命名：...**

您的场配置中有两个部分，其中&#x200B;**必须**包含
特定文件：`/cache`部分中的`/renders`和`/allowedClients`。 那些
部分必须如下所示：

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

您的场配置中有四个部分，允许您包含您自己的文件：`/cache`部分和`/virtualhosts`中的`/clientheaders`、`filters`、`/rules`。 所包含的文件需要命名如下：

| 区域 | 包含文件名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包 **含这些文件的默认版本** ，其名称前面加有单词 `default_`，如 `../filters/default_filters.any`.

**包含位于(...)的语句，位于任何已知位置之外：...**

除上述六个部分外，不允许您
要使用`$include`语句，例如，以下语句将生成此错误：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允许的客户端／渲染不包括自：...**

如果未在`/cache`部分为`/renders`和`/allowedClients`指定包含，则会生成此错误。 请参阅
包含的**文件(...)必须命名：...**&#x200B;部分，了解更多信息。

**过滤器不能使用glob模式允许请求**

允许使用`/glob`样式规则的请求是不安全的，该规则与完整的请求行匹配，例如，

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此语句用于允许对`css`文件进行请求，但也允许对&#x200B;**任何**&#x200B;资源的请求，后跟查询字符串`?a=.css`。 因此，禁止使用此类过滤器（另请参阅CVE-2016-0957）。

**包含的文件(...)与任何已知文件不匹配**

Apache虚拟主机配置中有两种类型的文件可指定为包括：重写和变量。
所包含的文件需要命名如下：

| 类型 | 包含文件名 |
|-----------|---------------------------------|
| 重写 | `conf.d/rewrites/rewrite.rules` |
| 变量 | `conf.d/variables/custom.vars` |

或者，您也可以包含重写规则的&#x200B;**default**&#x200B;版本，其名称为`conf.d/rewrites/default_rewrite.rules`。
请注意，不存在变量文件的默认版本。

**检测到已弃用的配置布局，启用兼容性模式**

此消息表示您的配置具有已弃用的版本1布局，包含一个完整的
具有`ams_`前缀的Apache配置和文件。 尽管向后支持
兼容性应切换到新布局。

## 本地验证调度程序配置语法，以便apache httpd能够开始{#local-validation}

一旦确定调度程序模块配置仅包含受支持的指令，您应检查语法是否正确，以便apache能够进行开始。 为了测试此功能，必须在本地安装Docker。 请注意，AEM不需要运行。

使用`validate.sh`脚本，如下所示：

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
2019/06/19 16:02:55 No issues found
Phase 1 finished
Phase 2: httpd -t validation in docker image
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
...
}
Syntax OK
Phase 2 finished
```

脚本执行以下操作：

1. 它从上一节运行validator以确保只包含受支持的指令。 如果配置无效，则脚本将失败。
2. 它执行`httpd -t command`以测试语法是否正确，以便apache httpd可以开始。 如果配置成功，则应准备好进行部署

## 在本地测试Apache和Dispatcher配置{#testing-apache-and-dispatcher-configuration-locally}

还可以在本地测试Apache和调度程序配置。 它要求在本地安装文档程序，并且您的配置要通过验证，如上所述。

使用`-d`参数执行验证程序工具（请注意，它与前面提到的`validator.sh`不同），该参数输出包含所有调度程序配置文件的文件夹。 然后执行`docker_run.sh`脚本，将该文件夹作为参数进行传递。 通过提供端口号(此处：8080)，启动一个Docker容器，使用您的配置运行调度程序。

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

这将开始容器中的调度程序，其后端指向本地Mac OS计算机上运行的AEM实例（端口4503）。

## 调试Apache和Dispatcher配置{#debugging-apache-and-dispatcher-configuration}

以下策略可用于增加调度程序模块的日志输出并查看本地和云环境中`RewriteRule`评估的结果。

这些模块的日志级别由变量`DISP_LOG_LEVEL`和`REWRITE_LOG_LEVEL`定义。 可以在文件`conf.d/variables/global.vars`中设置它们。 其相关部分如下：

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

在本地运行调度程序时，日志将直接打印到终端输出。 在大多数情况下，您希望这些日志在DEBUG中，这可以通过在运行Docker时将调试级别作为参数进行传递来完成。 例如：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`。

云环境的日志通过云管理器中提供的日志记录服务公开。

## 每个环境{#different-dispatcher-configurations-per-environment}的不同调度程序配置

此时，同一调度程序配置作为Cloud Service环境应用于所有AEM。 运行时将具有一个环境变量`ENVIRONMENT_TYPE`，它包含当前运行模式（dev、stage或prod）以及定义。 定义可以是`ENVIRONMENT_DEV`、`ENVIRONMENT_STAGE`或`ENVIRONMENT_PROD`。 在Apache配置中，变量可以直接在表达式中使用。 或者，可以使用定义来构建逻辑：

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

在调度程序配置中，可以使用相同的环境变量。 如果需要更多逻辑，请如上例所示定义变量，然后在调度程序配置部分使用它们：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

在本地测试配置时，可以通过将变量`DISP_RUN_MODE`直接传递到`docker_run.sh`脚本来模拟不同的环境类型：

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

不传递DISP_RUN_MODE值时的默认运行模式为“dev”。
要获得可用选项和变量的完整列表，请运行脚本`docker_run.sh`（不含参数）。

## 查看Docker容器{#viewing-dispatcher-configuration-in-use-by-docker-container}正在使用的调度程序配置

使用环境特定配置，可能难以确定实际的调度程序配置。 在使用`docker_run.sh`启动您的docker容器后，可以按如下方式转储它：

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

## AMS调度程序与AEM作为Cloud Service{#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}的主要区别

如以上参考页所述，AEM中作为Cloud Service的Apache和Dispatcher配置与AMS配置非常相似。 主要区别是：

* 在AEM中，作为Cloud Service，某些Apache指令不能使用（例如`Listen`或`LogLevel`）
* 在AEM中，作为Cloud Service，只能将部分Dispatcher配置放入包含文件，其命名很重要。 例如，要在不同主机之间重复使用的筛选器规则必须放入一个名为`filters/filters.any`的文件中。 有关详细信息，请参阅参考页面。
* 在AEM作为Cloud Service中，存在额外的验证，以禁止使用`/glob`编写的筛选器规则，以防止出现安全问题。 由于将使用`deny *`而不是`allow *`（不能使用），客户将从本地运行调度程序并执行试用和错误中受益，查看日志以准确了解调度程序过滤器为了添加这些路径而阻止的路径。

## 将调度程序配置从AMS迁移到AEM作为Cloud Service的准则

调度程序配置结构与AEM作为Cloud Service存在差异。 下面是如何从AMS调度程序配置版本2作为Cloud Service迁移到AEM的分步指南。

## 如何将AMS转换为AEM作为云服务调度程序配置

下节提供有关如何转换AMS配置的分步说明。 它假设
具有与[Cloud Manager调度程序配置](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)中描述的结构类似的存档

### 提取存档并删除最后的前缀

将存档解压到文件夹，并确保具有`conf`、`conf.d`的直接子文件夹开始,
`conf.dispatcher.d`和`conf.modules.d`。 如果他们不这样做，就在层级中向上移动。

### 删除未使用的子文件夹和文件

删除子文件夹`conf`和`conf.modules.d`，以及与`conf.d/*.conf`匹配的文件。

### 删除所有未发布的虚拟主机

删除`conf.d/enabled_vhosts`中具有`author`、`unhealthy`、`health`、
`lc`或`flush`。 `conf.d/available_vhosts`中所有非
链接到的内容也可以删除。

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

输入目录`conf.d/rewrites`。

删除任何名为`base_rewrite.rules`和`xforwarded_forcessl_rewrite.rules`的文件，并记住
删除虚拟主机文件中引用的`Include`语句。

如果`conf.d/rewrites`现在包含单个文件，则应将其重命名为`rewrite.rules`，但不应
忘记在虚拟主机文件中改编引用该文件的`Include`语句。

但是，如果文件夹包含多个特定于虚拟主机的文件，则其内容应为
复制到虚拟主机文件中引用这些语句的`Include`语句。

### 检查 variables

输入目录`conf.d/variables`。

删除任何名为`ams_default.vars`的文件，并记住删除虚拟文件中的`Include`语句
托管引用这些文件的文件。

如果`conf.d/variables`现在包含单个文件，则应将其重命名为`custom.vars`，但不应
忘记在虚拟主机文件中改编引用该文件的`Include`语句。

但是，如果文件夹包含多个特定于虚拟主机的文件，则其内容应为
复制到虚拟主机文件中引用这些语句的`Include`语句。

### 删除允许列表

删除文件夹`conf.d/whitelists`并删除虚拟主机文件中引用的`Include`语句
该子文件夹中的某个文件。

### 替换任何不再可用的变量

在所有虚拟主机文件中：

将`PUBLISH_DOCROOT`重命名为`DOCROOT`
删除引用名为`DISP_ID`、`PUBLISH_FORCE_SSL`或`PUBLISH_WHITELIST_ENABLED`的变量的部分

### 通过运行验证器检查状态

使用`httpd`子命令在目录中运行调度程序validator:

```
$ validator httpd .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到未的Apache指列入允许列表令，请删除它们。

### 删除所有未发布的场

删除`conf.dispatcher.d/enabled_farms`中具有`author`、`unhealthy`、`health`和
`lc`或`flush`。 `conf.dispatcher.d/available_farms`中所有非
链接到的内容也可以删除。

### 重命名场文件

必须重命名`conf.d/enabled_farms`中的所有场以匹配模式`*.farm`，例如a
名为`customerX_farm.any`的场文件应重命名为`customerX.farm`。

### 检查 cache

输入目录`conf.dispatcher.d/cache`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/cache`现在为空，则复制文件`conf.dispatcher.d/cache/rules.any`
从标准调度程序配置到此文件夹。 标准调度程序
可在此SDK的文件夹`src`中找到配置。 不要忘记调整
`$include`语句引用场文件中的`ams_*_cache.any`规则文件
还有。

如果`conf.dispatcher.d/cache`现在包含一个后缀为`_cache.any`的文件，
它应重命名为`rules.any`，不要忘记改编`$include`语句
在场文件中也引用该文件。

但是，如果文件夹包含多个具有该模式的场特定文件，则其内容
应该被复制到`$include`语句中，该语句在场文件中引用它们。

删除任何后缀为`_invalidate_allowed.any`的文件。

从默认位置复制文件`conf.dispatcher.d/cache/default_invalidate_any`
云调度程序配置中的AEM。

在每个场文件中，删除`cache/allowedClients`部分中的所有内容并替换它
与：

```
$include "../cache/default_invalidate.any"
```

### 检查 client headers

输入目录`conf.dispatcher.d/clientheaders`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/clientheaders`现在包含一个后缀为`_clientheaders.any`的文件，
它应重命名为`clientheaders.any`，不要忘记改编`$include`语句
在场文件中也引用该文件。

但是，如果文件夹包含多个具有该模式的场特定文件，则其内容
应该被复制到`$include`语句中，该语句在场文件中引用它们。

从默认位置复制文件`conf.dispatcher/clientheaders/default_clientheaders.any`
AEM作为Cloud Service调度程序配置到该位置。

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

输入目录`conf.dispatcher.d/filters`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/filters`现在包含单个文件，则应将其重命名为
`filters.any`，不要忘记改编`$include`语句，引用
文件。

但是，如果文件夹包含多个具有该模式的场特定文件，则其内容
应该被复制到`$include`语句中，该语句在场文件中引用它们。

从默认位置复制文件`conf.dispatcher/filters/default_filters.any`
AEM作为Cloud Service调度程序配置到该位置。

在每个场文件中，将如下所示的所有 filter include 语句：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

替换为语句：

```
$include "../filters/default_filters.any"
```

### 检查 renders

输入目录`conf.dispatcher.d/renders`。

移除该文件夹中的所有文件。

从默认位置复制文件`conf.dispatcher.d/renders/default_renders.any`
AEM作为Cloud Service调度程序配置到该位置。

在每个场文件中，删除`renders`部分中的所有内容并替换它
与：

```
$include "../renders/default_renders.any"
```

### 检查 virtualhosts

将目录`conf.dispatcher.d/vhosts`重命名为`conf.dispatcher.d/virtualhosts`并输入它。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/virtualhosts`现在包含单个文件，则应将其重命名为
`virtualhosts.any`，不要忘记改编`$include`语句，引用
文件。

但是，如果文件夹包含多个具有该模式的场特定文件，则其内容
应该被复制到`$include`语句中，该语句在场文件中引用它们。

从默认位置复制文件`conf.dispatcher/virtualhosts/default_virtualhosts.any`
AEM作为Cloud Service调度程序配置到该位置。

在每个场文件中，将如下所示的所有 filter include 语句：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

替换为语句：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 通过运行验证器检查状态

使用`dispatcher`子命令将AEM作为Cloud Service调度程序validator运行在您的目录中：

```
$ validator dispatcher .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到有关未定义变量 `PUBLISH_DOCROOT` 的错误，请将该变量重命名为 `DOCROOT`。

有关其他每个错误，请参阅验证器工具文档的“疑难解答”部分。

### 使用本地部署测试配置（需要安装Docker）

使用AEM中的脚本`docker_run.sh`作为Cloud Service调度程序工具，可以测试
您的配置不包含任何其他仅显示在
部署：

### 第1步：使用验证程序生成部署信息

```
validator full -d out .
```


这将验证完整配置并在 中生成部署信息`out`

### 第2步：将调度程序与该部署信息开始到docker映像中

在 macOS 计算机上运行 AEM 发布服务器，并监听端口 4503 时，您可以在该服务器前面运行启动 Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

这将启动容器并在本地端口 8080 上公开 Apache。

### 使用新的调度程序配置

恭喜！ 如果验证程序不再报告任何问题，并且
Docker容器开始未出现任何故障或警告，您
准备将配置移至`dispatcher/src`子目录
您的git存储库。

**使用AMS Dispatcher配置版本1的客户应联系客户支持，帮助他们从版本1迁移到版本2，以便遵循上述说明。**
