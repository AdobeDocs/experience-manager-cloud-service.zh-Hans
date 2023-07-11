---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: e1183791f543d17f98cb6c9ca0c513c8936ef477
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 47%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 12585 {#release-12585}

维护版本12585的不断改进概述如下，该版本于2023年7月11日公开发布。 此维护版本是对上一个维护版本 12549 的更新。

2023.7.0功能激活将提供此维护版本的完整功能集。 请参阅 [Experience Manager版本路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) 了解更多信息。

### 增强 {#enhancements-12585}

- 常规RDE稳定性改进(SKYOPS-61133、SKYOPS-55281、SKYOPS-61216和SKYOPS-61401)
- DXML-12327： AEM Guides：支持本机PDF发布中的语言变量
- DXML-11518： AEM Guides：增强了本机PDF发布中的元数据支持
- DXML-10093： AEM Guides：支持连接到外部数据源并将数据插入dita主题
- DXML-10699： AEM Guides：支持翻译中的XLIFF格式
- DXML-10141： AEM Guides：使用基于微服务的发布进行PDF（本机和DITA-OT）、HTML和自定义预设类型的选项

### 修复的问题 {#fixed-issues-12585}

- AEM Guides：各种本机PDF增强功能和稳定性修复
- SKYOPS-53130：改进RDE中的AC工具支持
- SKYOPS-57146：修复AEM启动时的Sling死锁

### 已知问题 {#known-issues-12585}

无。

### 嵌套的技术 {#embedded-tech-12585}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 版本 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.23.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
