---
title: 使用 Dispatcher 工具进行验证和调试
description: 了解本地验证、调试、灵活模式文件结构以及如何从旧模式迁移到灵活模式。
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '3028'
ht-degree: 1%

---

# 使用 Dispatcher 工具进行验证和调试 {#Dispatcher-in-the-cloud}

## 简介 {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>有关云中Dispatcher以及如何下载Dispatcher工具的更多信息，请参阅云中[Dispatcher](/help/implementing/dispatcher/disp-overview.md)页面。 如果您的Dispatcher配置处于旧模式，请参阅[旧模式文档](/help/implementing/dispatcher/validation-debug-legacy.md)。

以下各节介绍了灵活模式的文件结构、本地验证、调试以及从旧版模式迁移到灵活模式。

本文假定您项目的Dispatcher配置包含文件`opt-in/USE_SOURCES_DIRECTLY`。 与传统模式相比，此文件可让SDK和运行时以改进的方式验证和部署配置，从而消除有关文件数量和大小的限制。

如果您的Dispatcher配置不包含上述文件，Adobe建议您按照[从旧模式迁移到灵活模式](#migrating)部分中所述从旧模式迁移到灵活模式。

## 文件结构 {#flexible-mode-file-structure}

项目的Dispatcher子文件夹的结构如下所示：

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   ├── my_site.vhost # Created by customer
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── my_site.vhost -> ../available_vhosts/my_site.vhost  # Created by customer
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
│── opt-in
│   └── USE_SOURCES_DIRECTLY
└── conf.dispatcher.d
    ├── available_farms
    │   ├── my_farm.farm # Created by customer
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   ├── marketing_query_parameters.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── my_farm.farm -> ../available_farms/my_farm.farm  # Created by customer
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

以下是可修改的显着文件的说明：

**可自定义的文件**

以下文件可自定义，并在部署时传输到您的云实例：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以拥有一个或多个这些文件。 它们包含与主机名匹配的`<VirtualHost>`条目，并允许Apache使用不同的规则处理每个域流量。 文件在`available_vhosts`目录中创建，并使用`enabled_vhosts`目录中的符号链接启用。 从`.vhost`文件中包括其他文件，如重写和变量。

>[!NOTE]
>
>在灵活模式下，您应该使用相对路径而不是绝对路径。

确保始终至少有一台与Dispatcher失效所需的ServerAlias `\*.local`、`localhost`和`127.0.0.1`匹配的虚拟主机可用。 至少一个vhost配置中也需要服务器别名`*.adobeaemcloud.net`和`*.adobeaemcloud.com`，内部Adobe进程也需要这两个别名。

如果由于您有多个vhost文件而希望与确切的主机匹配，则可以遵循以下示例：

```
<VirtualHost *:80>
    ServerName    "example.com"
    # Put names of which domains are used for your published site/content here
    ServerAlias     "*example.com" "\*.local" "localhost" "127.0.0.1" "*.adobeaemcloud.net" "*.adobeaemcloud.com"
    # Use a document root that matches the one in conf.dispatcher.d/default.farm
    DocumentRoot "${DOCROOT}"
    # URI dereferencing algorithm is applied at Sling's level, do not decode parameters here
    AllowEncodedSlashes NoDecode
    # Add header breadcrumbs for help in troubleshooting which vhost file is chosen
    <IfModule mod_headers.c>
        Header add X-Vhost "publish-example-com"
    </IfModule>
  ...
</VirtualHost>
```

* `conf.d/enabled_vhosts/<CUSTOMER_CHOICE>.vhost`

此文件夹包含指向conf.dispatcher.d/available_vhosts下的文件的相对符号链接。

创建这些符号链接所需的命令示例：

Apple macOS、Linux和WSL

```
ln -s ../available_vhosts/wknd.vhost wknd.vhost
```

Microsoft Windows

```
mklink wknd.vhost ..\available_vhosts\wknd.vhost
```

>[!NOTE]
>
> 在Windows下使用符号链接时，您应在提升权限的命令提示符下、Windows Subsystem for Linux中运行，或分配了[创建符号链接](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links)权限。

* `conf.d/rewrites/rewrite.rules`

该文件包含在`.vhost`文件内。 它有一组`mod_rewrite`的重写规则。

* `conf.d/variables/custom.vars`

该文件包含在`.vhost`文件内。 您可以在此位置添加对Apache变量的定义。

* `conf.d/variables/global.vars`

该文件包含在`dispatcher_vhost.conf`文件内。 您可以在此文件中更改Dispatcher并重写日志级别。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以有一个或多个此类文件，这些文件包含与主机名匹配的场，并允许Dispatcher模块使用不同的规则处理每个场。 文件在`available_farms`目录中创建，并使用`enabled_farms`目录中的符号链接启用。 从`.farm`文件中包括筛选器、缓存规则和其他文件等其他文件。

* `conf.dispatcher.d/enabled_farms/<CUSTOMER_CHOICE>.farm`

此文件夹包含指向conf.dispatcher.d/available_farms下文件的相对符号链接。

创建这些符号链接所需的命令示例：

Apple macOS、Linux和WSL

```
ln -s ../available_farms/wknd.farm wknd.farm
```

Microsoft Windows

```
mklink wknd.farm ..\available_farms\wknd.farm
```

>[!NOTE]
>
> 在Windows下使用符号链接时，您应在提升权限的命令提示符下、Windows Subsystem for Linux中运行，或分配了[创建符号链接](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links)权限。

* `conf.dispatcher.d/cache/rules.any`

该文件包含在`.farm`文件内。 它指定高速缓存首选项。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

该文件包含在`.farm`文件内。 它指定应将哪些请求标头转发到后端。

* `conf.dispatcher.d/filters/filters.any`

该文件包含在`.farm`文件内。 它有一组规则，这些规则更改了应过滤掉的流量而不应将其发送到后端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

该文件包含在`.farm`文件内。 它包含要通过glob匹配匹配的主机名或URI路径的列表。 此匹配可确定用于为请求提供服务的后端。

* `opt-in/USE_SOURCES_DIRECTLY`

此文件实现了更灵活的Dispatcher配置，并删除了以前对文件数量和大小的限制。 它还促使SDK和运行时以改进的方式验证和部署配置。

上述文件引用了下面列出的不可变配置文件。 云环境中的Dispatcher不会处理对不可变文件的更改。

**不可变配置文件**

这些文件是基本框架的一部分，用于执行标准和最佳实践。 这些文件被视为不可变，因为在本地修改或删除它们不会对您的部署产生影响，因为它们不会传输到您的云实例。

建议上述文件引用下面列出的不可变文件，然后引用任何其他语句或覆盖。 将Dispatcher配置部署到云环境时，无论在本地开发中使用了什么版本，都会使用最新版本的不可变文件。

* `conf.d/available_vhosts/default.vhost`

包含示例虚拟主机。 对于您自己的虚拟主机，请创建此文件的副本，对其进行自定义，转到`conf.d/enabled_vhosts`并创建指向您的自定义副本的符号链接。
不要将default.vhost文件直接复制到`conf.d/enabled_vhosts`。

确保始终有与Dispatcher失效所需的ServerAlias `\*.local`、`localhost`和`127.0.0.1`匹配的虚拟主机可用。 内部Adobe进程需要服务器别名`*.adobeaemcloud.net`和`*.adobeaemcloud.com`。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用于说明如何包含虚拟主机和全局变量。

* `conf.d/rewrites/default_rewrite.rules`

重写默认规则适用于标准项目。 如果需要自定义，请修改`rewrite.rules`。 在自定义设置中，如果默认规则符合您的需求，您仍然可以首先包含这些规则。

* `conf.dispatcher.d/available_farms/default.farm`

包含一个Dispatcher场示例。 对于您自己的场，创建此文件的副本，对其进行自定义，转到`conf.d/enabled_farms`并创建指向您的自定义副本的符号链接。

* `conf.dispatcher.d/cache/default_invalidate.any`

基础框架的一部分，在启动时生成。 您是&#x200B;**必需的**，才能将此文件包含在您定义的每个场的`cache/allowedClients`部分中。

* `conf.dispatcher.d/cache/default_rules.any`

适用于标准项目的默认缓存规则。 如果需要自定义，请修改`conf.dispatcher.d/cache/rules.any`。 在自定义设置中，如果默认规则符合您的需求，您仍然可以首先包含这些规则。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

转发到后端的默认请求标头，适用于标准项目。 如果需要自定义，请修改`clientheaders.any`。 在自定义设置中，您仍然可以首先包含默认请求标头（如果它们符合您的需要）。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用于说明如何包含您的Dispatcher场。

* `conf.dispatcher.d/filters/default_filters.any`

适用于标准项目的默认筛选器。 如果需要自定义，请修改`filters.any`。 在自定义设置中，如果默认筛选器符合您的需求，您仍可以首先包含这些筛选器。

* `conf.dispatcher.d/renders/default_renders.any`

作为基本框架的一部分，此文件将在启动时生成。 您是&#x200B;**必需的**，才能将此文件包含在您定义的每个场的`renders`部分中。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

适用于标准项目的默认主机通配。 如果需要自定义，请修改`virtualhosts.any`。 在自定义设置中，不应包含默认主机通配符，因为它与&#x200B;**every**&#x200B;传入请求匹配。

## 支持的 Apache 模块 {#apache-modules}

请参阅[支持的Apache模块](/help/implementing/dispatcher/disp-overview.md#supported-directives)。

## 本地验证 {#local-validation-flexible-mode}

>[!NOTE]
>
>以下部分包含使用Mac或Linux® SDK版本的命令，但Windows SDK也可以以类似方式使用。

使用`validate.sh`脚本，如下所示：

```
$ validate.sh src/dispatcher
opt-in USE_SOURCES_DIRECTLY marker file detected
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv not found in deployment folder: /Users/foo/src - using files in 'conf.d' and 'conf.dispatcher.d' subfolders directly
processing configuration subfolder: conf.d
processing configuration subfolder: conf.dispatcher.d
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until localhost is available
localhost resolves to ::1
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {

... 

}
Syntax OK
Phase 2 finished
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt

...

no immutable file has been changed - check is SUCCESSFUL
Phase 3 finished
```

该脚本包含以下三个阶段：

1. 它运行验证器。 如果配置无效，脚本将失败。
2. 它会执行`httpd -t`命令来测试语法是否正确，以便Apache httpd可以启动。 如果成功，配置应准备好进行部署。
3. 检查Dispatcher SDK配置文件的子集是否未修改，是否与当前SDK版本匹配，这些文件将按照[文件结构部分](##flexible-mode-file-structure)中的说明不可更改。

在Cloud Manager部署期间，还将运行`httpd -t`语法检查，并且所有错误都包含在Cloud Manager `Build Images step failure`日志中。

>[!NOTE]
>
>请参阅[自动重新加载和验证](#automatic-loading)部分，了解在每次配置修改后运行`validate.sh`的有效替代方法。

### 阶段1 {#first-phase}

如果未列入允许列表指令，则该工具会记录错误并返回非零退出代码。 此外，它还会进一步扫描模式为`conf.dispatcher.d/enabled_farms/*.farm`的所有文件并检查：

* 不存在使用允许通过`/glob`的筛选器规则（有关更多详细信息，请参阅[CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)）。
* 没有公开管理员功能。 例如，访问路径，如`/crx/de or /system/console`。

验证工具仅报告未被列入允许列表的Apache指令被禁止使用的情况。 它不会报告Apache配置的语法或语义问题，因为此信息仅对运行环境中的Apache模块可用。

下面提供了用于调试该工具输出的常见验证错误的故障排除技术：

**在存档中找不到`conf.dispatcher.d`子文件夹**

您的存档应包含文件夹 `conf.d` 和 `conf.dispatcher.d`。 请注意，您不应 **在**&#x200B;存档 `etc/httpd` 中使用前缀。

**在`conf.dispatcher.d/enabled_farms`**&#x200B;中找不到任何场

您启用的场应位于所述子文件夹中。

**包含的文件(...)必须命名为： ...**

您的场配置中有两个部分，**必须**包含
特定文件： `/cache`部分中的`/renders`和`/allowedClients`。 这些
部分必须如下所示：

```
/renders {
    $include "../renders/default_renders.any"
}
```

和：

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**文件包含在未知位置： ...**

您的场配置中有四个部分，允许您包含自己的文件：`/cache`部分中的`/clientheaders`、`filters`、`/rules`以及`/virtualhosts`。 包含的文件必须按如下方式命名：

| 分区 | 包括文件名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包含这些文件的&#x200B;**default**&#x200B;版本，其名称前面加有单词`default_`，例如`../filters/default_filters.any`。

**Include语句位于(...)，位于任何已知位置之外： ...**

除上述六节外，严禁使用
例如，要使用`$include`语句，以下语句将生成此错误：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**不包括……**&#x200B;中允许的客户端/渲染器

当您未在`/cache`部分中为`/renders`和`/allowedClients`指定“include”时，将生成此错误。 请参阅
**包含的文件(...)必须命名为： ...**&#x200B;节，以获取更多信息。

**筛选器不能使用glob模式以允许请求**

允许具有`/glob`样式规则的请求是不安全的，例如，

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此语句旨在允许请求`css`个文件，但它也允许请求后面跟查询字符串`?a=.css`的&#x200B;**任意**&#x200B;资源。 因此，禁止使用此类过滤器（另见CVE-2016-0957）。

**包含的文件(...)不匹配任何已知文件**

默认情况下，可以将Apache虚拟主机配置中的两种文件类型指定为包含：重写和变量。

| 类型 | 包括文件名 |
|-----------|---------------------------------|
| 重写 | `conf.d/rewrites/rewrite.rules` |
| 变量 | `conf.d/variables/custom.vars` |

在灵活模式下，还可以包含其他文件，只要它们位于前缀为`conf.d`目录的子目录（在任何级别）中，如下所示。

| 包括文件上目录前缀 |
|-------------------------------------|
| `conf.d/includes` |
| `conf.d/modsec` |
| `conf.d/rewrites` |

例如，您可以在`conf.d/includes`目录下的某个已创建目录中包含一个文件，如下所示：

```
Include conf.d/includes/mynewdirectory/myincludefile.conf
```

或者，您也可以包含重写规则的&#x200B;**default**&#x200B;版本，其名称为`conf.d/rewrites/default_rewrite.rules`。
请注意，变量文件没有默认版本。

**检测到已弃用的配置布局，正在启用兼容模式**

此消息指示您的配置具有已弃用的版本1布局，其中包含完整的
带有`ams_`前缀的Apache配置和文件。 而向后仍支持此配置
兼容性，您应该切换到新布局。

第一个阶段也可以是&#x200B;**单独运行**，而不是从包装器`validate.sh`脚本运行。

当针对maven工件或`dispatcher/src`子目录运行时，它会报告验证失败：

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

在Windows上，Dispatcher验证器区分大小写。 因此，如果您不遵守配置所在路径的大小写，例如：

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

通过从Windows资源管理器复制并粘贴路径，然后在命令提示符下使用`cd`命令将该路径复制并粘贴来避免此错误。

### 阶段2 {#second-phase}

此阶段通过在Docker容器中启动Apache HTTPD来检查Apache语法。 必须本地安装Docker，但请注意，AEM不需要运行。

>[!NOTE]
>
>Windows用户必须使用支持Docker的Windows 10 Professional或其他分发。 此要求是在本地计算机上运行和调试Dispatcher的先决条件。
>对于Windows和macOS，Adobe建议使用Docker桌面。

此阶段也可以通过`bin/docker_run.sh src/dispatcher host.docker.internal:4503 8080`独立运行。

在Cloud Manager部署期间，还将运行`httpd -t`语法检查，并且任何错误都包含在Cloud Manager生成图像步骤失败日志中。

### 阶段3 {#third-phase}

如果在此阶段失败，则表示Adobe更改了一个或多个不可变文件。 在这种情况下，您必须将相应的不可变文件替换为SDK `src`目录中交付的新版本。 以下日志示例说明了此问题：

```
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt
(...)
checking existing 'conf.dispatcher.d/clientheaders/default_clientheaders.any' for changes
immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed:
--- /etc/httpd/conf.dispatcher.d/clientheaders/default_clientheaders.any
+++ /etc/httpd-actual/conf.dispatcher.d/clientheaders/default_clientheaders.any
@@ -40,4 +40,3 @@
"Sling-uploadmode"
"x-requested-with"
"If-Modified-Since"
-"Authorization"
** error: immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed!
  
```

此阶段也可以通过`bin/docker_immutability_check.sh src/dispatcher`独立运行。

本地不可变文件可以通过在Dispatcher文件夹上运行`bin/update_maven.sh src/dispatcher`脚本来更新，其中`src/dispatcher`是Dispatcher配置目录。 此脚本还会更新父目录中的任何`pom.xml`文件，以便同时更新maven不可变性检查。

## 调试Apache和Dispatcher配置 {#debugging-apache-and-dispatcher-configuration}

您可以使用`./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`在本地运行Apache Dispatcher。

如前所述，必须本地安装Docker，AEM不需要运行。 Windows用户必须使用支持Docker的Windows 10 Professional或其他分发。 此要求是在本地计算机上运行和调试Dispatcher的先决条件。

以下策略可用于增加Dispatcher模块的日志输出，并查看本地和云环境中`RewriteRule`评估的结果。

这些模块的日志级别由变量`DISP_LOG_LEVEL`和`REWRITE_LOG_LEVEL`定义。 可以在文件`conf.d/variables/global.vars`中设置它们。 其相关部分如下：

```
# Log level for the dispatcher
#
# Possible values are: error, warn, info, debug and trace1
# Default value: warn
#
# Define DISP_LOG_LEVEL warn
 
# Log level for mod_rewrite
#
# Possible values are: error, warn, info, debug and trace1 - trace8
# Default value: warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL warn
```

在本地运行Dispatcher时，日志将直接打印到终端输出中。 大多数情况下，希望这些日志处于DEBUG状态，可通过在运行Docker时将Debug级别作为参数传递来完成此操作。 例如：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`。

云环境的日志将通过Cloud Manager中提供的日志记录服务公开。

>[!NOTE]
>
>对于AEM as a Cloud Service上的环境，debug是最高详细级别。 不支持跟踪日志级别，因此当在云环境中工作时，应避免设置跟踪日志级别。

### 自动重新加载和验证 {#automatic-reloading}

>[!NOTE]
>
>由于Windows操作系统的限制，此功能仅适用于macOS和Linux®用户。

每次修改配置时，您不必运行本地验证(`validate.sh`)并启动Docker容器(`docker_run.sh`)，而是可以运行`docker_run_hot_reload.sh`脚本。 该脚本会监视对配置的任何更改，并自动重新加载它并重新运行验证。 通过使用此选项，您可以在调试时节省大量时间。

您可以使用以下命令运行脚本： `./bin/docker_run_hot_reload.sh src/dispatcher host.docker.internal:4503 8080`

输出的第一行看起来与`docker_run.sh`运行的结果类似。 例如：

```
~ bin/docker_run_hot_reload.sh src host.docker.internal:8081 8082
opt-in USE_SOURCES_DIRECTLY marker file detected
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/15-check-pod-name.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until host.docker.internal is available
host.docker.internal resolves to 192.168.65.2
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
Running script /docker_entrypoint.d/80-frontend-domain.sh
Running script /docker_entrypoint.d/zzz-import-sdk-config.sh
WARN Mon Jul  4 09:53:54 UTC 2022: Pseudo symlink conf.d seems to point to a non-existing file!
INFO Mon Jul  4 09:53:55 UTC 2022: Copied customer configuration to /etc/httpd.
INFO Mon Jul  4 09:53:55 UTC 2022: Start testing
Cloud manager validator 2.0.43
2022/07/04 09:53:55 No issues found
INFO Mon Jul  4 09:53:55 UTC 2022: Testing with fresh base configuration files.
INFO Mon Jul  4 09:53:55 UTC 2022: Apache httpd informationServer version: Apache/2.4.54 (Unix)
```

### 注入自定义环境变量 {#environment-variables}

自定义环境变量可以与Dispatcher SDK一起使用，方法是先在单独的文件中设置这些变量，然后在启动本地Dispatcher之前在`ENV_FILE`环境变量中引用它们。

包含自定义环境变量的文件如下所示：

```
COMMERCE_ENDPOINT=commerce-host
AEM_HTTP_PROXY_HOST=host.docker.internal
AEM_HTTP_PROXY_PORT=8000
```

并且它可以通过以下命令在本地Dispatcher SDK中使用：

```
export ENV_FILE=custom.env
./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080
```

## 每个环境不同的Dispatcher配置 {#different-dispatcher-configurations-per-environment}

目前，相同的Dispatcher配置适用于AEM as a Cloud Service上的所有环境。 运行时具有包含当前运行模式（开发、暂存或生产）和“定义”的环境变量`ENVIRONMENT_TYPE`。 “define”可以是`ENVIRONMENT_DEV`、`ENVIRONMENT_STAGE`或`ENVIRONMENT_PROD`。 在Apache配置中，可直接在表达式中使用变量。 或者，“define”可用于构建逻辑：

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

在Dispatcher配置中，相同的环境变量可用。 如果需要更多逻辑，请定义上述示例中显示的变量，然后在Dispatcher配置部分中使用它们：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

或者，您可以在httpd/dispatcher配置中使用Cloud Manager环境变量，但不要使用环境密钥。 如果某个程序具有多个开发环境，并且其中某些开发环境的httpd/dispatcher配置值不同，则此方法尤为重要。 将使用与上述示例中相同的${VIRTUALHOST}语法，但不会使用上述变量文件中的Define声明。 有关配置Cloud Manager环境变量的说明，请阅读[Cloud Manager文档](/help/implementing/cloud-manager/environment-variables.md)。

在本地测试您的配置时，您可以通过将变量`DISP_RUN_MODE`直接传递到`docker_run.sh`脚本来模拟不同的环境类型：

```
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
```

不传入DISP_RUN_MODE的值时的缺省运行模式为“dev”。
要获得可用选项和变量的完整列表，请运行不带参数的脚本`docker_run.sh`。

## 查看Docker容器正在使用的Dispatcher配置 {#viewing-dispatcher-configuration-in-use-by-docker-container}

使用特定于环境的配置，可能很难确定实际的Dispatcher配置是什么样的。 使用`docker_run.sh`启动Docker容器后，可按如下方式转储：

* 确定正在使用的Docker容器ID：

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

## 从旧模式迁移到灵活模式 {#migrating}

在Cloud Manager 2021.7.0版本中，新的Cloud Manager程序将生成具有[AEM原型28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)或更高版本的Maven项目结构，其中包括文件&#x200B;**opt-in/USE_SOURCES_DIRECTLY**。 它删除了[旧模式](/help/implementing/dispatcher/validation-debug-legacy.md)以前对文件数量和大小的限制，还导致SDK和运行时以改进的方式验证和部署配置。 如果您的Dispatcher配置没有此文件，强烈建议您迁移。 请使用以下步骤确保安全过渡：

1. **本地测试。**&#x200B;使用最新的Dispatcher tools SDK，添加文件夹和文件`opt-in/USE_SOURCES_DIRECTLY`。 按照本文中的“本地验证”说明进行操作，以便测试Dispatcher是否可以在本地工作。
1. **云开发测试：**
   * 将文件`opt-in/USE_SOURCES_DIRECTLY`提交到非生产管道部署到云开发环境的Git分支。
   * 使用Cloud Manager部署到云开发环境。
   * 彻底测试。 在将更改部署到更高环境之前，务必要验证Apache和Dispatcher配置是否按预期运行。 检查与自定义配置相关的所有行为。 如果您认为部署的Dispatcher配置不反映您的自定义配置，请提交客户支持工单。

   >[!NOTE]
   >
   >在灵活模式下，您应该使用相对路径而不是绝对路径。
1. **部署到生产：**
   * 将文件`opt-in/USE_SOURCES_DIRECTLY`提交到由生产管道部署到云暂存和生产环境的Git分支。
   * 使用Cloud Manager部署到暂存环境。
   * 彻底测试。 在将更改部署到更高环境之前，务必要验证Apache和Dispatcher配置是否按预期运行。 检查与自定义配置相关的所有行为。 如果您认为部署的Dispatcher配置不反映您的自定义配置，请提交客户支持工单。
   * 使用Cloud Manager继续部署到生产环境。
