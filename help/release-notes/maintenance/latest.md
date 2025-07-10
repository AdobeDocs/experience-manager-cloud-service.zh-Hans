---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 17064d27dd34bbd5aad89f814481c29b0f6a7fe1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 58%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 21484 {#21484}

以下总结了维护版本21484的持续改进，该版本于2025年7月10日公开发布。 上一个维护版本是版本 21331。

激活 2025.7.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-21484}

无。

### 修复的问题 {#fixed-issues-21484}

无。

#### AEM 指南 {#guides-21484}

* GUIDES-29781：在Source视图的元素中添加XML注释时，切换视图时注释周围的前导和尾随空格会丢失。
* GUIDES-29078：在浏览器刷新后在“创作”视图中打开主题时，先前在“文件属性”面板中应用的标记不会保留，添加新标记会覆盖现有标记，尤其是当大量标记可供选择时。
* GUIDES-28214：尝试通过AEM工作流创建审阅任务失败，因为未创建审阅节点。
* GUIDES-28104：发布具有`chunk=to-content`属性的DITA映射会在新的AEM Sites输出中创建重复的JCR节点，从而导致AEM Sites中的内容结构冗余。
* GUIDES-29065和GUIDES-28793：处理大型收藏集时会发现性能问题，例如加载时间较长以及间歇性超时。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-21484}

无。

### 已弃用的功能和 API {#deprecated-21484}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-21484}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 5 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-21484}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
