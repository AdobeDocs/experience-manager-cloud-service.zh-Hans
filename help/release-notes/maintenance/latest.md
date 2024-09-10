---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9323464610b804ff407f5eedf404ab2cca93a8da
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 46%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 17689 {#release-17689}

以下总结了维护版本17689的不断改进，该版本于2024年9月10日公开发布。 上一个维护版本是版本 17569。

2024.9.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-17689}

* Assets-41404：进行了相应更改以支持DRM改进。
* Assets-41621：更新了异步资产复制作业。
* Assets-32166：更新了异步资产移动作业。
* Assets-41429： DM OpenAPI中的图像预设支持。
* Assets-38968：改进内容片段引用的表示方式。
* Assets-41787、ASSETS-41183：对Assets批量操作框架的改进。
* GRANITE-52917：优化了内容Copy包的安装时间。
* SCRNS-3980：检测播放器上的灰色屏幕，查看是否有未计划任何资产的子序列。

### 修复的问题 {#fixed-issues-17689}

* Assets-40875：由AssetDeleteHandler记录的虚假NPE。
* Assets-42422：避免为单个资产移动触发异步作业。
* Assets-41234： Unified Shell — 如果在打开搜索栏时打开，全局导航可能无法工作。
* Assets-42256： Unified Shell — 标记/徽章，指示环境仅间歇性地工作。
* Assets-41271：防止在移动操作期间不必要地重新发布Assets。
* Assets-38894：按处理监视程序限制重试。
* Assets-40815：使用预览PDF演绎版在链接共享UI中显示PPT文件。
* Assets-37123：无法在链接共享对话框中加载资源预览。
* CQ-4358156：更新要删除的标记的反链接。
* SCRNS-4495：修复的“粘贴”按钮对于不同的用户组无法正常工作。
* SCRNS-4512：从AEMaaCS屏幕中删除与设备相关的组件。
* SCRNS-4466：在渠道功能板上，隐藏 — 查看清单、生成离线内容、更新清单缓存、显示面板。
* SCRNS-4513：在列表视图中为搜索结果页面添加列标题。

### 已知问题 {#known-issues-17689}

* Forms-14340：实例化FormsAndDocumentOmniSearchHandler和CloudStorageSubmitActionInserter时出错。 这些是无害的日志语句。
* Forms-15818：组件描述符条目&quot;OSGI-INF/com.adobe.aemfd.docmanager.impl.在服务器日志中找不到*.xml&#39;语句。 这些是无害的日志语句。
* SITES-23662：无法从服务器日志中的JCR日志语句中提取触发发布的用户。 这是针对正在开发的功能，该功能可能会在日志中导致“在批次OSGI事件中找不到有效用户ID”的间歇性且无害的错误。

### 更改通知 {#change-notice-17689}

* 从 2024 年 9 月开始，AEM as a Cloud Service 将会通过 Sling Model Exporter 框架禁用资源解析器的序列化。请参阅[该文档](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)了解更多详情。

### 已弃用的功能和 API {#deprecated-17689}

请注意，我们正在更新 `com.day.cq.wcm.api`，并且在当前版本中，我们已将其中的一些方法和类标记为 `@Deprecated`。这些将在未来的版本中删除，所以如果您正在使用其中任何一个，请考虑切换到其建议的替代方案。

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-17689}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 4 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-17689}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.68.0 | [Oak API 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.26.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
