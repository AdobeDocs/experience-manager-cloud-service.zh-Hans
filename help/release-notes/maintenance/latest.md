---
title: 的最新维护发行说明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新维护发行说明 [!DNL Adobe Experience Manager] as a Cloud Service。
source-git-commit: c6acdd922c052d0db5bf1f05bc03329fbc44ca33
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 32%

---


# 维护版本说明 {#maintenance-release-notes}

以下部分概述了当前维护版本的Experience Manageras a Cloud Service的技术发行说明。

## 发行版本 11382 {#release-11382}

以下是2023年3月28日公开发布的维护版本11382的持续改进。 此维护版本是对上一个维护版本 11289 的更新。

此维护版本的功能支持将为您提供完整功能集。有关完整详细信息，请参阅[最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 修复的问题 {#fixed-issues}

- ASSETS-21023 — 修复了智能裁剪呈现，在该呈现版本中，当客户尝试通过API访问这些呈现时，他们可能会在所有AEM环境的发布者实例上看到空指针异常。
- SKYOPS-49280 — 使用RDE在Publish中安装配置或包更新时，可能无法观察到结果，因为Publish调度程序缓存未失效

#### Sites {#sites-issues}

- SITES-7796 — 内容作者在导出到目标时能够发布主控内容片段及其各自的变体
- SITES-97 - GraphQL:分页和排序，混合过滤

>[!NOTE]
>
> 在SITES-97中，GraphQL实施已做出一些改进，可能会导致意外行为。 请参阅 [AEM GraphQL对处理空值的更改](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-21792.html) 以了解更多信息。

#### Assets {#assets-issues}

- ASSETS-20076 — 添加对与当前图像水印支持匹配的视频水印支持
- ASSETS-21428 — 为CSS更改添加了排除项

#### Forms {#forms-issues}

- CQ-4351502 — 更新服务用户映射以允许在站点中进行读取访问

#### Platform {#platform-issues}

- SITES-11040 — 在调度程序中有条件地启用GraphQL持久化查询缓存

### 嵌套的技术 {#embedded-tech}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 版本 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.21.2 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
