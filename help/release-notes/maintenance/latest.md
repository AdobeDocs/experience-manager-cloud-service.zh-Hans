---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 5e216e45a1400299efcc418007ddbe93f0c571a1
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 35%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 15939 {#release-15939}

以下总结了维护版本15939的不断改进，该版本于2024年4月17日公开发布。 上一个维护版本是版本 15860。

2024.4.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hans)。

### 增强 {#enhancements-15939}

* GRANITE-39892：更新队列大小限制的分布，发布准备就绪。
* GRANITE-48777：将QS更新为com.adobe.granite.security.user-0.4.84，已完成。
* GRANITE-49421：为区段服务主体添加了属性。
* GRANITE-49855：编写功能模型分析器，在使用新commons.json的情况下，该分析器无法通过快速入门构建。
* GRANITE-47995：允许切换cq：isDelivered的写入。
* GRANITE-36205：将内部Oak发行版本更新为最新版本。
* GRANITE-50156将AEMCS关联绑定到通用编辑器的IMS用户ID。
* GRANITE-50556：将交叉通路捆绑包升级到v0.1.18。
* GRANITE-50728：将FileVault更新为3.7.3-T20240308111857-81fa88f1。
* GRANITE-50957：将QS更新为com.adobe.granite.repository ，从而更新为1.8.114。
* GRANITE-50158：在YAML加载程序中添加对“服务器凭据”流的OAuth服务器支持。
* GRANITE-51327：将Oak更新到最新公共版本(1.62.0)。
* SKYOPS-68091将Java 11运行时映像更新到版本3.0.0。
* SKYOPS-70421：升级org.apache.sling.servlet-helpers捆绑包
* SKYOPS-73483：允许在AEM上记录令牌。

### 修复的问题 {#fixed-issues-15939}

* GRANITE-46901：将量度添加到消息传送客户端。
* GRANITE-48793：将QS更新为com.adobe.granite.crx-explorer-1.1.28。
* GRANITE-48937： Omniseaarch在aem/start.html页面上不起作用。
* GRANITE-49638：修复RUM转换器工厂的内容类型配置错误。
* GRANITE-50141： IMSProviderImpl正在发送垃圾邮件。
* SITES-20949：在Youtube添加referrerpolicy=&quot;strict-origin-when-cross-origin&quot;后，ComponentsIT.testEmbed失败。
* SITES-21233：核心组件更新 — 升级到15860后，修复适用于GS1美国的折叠面板。
* SKYOPS-74819：Apache Commons中重复键向后兼容性损坏。
* SKYOPS-67087：在某些情况下，Clientlib聚合不起作用。
* CQ-4355415：AEM通知链接在6.5 SP18中不起作用。

### 已知问题 {#known-issues-15939}

无。

### 已弃用的功能和 API {#deprecated-15939}

* [在 Adobe Developer Console 中弃用 JWT 凭据](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

查看[已弃用和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)，了解 AEM as a Cloud Service 中已弃用或移除的功能。

### 嵌套的技术 {#embedded-tech-15939}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.24.6 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
