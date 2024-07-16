---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 573de431328650778b3ef0979a24190477382310
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 42%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 17098 {#release-17098}

以下总结了维护版本17098的不断改进，该版本于2024年7月16日公开发布。 上一个维护版本是版本 16971。

2024.7.0功能激活将提供此维护版本的完整功能集。 有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-17098}

- SKYOPS-79817：为服务用户映射启用Sling功能分析器任务

### 修复的问题 {#fixed-issues-17098}

- Assets-39665：从6.5迁移到AEMCS后，智能裁剪同步无法正常工作
- Forms-14993：Forms API为以前使用的宣传资料返回500
- GRANITE-52120：CRXDE在显示访问控制数据时返回500
- GRANITE-52573：在重写的URL中使用//时请求返回400
- GRANITE-52746：创建节点对话框中未加载所有节点类型
- GRANITE-52777：请求被封装时对404的处理中断
- GRANITE-52871：确保publish-worker与golden-publish同步，并在压缩前完成
- SKYOPS-79173：复制程序未复制到与给定AgentIdFilter匹配的多个代理
- SKYOPS-80075：资产名称中存在变音问题，导致发布队列阻塞(Mac)
- SKYOPS-81032：使用增强型日志记录时过滤掉请求生成的日志以获取日志

### 已知问题 {#known-issues-17098}

无

### 更改通知 {#change-notice-17098}

- 从 2024 年 9 月开始，AEM as a Cloud Service 将会通过 Sling Model Exporter 框架禁用资源解析器的序列化。请参阅[该文档](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)了解更多详情。

### 已弃用的功能和 API {#deprecated-17098}

AEM as a Cloud Service中已弃用和已删除的功能和API在[已弃用和已删除的功能和API](/help/release-notes/deprecated-removed-features.md)文档中进行了详细介绍。

### 嵌套的技术 {#embedded-tech-17098}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.25.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
