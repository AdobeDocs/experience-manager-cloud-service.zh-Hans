---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: ea3a476f7f2d7d97a2428c6facf61b746dba7a23
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 65%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 11873 {#release-11873}

以下是2023年5月3日公开发布的维护版本11873的持续改进。 此维护版本是对上一个维护版本 11835 的更新。

此维护版本的功能支持将为您提供完整功能集。有关完整详细信息，请参阅[最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 增强功能 {#enhancements}

- SITES-1200 — 通过基于标记的过滤增强了搜索API
- GRANITE-42939 — 向oauth-server代码添加弃用批注和警告

### 已知问题 {#known-issues-11873}

无.

### 修复的问题 {#fixed-issues-11873}

- SKYSI-19884/SKYOPS-53745 — 修复了PublishPageRenderingErrorsHigh的问题
- GRANITE-4388 — 修复了在Mongo上写入大量DAM资产后吞吐量下降的问题
- SITES-11922 — 修复了从预览中取消发布时未删除同步状态的问题
- ASSETS-21648 — 修复了资产相关功能的权限问题

### 嵌套的技术 {#embedded-tech-11873}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 版本 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.21.2 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
