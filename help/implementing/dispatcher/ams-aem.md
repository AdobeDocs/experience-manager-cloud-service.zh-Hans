---
title: 将 Dispatcher 配置从 AMS 迁移到 AEM as a Cloud Service
description: 将 Dispatcher 配置从 AMS 迁移到 AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 17%

---

# 将 Dispatcher 配置从 AMS 迁移到 AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## AMS Dispatcher与AEMas a Cloud Service的主要区别 {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

AEMas a Cloud Service中的Apache和Dispatcher配置与AMS配置非常相似。 主要区别包括：

* 在AEMas a Cloud Service中，某些Apache指令可能不被使用(例如 `Listen` 或 `LogLevel`)
* 在AEMas a Cloud Service中，只能将部分Dispatcher配置放入包含文件中，其命名很重要。 例如，要在不同主机之间重复使用的过滤器规则必须放入名为 `filters/filters.any`. 有关更多信息，请参阅参考页面。
* 在AEMas a Cloud Service中，存在额外的验证，以禁止使用编写的过滤器规则 `/glob` 以防止出现安全问题。 自 `deny *` 将使用而不是 `allow *` （不能使用），客户将从在本地运行Dispatcher以及执行试用和错误中受益，通过查看日志可准确了解Dispatcher过滤器为了添加这些过滤器而阻止的路径。

## 将调度程序配置从AMS迁移到AEMas a Cloud Service的准则

Dispatcher配置结构在Managed Services和AEMas a Cloud Service之间存在差异。 下面提供了有关如何从AMS Dispatcher配置版本2迁移到AEMas a Cloud Service的分步指南。

## 如何将AMS转换为AEM as a Cloud Service Dispatcher配置

以下部分提供了有关如何转换AMS配置的分步说明。 它假定您有一个存档，其结构与 [Cloud Manager Dispatcher配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### 提取存档并删除最后的前缀

将存档解压缩到文件夹，并确保子文件夹的直接开头为 `conf`, `conf.d`,
`conf.dispatcher.d` 和 `conf.modules.d`. 如果没有，请在层级中向上移动。

### 删除未使用的子文件夹和文件

删除子文件夹 `conf` 和 `conf.modules.d`，以及文件匹配 `conf.d/*.conf`.

### 删除所有未发布的虚拟主机

删除 `conf.d/enabled_vhosts` 具有 `author`, `unhealthy`, `health`,
`lc` 或 `flush` 以它的名称。 中的所有虚拟主机文件 `conf.d/available_vhosts` 也可以删除未链接到的访客。

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

进入目录 `conf.d/rewrites`.

删除任何名为 `base_rewrite.rules` 和 `xforwarded_forcessl_rewrite.rules` 并记住删除 `Include` 虚拟主机文件中引用这些语句的语句。

如果 `conf.d/rewrites` 现在包含单个文件，应将其重命名为 `rewrite.rules` 别忘了调整 `Include` 语句引用虚拟主机文件中该文件。

但是，如果文件夹包含多个特定于虚拟主机的文件，则应将其内容复制到 `Include` 在虚拟主机文件中引用它们的语句。

### 检查 variables

进入目录 `conf.d/variables`.

删除任何名为 `ams_default.vars` 并记住删除 `Include` 虚拟主机文件中引用这些语句的语句。

如果 `conf.d/variables` 现在包含单个文件，应将其重命名为 `custom.vars` 别忘了调整 `Include` 语句引用虚拟主机文件中该文件。

但是，如果文件夹包含多个特定于虚拟主机的文件，则应将其内容复制到 `Include` 在虚拟主机文件中引用它们的语句。

### 删除允许列表

删除文件夹 `conf.d/whitelists` 删除 `Include` 虚拟主机文件中引用该子文件夹中某个文件的语句。

### 替换任何不再可用的变量

在所有虚拟主机文件中：

重命名 `PUBLISH_DOCROOT` to `DOCROOT`
删除引用名为 `DISP_ID`, `PUBLISH_FORCE_SSL` 或 `PUBLISH_WHITELIST_ENABLED`

### 通过运行验证器检查状态

在目录中使用 `httpd` 子命令：

```
$ validator httpd .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到未的Apache指列入允许列表令，请删除它们。

### 删除所有未发布的场

删除 `conf.dispatcher.d/enabled_farms` 具有 `author`, `unhealthy`, `health`,
`lc` 或 `flush` 以它的名称。 中的所有场文件 `conf.dispatcher.d/available_farms` 也可以删除未链接到的访客。

### 重命名场文件

所有农场 `conf.d/enabled_farms` 必须重命名以匹配模式 `*.farm`，例如名为的场文件 `customerX_farm.any` 应重命名 `customerX.farm`.

### 检查 cache

进入目录 `conf.dispatcher.d/cache`.

移除所有前缀为 `ams_` 的文件。

如果 `conf.dispatcher.d/cache` 现在为空，请复制文件 `conf.dispatcher.d/cache/rules.any`
从标准Dispatcher配置到此文件夹。 标准Dispatcher配置可在文件夹中找到 `src` 的SDK。 不要忘记调整
`$include` 引用 `ams_*_cache.any` 场文件中的规则文件。

如果 `conf.dispatcher.d/cache` 现在包含带后缀的单个文件 `_cache.any`，则应将其重命名为 `rules.any` 别忘了调整 `$include` 语句，引用场文件中该文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则应将其内容复制到 `$include` 在场文件中引用它们的语句。

移除所有带后缀的文件 `_invalidate_allowed.any`.

复制文件 `conf.dispatcher.d/cache/default_invalidate_any` 从云调度程序配置中的默认AEM到该位置。

在每个场文件中，删除 `cache/allowedClients` 部分，替换为：

```
$include "../cache/default_invalidate.any"
```

### 检查 client headers

进入目录 `conf.dispatcher.d/clientheaders`.

移除所有前缀为 `ams_` 的文件。

如果 `conf.dispatcher.d/clientheaders` 现在包含带后缀的单个文件 `_clientheaders.any`，则应将其重命名为 `clientheaders.any` 别忘了调整 `$include` 语句，引用场文件中该文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则应将其内容复制到 `$include` 在场文件中引用它们的语句。

复制文件 `conf.dispatcher/clientheaders/default_clientheaders.any` 从默认的AEMas a Cloud ServiceDispatcher配置到该位置。

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

进入目录 `conf.dispatcher.d/filters`.

移除所有前缀为 `ams_` 的文件。

如果 `conf.dispatcher.d/filters` 现在包含单个文件，应将其重命名为
`filters.any` 别忘了调整 `$include` 语句，引用场文件中该文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则应将其内容复制到 `$include` 在场文件中引用它们的语句。

复制文件 `conf.dispatcher/filters/default_filters.any` 从默认的AEMas a Cloud ServiceDispatcher配置到该位置。

在每个场文件中，将如下所示的任何filter include语句：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

替换为语句：

```
$include "../filters/default_filters.any"
```

### 检查 renders

进入目录 `conf.dispatcher.d/renders`.

移除该文件夹中的所有文件。

复制文件 `conf.dispatcher.d/renders/default_renders.any` 从默认的AEMas a Cloud ServiceDispatcher配置到该位置。

在每个场文件中，删除 `renders` 部分，替换为：

```
$include "../renders/default_renders.any"
```

### 检查 virtualhosts

重命名目录 `conf.dispatcher.d/vhosts` to `conf.dispatcher.d/virtualhosts` 然后输入。

移除所有前缀为 `ams_` 的文件。

如果 `conf.dispatcher.d/virtualhosts` 现在包含单个文件，应将其重命名为
`virtualhosts.any` 别忘了调整 `$include` 语句，引用场文件中该文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则应将其内容复制到 `$include` 在场文件中引用它们的语句。

复制文件 `conf.dispatcher/virtualhosts/default_virtualhosts.any` 从默认的AEMas a Cloud ServiceDispatcher配置到该位置。

在每个场文件中，将如下所示的任何filter include语句：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

替换为语句：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 通过运行验证器检查状态

在目录中使用 `dispatcher` 子命令：

```
$ validator dispatcher .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到有关未定义变量 `PUBLISH_DOCROOT` 的错误，请将该变量重命名为 `DOCROOT`。

有关其他每个错误，请参阅验证器工具文档的“疑难解答”部分。

### 在本地部署中测试您的配置（需要安装Docker）

使用脚本 `docker_run.sh` 在AEMas a Cloud ServiceDispatcher工具中，您可以测试配置不包含只会在部署中显示的任何其他错误：

### 步骤1:使用验证器生成部署信息

```
validator full -d out .
```


这将验证完整配置并在 中生成部署信息`out`

### 步骤2:使用该部署信息在Docker映像中启动Dispatcher

如果AEM发布服务器在macOS计算机上运行，并监听端口4503，则可以在该服务器前面运行启动Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

这将启动容器并在本地端口 8080 上公开 Apache。

### 使用新的Dispatcher配置

恭喜！如果验证器不再报告任何问题，并且Docker容器启动时没有出现任何故障或警告，则可以将配置移动到 `dispatcher/src` git存储库的子目录。

**使用AMS Dispatcher配置版本1的客户应联系客户支持，以帮助他们从版本1迁移到版本2，以便按照上述说明操作。**
