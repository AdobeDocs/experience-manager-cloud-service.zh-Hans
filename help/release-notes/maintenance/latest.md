---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 60952db4172b882b71a0b230fc8f4c27154e9cc0
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 71%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 15977 {#release-15977}

下面总结了维护版本 15977 的持续改进，该版本已于 2024 年 4 月 19 日公开发布。上一个维护版本是版本 15939。

2024.4.0 功能激活提供此维护版本的全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-15977}

* GRANITE-51335：优化 AEM 运行状况检查以提高实例稳定性。

### 修复的问题 {#fixed-issues-15977}

* CQ-4357226：修复 IMS 配置对 OAuth 凭证的支持回归问题。
* GRANITE-51335：速率限制升级至 5.0.4 修复了 Felix 运行状况检查注册。

### 已知问题 {#known-issues-15977}

* **（仅适用于 AEM Forms）**&#x200B;安装 AEM Cloud Foundation 维护版本 15977 后，自适应表单字段在表单创作期间和发布表单时以错误的顺序呈现。如果您使用AEM Forms，Adobe建议在即将发布的维护版本中解决该问题之前不要升级到15977版本。 这样做可以帮助您避免任何不便。

### 已弃用的功能和 API {#deprecated-15977}

* [在 Adobe Developer Console 中弃用 JWT 凭据](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* 自2024年5月1日起，AdobeDynamic Media将停止支持以下内容：

   * SSL（安全套接字层）2.0
   * SSL 3.0
   * TLS（传输层安全性） 1.0和1.1
   * TLS 1.2中的以下弱加密：
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


要了解AEMas a Cloud Service中已弃用或删除的内容，请参阅 [已弃用和已删除的功能和API](/help/release-notes/deprecated-removed-features.md).

### 嵌套的技术 {#embedded-tech-15977}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.24.6 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
