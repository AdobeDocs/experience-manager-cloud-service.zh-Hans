---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 8f7c2fc175a542df5725693cfc332802d54e1e88
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 88%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 16544 {#release-16544}

下面总结了维护版本 16544 的持续改进，该版本已于 2024 年 6 月 4 日公开发布。上一个维护版本是版本 16461。

2024.6.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!CAUTION]
>
>请使用下面引用的SDK，因为之前的该SDK已经确认了回归：
>`AEM SDK v2024.06.16647.20240607T103723Z-240500`

### 增强 {#enhancements-16544}

* GRANITE-41133：支持 Jakarta Servlet API 5 和 OSGi Servlet Whiteboard API。
* GRANITE-51355：弃用 org.slf4j.event。
* GRANITE-51565：当本地组从 AEM 发布时，AEM 会失去与外部组的本地组关系。
* GRANITE-51707：在 http 重定向期间设置 cookie saml_request_path 进行身份验证。
* GRANITE-52010：将 Jackrabbit 版本更新到 2.20.16。
* GRANITE-52057：将 Filevault 更新至 3.7.3-T20240514105118-694f6aea，修复 JCRVLT-745。
* SKYOPS-35998：更新“Sling RepoInit”的依赖项：Repoinit Parser 1.9.0、Repoinit JCR 1.1.46。

### 修复的问题 {#fixed-issues-16544}

* GRANITE-51375：如果未指定中间路径，idp-sync 将引发 NPE。
* GUIDES-17171：超过 15KB 的主题复制和粘贴操作失败，并出现意外错误。
* GUIDES-17088：从&#x200B;**文件属性**&#x200B;面板更改文档状态的功能无法正常工作，只能更改为&#x200B;*草稿*&#x200B;状态。
* GUIDES-16931：创建版本后，主题中的链接图像无法显示在基线中。
* GUIDES-16896：当&#x200B;**用户偏好设置**&#x200B;设置为按&#x200B;**文件名**&#x200B;查看文件时，可重复使用的内容面板不会列出元素。

有关 Experience Manager Guides 中的新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/cn/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-16544}

无。

### 更改通知 {#change-notice-16544}

从2024年9月开始，AEMas a Cloud Service将通过Sling模型导出器框架禁用资源解析器的序列化。 请参阅 [文档](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) 以了解更多详细信息。

### 已弃用的功能和 API {#deprecated-16544}

若要了解 AEM as a Cloud Service 中已弃用或移除的功能，请参阅[已弃用和已移除的功能和 API。](/help/release-notes/deprecated-removed-features.md)

### 嵌套的技术 {#embedded-tech-16544}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.25.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
