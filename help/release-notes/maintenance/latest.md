---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 4353f2a9f6cd649a4377adb9891e0873a51d6ab2
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 11873 {#release-11873}

下面总结维护版本 11873 的持续改进，该版本于 2023 年 5 月 3 日公开发布。此维护版本是对上一个维护版本 11835 的更新。

此维护版本的功能支持将为您提供完整功能集。有关完整详细信息，请参阅[最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 增强功能 {#enhancements}

- SITES-1200 - 增强 API 搜索功能，带有基于标签的过滤功能
- GRANITE-42939 - 向 oauth 服务器代码添加弃用注释和警告

### 已知问题 {#known-issues-11873}

- SITES-13253 — 核心组件中的RecursionTooDeepException v2.22.6
- SITES-13256 — 配置了特殊URL的核心WCM Teaser中断页面渲染
- GRANITE-45462 — 消息传送客户端多区域配置
- GRANITE-45562 — 图像组合返回200而不是404时出现问题

### 修复的问题 {#fixed-issues-11873}

- SKYSI-19884/SKYOPS-53745 - 修复了 PublishPageRenderingErrorsHigh 的问题
- GRANITE-4388 - 修复了在 Mongo 上写入大量 DAM 资产后吞吐量下降的问题
- SITES-11922 - 修复了从未删除同步状态的预览中取消发布的问题
- ASSETS-21648 - 修复了资产相关功能的权限问题

### 嵌套的技术 {#embedded-tech-11873}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | 版本 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.22.6 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
