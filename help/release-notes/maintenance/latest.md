---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 100%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 11835 {#release-11835}

下面总结了维护版本 11835 的持续改进，该版本已于 2023 年 4 月 19 日公开发布。此维护版本是对上一个维护版本 11382 的更新。

此维护版本的功能支持将为您提供完整功能集。有关完整详细信息，请参阅[最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 修复的问题 {#fixed-issues-11835}

- SITES-12573 - 如果未指定一个变量，则在筛选器中使用变量的 GraphQL 查询将失败。如果您将 GraphQL 与 AEM as a Cloud Service 结合使用，请不要更新到此版本。
- SKYOPS-51970 - 识别出 buildImage 步骤中使用的 FACT 版本的回归，导致不匹配的用户映射。
- GRANITE-44542 - 对于没有为包过滤器中包含的文件夹指定包节点类型（通过提供带有 jcr:primaryType 的 .content.xml）的客户，已报告了问题。这导致这些文件夹被视为 nt:folder，从而在各种情况下产生问题。
- SKYOPS-56928 - Apache HTTPD 回归可能导致 404 错误。如果您遇到这些问题，出于安全原因，建议回滚到上一版本并避免在该时段内运行任何管道。

### 嵌套的技术 {#embedded-tech-11835}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 版本 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.21.2 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
