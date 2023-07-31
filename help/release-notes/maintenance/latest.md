---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 704f4e250975d8c0cbcfdc5e49b9c03d3a3e2939
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 82%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 12790 {#release-12790}

下面总结了维护版本 12790 的持续改进，该版本已于 2023 年 7 月 21 日公开发布。此维护版本是对上一个维护版本 12697 的更新。

激活 2023.7.0 功能后可为此次维护版本提供完整的功能集。有关更多信息，请参阅[ Experience Manager 发布路线图。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

### 增强 {#enhancements-12790}

无。

### 修复的问题 {#fixed-issues-112790}

- SLING-11974 — 修复了SlingHttpServletRequest#getUserPrincipal中对未经身份验证的请求的回归。 此修复程序可确保即使对于未经身份验证的请求，也会返回主体。

### 已知问题 {#known-issues-12790}

- GRANITE-46601 — 如果在没有SDK的情况下，快速入门SDK将无法在jdk 11.0.20上启动 `-Djdk.util.zip.disableZip64ExtraFieldValidation=true` java选项

### 嵌套的技术 {#embedded-tech-12790}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.23.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
