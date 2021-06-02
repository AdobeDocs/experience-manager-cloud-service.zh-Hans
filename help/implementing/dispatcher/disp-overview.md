---
title: 云中的调度程序
description: '云中的调度程序 '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 6eb200fe661873374258a5953a07b38b2251da43
workflow-type: tm+mt
source-wordcount: '4233'
ht-degree: 6%

---

# 云中的调度程序 {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="云中的调度程序"
>abstract="本节介绍如何将AEM构建为Cloud ServiceApache和Dispatcher配置，以及如何在部署到云环境之前在本地验证和运行该配置。 此外，还介绍了如何在云环境中进行调试。"

## Apache和Dispatcher配置和测试{#apache-and-dispatcher-configuration-and-testing}

本节介绍如何将AEM构建为Cloud ServiceApache和Dispatcher配置，以及如何在部署到云环境之前在本地验证和运行该配置。 此外，还介绍了如何在云环境中进行调试。 有关Dispatcher的其他信息，请参阅[AEM Dispatcher文档](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans)。

>[!NOTE]
>Windows用户需要使用支持Docker的Windows 10专业版或其他发行版。 这是在本地计算机上运行和调试Dispatcher的先决条件。 以下部分包括使用Mac或Linux版本的SDK的命令，但Windows SDK也可以以类似的方式使用。

## 调度程序工具{#dispatcher-sdk}

Dispatcher工具是整体AEM as a Dispatcher SDK的一部分，它提供：

* 一种原版文件结构，其中包含要包含在Dispatcher的Maven项目中的配置文件。
* 用于验证Dispatcher配置是否仅包含AEM作为Cloud Service支持的指令的工具。        此外，工具还会验证语法是否正确，以便Apache可以成功启动。
* 在本地调度程序的Docker图像。

## 下载和提取工具{#extracting-the-sdk}

[AEM as a Dispatcher SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)的一部分Dispatcher工具可从位于[Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)门户的zip文件下载。 该新Dispatcher工具版本中提供的任何新配置都可用于部署到在云或更高版本中运行该AEM版本的云环境。

解压缩SDK，该SDK捆绑了适用于macOS/Linux和Windows的Dispatcher工具。

**对于macOS/Linux**，请使Dispatcher工具对象可执行并运行它。它将自解压存储到的目录下的Dispatcher工具文件（其中`version`是Dispatcher工具的版本）。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**对于Windows**，解压Dispatcher工具zip存档。

## 文件结构{#file-structure}

项目的Dispatcher子文件夹的结构如下所述，应该复制到Maven项目Dispatcher文件夹中：

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

以下文件是可自定义的，并将在部署时传输到您的云实例：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以拥有一个或多个这些文件。 它们包含与主机名匹配的`<VirtualHost>`条目，并允许Apache使用不同的规则处理每个域流量。 文件在`available_vhosts`目录中创建，并在`enabled_vhosts`目录中通过符号链接启用。 在`.vhost`文件中，将包含重写和变量等其他文件。

* `conf.d/rewrites/rewrite.rules`

此文件包含在`.vhost`文件内。 它有一组用于`mod_rewrite`的重写规则。

>[!NOTE]
>
>目前，必须使用单个重写文件，而不是特定于站点的文件。 通常，可自定义文件的内容总和必须小于1MB。

* `conf.d/variables/custom.vars`

此文件包含在`.vhost`文件内。 您可以在此位置放置Apache变量的定义。

* `conf.d/variables/global.vars`

此文件包含在`dispatcher_vhost.conf`文件内。 您可以更改Dispatcher并重写此文件中的日志级别。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以具有一个或多个这些文件，并且它们包含场以匹配主机名，并允许调度程序模块使用不同的规则处理每个场。 文件在`available_farms`目录中创建，并在`enabled_farms`目录中通过符号链接启用。 在`.farm`文件中，将包含过滤器、缓存规则等其他文件。

* `conf.dispatcher.d/cache/rules.any`

此文件包含在`.farm`文件内。 它指定缓存首选项。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此文件包含在`.farm`文件内。 它指定应将哪些请求标头转发到后端。

* `conf.dispatcher.d/filters/filters.any`

此文件包含在`.farm`文件内。 它有一组规则，用于更改应过滤掉的流量，而不是将流量发送到后端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此文件包含在`.farm`文件内。 它有一个主机名或要通过全局匹配进行匹配的URI路径列表。 这可确定要用于提供请求的后端。

上述文件引用下面列出的不可更改配置文件。 云环境中的Dispatcher将不会处理对不可变文件所做的更改。

**不可变配置文件**

这些文件是基本框架的一部分，可实施标准和最佳实践。 这些文件被视为不可更改，因为在本地修改或删除它们不会对您的部署产生任何影响，因为它们将不会传输到您的云实例。

建议上述文件引用下面列出的不可变文件，然后引用任何其他语句或覆盖。 将Dispatcher配置部署到云环境后，无论本地开发中使用的是哪个版本，都会使用最新版本的不可变文件。

* `conf.d/available_vhosts/default.vhost`

包含一个示例虚拟主机。 对于您自己的虚拟主机，请创建此文件的副本并对其进行自定义，转到`conf.d/enabled_vhosts`并创建指向自定义副本的符号链接。

* `conf.d/dispatcher_vhost.conf`

基础框架的一部分，用于说明如何包含虚拟主机和全局变量。

* `conf.d/rewrites/default_rewrite.rules`

适用于标准项目的默认重写规则。 如果需要自定义，请修改`rewrite.rules`。 在自定义中，如果默认规则符合您的需求，您仍可以先包含这些规则。

* `conf.dispatcher.d/available_farms/default.farm`

包含示例Dispatcher场。 对于您自己的场，请创建此文件的副本并对其进行自定义，转到`conf.d/enabled_farms`并创建指向自定义副本的符号链接。

* `conf.dispatcher.d/cache/default_invalidate.any`

作为基础框架的一部分，将在启动时生成。 您需要&#x200B;****&#x200B;在`cache/allowedClients`部分中的每个场中包含此文件。

* `conf.dispatcher.d/cache/default_rules.any`

适用于标准项目的默认缓存规则。 如果需要自定义，请修改`conf.dispatcher.d/cache/rules.any`。 在自定义中，如果默认规则符合您的需求，您仍可以先包含这些规则。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

要转发到后端（适用于标准项目）的默认请求标头。 如果需要自定义，请修改`clientheaders.any`。 在自定义中，如果默认请求标头符合您的需求，您仍可以先包含它们。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用于说明如何包含调度程序场。

* `conf.dispatcher.d/filters/default_filters.any`

适用于标准项目的默认过滤器。 如果需要自定义，请修改`filters.any`。 在自定义中，如果默认过滤器符合您的需求，您仍可以先包含这些过滤器。

* `conf.dispatcher.d/renders/default_renders.any`

作为基本框架的一部分，此文件将在启动时生成。 您需要&#x200B;****&#x200B;在`renders`部分中的每个场中包含此文件。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

适用于标准项目的默认主机代换。 如果需要自定义，请修改`virtualhosts.any`。 在自定义中，您不应包含默认的代换主机，因为它与&#x200B;**每个**&#x200B;传入请求匹配。

>[!NOTE]
>
>AEM作为Cloud Servicemaven原型将生成相同的Dispatcher配置文件结构。

以下各节介绍如何在本地验证配置，以便在部署内部版本时，在Cloud Manager中传递关联的质量门。

## Dispatcher配置{#local-validation-of-dispatcher-configuration}中支持的指令的本地验证

该验证工具在SDK中以Mac OS、Linux或Windows二进制形式提供，允许客户运行Cloud Manager在构建和部署版本时将执行的相同验证。`bin/validator`

该调用将作为：`validator full [-d folder] [-w allowlist] zip-file | src folder`

该工具通过扫描模式为`conf.d/enabled_vhosts/*.vhost`的所有文件，验证Dispatcher配置是否使用了AEM as a Cloud Service支持的相应指令。

在Windows上，调度程序验证器区分大小写。 因此，如果您不遵循配置所在路径的大小写，则可能无法验证配置，例如：

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

通过从Windows资源管理器复制并粘贴路径，然后在命令提示符下使用`cd`命令将该路径复制并粘贴到该路径中，可避免出现此错误。

通过运行验证器的命令，可以列出Apache配置文件中允许的允许列表指令：

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

下表显示了支持的Apache模块：

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
| `mod_proxy` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html) |
| `mod_proxy_http` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |

客户无法添加任意模块，但将来可能会考虑将其他模块添加到产品中。 如上所述，客户可以通过在SDK中执行验证器的命令，找到可用于给定Dispatcher版允许列表本的指令列表。

允许列表包含客户配置中允许的Apache指令列表。 如果未指列入允许列表令，该工具将记录错误并返回非零退出代码。 如果命允许列表令行上未提供任何（即应调用该命令的方式），则该工具会使用Cloud Manager将用于验允许列表证的默认，然后再部署到云环境。

此外，它还会以模式`conf.dispatcher.d/enabled_farms/*.farm`扫描所有文件，并检查：

* 不存在通过`/glob`允许使用的过滤器规则（有关更多详细信息，请参阅[CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)）
* 未显示管理员功能。 例如，对路径（如`/crx/de or /system/console`）的访问。

当针对maven对象或`dispatcher/src`子目录运行时，它将报告验证失败：

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

请注意，验证工具仅报告未的Apache指令的禁止使列入允许列表用。 它不会报告Apache配置的语法或语义问题，因为此信息仅适用于运行环境中的Apache模块。

以下是调试工具输出的常见验证错误的故障诊断技术：

**在存档中找 `conf.dispatcher.d` 不到子文件夹**

您的存档应包含文件夹 `conf.d` 和 `conf.dispatcher.d`。 请注意，您不应 **在**&#x200B;存档 `etc/httpd` 中使用前缀。

**在中找不到任何场`conf.dispatcher.d/enabled_farms`**

您已启用的场应位于上述子文件夹中。

**包含的文件(...)必须命名为：...**

场配置中有两个部分，**必须**包含
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

场配置中有四个部分，允许您在其中包含自己的文件：`/cache`部分和`/virtualhosts`部分的`/clientheaders`、`filters`、`/rules`。 所包含的文件需要命名如下：

| 区域 | 包含文件名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包 **含这些文件的默认版本** ，其名称前面加有单词 `default_`，如 `../filters/default_filters.any`.

**在任何已知位置之外的(...)包含语句：...**

除上述六节外，不允许
要使用`$include`语句，例如，以下语句将生成此错误：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允许的客户端/呈现器不包括在以下位置：...**

如果未在`/cache`部分中为`/renders`和`/allowedClients`指定包含项，则会生成此错误。 请参阅
**包含的文件(...)必须命名：...**&#x200B;部分以了解详细信息。

**筛选器不得使用全局模式来允许请求**

允许具有`/glob`样式规则的请求是不安全的，该规则与完整的请求行(例如，

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此语句用于允许`css`文件的请求，但也允许对&#x200B;**任意**&#x200B;资源的请求，后跟查询字符串`?a=.css`。 因此，禁止使用此类过滤器（另请参阅CVE-2016-0957）。

**包含的文件(...)与任何已知文件都不匹配**

Apache虚拟主机配置中有两种类型的文件可指定为：重写和变量。
所包含的文件需要命名如下：

| 类型 | 包含文件名 |
|-----------|---------------------------------|
| 重写 | `conf.d/rewrites/rewrite.rules` |
| 变量 | `conf.d/variables/custom.vars` |

或者，您也可以包含重写规则的&#x200B;**default**&#x200B;版本，其名称为`conf.d/rewrites/default_rewrite.rules`。
请注意，变量文件没有默认版本。

**检测到已弃用的配置布局，启用兼容性模式**

此消息表示您的配置具有已弃用的版本1布局，其中包含一个完整的
前缀为`ams_`的Apache配置和文件。 虽然向后支持
兼容性，则应切换到新布局。

## 本地验证Dispatcher配置语法，以便Apache httpd可以启动{#local-validation}

在确定Dispatcher模块配置仅包含受支持的指令后，您应该检查语法是否正确，以便Apache能够启动。 要测试此功能，必须在本地安装Docker。 请注意，AEM不需要运行。

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

脚本会执行以下操作：

1. 它会从上一部分运行验证器，以确保仅包含受支持的指令。 如果配置无效，脚本将失败。
2. 它会执行`httpd -t command`以测试语法是否正确，以便Apache httpd可以启动。 如果成功，配置应准备好进行部署。
3. 检查Dispatcher SDK配置文件的子集（如[文件结构部分](#file-structure)中所述）是否未修改。 这是一项新检查，它随AEM SDK版本v2021.1.4738引入，其中还包含Dispatcher工具版本2.0.36。在此更新之前，客户可能错误地假定这些不可变文件的任何本地SDK修改也将应用于云环境。

在Cloud Manager部署期间，将同时执行`httpd -t syntax`检查，并且Cloud Manager `Build Images step failure`日志中将包含任何错误。

## 在本地测试Apache和Dispatcher配置{#testing-apache-and-dispatcher-configuration-locally}

也可以在本地测试Apache和Dispatcher配置。 它要求将文档安装在本地，并且您的配置要通过上述验证。

使用`-d`参数执行验证器工具（请注意，它与前面提到的`validator.sh`不同），该参数会输出包含所有Dispatcher配置文件的文件夹。 然后执行`docker_run.sh`脚本，并将该文件夹作为参数进行传递。 通过提供端口号(此处为：8080)，将启动Docker容器以使用您的配置运行Dispatcher。

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

这会启动容器中的AEM，其后端指向在本地Mac OS计算机上的端口4503处运行的Dispatcher实例。

## 调试Apache和Dispatcher配置{#debugging-apache-and-dispatcher-configuration}

以下策略可用于增加Dispatcher模块的日志输出，并查看本地和云环境中`RewriteRule`评估的结果。

这些模块的日志级别由变量`DISP_LOG_LEVEL`和`REWRITE_LOG_LEVEL`定义。 可以在文件`conf.d/variables/global.vars`中设置这些参数。 其相关部分如下：

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

在本地运行Dispatcher时，日志会直接打印到终端输出。 大多数情况下，您希望这些日志处于DEBUG中，这可以通过在运行Docker时将调试级别作为参数传递来完成。 例如：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`。

云环境的日志通过Cloud Manager中提供的日志记录服务公开。

## 每个环境{#different-dispatcher-configurations-per-environment}的Dispatcher配置不同

当前，同一Dispatcher配置适用于作为Cloud Service环境的所有AEM。 运行时将有一个环境变量`ENVIRONMENT_TYPE`，其中包含当前运行模式（开发、暂存或生产）以及定义。 定义可以是`ENVIRONMENT_DEV`、`ENVIRONMENT_STAGE`或`ENVIRONMENT_PROD`。 在Apache配置中，变量可以直接在表达式中使用。 或者，也可以使用定义来构建逻辑：

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

在Dispatcher配置中，可以使用相同的环境变量。 如果需要更多逻辑，请如上面的示例所示定义变量，然后在Dispatcher配置部分中使用它们：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

在本地测试配置时，您可以通过将变量`DISP_RUN_MODE`直接传递到`docker_run.sh`脚本来模拟不同的环境类型：

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

未传入DISP_RUN_MODE值时，默认运行模式为“dev”。
要获取可用选项和变量的完整列表，请运行不带参数的脚本`docker_run.sh`。

## 查看Docker容器{#viewing-dispatcher-configuration-in-use-by-docker-container}正在使用的Dispatcher配置

对于特定于环境的配置，可能很难确定实际的Dispatcher配置。 使用`docker_run.sh`启动Docker容器后，可按如下方式倾弃该容器：

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

## AMS Dispatcher与AEM as a Savier的主要区别{#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

如上面的参考页面所述，AEM as aCloud Service中的Apache和Dispatcher配置与AMS配置非常相似。 主要区别包括：

* 在AEM as aCloud Service中，不能使用某些Apache指令（例如`Listen`或`LogLevel`）
* 在AEM as a Cloud Service中，只能将部分Dispatcher配置放入包含文件中，其命名很重要。 例如，要在不同主机之间重复使用的过滤器规则必须放入名为`filters/filters.any`的文件中。 有关更多信息，请参阅参考页面。
* 在AEM as aCloud Service中，有额外的验证来禁止使用`/glob`编写的过滤器规则，以防止出现安全问题。 由于将使用`deny *`而不是`allow *`（不能使用），因此客户将从在本地运行Dispatcher以及执行试用和错误中受益，查看日志可准确了解Dispatcher过滤器为了添加这些过滤器而阻止的路径。

## 将调度程序配置从AMS迁移到AEM as aCloud Service的准则

Dispatcher配置结构在Managed Services与AEM as a Dispatcher之间存在差异。 下面提供了关于如何从AMS Dispatcher配置版本2迁移到AEM as aCloud Service的分步指南。

## 如何将AMS转换为AEM as a Cloud Service Dispatcher配置

以下部分提供了有关如何转换AMS配置的分步说明。 它假定
具有与[Cloud Manager Dispatcher配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)中所述结构类似的存档

### 提取存档并删除最后的前缀

将存档解压缩到文件夹中，并确保子文件夹的直接开头为`conf`、`conf.d`、
`conf.dispatcher.d`和`conf.modules.d`。 如果没有，请在层级中向上移动。

### 删除未使用的子文件夹和文件

删除子文件夹`conf`和`conf.modules.d`，以及与`conf.d/*.conf`匹配的文件。

### 删除所有未发布的虚拟主机

删除`conf.d/enabled_vhosts`中具有`author`、`unhealthy`、`health`的所有虚拟主机文件，
`lc`或`flush`。 `conf.d/available_vhosts`中所有非虚拟主机文件
也可以删除链接到的。

### 移除或注释未引用端口 80 的虚拟主机部分

如果虚拟主机文件中仍有部分内容专门引用端口80以外的其他端口，例如：

```
<VirtualHost *:443>
...
</VirtualHost>
```

，
则请移除或注释该部分。这些部分中的语句将不会得到处理，但是如果保留它们，您可能最终仍会对其进行编辑，并且不会有任何效果，这可能会造成混淆。

### 检查 rewrites

进入目录`conf.d/rewrites`。

移除任何名为`base_rewrite.rules`和`xforwarded_forcessl_rewrite.rules`的文件，并记住
删除虚拟主机文件中引用`Include`语句。

如果`conf.d/rewrites`现在包含单个文件，则应将其重命名为`rewrite.rules`，但不应
也请忘记修改虚拟主机文件中引用该文件的`Include`语句。

但是，如果文件夹包含多个特定于虚拟主机的文件，则其内容应为
复制到虚拟主机文件中引用`Include`语句的。

### 检查 variables

进入目录`conf.d/variables`。

移除任何名为`ams_default.vars`的文件，并记住移除虚拟中的`Include`语句
主机文件。

如果`conf.d/variables`现在包含单个文件，则应将其重命名为`custom.vars`，但不应
也请忘记修改虚拟主机文件中引用该文件的`Include`语句。

但是，如果文件夹包含多个特定于虚拟主机的文件，则其内容应为
复制到虚拟主机文件中引用`Include`语句的。

### 删除允许列表

删除文件夹`conf.d/whitelists`，并删除虚拟主机文件中引用的`Include`语句
子文件夹中的一些文件。

### 替换任何不再可用的变量

在所有虚拟主机文件中：

将`PUBLISH_DOCROOT`重命名为`DOCROOT`
删除引用名为`DISP_ID`、`PUBLISH_FORCE_SSL`或`PUBLISH_WHITELIST_ENABLED`的变量的部分

### 通过运行验证器检查状态

使用`httpd`子命令在目录中运行Dispatcher验证器：

```
$ validator httpd .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到未的Apache指列入允许列表令，请删除它们。

### 删除所有未发布的场

删除`conf.dispatcher.d/enabled_farms`中具有`author`、`unhealthy`、`health`、
`lc`或`flush`。 `conf.dispatcher.d/available_farms`中所有非
也可以删除链接到的。

### 重命名场文件

必须重命名`conf.d/enabled_farms`中的所有场以匹配模式`*.farm`，例如
名为`customerX_farm.any`的场文件应重命名为`customerX.farm`。

### 检查 cache

进入目录`conf.dispatcher.d/cache`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/cache`现在为空，请复制文件`conf.dispatcher.d/cache/rules.any`
从标准Dispatcher配置到此文件夹。 标准Dispatcher
可在此SDK的文件夹`src`中找到配置。 不要忘记调整
引用场文件中`ams_*_cache.any`规则文件的`$include`语句
也是。

相反，如果`conf.dispatcher.d/cache`现在包含一个后缀为`_cache.any`的文件，
它应重命名为`rules.any`，并且不要忘记修改`$include`语句
在场文件中也引用该文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则其内容为
应该复制到场文件中引用它们的`$include`语句中。

移除所有后缀为`_invalidate_allowed.any`的文件。

从默认位置复制文件`conf.dispatcher.d/cache/default_invalidate_any`
AEM中的。

在每个场文件中，删除`cache/allowedClients`部分中的所有内容并将其替换
与：

```
$include "../cache/default_invalidate.any"
```

### 检查 client headers

进入目录`conf.dispatcher.d/clientheaders`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/clientheaders`现在包含一个后缀为`_clientheaders.any`的文件，
它应重命名为`clientheaders.any`，并且不要忘记修改`$include`语句
在场文件中也引用该文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则其内容为
应该复制到场文件中引用它们的`$include`语句中。

从默认位置复制文件`conf.dispatcher/clientheaders/default_clientheaders.any`
AEM作为该位置的Cloud ServiceDispatcher配置。

在每个场文件中，将如下所示的任何clientheader include语句：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

替换为语句：

```
$include "../clientheaders/default_clientheaders.any"
```

### 检查 filter

进入目录`conf.dispatcher.d/filters`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/filters`现在包含单个文件，则应将其重命名为
`filters.any`，并且不要忘记修改引用该变量的`$include`语句
文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则其内容为
应该复制到场文件中引用它们的`$include`语句中。

从默认位置复制文件`conf.dispatcher/filters/default_filters.any`
AEM作为该位置的Cloud ServiceDispatcher配置。

在每个场文件中，将如下所示的任何filter include语句：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

替换为语句：

```
$include "../filters/default_filters.any"
```

### 检查 renders

进入目录`conf.dispatcher.d/renders`。

移除该文件夹中的所有文件。

从默认位置复制文件`conf.dispatcher.d/renders/default_renders.any`
AEM作为该位置的Cloud ServiceDispatcher配置。

在每个场文件中，删除`renders`部分中的所有内容并将其替换
与：

```
$include "../renders/default_renders.any"
```

### 检查 virtualhosts

将目录`conf.dispatcher.d/vhosts`重命名为`conf.dispatcher.d/virtualhosts`并输入。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/virtualhosts`现在包含单个文件，则应将其重命名为
`virtualhosts.any`，并且不要忘记修改引用该变量的`$include`语句
文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则其内容为
应该复制到场文件中引用它们的`$include`语句中。

从默认位置复制文件`conf.dispatcher/virtualhosts/default_virtualhosts.any`
AEM作为该位置的Cloud ServiceDispatcher配置。

在每个场文件中，将如下所示的任何filter include语句：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

替换为语句：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 通过运行验证器检查状态

使用`dispatcher`子命令在目录中将AEM作为Cloud ServiceDispatcher验证器运行：

```
$ validator dispatcher .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到有关未定义变量 `PUBLISH_DOCROOT` 的错误，请将该变量重命名为 `DOCROOT`。

有关其他每个错误，请参阅验证器工具文档的“疑难解答”部分。

### 在本地部署中测试您的配置（需要安装Docker）

使用AEM中的脚本`docker_run.sh`作为Cloud Service调度程序工具，您可以测试
您的配置不包含只会在
部署：

### 步骤1:使用验证器生成部署信息

```
validator full -d out .
```


这将验证完整配置并在 中生成部署信息`out`

### 步骤2:使用该部署信息在Docker映像中启动Dispatcher

当您的AEM发布服务器在macOS计算机上运行，监听端口4503时，
您可以在该服务器前面运行启动Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

这将启动容器并在本地端口 8080 上公开 Apache。

### 使用新的Dispatcher配置

恭喜！ 如果验证器不再报告任何问题，并且
docker容器启动时没有出现任何故障或警告，您
已准备好将配置移动到`dispatcher/src`子目录
的URL。

**使用AMS Dispatcher配置版本1的客户应联系客户支持，以帮助他们从版本1迁移到版本2，以便按照上述说明操作。**
