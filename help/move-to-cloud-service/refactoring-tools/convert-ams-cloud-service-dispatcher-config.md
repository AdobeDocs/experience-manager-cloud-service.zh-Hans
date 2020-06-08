---
title: 将AMS转换为Adobe Experience Manager作为云服务调度程序配置
description: 将AMS转换为Adobe Experience Manager作为云服务调度程序配置
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---


# 将AMS转换为Adobe Experience Manager(AEM)作为云服务调度程序配置

## 简介 {#introduction}

本节提供有关如何转换AMS配置的分步说明。

>[!NOTE]
>它假定您有一个与管理调度程序配置中所述结构相 [似的存档](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)。

## 将AMS转换为AEM作为云服务调度程序配置的步骤

1. **提取存档并删除最终前缀**

   将存档解压到文件夹，并确保使用conf、conf.d、conf.dispatcher.d和conf.modules.d开始的即时子文件夹。 如果他们不这样做，就在层级中向上移动。

1. **删除未使用的子文件夹和文件**

   删除子文件夹conf和conf.modules.d以及与conf.d/*.conf匹配的文件。

1. **删除所有非发布虚拟主机**

1. **删除任何虚拟主机文件**

   在conf.d/enabled_vhosts中，名称中含有作者、不健康、健康、lc或刷新。 conf.d/available_vhosts中未链接的所有虚拟主机文件也可以删除。

1. 删除或注释不引用端口80的虚拟主机部分

   如果您的虚拟主机文件中仍有部分专门引用端口80以外的其他端口，例如

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
删除或添加注释。 这些部分中的语句将不会得到处理，但是，如果保留这些语句，您最终可能仍会编辑它们而无效，这会令人混淆。

1. **检查重写**

   * 输入目录conf.d/rewrites。

   * 删除名为base_rewrite.rules和xforwarded_forcessl_rewrite.rules的任何文件，并记住删除引用它们的虚拟主机文件中的“包括”语句。

   * 如果conf.d/rewrites现在包含单个文件，则应将其重命名为rewrite.rules，不要忘记在虚拟主机文件中也改编引用该文件的“包括”语句。

   * 但是，如果文件夹包含多个特定于虚拟主机的文件，则应将其内容复制到虚拟主机文件中引用这些文件的“包含”语句。

1. **检查变量**

   1. 输入目录conf.d/variables。

   1. 删除名为ams_default.vars的任何文件，并记住删除引用这些文件的虚拟主机文件中的“包括”语句。

   1. 如果conf.d/variables现在包含单个文件，则应将其重命名为custom.vars，不要忘记在虚拟主机文件中也改编引用该文件的“包括”语句。

   1. 但是，如果文件夹包含多个特定于虚拟主机的文件，则应将其内容复制到虚拟主机文件中引用这些文件的“包含”语句。

1. **删除白名单**

   删除文件夹conf.d/whitelists，并删除虚拟主机文件中引用该子文件夹中某个文件的“包括”语句。

1. **替换任何不再可用的变量**

   在所有虚拟主机文件中：

   将PUBLISH_DOCROOT重命名为DISP_ID、PUBLISH_FORCE_SSL或PUBLISH_WHITELIST_ENABLED变量的节

1. **通过运行验证程序检查您的状态**

   使用httpd子命令在您的目录中运行调度程序validator:

   `$ validator httpd`
如果看到缺少包含文件的错误，请检查是否正确重命名了这些文件。

   如果看到未列入白名单的Apache指令，请删除它们。

1. **删除所有非发布场**

   删除conf.dispatcher.d/enabled_farms中名称中含有作者、不健康、健康、lc或刷新的任何场文件。 conf.dispatcher.d/available_farms中未链接的所有场文件也可以删除。

1. **重命名场文件**

   conf.dispatcher.d/enabled_farms中的所有场都必须重命名为与模式*.farm匹配，因此，例如，名为customerX_farm.any的场文件应重命名为customerX.farm。

1. **检查缓存**

   输入目录conf.dispatcher.d/cache。

   删除任何前缀ams_。

   如果conf.dispatcher.d/cache现在为空，请将文件conf.dispatcher.d/cache/rules.any从标准调度程序配置复制到此文件夹。 标准调度程序配置可在此SDK的文件夹src中找到。 不要忘记也改编引用农场文件中ams_*_cache.any规则文件的$include语句。

   如果conf.dispatcher.d/cache现在包含带后缀_cache.any的单个文件，则应将其重命名为rules.any，并且不要忘记在场文件中也改编引用该文件的$include语句。

   但是，如果文件夹包含多个具有该模式的特定场文件，则应将其内容复制到$include语句中，该语句在场文件中引用这些文件。

   删除任何具有_invalidate_allowed.any后缀的文件。

   将文件conf.dispatcher.d/cache/default_invalidate_any从默认调度程序配置复制到该位置。

   在每个场文件中，删除cache/allowedClients部分中的任何内容，并将其替换为：

   $include &quot;../cache/default_invalidate.any&quot;

1. **检查客户端标头**

   输入目录conf.dispatcher.d/clientheaders。

   删除任何前缀ams_。

   如果conf.dispatcher.d/clientheaders现在包含一个带后缀_clientheaders.any的文件，则应将其重命名为clientheaders.any，并且不要忘记在场文件中也改编引用该文件的$include语句。

   但是，如果文件夹包含多个具有该模式的特定场文件，则应将其内容复制到$include语句中，该语句在场文件中引用这些文件。

   将文件conf.dispatcher/clientheaders/default_clientheaders.any从默认调度程序配置复制到该位置。

   在每个场文件中，替换任何clientheader包含如下语句：

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   with语句：

   `$include "../clientheaders/default_clientheaders.any"`

1. **检查筛选器**

   * 输入目录conf.dispatcher.d/过滤器。

   * 删除任何前缀ams_。

   * 如果conf.dispatcher.d/过滤器现在包含单个文件，则应将其重命名为过滤器.any，并且不要忘记在场文件中改编引用该文件的$include语句。

   * 但是，如果文件夹包含多个具有该模式的特定场文件，则应将其内容复制到$include语句中，该语句在场文件中引用这些文件。

   * 将文件conf.dispatcher/filters/default_filters.any从默认调度程序配置复制到该位置。

   * 在每个场文件中，替换任何筛选器都包含如下语句：

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`with语句：

      `$include "../filters/default_filters.any"`

1. **检查渲染**

   * 输入目录conf.dispatcher.d/renders。

   * 删除该文件夹中的所有文件。

   * 将文件conf.dispatcher.d/renders/default_renders.any从默认调度程序配置复制到该位置。

   * 在每个场文件中，删除渲染部分中的任何内容，并将其替换为：

      `$include "../renders/default_renders.any"`

1. **检查虚拟主机**

   * 重命名该目 `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` 录并输入它。

   * 删除任何预先修复的文件 `ams_`。

   * 如果conf.dispatcher.d/virtualhosts现在包含单个文件，则应将其重命名为virtualhosts.any，并且不要忘记在场文件中也改编引用该文件的$include语句。

   * 但是，如果文件夹包含多个具有该模式的特定场文件，则应将其内容复制到$include语句中，该语句在场文件中引用这些文件。

   * 将文件conf.dispatcher/virtualhosts/default_virtualhosts.any从默认调度程序配置复制到该位置。

   * 在每个场文件中，替换任何筛选器都包含如下语句：

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
with语句：

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **通过运行验证程序检查您的状态**

   * 使用调度程序子命令在您的目录中运行调度程序validator:

      `$ validator dispatcher`

   * 如果看到缺少包含文件的错误，请检查是否正确重命名了这些文件。

   * 如果看到有关未定义变量的 `PUBLISH_DOCROOT`错误，请将其重命名 `DOCROOT`为。

   * 有关所有其他错误，请参阅验证程序工具文档的“疑难解答”部分。

## 使用本地部署测试配置 {#testing-config-local-deployment}

>[!IMPORTANT]
> 使用本地部署测试配置需要安装Docker。

使用Dispatcher `docker_run.sh` SDK中的脚本，您可以测试配置是否不包含任何只会在部署中显示的其他错误：

1. 使用验证程序生成部署信息

   `validator full -d out`
这将验证完整配置并生成外部部署信息

1. 将调度程序与该部署信息开始到docker映像中

   在macOS计算机上运行AEM发布服务器时，监听端口4503，您可以按如下方式在该服务器前运行开始程序：

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   这将开始容器并暴露本地端口8080上的Apache。

## 使用新的调度程序配置 {#using-dispatcher-config}

如果验证程序不再报告任何问题，且Docker容器开始未出现任何故障或警告，您就可以将配置移动到git存储库的`ispatcher/src` d子目录。