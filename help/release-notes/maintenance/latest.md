---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 5d00bed4008c70e81f3a70d219ddc411ec8bdc59
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 94%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 21484 {#21484}

以下是维护版本 21484 的持续改进摘要，该版本已于 2025 年 7 月 10 日正式发布。上一个维护版本是版本 21331。

激活 2025.7.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-21484}

无。

### 修复的问题 {#fixed-issues-21484}

无。

#### AEM Guides {#guides-21484}

* GUIDES-29781：在源视图中的元素内添加 XML 注释时，切换视图时注释周围的前导空格和尾随空格会丢失。
* GUIDES-29078：刷新浏览器后在“创作”视图中打开某个主题时，“文件属性”面板中先前应用的标记不会被保留，且在可选标记数量较多的情况下，新增标记会覆盖原有标记。
* GUIDES-28214：由于审核节点未被创建，通过 AEM 工作流创建审核任务的尝试始终失败。
* GUIDES-28104：在发布带有 `chunk=to-content` 属性的 DITA 映射时，新的 AEM Sites 输出中会生成重复的 JCR 节点，导致 AEM Sites 中出现冗余的内容结构。
* GUIDES-29065、GUIDES-28793：在处理大型集合时，会出现加载时间较长及间歇性超时等性能问题。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-21484}

* 在软件分发门户中提供的SDK在本地运行时出现问题。 请继续使用以前的SDK进行本地测试。

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
