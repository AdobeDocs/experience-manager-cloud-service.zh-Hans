---
title: 将 AMS 转换为 Adobe Experience Manager as a Cloud Service Dispatcher 配置
description: 将 AMS 转换为 Adobe Experience Manager as a Cloud Service Dispatcher 配置
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 37%

---


# 将 AMS 转换为 Adobe Experience Manager (AEM) as a Cloud Service Dispatcher 配置

## 简介 {#introduction}

本节提供了有关如何转换AMS配置的分步说明。

>[!NOTE]
>本文假定您有一个存档，其结构与[管理 Dispatcher 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/dispatcher-configurations.html)中所述的结构相似。

## 将 AMS 转换为 AEM as a Cloud Service Dispatcher 配置的步骤

1. **提取存档并删除最后的前缀**

   将存档解压缩到一个文件夹，并确保直接子文件夹以conf、conf.d、conf.dispatcher.d和conf.modules.d开头。如果没有，则将其在层次结构中向上移动。

1. **删除未使用的子文件夹和文件**

   删除子文件夹conf和conf.modules.d，以及与conf.d/*.conf匹配的文件。

1. **删除所有未发布的虚拟主机**

1. **移除所有虚拟主机文件**

   conf.d/enabled_vhosts中名称含有author、unhealthy、health、lc或flush的文件。 也可以移除 conf.d/available_vhosts 中未链接到的所有虚拟主机文件。

1. 移除或注释未引用端口 80 的虚拟主机部分

   例如，如果您的虚拟主机文件中仍有部分内容专门引用端口80以外的端口，

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`，
则请移除或注释该部分。不会处理这些部分中的语句，但是如果保留它们，您可能最终仍会对其进行编辑，并且不会有任何效果，这会造成混淆。

1. **检查 rewrites**

   * 进入目录 conf.d/rewrites。

   * 移除任何名为 base_rewrite.rules 和 xforwarded_forcessl_rewrite.rules 的文件，并记得移除虚拟主机文件中引用这些文件的 Include 语句。

   * 如果conf.d/rewrites现在包含单个文件，则应将其重命名为rewrite.rules，并且不要忘记修改虚拟主机文件中引用该文件的Include语句。

   * 但是，如果该文件夹包含多个特定于虚拟主机的文件，则应将其内容复制到虚拟主机文件中引用这些文件的Include语句中。

1. **检查 variables**

   1. 进入目录 conf.d/variables。

   1. 移除任何名为 ams_default.vars 的文件，并记得移除虚拟主机文件中引用这些文件的 Include 语句。

   1. 如果conf.d/variables现在包含单个文件，则应将其重命名为custom.vars，并且不要忘记修改虚拟主机文件中引用该文件的Include语句。

   1. 但是，如果该文件夹包含多个特定于虚拟主机的文件，则应将其内容复制到虚拟主机文件中引用这些文件的Include语句中。

1. **移除白名单**

   移除文件夹 conf.d/whitelists，并移除虚拟主机文件中引用该子文件夹中某些文件的 Include 语句。

1. **替换任何不再可用的变量**

   在所有虚拟主机文件中：

   将 PUBLISH_DOCROOT 重命名为 DOCROOT
移除引用名称为 DISP_ID、PUBLISH_FORCE_SSL 或 PUBLISH_WHITELIST_ENABLED 的变量的部分

1. **通过运行验证器检查状态**

   使用httpd子命令在目录中运行Dispatcher验证器：

   `$ validator httpd`
如果看到有关缺少“include”文件的错误，请检查是否正确重命名了这些文件。

   如果看到未列入白名单的 Apache 指令，请将其删除。

1. **删除所有未发布的场**

   移除conf.dispatcher.d/enabled_farms中名称含有author、unhealthy、health、lc或flush的所有场文件。 也可以移除 conf.dispatcher.d/available_farms 中未链接到的所有场文件。

1. **重命名场文件**

   必须重命名conf.dispatcher.d/enabled_farms中的所有场以匹配模式*.farm。 例如，将`customerX_farm.any`重命名为`customerX.farm`。

1. **检查 cache**

   进入目录 conf.dispatcher.d/cache。

   移除所有前缀为 `ams_` 的文件。

   如果conf.dispatcher.d/cache现在为空，请将文件`conf.dispatcher.d/cache/rules.any`从标准Dispatcher配置复制到此文件夹。 标准Dispatcher配置可在此SDK的src文件夹中找到。 同时，不要忘记修改场文件中引用`ams_*_cache.any`规则文件的$include语句。

   如果conf.dispatcher.d/cache现在包含后缀为`_cache.any`的单个文件，则应将其重命名为`rules.any`。 请记得修改场文件中引用该文件的$include语句。

   但是，如果文件夹包含多个使用该模式且特定于场的文件，则应将其内容复制到场文件中引用这些文件的$include语句中。

   移除任何后缀`_invalidate_allowed.any`的文件。

   将文件conf.dispatcher.d/cache/default_invalidate_any从默认Dispatcher配置复制到该位置。

   在每个场文件中，移除 cache/allowedClients 部分中的所有内容，并将其替换为：

   $include &quot;../cache/default_invalidate.any&quot;

1. **检查 client headers**

   进入目录 conf.dispatcher.d/clientheaders。

   移除所有前缀为 `ams_` 的文件。

   如果conf.dispatcher.d/clientheaders包含后缀为`_clientheaders.any`的单个文件，请将其重命名为`clientheaders.any`。 请记得修改场文件中引用该文件的$include语句。

   但是，如果文件夹包含多个使用该模式且特定于场的文件，则应将其内容复制到场文件中引用这些文件的$include语句中。

   将文件`conf.dispatcher/clientheaders/default_clientheaders.any`从默认Dispatcher配置复制到该位置。

   在每个场文件中，替换以下所示的任何`clientheader`个“include”语句：

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   替换为语句：

   `$include "../clientheaders/default_clientheaders.any"`

1. **检查 filter**

   * 进入目录 conf.dispatcher.d/filters。

   * 移除所有前缀为 `ams_` 的文件。

   * 如果conf.dispatcher.d/filters现在包含单个文件，请将其重命名为`filters.any`。 请记得修改场文件中引用该文件的$include语句。

   * 但是，如果文件夹包含多个使用该模式且特定于场的文件，则应将其内容复制到场文件中引用这些文件的$include语句中。

   * 将文件`conf.dispatcher/filters/default_filters.any`从默认Dispatcher配置复制到该位置。

   * 在每个场文件中，替换以下所示的所有filter“include”语句：

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`
替换为语句：

     `$include "../filters/default_filters.any"`

1. **检查 renders**

   * 进入目录 conf.dispatcher.d/renders。

   * 移除该文件夹中的所有文件。

   * 将文件`conf.dispatcher.d/renders/default_renders.any`从默认Dispatcher配置复制到该位置。

   * 在每个场文件中，移除 renders 部分中的所有内容，并将其替换为：

     `$include "../renders/default_renders.any"`

1. **检查 virtualhosts**

   * 重命名目录 `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts`，并进入该目录。

   * 移除所有前缀为 `ams_` 的文件。

   * 如果conf.dispatcher.d/virtualhosts现在包含单个文件，请将其重命名为`virtualhosts.any`。 请记得修改场文件中引用该文件的$include语句。

   * 但是，如果文件夹包含多个使用该模式且特定于场的文件，则应将其内容复制到场文件中引用这些文件的$include语句中。

   * 将文件`conf.dispatcher/virtualhosts/default_virtualhosts.any`从默认Dispatcher配置复制到该位置。

   * 在每个场文件中，替换以下所示的所有filter“include”语句：

     `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
替换为语句：

     `$include "../virtualhosts/default_virtualhosts.any"`


1. **通过运行验证器检查状态**

   * 使用Dispatcher子命令在目录中运行Dispatcher验证器：

     `$ validator dispatcher`

   * 如果看到有关缺少“include”文件的错误，请检查是否正确重命名了这些文件。

   * 如果看到有关未定义变量 `PUBLISH_DOCROOT` 的错误，请将该变量重命名为 `DOCROOT`。

   * 有关其他每个错误，请参阅验证器工具文档的“疑难解答”部分。

## 在本地部署中测试您的配置 {#testing-config-local-deployment}

>[!IMPORTANT]
>
>在本地部署中测试您的配置需要安装 Docker。

使用 Dispatcher SDK 中的脚本 `docker_run.sh`，您可以测试配置不包含只会在部署中显示的任何其他错误：

1. 使用验证器生成部署信息。

   `validator full -d out`
验证完整配置并在out中生成部署信息。

1. 使用该部署信息在Docker映像中启动Dispatcher。

   在macOS计算机上运行AEM发布服务器，并监听端口4503时，您可以在该服务器前面运行启动Dispatcher，如下所示：

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   启动容器并在本地端口8080上公开Apache。

## 使用新的Dispatcher配置 {#using-dispatcher-config}

如果验证器不再报告任何问题，并且 Docker 容器启动时没有出现任何故障或警告，则可以将配置移动到 Git 存储库的 d`ispatcher/src` 子目录中。