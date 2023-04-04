---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
source-git-commit: c6acdd922c052d0db5bf1f05bc03329fbc44ca33
workflow-type: ht
source-wordcount: '306'
ht-degree: 100%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 11382 {#release-11382}

下面总结维护版本 11382 的持续改进，该版本于 2023 年 3 月 28 日公开发布。此维护版本是对上一个维护版本 11289 的更新。

此维护版本的功能支持将为您提供完整功能集。有关完整详细信息，请参阅[最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 修复的问题 {#fixed-issues}

- ASSETS-21023 - 修复了智能裁剪演绎版，其中客户在尝试通过 API 访问这些演绎版时，可能会在所有 AEM 环境的 Publisher 实例上观察到空指针异常。
- SKYOPS-49280 - 在使用 RDE 将配置或捆绑包更新安装到 Publish 中时，可能因 Publish Dispatcher 缓存未失效而无法观察到结果

#### Sites {#sites-issues}

- SITES-7796 - 内容作者能够在导出到目标时发布主内容片段及其各自的变体
- SITES-97 - GraphQL：分页和排序，混合过滤

>[!NOTE]
>
> 在 SITES-97 中，对 GraphQL 实现进行了一些改进，这些改进可能会导致意外行为。有关详细信息，请参阅 [AEM GraphQL 关于空值处理的更改](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-21792.html)。

#### Assets {#assets-issues}

- ASSETS-20076 - 添加与当前图像水印支持相匹配的视频水印支持
- ASSETS-21428 - 添加了 CSS 更改的排除项

#### Forms {#forms-issues}

- CQ-4351502 - 更新服务用户映射以允许在 Sites 中进行读取访问

#### Platform {#platform-issues}

- SITES-11040 - 在 Dispatcher 中有条件地启用 GraphQL 持久查询缓存

### 嵌套的技术 {#embedded-tech}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 版本 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.21.2 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
