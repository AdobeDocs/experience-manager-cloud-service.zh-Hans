---
title: 将 AMS 转换为 Adobe Experience Manager as a Cloud Service Dispatcher 配置
description: 将 AMS 转换为 Adobe Experience Manager as a Cloud Service Dispatcher 配置
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 99%

---


# 将 AMS 转换为 Adobe Experience Manager (AEM) as a Cloud Service Dispatcher 配置

## 简介 {#introduction}

本节提供了有关如何转换 AMS 配置的分步说明。

>[!NOTE]
>本文假定您有一个存档，其结构与[管理 Dispatcher 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)中所述的结构相似。

## 将 AMS 转换为 AEM as a Cloud Service Dispatcher 配置的步骤

1. **提取存档并删除最后的前缀**

   将存档解压缩到一个文件夹，并确保下面一层子文件夹以 conf、conf.d、conf.dispatcher.d 和 conf.modules.d 开头。如果不是，请在层次结构中将其向上移动。

1. **删除未使用的子文件夹和文件**

   移除子文件夹 conf 和 conf.modules.d，以及与 conf.d/*.conf 匹配的文件。

1. **删除所有未发布的虚拟主机**

1. **移除所有虚拟主机文件**

   conf.d/enabled_vhosts 中名称含有 author、unhealthy、health、lc 或 flush 的文件。也可以移除 conf.d/available_vhosts 中未链接到的所有虚拟主机文件。

1. 移除或注释未引用端口 80 的虚拟主机部分

   如果您的虚拟主机文件中仍然有部分内容专门引用端口 80 以外的其他端口，例如

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`，
则请移除或注释该部分。这些部分中的语句将不会得到处理，但是如果保留它们，您可能最终仍会对其进行编辑，并且不会有任何效果，这可能会造成混淆。

1. **检查 rewrites**

   * 进入目录 conf.d/rewrites。

   * 移除任何名为 base_rewrite.rules 和 xforwarded_forcessl_rewrite.rules 的文件，并记得移除虚拟主机文件中引用这些文件的 Include 语句。

   * 如果 conf.d/rewrites 现在包含单个文件，则应将其重命名为 rewrite.rules，并且不要忘记修改虚拟主机文件中引用该文件的 Include 语句。

   * 但是，如果文件夹包含多个特定于虚拟主机的文件，则应将其内容复制到虚拟主机文件中引用这些文件的 Include 语句中。

1. **检查 variables**

   1. 进入目录 conf.d/variables。

   1. 移除任何名为 ams_default.vars 的文件，并记得移除虚拟主机文件中引用这些文件的 Include 语句。

   1. 如果 conf.d/variables 现在包含单个文件，则应将其重命名为 custom.vars，并且不要忘记修改虚拟主机文件中引用该文件的 Include 语句。

   1. 但是，如果文件夹包含多个特定于虚拟主机的文件，则应将其内容复制到虚拟主机文件中引用这些文件的 Include 语句中。

1. **移除白名单**

   移除文件夹 conf.d/whitelists，并移除虚拟主机文件中引用该子文件夹中某些文件的 Include 语句。

1. **替换任何不再可用的变量**

   在所有虚拟主机文件中：

   将 PUBLISH_DOCROOT 重命名为 DOCROOT
移除引用名称为 DISP_ID、PUBLISH_FORCE_SSL 或 PUBLISH_WHITELIST_ENABLED 的变量的部分

1. **通过运行验证器检查状态**

   使用 httpd 子命令在目录中运行 Dispatcher 验证器：

   `$ validator httpd`
如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

   如果看到未列入白名单的 Apache 指令，请将其删除。

1. **删除所有未发布的场**

   移除 conf.dispatcher.d/enabled_farms 中名称含有 author、unhealthy、health、lc 或 flush 的所有场文件。也可以移除 conf.dispatcher.d/available_farms 中未链接到的所有场文件。

1. **重命名场文件**

   必须重命名 conf.dispatcher.d/enabled_farms 中的所有场文件，使其名称匹配 *.farm 模式，例如，将名为 customerX_farm.any 的场文件重命名为 customerX.farm。

1. **检查 cache**

   进入目录 conf.dispatcher.d/cache。

   移除所有前缀为 ams_ 的文件。

   如果 conf.dispatcher.d/cache 现在为空，请将文件 conf.dispatcher.d/cache/rules.any 从标准 Dispatcher 配置复制到此文件夹。标准 Dispatcher 配置可以在此 SDK 的 src 文件夹中找到。同时不要忘记修改场文件中引用 ams_*_cache.any 规则文件的 $include 语句。

   相反，如果 conf.d/variables 现在包含名为 suffix _cache.any 的单个文件，则应将其重命名为 rules.any，并且不要忘记修改场文件中引用该文件的 $include 语句。

   但是，如果文件夹包含多个使用该模式且特定于场的文件，则应将其内容复制到场文件中引用这些文件的 $include 语句中。

   移除任何含有 suffix _invalidate_allowed.any 的文件。

   将文件 conf.dispatcher.d/cache/default_invalidate_any 从默认 Dispatcher 配置复制到该位置。

   在每个场文件中，移除 cache/allowedClients 部分中的所有内容，并将其替换为：

   $include &quot;../cache/default_invalidate.any&quot;

1. **检查 client headers**

   进入目录 conf.dispatcher.d/clientheaders。

   移除所有前缀为 ams_ 的文件。

   如果 conf.dispatcher.d/clientheaders 现在包含名为 suffix _clientheaders.any 的单个文件，则应将其重命名为 clientheaders.any，并且不要忘记修改场文件中引用该文件的 $include 语句。

   但是，如果文件夹包含多个使用该模式且特定于场的文件，则应将其内容复制到场文件中引用这些文件的 $include 语句中。

   将文件 conf.dispatcher/clientheaders/default_clientheaders.any 从默认 Dispatcher 配置复制到该位置。

   在每个场文件中，将如下所示的所有 clientheader include 语句：

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   替换为语句：

   `$include "../clientheaders/default_clientheaders.any"`

1. **检查 filter**

   * 进入目录 conf.dispatcher.d/filters。

   * 移除所有前缀为 ams_ 的文件。

   * 如果 conf.dispatcher.d/filters 现在包含单个文件，则应将其重命名为 filters.any，并且不要忘记修改场文件中引用该文件的 $include 语句。

   * 但是，如果文件夹包含多个使用该模式且特定于场的文件，则应将其内容复制到场文件中引用这些文件的 $include 语句中。

   * 将文件 conf.dispatcher/filters/default_filters.any 从默认 Dispatcher 配置复制到该位置。

   * 在每个场文件中，将如下所示的所有 filter include 语句：

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`
替换为语句：

      `$include "../filters/default_filters.any"`

1. **检查 renders**

   * 进入目录 conf.dispatcher.d/renders。

   * 移除该文件夹中的所有文件。

   * 将文件 conf.dispatcher.d/renders/default_renders.any 从默认 Dispatcher 配置复制到该位置。

   * 在每个场文件中，移除 renders 部分中的所有内容，并将其替换为：

      `$include "../renders/default_renders.any"`

1. **检查 virtualhosts**

   * 重命名目录 `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts`，并进入该目录。

   * 移除所有前缀为 `ams_` 的文件。

   * 如果 conf.dispatcher.d/virtualhosts 现在包含单个文件，则应将其重命名为 virtualhosts.any，并且不要忘记修改场文件中引用该文件的 $include 语句。

   * 但是，如果文件夹包含多个使用该模式且特定于场的文件，则应将其内容复制到场文件中引用这些文件的 $include 语句中。

   * 将文件 conf.dispatcher/virtualhosts/default_virtualhosts.any 从默认 Dispatcher 配置复制到该位置。

   * 在每个场文件中，将如下所示的所有 filter include 语句：

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
替换为语句：

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **通过运行验证器检查状态**

   * 使用 Dispatcher 子命令在目录中运行 Dispatcher 验证器：

      `$ validator dispatcher`

   * 如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

   * 如果看到有关未定义变量 `PUBLISH_DOCROOT` 的错误，请将该变量重命名为 `DOCROOT`。

   * 有关其他每个错误，请参阅验证器工具文档的“疑难解答”部分。

## 在本地部署中测试您的配置 {#testing-config-local-deployment}

>[!IMPORTANT]
>
>在本地部署中测试您的配置需要安装 Docker。

使用 Dispatcher SDK 中的脚本 `docker_run.sh`，您可以测试配置不包含只会在部署中显示的任何其他错误：

1. 使用验证程序生成部署信息

   `validator full -d out`
这将验证完整配置并在 out 中生成部署信息

1. 使用该部署信息在 Docker 映像中启动 Dispatcher

   在 macOS 计算机上运行 AEM 发布服务器，并监听端口 4503 时，您可以在该服务器前面运行启动 Dispatcher，如下所示：

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   这将启动容器并在本地端口 8080 上公开 Apache。

## 使用新的 Dispatcher 配置 {#using-dispatcher-config}

如果验证器不再报告任何问题，并且 Docker 容器启动时没有出现任何故障或警告，则可以将配置移动到 Git 存储库的 d`ispatcher/src` 子目录中。