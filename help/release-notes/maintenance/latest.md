---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: dc7f95ac98fd300a803e307ce11a51937d604a07
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 30%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 18459 {#18459}

以下总结了维护版本18459的不断改进，该版本于2024年11月5日公开发布。 上一个维护版本是版本 18311。

激活 2024.11.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-18459}

* CQ-4357471：在AEMaaCS中添加对i18n词典翻译的支持。
* SITES-23591：内容片段：升级内容片段以支持UUID。
* SITES-25440：内容片段：CFM搜索API可显示复制状态。
* SITES-24369：内容片段：OpenAPI文档改进。
* SITES-25478：内容片段：为外部资产引用添加后端支持。
* SITES-26119：内容片段：添加对引用类型中的外部资产引用的支持。
* SITES-21199：带有通用编辑器的Edge Delivery：为从页面创建的模板添加支持。
* SITES-20311：带有通用编辑器的Edge Delivery：添加支持以将CSV导入电子表格。
* SITES-24821：带有通用编辑器的Edge Delivery：将aem.page / aem.live设置为默认与Edge Delivery集成。

### 修复的问题 {#fixed-issues-18459}

* CQ-4358730：当要翻译的键超过10个时，CQPagePreviewGenerator失败。
* Forms-14978：为主题编辑器的基于核心组件的表单启用页面加载。
* Forms-16596：辅助功能问题：屏幕Reader无法识别已禁用的按钮。
* SITES-10575： MSM：Blueprint Bloomfilter加载器尝试加载超过100,000行。
* SITES-20755：内容片段：刷新UUID的资源引用不显示缩略图。
* SITES-26253：内容片段：UUID迁移：将sling作业主题更改为通用。
* SITES-21338：内容片段：referencedBy端点未返回正确的页面引用。
* SITES-24421：内容片段：编辑CF端点不适用于通过GETCF检索的CF。
* SITES-25461：内容片段：在搜索CF时按模型过滤应不区分大小写。
* SITES-25471：内容片段：修复了ModelValidatorServlet中全局模型的验证问题。
* SITES-25795：内容片段：当没有cq日期集时，CF模型API失败。
* SITES-25817：内容片段：增强promoteLaunch：更新CF启动项的上次提升。
* SITES-26030：内容片段：端点/referencesTree未返回所需的标头。
* SITES-26031：内容片段：CFM搜索端点未返回复制状态。
* SITES-26213：内容片段：取消发布内容片段应仅验证已发布的引用。
* SITES-26226：内容片段：当给定路径均不可用时，出现开始工作流问题。
* SITES-26238：内容片段：API返回的资产引用的顺序与JCR中的顺序不同。
* SITES-25456：事件：移动页面时，除页面移动事件外，还会生成页面删除事件。
* SITES-25658：事件：页面内容状态事件中未填充层和sourceUrl。
* SITES-6497：启动项：在启动项中创建页面不起作用。
* SITES-25393：带有通用编辑器的Edge Delivery：呈现带单个段落的格式化富文本时，文本节点丢失。
* SITES-24643：带有通用编辑器的Edge Delivery：OpenGraph和twitter元数据属性在页面元数据模型中不起作用。

### 已知问题 {#known-issues-18459}

无。

### 已弃用的功能和 API {#deprecated-18459}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-18459}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 21 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-18459}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
