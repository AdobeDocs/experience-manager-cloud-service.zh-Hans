---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 8ee3da55024c0f5246f6c194bc07172b4b71823a
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 49%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 22758 {#22758}

以下总结了维护版本22758的持续改进，该版本于2025年10月1日公开发布。 上一个维护版本是版本 22450。

激活 2025.10.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[&#x200B; Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-22758}

* Assets-56227：重命名adobe-countdown-timer修饰符。
* CNTBF-493：将Bump content-backflow包版本更改为2.0.28。
* CQ-4361110： Granite翻译。
* CQ-4361112：最新的AEM翻译。
* GRANITE-56026：改进权限API状态代码响应。
* GRANITE-61015：已将`org.apache.commons.io.channels`包添加到公共导出列表。
* GRANITE-61167： Felix日志已更新为最新的OSGI规范。
* GRANITE-61167：更新Felix依赖项。
* GRANITE-61169：改进对受保护字符串的检查。
* GRANITE-61622：更新Sling依赖项。
* GRANITE-61663：将`com.adobe.granite.repository.indexdefs-1.0.2`添加到快速入门。
* GRANITE-61811：将`com.adobe.granite.repository-2.0.0`添加到快速入门。
* SITES-32014：侦听外部事件以更新服务注册。
* SITES-34277：修复页面翻译工作流中的阻塞错误。
* SKYOPS-108706：升级后的版本可切换捆绑到最新版本（etag缓存）。
* SKYOPS-114210：正在更新到最新版本的aem.pss.service捆绑包。
* SKYOPS-116171：更新至 Sling ResourceResolver 1.12.12。
* SKYOPS-119811：发布了dispatcher-publish 2.0.258。

### 修复的问题 {#fixed-issues-22758}

* GRANITE-61875：修复了“表达式评估无效”的触发器 — 作者无法保存内容片段，且无法下载资产。
* SITES-22059：修复PDF查看器组件中的JS错误。 核心组件网站> PDF查看器中的未本地化的“文件预览不可用”字符串。
* GRANITE-59704：修复htmllibmanager.debug会导致编辑模式失败。
* GRANITE-61042：将FELIX-6796（ServiceTracker NPE修复）集成到AEM Felix Web控制台捆绑包中。
* GRANITE-61165：Workspace.copy()引发RepositoryException。
* GRANITE-61875：将ui.commons更新为5.10.50。

### 已知问题 {#known-issues-22758}

无。

### 已弃用的功能和 API {#deprecated-22758}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-22758}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 13 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-22758}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.86.0 | [Oak 1.86.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.30.1 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
