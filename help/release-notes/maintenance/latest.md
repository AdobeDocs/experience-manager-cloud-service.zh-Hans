---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
source-git-commit: 3378322c16f12c5ec4a741b912bbe0833f68d8e4
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 85%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 11382 {#release-11382}

下面总结维护版本 11382 的持续改进，该版本于 2023 年 3 月 28 日公开发布。此维护版本是对上一个维护版本 11289 的更新。

此维护版本的功能支持将为您提供完整功能集。有关完整详细信息，请参阅[最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

>[!IMPORTANT]
>
> CloudManager UI中显示“2023.3.11382”，而官方版本为“2023.02”，这种差异可以指出。 这是由于2023.02功能延迟激活所致。
> 我们正在为即将发行的版本修复此问题。

### 已知问题 {#known-issues-11382}

- SITES-12573 - 如果未指定一个变量，则在筛选器中使用变量的 GraphQL 查询将失败。如果您将 GraphQL 与 AEM as a Cloud Service 结合使用，请不要更新到此版本。
- SKYOPS-51970 - 识别出 buildImage 步骤中使用的 FACT 版本的回归，导致不匹配的用户映射。
- GRANITE-44542 - 对于没有为包过滤器中包含的文件夹指定包节点类型（通过提供带有 jcr:primaryType 的 .content.xml）的客户，已报告了问题。这导致这些文件夹被视为 nt:folder，从而在各种情况下产生问题。
- SKYOPS-56928 - Apache HTTPD回归可能导致404错误。 如果您出于安全原因遇到这些问题，建议回滚到以前的版本并避免在该时间段内运行任何管道。

### 修复的问题 {#fixed-issues-11382}

- ASSETS-21023 - 修复了智能裁剪演绎版，其中客户在尝试通过 API 访问这些演绎版时，可能会在所有 AEM 环境的 Publisher 实例上观察到空指针异常。
- SKYOPS-49280 - 在使用 RDE 将配置或捆绑包更新安装到 Publish 中时，可能因 Publish Dispatcher 缓存未失效而无法观察到结果

#### Sites {#sites-issues-11382}

- SITES-7796 - 内容作者能够在导出到目标时发布主内容片段及其各自的变体
- SITES-97 - GraphQL：分页和排序，混合过滤

>[!NOTE]
>
> 在 SITES-97 中，对 GraphQL 实现进行了一些改进，这些改进可能会导致意外行为。有关详细信息，请参阅 [AEM GraphQL 关于空值处理的更改](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-21792.html)。

#### Assets {#assets-issues-11382}

- ASSETS-20076 - 添加与当前图像水印支持相匹配的视频水印支持
- ASSETS-21428 - 添加了 CSS 更改的排除项

#### Forms {#forms-issues-11382}

- CQ-4351502 - 更新服务用户映射以允许在 Sites 中进行读取访问

#### Platform {#platform-issues-11382}

- SITES-11040 - 在 Dispatcher 中有条件地启用 GraphQL 持久查询缓存

### 嵌套的技术 {#embedded-tech-11382}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 版本 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.21.2 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
