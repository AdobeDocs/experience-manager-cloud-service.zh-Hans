---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 2e90e40a0fe439653987a23792a4c1ec612aafd6
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 57%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 21570 {#21570}

以下总结了维护版本21570的持续改进，该版本于2025年7月15日公开发布。 上一个维护版本是版本 21484。

>[!NOTE]
>
>[版本21484](/help/release-notes/maintenance/2025/2025-7-0.md#21484)已设为私有，并由版本21570替换。

激活 2025.7.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-21570}

* 已迁移到Apache Httpd 2.4.63

### 修复的问题 {#fixed-issues-21570}

* SKYOPS-112722 — 修复了导致虚URL解析失败的问题

### 已知问题 {#known-issues-21570}

* 相关的AEM SDK具有不同的版本ID (21575)，可通过软件分发门户获取。
* Apache HTTP Server版本2.4.63对`mod_rewrite`处理URL中的问号(`?`)的方式进行了重大更改。 实施此更改是为了防止使用被视为安全风险的`UnsafeAllow3F`标志。 这会影响依赖于URL模式中问号检测的任何`RewriteRule`指令。

### 已弃用的功能和 API {#deprecated-21570}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-21570}

无

### 嵌入的技术 {#embedded-tech-21570}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
