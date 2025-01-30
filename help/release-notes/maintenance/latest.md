---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a3c414f9b5e575856a942e02661e8c70a7083495
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 35%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 19149 {#19149}

以下总结了维护版本19149的持续改进，该版本于2025年1月21日公开发布。 上一个维护版本是版本 18751。

激活 2025.1.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-19149}

* Assets-45286：显示下载存档异步作业的粒度进度。
* Assets-46296：支持资产选择器中的Dynamic Media模板。
* Assets-44796：为DAM异步资源作业触发Assets事件。

### 修复的问题 {#fixed-issues-19149}

* GRANITE-55074：确保在错误响应上设置CORS响应标头。
* Assets-43755：改进了可批量处理资源的可扩展性。
* Assets-45399：在创建Asset Live-copy后重定向到Assets Console。
* Assets-45462：自定义文件夹缩略图存在浏览器缓存问题。
* Assets-46398：隐藏DM模板的下载和重新处理操作。
* Assets-44484：重新保存连接的Assets配置时出现问题。
* Assets-44122：异步复制资源作业在复制到当前文件夹时不会重命名目标文件夹。
* Assets-44463：成功导出元数据时，“下载CSV”按钮不可见。
* Assets-45134：使用目标标题移动作业会覆盖所有文件夹标题。
* Assets-45137：与通过Assets视图批量上传冲突。
* Assets-45758：资源关系在添加关系后获得无限忙/加载动画。
* Assets-44148： AEM中的NODE_MOVED事件可能会导致日志中出现假的NPE。
* Assets-28607：设置自定义视频缩略图时出现JS错误。
* GRANITE-55781：改进Adobe Developer Console和AEM之间的组同步。 有关[用户组和产品配置文件同步中的更改](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)的更多详细信息。
* GRANITE-55754：确保SDK启动脚本支持Java 21。
* GRANITE-54248：无法滚动查看大型资源文件夹中的所有项目。
* SCRNS-4597：搜索结果列表视图改进。


### 已知问题 {#known-issues-19149}

无。

### 已弃用的功能和 API {#deprecated-19149}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

#### 用户组和产品轮廓同步变更

使用Adobe Admin Console进行权限管理时，不得使用以下组，因为它们将不再与AEM同步：
* 以_GROUP_NAME_SUFFIX结尾的AEM组。
* 来自其他环境、项目或产品的产品配置文件。

有关更多详细信息，请检查用户组和产品配置文件同步中的[更改](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)。

#### 弃用SPA编辑器 {#deprecate-spa-editor}

[从2025.1.0版开始的新项目已弃用SPA编辑器](/help/implementing/developing/hybrid/introduction.md)。现有项目仍支持SPA编辑器，但不应将其用于新项目。

在AEM中管理Headless内容的首选编辑器包括：

* [用于可视化编辑的通用编辑器](/help/edge/wysiwyg-authoring/authoring.md)。
* [用于基于表单的编辑的内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)。

### 安全修复 {#security-19149}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 4 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-19149}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
