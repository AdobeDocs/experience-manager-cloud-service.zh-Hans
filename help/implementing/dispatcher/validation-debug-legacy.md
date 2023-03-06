---
title: 使用Dispatcher工具进行验证和调试（旧版）
description: 使用Dispatcher工具进行验证和调试（旧版）
feature: Dispatcher
hidefromtoc: true
exl-id: dc04d035-f002-42ef-9c2e-77602910c2ec
source-git-commit: 33dfe795140f2780f7f2cf876f3ebc725310214d
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 1%

---

# 使用Dispatcher工具进行验证和调试（旧版）  {#Dispatcher-tools-legacy}

## 简介 {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>有关云中Dispatcher以及如何下载Dispatcher工具的更多信息，请参阅 [云中的调度程序](/help/implementing/dispatcher/disp-overview.md) 页面。

以下部分介绍了旧版模式的文件结构、本地验证、调试以及如何从旧版模式迁移到 [柔性模式](/help/implementing/dispatcher/validation-debug.md).

本文假设您项目的Dispatcher配置不包含文件opt-in/USE_SOURCES_DIRECTLY。 因此，它对文件的数量和大小存在限制，例如：

* 必须使用的单个重写文件，而不是特定于站点的文件。
* 可自定义文件的内容总和必须小于1MB。

从Cloud Manager 2021.7.0版本开始，新的Cloud Manager程序会生成具有AEM原型28及更高版本的maven项目结构，其中包括上述文件。

它是 **强烈建议** ，您将从旧模式迁移到灵活模式，如迁移一节中所述 [从旧模式迁移到灵活模式](#migrating-flexible). 使用灵活模式还导致SDK和运行时以改进的方式验证和部署配置。

## 文件结构 {#legacy-mode-file-structure}

项目的Dispatcher子文件夹的结构（在旧版模式下）如下所示：

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
    │   ├── marketing_query_parameters.any
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

以下是可修改的显着文件的说明：

**可自定义的文件**

以下文件可自定义，将在部署时传输到您的云实例：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以拥有一个或多个这些文件。 它们包含 `<VirtualHost>` 条目匹配主机名，并允许Apache使用不同的规则处理每个域流量。 文件创建于 `available_vhosts` 目录，并通过中的符号链接启用 `enabled_vhosts` 目录。 从 `.vhost` 文件、重写和变量等其他文件将包括在内。

* `conf.d/rewrites/rewrite.rules`

此文件包含在 `.vhost` 文件。 它有一组重写规则 `mod_rewrite`.

>[!NOTE]
>
>目前，必须使用单个重写文件，而不是特定于站点的文件。 通常，可自定义文件的内容总和必须小于1MB。

* `conf.d/variables/custom.vars`

此文件包含在 `.vhost` 文件。 您可以在此位置添加针对Apache变量的定义。

* `conf.d/variables/global.vars`

此文件包含在 `dispatcher_vhost.conf` 文件。 您可以在此文件中更改Dispatcher并重写日志级别。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以有一个或多个这些文件，它们包含与主机名匹配的场，并允许Dispatcher模块使用不同的规则处理每个场。 文件创建于 `available_farms` 目录，并通过中的符号链接启用 `enabled_farms` 目录。 从 `.farm` 文件、过滤器、缓存规则等文件和其他文件将包括在内。

* `conf.dispatcher.d/cache/rules.any`

此文件包含在 `.farm` 文件。 它指定高速缓存首选项。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此文件包含在 `.farm` 文件。 它指定应将哪些请求标头转发到后端。

* `conf.dispatcher.d/filters/filters.any`

此文件包含在 `.farm` 文件。 它有一组规则，用于更改应该过滤掉的流量，而不是使其流向后端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此文件包含在 `.farm` 文件。 它包含要通过glob匹配匹配的主机名或URI路径的列表。 这决定了使用哪个后端来提供请求。

上述文件引用了下面列出的不可变配置文件。 云环境中的Dispatcher不会处理对不可变文件的更改。

**不可变配置文件**

这些文件是基本框架的一部分，并强制执行标准和最佳实践。 这些文件被视为不可变，因为在本地修改或删除它们将不会对您的部署产生影响，因为它们将不会传输到您的云实例。

建议上述文件引用下面列出的不可变文件，然后引用任何其他语句或覆盖。 将Dispatcher配置部署到云环境时，将使用不可变文件的最新版本，无论本地开发中使用了什么版本。

* `conf.d/available_vhosts/default.vhost`

包含一个示例虚拟主机。 对于您自己的虚拟主机，请创建此文件的副本，对其进行自定义，然后转到 `conf.d/enabled_vhosts` 和创建指向自定义副本的符号链接。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用于说明如何包含虚拟主机和全局变量。

* `conf.d/rewrites/default_rewrite.rules`

适用于标准项目的默认重写规则。 如果需要自定义，请修改 `rewrite.rules`. 在自定义设置中，如果默认规则符合您的需求，您仍然可以首先包含这些规则。

* `conf.dispatcher.d/available_farms/default.farm`

包含一个示例Dispatcher场。 对于您自己的场，创建此文件的副本，对其进行自定义，转到 `conf.d/enabled_farms` 和创建指向自定义副本的符号链接。

* `conf.dispatcher.d/cache/default_invalidate.any`

基础框架的一部分，在启动时生成。 您是 **必需** 要将此文件包含在您定义的每个场中，请在 `cache/allowedClients` 部分。

* `conf.dispatcher.d/cache/default_rules.any`

适用于标准项目的默认缓存规则。 如果需要自定义，请修改 `conf.dispatcher.d/cache/rules.any`. 在自定义设置中，如果默认规则符合您的需求，您仍然可以首先包含这些规则。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

转发到后端的默认请求标头，适用于标准项目。 如果需要自定义，请修改 `clientheaders.any`. 在自定义设置中，您仍然可以首先包含默认请求标头（如果它们符合您的需要）。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用于说明如何包含Dispatcher场。

* `conf.dispatcher.d/filters/default_filters.any`

适用于标准项目的默认筛选器。 如果需要自定义，请修改 `filters.any`. 在自定义设置中，如果默认筛选器符合您的需求，您仍可以首先包含这些筛选器。

* `conf.dispatcher.d/renders/default_renders.any`

作为基本框架的一部分，此文件将在启动时生成。 您是 **必需** 要将此文件包含在您定义的每个场中，请在 `renders` 部分。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

适用于标准项目的默认主机通配。 如果需要自定义，请修改 `virtualhosts.any`. 在自定义设置中，不应包含默认主机通配，因为它与默认主机通配 **每** 传入请求。

## 支持的 Apache 模块 {#apache-modules}

参见 [支持的Apache模块](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## 本地验证 {#local-validation-legacy-mode}

>[!NOTE]
>以下部分包含使用Mac或Linux版本的SDK的命令，但Windows SDK也可以以类似的方式使用。

使用 `validate.sh` 脚本，如下所示：

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv found in deployment folder: /tmp/dispatcher_validation_1625150390 - using files listed there
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

该脚本执行以下操作：

1. 它运行验证器。 如果配置无效，脚本将失败。
2. 它会执行 `httpd -t` 用于测试语法是否正确以使apache httpd可以启动的命令。 如果成功，配置应准备好进行部署。
3. 检查Dispatcher SDK配置文件的子集，该文件旨在不可变，如 [文件结构部分](##legacy-mode-file-structure)尚未修改。 这是随AEM SDK版本v2021.1.4738引入的新检查，其中还包含Dispatcher工具版本2.0.36。在此更新之前，客户可能错误地认为这些不可变文件的任何本地SDK修改也将应用于云环境。

在Cloud Manager部署期间， `httpd -t` 语法检查也将执行，所有错误都将包含在Cloud Manager中 `Build Images step failure` 日志。

### 阶段1 {#first-phase}

如果未列入允许列表指令，则该工具会记录错误并返回非零退出代码。 此外，它还进一步扫描所有具有模式的文件 `conf.dispatcher.d/enabled_farms/*.farm` 并检查：

* 不存在使用允许通过以下方式访问的筛选规则 `/glob` (请参阅 [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) 了解更多详细信息。
* 未公开任何管理功能。 例如，访问路径，如 `/crx/de or /system/console`.

请注意，验证工具仅报告禁止使用尚未列入允许列表的Apache指令。 它不会报告Apache配置的语法或语义问题，因为此信息仅对运行环境中的Apache模块可用。

下面提供了用于调试工具输出的常见验证错误的故障排除技术：

**找不到 `conf.dispatcher.d` 存档中的子文件夹**

您的存档应包含文件夹 `conf.d` 和 `conf.dispatcher.d`。 请注意，您不应 **在**&#x200B;存档 `etc/httpd` 中使用前缀。

**在中找不到任何场`conf.dispatcher.d/enabled_farms`**

您启用的场应位于所述子文件夹中。

**包含的文件(...)必须命名为： ...**

您的场配置中有两个部分 **必须** 包括特定文件： `/renders` 和 `/allowedClients` 在 `/cache` 部分。 这些部分必须如下所示：

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

在您的场配置中，有四个部分允许您包含自己的文件： `/clientheaders`， `filters`， `/rules` 在 `/cache` 部分和 `/virtualhosts`. 包含的文件需要按如下方式命名：

| 分区 | 包括文件名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包括 **默认** 这些文件的版本，其名称前面加有单词 `default_`例如， `../filters/default_filters.any`.

**include语句位于(...)，位于任何已知位置之外： ...**

除上述六节外，严禁使用 `$include` 语句，例如，以下语句将生成此错误：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**不包括……中允许的客户端/渲染**

如果不为指定包含，则会生成此错误 `/renders` 和 `/allowedClients` 在 `/cache` 部分。 请参阅
**包含的文件(...)必须命名为： ...** 部分以了解更多信息。

**过滤器不得使用glob模式以允许请求**

允许具有的请求是不安全的 `/glob` 样式规则，该规则与完整的请求行匹配，例如，

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此语句用于允许请求 `css` 文件，但它还允许请求 **任意** 后跟查询字符串的资源 `?a=.css`. 因此，禁止使用此类过滤器（另见CVE-2016-0957）。

**包含的文件(...)不匹配任何已知文件**

在Apache虚拟主机配置中，有两种类型的文件可以指定为包含：重写和变量。
包含的文件需要按如下方式命名：

| 类型 | 包括文件名 |
|-----------|---------------------------------|
| 重写 | `conf.d/rewrites/rewrite.rules` |
| 变量 | `conf.d/variables/custom.vars` |

>[!TIP]
>
>为了能够以更少限制的方式包含更多文件，您可能希望切换到灵活的Dispatcher配置模式。 请参阅文档 [使用Dispatcher工具验证和调试](/help/implementing/dispatcher/validation-debug.md) 以了解有关灵活模式的更多详细信息。

或者，您也可以包括 **默认** 重写规则的版本，其名称为 `conf.d/rewrites/default_rewrite.rules`.
请注意，变量文件没有默认版本。

**检测到已弃用的配置布局，正在启用兼容模式**

此消息表示您的配置具有已弃用的版本1布局，其中包含完整的Apache配置和文件，其中 `ams_` 前缀。 虽然向后兼容性仍支持此功能，但您应该切换到新布局。

请注意，第一阶段还可以 **单独运行**，而不是从包装中 `validate.sh` 脚本。

针对您的maven工件或您的 `dispatcher/src` 子目录，它将报告验证失败：

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

在Windows上，Dispatcher验证器区分大小写。 因此，如果您不遵守配置所在路径的大小写，例如：

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

从Windows资源管理器复制并粘贴路径，然后在命令提示符下使用 `cd` 命令进入那条路。

### 阶段2 {#second-phase}

此阶段通过在映像中启动Docker来检查Apache语法。 必须本地安装Docker，但请注意，AEM无需运行。

>[!NOTE]
>Windows用户需要使用支持Docker的Windows 10 Professional或其他发行版。 这是在本地计算机上运行和调试Dispatcher的先决条件。

此阶段也可以独立运行 `validator full -d out src/dispatcher`，生成下一个命令所需的out目录 `bin/docker_run.sh out host.docker.internal:4503 8080`.

在Cloud Manager部署期间， `httpd -t` 语法检查也将执行，所有错误都将包含在Cloud Manager构建图像步骤失败日志中。

### 阶段3 {#third-phase}

如果在此阶段失败，则意味着Adobe更改了一个或多个不可变文件，您必须将相应的不可变文件替换为 `src` SDK的目录。 以下日志示例说明了此问题：

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

此阶段也可以独立运行 `validator full -d out src/dispatcher`，生成下一个命令所需的out目录 `bin/docker_immutability_check.sh out`.

## 调试Apache和Dispatcher配置 {#debugging-apache-and-dispatcher-configuration}

请注意，您可以使用在本地运行Apache Dispatcher `./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

如前所述，必须本地安装Docker，AEM无需运行。 Windows用户需要使用支持Docker的Windows 10 Professional或其他发行版。 这是在本地计算机上运行和调试Dispatcher的先决条件。

以下策略可用于增加Dispatcher模块的日志输出并查看结果 `RewriteRule` 在本地和云环境中进行评估。

这些模块的日志级别由变量定义 `DISP_LOG_LEVEL` 和 `REWRITE_LOG_LEVEL`. 可以在文件中设置它们 `conf.d/variables/global.vars`. 其有关部分如下：

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

在本地运行Dispatcher时，日志将直接打印到终端输出。 大多数情况下，您希望这些日志处于DEBUG状态，这可以通过在运行Docker时将Debug级别作为参数传递来完成。 例如：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`。

云环境的日志通过Cloud Manager中提供的日志记录服务公开。

## 每个环境的不同Dispatcher配置 {#different-dispatcher-configurations-per-environment}

目前，相同的Dispatcher配置应用于所有AEMas a Cloud Service的环境。 运行时将具有环境变量 `ENVIRONMENT_TYPE` 包含当前运行模式（dev、stage或prod）以及定义。 定义可以是 `ENVIRONMENT_DEV`， `ENVIRONMENT_STAGE` 或 `ENVIRONMENT_PROD`. 在Apache配置中，可直接在表达式中使用变量。 或者，可以使用定义来构建逻辑：

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

在本地测试配置时，您可以通过传递变量来模拟不同的环境类型 `DISP_RUN_MODE` 到 `docker_run.sh` 直接脚本：

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

不传入DISP_RUN_MODE的值时的缺省运行模式为“dev”。
要获得可用选项和变量的完整列表，请运行脚本 `docker_run.sh` 没有参数。

## 查看Docker容器正在使用的Dispatcher配置 {#viewing-dispatcher-configuration-in-use-by-docker-container}

使用特定于环境的配置，可能很难确定实际的Dispatcher配置是什么样的。 使用启动Docker容器后 `docker_run.sh` 可以按如下方式转储：

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

## 从旧模式迁移到灵活模式 {#migrating-flexible}

在Cloud Manager 2021.7.0版本中，新的Cloud Manager程序会生成具有AEM原型28或更高版本的maven项目结构，其中包括文件 **opt-in/USE_SOURCES_DIRECTLY**. 这消除了原有模式对文件数量和大小的限制，还导致SDK和运行时以改进的方式验证和部署配置。 如果您的Dispatcher配置没有此文件，强烈建议您迁移。 使用中描述的方法 [柔性模式](/help/implementing/dispatcher/validation-debug.md#migrating) 页面。
