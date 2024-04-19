---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: f15b42e4012385c461b5440b92f53c4e58fb8ac2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 71%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 15977 {#release-15977}

以下总结了维护版本15977的不断改进，该版本于2024年4月19日公开发布。 上一个维护版本是版本 15939。

2024.4.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-15977}

* GRANITE-51335：优化AEM运行状况检查以提高实例稳定性。

### 修复的问题 {#fixed-issues-15977}

* CQ-4357226：修复了支持OAuth凭据的IMS配置中的回归。
* GRANITE-51335： Ratelimit升级到5.0.4已修复Felix运行状况检查注册。

### 已知问题 {#known-issues-15977}

无。

### 已弃用的功能和 API {#deprecated-15977}

* [在 Adobe Developer Console 中弃用 JWT 凭据](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

查看[已弃用和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)，了解 AEM as a Cloud Service 中已弃用或移除的功能。

### 嵌套的技术 {#embedded-tech-15977}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.24.6 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
