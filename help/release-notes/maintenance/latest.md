---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 573de431328650778b3ef0979a24190477382310
workflow-type: ht
source-wordcount: '332'
ht-degree: 100%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 17098 {#release-17098}

下面总结了维护版本 16799 的持续改进，该版本已于 2024 年 7 月 16 日公开发行。上一个维护版本是版本 16971。

2024.7.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-17098}

- SKYOPS-79817：为服务用户映射启用 Sling 功能分析器任务

### 修复的问题 {#fixed-issues-17098}

- ASSETS-39665：从 6.5 迁移到 AEMCS 后，Smart Crops Sync 不起作用
- FORMS-14993：表格 API 返回 500，用于之前的工作抵押品
- GRANITE-52120：显示 Access 控制数据时 CRXDE 返回 500
- GRANITE-52573：在重写的 URL 中使用 // 时请求返回 400
- GRANITE-52746：创建节点对话框中未加载所有节点类型
- GRANITE-52777：请求包装时 404 处理中断
- GRANITE-52871：确保 publish-worker 与 golden-publish 同步并在压缩之前完成
- SKYOPS-79173：复制器未复制到与给定 AgentIdFilter 匹配的多个代理
- SKYOPS-80075：资产名称中的变音符号问题导致发布队列阻塞（Mac）
- SKYOPS-81032：使用增强日志记录时，过滤掉获取日志的请求生成的日志

### 已知问题 {#known-issues-17098}

无

### 更改通知 {#change-notice-17098}

- 从 2024 年 9 月开始，AEM as a Cloud Service 将会通过 Sling Model Exporter 框架禁用资源解析器的序列化。请参阅[该文档](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)了解更多详情。

### 已弃用的功能和 API {#deprecated-17098}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 嵌套的技术 {#embedded-tech-17098}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.25.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
