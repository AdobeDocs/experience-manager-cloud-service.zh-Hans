---
title: 使用 Dispatcher 工具进行验证和调试
description: 使用 Dispatcher 工具进行验证和调试
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
source-git-commit: 6f80c6d32d3eca1b0ef2977c740ef043529fab96
workflow-type: tm+mt
source-wordcount: '2653'
ht-degree: 2%

---

# 使用 Dispatcher 工具进行验证和调试 {#Dispatcher-in-the-cloud}

## 简介 {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>有关云中的Dispatcher以及如何下载Dispatcher工具的更多信息，请参阅 [云中的调度程序](/help/implementing/dispatcher/disp-overview.md) 页面。 如果您的调度程序配置处于旧版模式，请参阅 [旧模式文档](/help/implementing/dispatcher/validation-debug-legacy.md).

以下各节介绍了灵活模式的文件结构、本地验证、调试以及从旧版模式迁移到灵活模式。

本文假定项目的调度程序配置包含文件 `opt-in/USE_SOURCES_DIRECTLY`，这会导致SDK和运行时以与旧版模式相比的改进方式验证和部署配置，从而消除对文件数量和大小的限制。

因此，如果调度程序配置不包含上述文件，则 **强烈推荐** 模式迁移到灵活模式(如 [从旧版模式迁移到灵活模式](#migrating) 中。

## 文件结构 {#flexible-mode-file-structure}

项目的Dispatcher子文件夹的结构如下所示：

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
│── opt-in
│   └── USE_SOURCES_DIRECTLY
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
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

以下是可修改的显着文件说明：

**可自定义的文件**

以下文件是可自定义的，并将在部署时传输到您的云实例：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以拥有一个或多个这些文件。 包含 `<VirtualHost>` 匹配主机名并允许Apache使用不同规则处理每个域流量的条目。 文件是在 `available_vhosts` 目录，并在中通过符号链接启用 `enabled_vhosts` 目录访问Advertising Cloud的帮助。 从 `.vhost` 将包含文件、重写和变量等其他文件。

>[!NOTE]
>
>在灵活模式下，您应使用相对路径而不是绝对路径。

* `conf.d/rewrites/rewrite.rules`

此文件包含在 `.vhost` 文件。 它有一套重写规则 `mod_rewrite`.

* `conf.d/variables/custom.vars`

此文件包含在 `.vhost` 文件。 您可以在此位置为Apache变量添加定义。

* `conf.d/variables/global.vars`

此文件包含于 `dispatcher_vhost.conf` 文件。 您可以更改Dispatcher并重写此文件中的日志级别。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以具有一个或多个这些文件，并且它们包含场以匹配主机名，并允许调度程序模块使用不同的规则处理每个场。 文件是在 `available_farms` 目录，并在中通过符号链接启用 `enabled_farms` 目录访问Advertising Cloud的帮助。 从 `.farm` 将包含文件、过滤器、缓存规则等其他文件。

* `conf.dispatcher.d/cache/rules.any`

此文件包含在 `.farm` 文件。 它指定缓存首选项。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此文件包含在 `.farm` 文件。 它指定应将哪些请求标头转发到后端。

* `conf.dispatcher.d/filters/filters.any`

此文件包含在 `.farm` 文件。 它有一组规则，用于更改应过滤掉的流量，而不是将流量发送到后端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此文件包含在 `.farm` 文件。 它有一个主机名或要通过全局匹配进行匹配的URI路径列表。 这可确定要用于提供请求的后端。

* `opt-in/USE_SOURCES_DIRECTLY`

此文件支持更灵活的调度程序配置，并消除了以前对文件数量和大小的限制。 它还会导致SDK和运行时以改进的方式验证和部署配置。

上述文件引用下面列出的不可更改配置文件。 云环境中的Dispatcher将不会处理对不可变文件所做的更改。

**不可变配置文件**

这些文件是基本框架的一部分，可实施标准和最佳实践。 这些文件被视为不可更改，因为在本地修改或删除它们不会对您的部署产生任何影响，因为它们将不会传输到您的云实例。

建议上述文件引用下面列出的不可变文件，然后引用任何其他语句或覆盖。 将Dispatcher配置部署到云环境后，无论本地开发中使用的是哪个版本，都会使用最新版本的不可变文件。

* `conf.d/available_vhosts/default.vhost`

包含一个示例虚拟主机。 对于您自己的虚拟主机，请创建此文件的副本并对其进行自定义，然后转到 `conf.d/enabled_vhosts` 并创建指向自定义副本的符号链接。

确保虚拟主机始终可用，与ServerAlias匹配 `\*.local` 以及内部Adobe进程所需的本地主机。

* `conf.d/dispatcher_vhost.conf`

基础框架的一部分，用于说明如何包含虚拟主机和全局变量。

* `conf.d/rewrites/default_rewrite.rules`

适用于标准项目的默认重写规则。 如果需要自定义，请修改 `rewrite.rules`. 在自定义中，如果默认规则符合您的需求，您仍可以先包含这些规则。

* `conf.dispatcher.d/available_farms/default.farm`

包含示例Dispatcher场。 对于您自己的场，请创建此文件的副本并对其进行自定义，然后转到 `conf.d/enabled_farms` 并创建指向自定义副本的符号链接。

* `conf.dispatcher.d/cache/default_invalidate.any`

作为基础框架的一部分，将在启动时生成。 您是 **必需** 要在您定义的每个场中包含此文件，请在 `cache/allowedClients` 中。

* `conf.dispatcher.d/cache/default_rules.any`

适用于标准项目的默认缓存规则。 如果需要自定义，请修改 `conf.dispatcher.d/cache/rules.any`. 在自定义中，如果默认规则符合您的需求，您仍可以先包含这些规则。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

要转发到后端（适用于标准项目）的默认请求标头。 如果需要自定义，请修改 `clientheaders.any`. 在自定义中，如果默认请求标头符合您的需求，您仍可以先包含它们。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用于说明如何包含调度程序场。

* `conf.dispatcher.d/filters/default_filters.any`

适用于标准项目的默认过滤器。 如果需要自定义，请修改 `filters.any`. 在自定义中，如果默认过滤器符合您的需求，您仍可以先包含这些过滤器。

* `conf.dispatcher.d/renders/default_renders.any`

作为基本框架的一部分，此文件将在启动时生成。 您是 **必需** 要在您定义的每个场中包含此文件，请在 `renders` 中。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

适用于标准项目的默认主机代换。 如果需要自定义，请修改 `virtualhosts.any`. 在自定义中，您不应包含默认的代换主机，因为它与 **每个** 传入请求。

## 支持的Apache模块 {#apache-modules}

请参阅 [支持的Apache模块](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## 本地验证 {#local-validation-flexible-mode}

>[!NOTE]
>
>以下部分包括使用Mac或Linux版本的SDK的命令，但Windows SDK也可以以类似的方式使用。

使用 `validate.sh` 脚本，如下所示：

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

该脚本分为以下三个阶段：

1. 它运行验证器。 如果配置无效，脚本将失败。
2. 它执行 `httpd -t` 命令来测试语法是否正确，以便apache httpd可以启动。 如果成功，配置应准备好进行部署。
3. 检查Dispatcher SDK配置文件的子集，这些文件的子集不可更改，如 [文件结构部分](##flexible-mode-file-structure)，尚未修改。

在Cloud Manager部署期间， `httpd -t` 语法检查也会执行，并且Cloud Manager中会包含任何错误 `Build Images step failure` 日志。

>[!NOTE]
>
>请参阅 [自动加载和验证](#automatic-loading) 部分，以了解运行 `validate.sh` 在每次配置修改后。

### 阶段1 {#first-phase}

如果未指列入允许列表令，该工具将记录错误并返回非零退出代码。 此外，它还以模式扫描所有文件 `conf.dispatcher.d/enabled_farms/*.farm` 并检查：

* 不存在通过 `/glob` (请参阅 [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) 以了解更多详细信息。
* 未显示管理员功能。 例如，对路径(如 `/crx/de or /system/console`.

请注意，验证工具仅报告未的Apache指令的禁止使列入允许列表用。 它不会报告Apache配置的语法或语义问题，因为此信息仅适用于运行环境中的Apache模块。

以下是调试工具输出的常见验证错误的故障诊断技术：

**无法找到 `conf.dispatcher.d` 存档中的子文件夹**

您的存档应包含文件夹 `conf.d` 和 `conf.dispatcher.d`。 请注意，您不应 **在**&#x200B;存档 `etc/httpd` 中使用前缀。

**在中找不到任何场`conf.dispatcher.d/enabled_farms`**

您已启用的场应位于上述子文件夹中。

**包含的文件(...)必须命名为：...**

您的场配置中有两个部分： **必须** 包括特定文件： `/renders` 和 `/allowedClients` 在 `/cache` 中。 这些部分必须如下所示：

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

场配置中有四个部分，允许您在其中包含自己的文件： `/clientheaders`, `filters`, `/rules` in `/cache` 部分和 `/virtualhosts`. 所包含的文件需要命名如下：

| 区域 | 包含文件名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包 **含这些文件的默认版本** ，其名称前面加有单词 `default_`，如 `../filters/default_filters.any`.

**在任何已知位置之外的(...)包含语句：...**

除上文各段所述的六个部分外，您不得使用 `$include` 语句，例如，以下内容将生成此错误：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允许的客户端/呈现器不包括在以下位置：...**

如果未为指定包含，则会生成此错误 `/renders` 和 `/allowedClients` 在 `/cache` 中。 请参阅
**包含的文件(...)必须命名为：...** 的子菜单。

**筛选器不得使用全局模式来允许请求**

允许使用 `/glob` 样式规则，与完整的请求行(例如，

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此语句用于允许 `css` 文件，但它也允许请求 **any** 资源后跟查询字符串 `?a=.css`. 因此，禁止使用此类过滤器（另请参阅CVE-2016-0957）。

**包含的文件(...)与任何已知文件都不匹配**

Apache虚拟主机配置中有两种类型的文件可指定为：重写和变量。
所包含的文件需要命名如下：

| 类型 | 包含文件名 |
|-----------|---------------------------------|
| 重写 | `conf.d/rewrites/rewrite.rules` |
| 变量 | `conf.d/variables/custom.vars` |

或者，您也可以将 **默认** 重写规则的版本，其名称为 `conf.d/rewrites/default_rewrite.rules`.
请注意，变量文件没有默认版本。

**检测到已弃用的配置布局，启用兼容性模式**

此消息表示您的配置具有已弃用的版本1布局，其中包含完整的Apache配置和 `ams_` 前缀。 虽然向后兼容性仍支持这种方式，但您应切换到新布局。

请注意，第一阶段也可以 **单独运行**，而不是包装器中的 `validate.sh` 脚本。

在你的玛文藏物或 `dispatcher/src` 子目录，它将报告验证失败：

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

在Windows上，调度程序验证器区分大小写。 因此，如果您不遵循配置所在路径的大小写，则可能无法验证配置，例如：

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

通过从Windows资源管理器复制并粘贴路径，然后在命令提示符下使用 `cd` 命令进入该路径。

### 阶段2 {#second-phase}

此阶段通过在图像中启动Docker来检查Apache语法。 Docker必须安装在本地，但请注意，AEM无需运行。

>[!NOTE]
>
>Windows用户需要使用支持Docker的Windows 10专业版或其他发行版。 这是在本地计算机上运行和调试Dispatcher的先决条件。

此阶段也可以单独运行 `bin/docker_run.sh src/dispatcher host.docker.internal:4503 8080`.

在Cloud Manager部署期间， `httpd -t` 语法检查也会执行，并且任何错误都将包含在Cloud Manager“生成图像”步骤失败日志中。

### 阶段3 {#third-phase}

如果此阶段出现故障，则意味着Adobe已更改一个或多个不可变文件，您必须将相应不可变文件替换为 `src` SDK目录。 以下日志示例说明了此问题：

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

此阶段也可以单独运行 `bin/docker_immutability_check.sh src/dispatcher`.

## 调试Apache和Dispatcher配置 {#debugging-apache-and-dispatcher-configuration}

请注意，您可以使用 `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

如前所述，Docker必须安装在本地，并且AEM无需运行。 Windows用户需要使用支持Docker的Windows 10专业版或其他发行版。 这是在本地计算机上运行和调试Dispatcher的先决条件。

以下策略可用于增加Dispatcher模块的日志输出并查看 `RewriteRule` 在本地和云环境中进行评估。

这些模块的日志级别由变量定义 `DISP_LOG_LEVEL` 和 `REWRITE_LOG_LEVEL`. 可以在文件中设置它们 `conf.d/variables/global.vars`. 其相关部分如下：

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

在本地运行Dispatcher时，日志会直接打印到终端输出。 大多数情况下，您希望这些日志处于DEBUG中，这可以通过在运行Docker时将调试级别作为参数传递来完成。 例如：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`。

云环境的日志通过Cloud Manager中提供的日志记录服务公开。

### 自动加载和验证 {#automatic-loading}

>[!NOTE]
>
>由于Windows操作系统限制，此功能仅适用于Linux用户。

而不是运行本地验证(`validate.sh`)和启动Docker容器(`docker_run.sh`)每次修改配置时，您也可以 `docker_run_hot_reload.sh` 脚本。  脚本会监视对配置的任何更改，并自动重新加载该配置并重新运行验证。 使用此选项，可在调试时节省大量时间。

您可以使用以下命令运行脚本： `./bin/docker_run_hot_reload.sh src/dispatcher host.docker.internal:4503 8080`

请注意，第一行输出将类似于为 `docker_run.sh`，例如：

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

## 每个环境的不同Dispatcher配置 {#different-dispatcher-configurations-per-environment}

当前，相同的Dispatcher配置适用于所有AEMas a Cloud Service环境。 运行时将具有一个环境变量 `ENVIRONMENT_TYPE` 包含当前运行模式（dev、stage或prod）以及定义的活动。 定义可以是 `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` 或 `ENVIRONMENT_PROD`. 在Apache配置中，变量可以直接在表达式中使用。 或者，也可以使用定义来构建逻辑：

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

或者，您也可以在httpd/dispatcher配置中使用Cloud Manager环境变量，但不能使用环境密钥。 如果某个程序具有多个开发环境，并且其中某些开发环境的httpd/dispatcher配置值不同，则此方法尤为重要。 与上面的示例一样，会使用相同的${VIRTUALHOST}语法，但不会使用上述变量文件中的Define声明。 阅读 [Cloud Manager文档](/help/implementing/cloud-manager/environment-variables.md) 有关配置Cloud Manager环境变量的说明。

在本地测试配置时，您可以通过传递变量来模拟不同的环境类型 `DISP_RUN_MODE` 到 `docker_run.sh` 直接脚本：

```
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
```

未传入DISP_RUN_MODE值时，默认运行模式为“dev”。
有关可用选项和变量的完整列表，请运行脚本 `docker_run.sh` 没有参数。

## 查看Docker容器正在使用的Dispatcher配置 {#viewing-dispatcher-configuration-in-use-by-docker-container}

对于特定于环境的配置，可能很难确定实际的Dispatcher配置。 启动Docker容器后， `docker_run.sh` 可以按如下方式倾弃：

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

## 从旧版模式迁移到灵活模式 {#migrating}

在Cloud Manager 2021.7.0版本中，新的Cloud Manager计划通过 [AEM原型28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) 或更高版本，包括文件 **选择加入/USE_SOURCES_DIRECTLY**. 这消除了 [旧模式](/help/implementing/dispatcher/validation-debug-legacy.md) 大小，还会导致SDK和运行时以改进的方式验证和部署配置。 如果您的调度程序配置没有此文件，强烈建议您迁移。 请执行以下步骤以确保安全过渡：

1. **本地测试。** 使用最新的调度程序工具SDK，添加文件夹和文件 `opt-in/USE_SOURCES_DIRECTLY`. 按照本文中的“本地验证”说明来测试调度程序是否在本地工作。
1. **云开发测试：**
   * 提交文件 `opt-in/USE_SOURCES_DIRECTLY` 到由非生产管道部署到云开发环境的git分支。
   * 使用Cloud Manager部署到云开发环境。
   * 彻底测试。 在将更改部署到更高环境之前，务必要验证Apache和Dispatcher配置是否按预期行事。 检查与您的自定义配置相关的所有行为！ 如果您认为已部署的Dispatcher配置不反映您的自定义配置，请提交客户支持票证。

   >[!NOTE]
   >
   >在灵活模式下，您应使用相对路径而不是绝对路径。
1. **部署到生产环境：**
   * 提交文件 `opt-in/USE_SOURCES_DIRECTLY` 到由生产管道部署到云暂存和生产环境的git分支。
   * 使用Cloud Manager部署到暂存环境。
   * 彻底测试。 在将更改部署到更高环境之前，务必要验证Apache和Dispatcher配置是否按预期行事。 检查与您的自定义配置相关的所有行为！ 如果您认为已部署的Dispatcher配置不反映您的自定义配置，请提交客户支持票证。
   * 使用Cloud Manager继续将部署到生产环境。
