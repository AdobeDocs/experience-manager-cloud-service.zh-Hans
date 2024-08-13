---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a1baa7f29c6e15af11347debdd341f9972c06e83
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 100%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 17258 {#release-17258}

下面总结了维护版本 17258 的持续改进，该版本已于 2024 年 7 月 30 日公开发行。上一个维护版本是版本 17098。

2024.8.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-17258}

* ASSETS-31445 - 初始动态媒体模板功能
* ASSETS-40399 - 更新了 DM 自动转录队列设置
* ASSETS-40873 - 允许通过 OSGI 配置设置元数据导出最大行数

### 修复的问题 {#fixed-issues-17258}

* ASSETS-30613 - 替换资产不会在新的交付层中删除和添加资产
* ASSETS-31882 - 禁止访问作者中的流式清单文件
* ASSETS-39598 - 批量导入无法从 S3 后端删除名称中带有特殊字符的资产
* CNTBF-209 - 回流作业取消改进
* SCRNS-3762 - 改进序列频道中的 playerLogger，以便在浏览器上预览频道时将日志放在控制台上
* SCRNS-4455：频道内容提供商中 NON-ADMIN 用户缺少“管理发布”和“快速发布”按钮。
* SITES-22940 - 无法将内容片段视为工作流负载

### 已知问题 {#known-issues-17258}

无

### 更改通知 {#change-notice-17258}

* 从 2024 年 9 月开始，AEM as a Cloud Service 将会通过 Sling Model Exporter 框架禁用资源解析器的序列化。请参阅[该文档](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)了解更多详情。

### 已弃用的功能和 API {#deprecated-17258}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 嵌套的技术 {#embedded-tech-17258}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.25.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
