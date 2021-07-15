---
title: 使用Dispatcher工具验证和调试
description: 使用Dispatcher工具验证和调试
feature: Dispatcher
source-git-commit: 5545f7c271137050d522904bfa94e20f0286e059
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 1%

---

# 使用Dispatcher工具验证和调试 {#Dispatcher-in-the-cloud}

## 简介 {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>有关云中Dispatcher以及如何下载Dispatcher工具的更多信息，请参阅云中的[Dispatcher](/help/implementing/dispatcher/disp-overview.md)页面。 如果您的调度程序配置处于旧版模式，请参阅旧版模式文档](/help/implementing/dispatcher/validation-debug-legacy.md)。[

以下各节介绍了灵活模式的文件结构、本地验证、调试以及从旧版模式迁移到灵活模式。

本文假定您项目的Dispatcher配置包含文件`opt-in/USE_SOURCES_DIRECTLY`，这会导致SDK和运行时以与旧版模式相比的改进方式验证和部署配置，从而消除对文件数量和大小的限制。

因此，如果调度程序配置不包含上述文件，则强烈建议您从旧版模式迁移到灵活模式（如[从旧版模式迁移到灵活模式](#migrating)一节中所述），如&#x200B;**。**

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

您可以拥有一个或多个这些文件。 它们包含与主机名匹配的`<VirtualHost>`条目，并允许Apache使用不同的规则处理每个域流量。 文件在`available_vhosts`目录中创建，并在`enabled_vhosts`目录中通过符号链接启用。 在`.vhost`文件中，将包含重写和变量等其他文件。

* `conf.d/rewrites/rewrite.rules`

此文件包含在`.vhost`文件内。 它有一组用于`mod_rewrite`的重写规则。

* `conf.d/variables/custom.vars`

此文件包含在`.vhost`文件内。 您可以在此位置为Apache变量添加定义。

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

* `opt-in/USE_SOURCES_DIRECTLY`

此文件支持更灵活的调度程序配置，并消除了以前对文件数量和大小的限制。 它还会导致SDK和运行时以改进的方式验证和部署配置。

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

## 支持的Apache模块 {#apache-modules}

请参阅[支持的Apache模块](/help/implementing/dispatcher/disp-overview.md#supported-directives)。

## 本地验证 {#local-validation-flexible-mode}

>[!NOTE]
>以下部分包括使用Mac或Linux版本的SDK的命令，但Windows SDK也可以以类似的方式使用。

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

该脚本分为以下三个阶段：

1. 它运行验证器。 如果配置无效，脚本将失败。
2. 它执行`httpd -t`命令以测试语法是否正确，以便Apache httpd可以启动。 如果成功，配置应准备好进行部署。
3. 检查Dispatcher SDK配置文件的子集（如[文件结构部分](##flexible-mode-file-structure)中所述）是否未修改。

在Cloud Manager部署期间，将同时执行`httpd -t`语法检查，并且Cloud Manager `Build Images step failure`日志中将包含任何错误。

### 阶段1 {#first-phase}

如果未指列入允许列表令，该工具将记录错误并返回非零退出代码。 此外，它还会以模式`conf.dispatcher.d/enabled_farms/*.farm`扫描所有文件，并检查：

* 不存在通过`/glob`允许使用的过滤器规则（有关更多详细信息，请参阅[CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)）。
* 未显示管理员功能。 例如，对路径（如`/crx/de or /system/console`）的访问。

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
前缀为`ams_`的Apache配置和文件。 虽然向后仍支持此设置
兼容性，则应切换到新布局。

请注意，第一个阶段也可以是&#x200B;**单独运行**，而不是从包装器`validate.sh`脚本中运行。

当针对maven对象或`dispatcher/src`子目录运行时，它将报告验证失败：

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

通过从Windows资源管理器复制并粘贴路径，然后在命令提示符下使用`cd`命令将该路径复制并粘贴到该路径中，可避免出现此错误。

### 阶段2 {#second-phase}

此阶段通过在图像中启动Docker来检查Apache语法。 Docker必须安装在本地，但请注意，AEM无需运行。

>[!NOTE]
>Windows用户需要使用支持Docker的Windows 10专业版或其他发行版。 这是在本地计算机上运行和调试Dispatcher的先决条件。

此阶段也可通过`bin/docker_run.sh src/dispatcher host.internal.docker:4503 8080`独立运行。

在Cloud Manager部署期间，还将执行`httpd -t`语法检查，并且任何错误都将包含在Cloud Manager构建映像步骤失败日志中。

### 阶段3 {#third-phase}

如果此阶段出现故障，则意味着Adobe更改了一个或多个不可变文件，您必须将相应的不可变文件替换为在SDK的`src`目录中提供的新版本。 以下日志示例说明了此问题：

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

此阶段也可通过`bin/docker_immutability_check.sh src/dispatcher`独立运行。

## 调试Apache和Dispatcher配置 {#debugging-apache-and-dispatcher-configuration}

请注意，您可以使用`./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`在本地运行apache Dispatcher。

如前所述，Docker必须安装在本地，并且AEM无需运行。 Windows用户需要使用支持Docker的Windows 10专业版或其他发行版。 这是在本地计算机上运行和调试Dispatcher的先决条件。

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

## 每个环境的不同Dispatcher配置 {#different-dispatcher-configurations-per-environment}

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

## 查看Docker容器正在使用的Dispatcher配置 {#viewing-dispatcher-configuration-in-use-by-docker-container}

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

## 从旧版模式迁移到灵活模式 {#migrating}

在Cloud Manager 2021.7.0版本中，新的Cloud Manager程序会生成具有[AEM原型28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en)或更高版本的Maven项目结构，其中包括文件&#x200B;**opt-in/USE_SOURCES_DIRECTLY**。 这消除了[旧版模式](/help/implementing/dispatcher/validation-debug-legacy.md)以前对文件数量和大小的限制，还会导致SDK和运行时以改进的方式验证和部署配置。 如果您的调度程序配置没有此文件，强烈建议您迁移。 请执行以下步骤以确保安全过渡：

1. **本地测试。** 使用最新的调度程序工具SDK，添加文件夹和文 `opt-in/USE_SOURCES_DIRECTLY`件。按照本文中的“本地验证”说明来测试调度程序是否在本地工作。
2. **云开发测试：**
   * 将文件`opt-in/USE_SOURCES_DIRECTLY`提交到由非生产管道部署到云开发环境的git分支。
   * 使用Cloud Manager部署到云开发环境。
   * 彻底测试。 在将更改部署到更高环境之前，务必要验证Apache和Dispatcher配置是否按预期行事。 检查与您的自定义配置相关的所有行为！ 如果您认为已部署的Dispatcher配置不反映您的自定义配置，请提交客户支持票证。
3. **部署到生产环境：**
   * 将文件`opt-in/USE_SOURCES_DIRECTLY`提交到由生产管道部署到云暂存和生产环境的git分支。
   * 使用Cloud Manager部署到暂存环境。
   * 彻底测试。 在将更改部署到更高环境之前，务必要验证Apache和Dispatcher配置是否按预期行事。 检查与您的自定义配置相关的所有行为！ 如果您认为已部署的Dispatcher配置不反映您的自定义配置，请提交客户支持票证。
   * 使用Cloud Manager继续将部署到生产环境。
