---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: ca9b5965dbfade36763e2432601559c9abcd2d41
workflow-type: ht
source-wordcount: '572'
ht-degree: 100%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 17689 {#release-17689}

下面总结了对维护版本 17689 的持续改进，该版本已于 2024 年 9 月 10 日公开发布。上一个维护版本是版本 17569。

2024.9.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-17689}

* ASSETS-41404：经过更改以支持改进 DRM。
* ASSETS-41621：更新了异步资产复制作业。
* ASSETS-32166：更新了异步资产移动作业。
* ASSETS-41429：DM OpenAPI 中支持图像预设。
* ASSETS-38968：改进内容片段引用的展现方案。
* ASSETS-41787、ASSETS-41183：改进资产批量操作框架。
* GRANITE-52917：优化以缩短内容复制包的安装时间。
* SCRNS-3980：检测没有计划资产的子序列的播放器灰屏的情况。

### 修复的问题 {#fixed-issues-17689}

* ASSETS-40875：AssetDeleteHandler 记录了虚假的 NPE。
* ASSETS-42422：避免触发单个资产移动的异步作业。
* ASSETS-41234：Unified Shell，如果在搜索栏打开时打开全局导航，则它可能会不起作用。
* ASSETS-42256：Unified Shell，标记/徽章指示环境仅间歇性地工作。
* ASSETS-41271：防止在移动操作期间不必要地重新发布资产。
* ASSETS-38894：通过处理监视器限制重试。
* ASSETS-40815：使用预览 PDF 演绎版在链接共享 UI 中显示 PPT 文件。
* ASSETS-37123：无法在链接共享对话框中加载资产预览。
* CQ-4358156：更新被删除的标记的反向链接。
* SCRNS-4495：修复了粘贴按钮对于不同的用户组无法正常使用的问题。
* SCRNS-4512：从 AEMaaCS 屏幕中删除与设备相关的组件。
* SCRNS-4466：在渠道仪表板上，隐藏 - 查看清单，生成离线内容，更新清单缓存，显示面板。
* SCRNS-4513：在列表视图中为搜索结果页面添加列标题。

### 已知问题 {#known-issues-17689}

* FORMS-14340：FormsAndDocumentOmniSearchHandler 和 CloudStorageSubmitActionInserter 实例化时出错。这些是无害的日志语句。
* FORMS-15818：组件描述符条目“OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml”在服务器日志中未找到语句。这些是无害的日志语句。
* SITES-23662：无法从服务器日志中的 JCR 日志语句中提取触发发布的用户。这是针对正在开发的功能，可能会导致日志中出现间歇性且无害的“无法在 OSGI 事件批次中找到有效的用户 ID”错误。

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
