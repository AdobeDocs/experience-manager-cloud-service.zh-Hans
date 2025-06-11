---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d3cdc3d69c0002c5b124150050f905123457331c
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 48%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 21193 {#21193}

以下总结了维护版本21193的不断改进，该版本于2025年6月10日公开发布。 上一个维护版本是版本 21005。

激活 2025.6.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-21193}

* Assets-51245：提高了触屏UI中大型文件夹列表的性能。
* Assets-51686：改进了批量操作作业，包括更轻松的作业取消、增强的日志记录、审核下载以获取大量结果。
* CQ-4360131：改进了OpenAPI端点的错误响应，允许API客户端接收正确的结构化错误信息。

### 修复的问题 {#fixed-issues-21193}

* Assets-41007：已删除的资产可以在Content Hub中保持可见。
* Assets-50994： AemRequestEventFilter导致Jetty线程过多争用。
* Assets-50155：触发了重复的元数据更改事件。
* Assets-50716：在Assets列表视图中按标题排序无法按预期工作。
* Assets-50820：确保正确拒绝对资源关系API的无效请求，并显示400错误。
* Assets-50562：默认情况下，资源上传API会创建名称冲突版本。
* Assets-50992： Assets API initiateUpload.json端点应返回“application/json”内容类型。
* Assets-51322：自动移除并过期在失败作业后无限期保留的异步阻止程序。
* Assets-51809：由于浏览器缓存，CSV编辑器未显示最近保存的更改。
* SITES-31678：具有上下文感知引用的体验片段(XF)未在XF发布API中解析正确的语言根。


### 已知问题 {#known-issues-21193}

无。

### 已弃用的功能和 API {#deprecated-21193}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-21193}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 2 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-21193}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
