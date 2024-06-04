---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 558babc0124a8ee8c1337b91c5ef016ed238c935
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 46%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 16544 {#release-16544}

以下总结了维护版本16544的不断改进，该版本于2024年6月4日公开发布。 上一个维护版本是版本 16461。

2024.6.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-16544}

* GRANITE-41133：支持Jakarta Servlet API 5和OSGi Servlet Whiteboard API。
* GRANITE-51355：弃用org.slf4j.event。
* GRANITE-51565：从AEM发布本地组时，AEM会丢失与外部组的本地组关系。
* GRANITE-51707：在http重定向期间设置Cookie saml_request_path以进行身份验证。
* GRANITE-52010：将 Jackrabbit 版本更新到 2.20.16。
* GRANITE-52057：将Filevault更新为3.7.3-T20240514105118-694f6aea，以修复JCRVLT-745。
* SKYOPS-35998：更新“Sling RepoInit”依赖项：Repoinit解析器1.9.0、Repoinit JCR 1.1.46。

### 修复的问题 {#fixed-issues-16544}

* DXML-17171： AEM Guides：对超过15KB的主题执行复制和粘贴操作失败，并出现意外错误。
* DXML-17088： AEM Guides：用于更改文档状态的功能 **文件属性** 面板无法正常工作，并且已更改为 *草稿* 省/州。
* DXML-16931： AEM Guides：主题中的链接图像在创建版本后无法在基线中显示。
* DXML-16896： AEM Guides：可重用内容面板在以下情况下不列出元素： **用户首选项** 设置为通过以下方式查看文件 **文件名**.
* GRANITE-51375：如果未指定中间路径，则idp-sync会引发NPE。

### 已知问题 {#known-issues-16544}

无。

### 已弃用的功能和 API {#deprecated-16544}

若要了解 AEM as a Cloud Service 中已弃用或移除的功能，请参阅[已弃用和已移除的功能和 API。](/help/release-notes/deprecated-removed-features.md)

### 嵌套的技术 {#embedded-tech-16544}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.25.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
