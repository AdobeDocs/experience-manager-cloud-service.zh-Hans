---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新维护发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新维护发行说明。'
source-git-commit: edb8949b532b80a55106e706a49e2ada68722a67
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 33%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述了 Experience Manager as a Cloud Service 的最新维护版本的技术发行说明。

## 发行版本 11289 {#release-11289}

以下是维护版本11289的持续改进，该版本于2023年3月7日公开发布。 此维护版本是以前的维护版本10912的更新。

此维护版本的功能支持将为您提供完整功能集。有关完整详细信息，请参阅[最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 已知问题 {#known-issues}

如果您使用的是 CORS，请不要升级。已发现此版本中影响GraphQL内容投放功能的问题。 更改了有关如何缓存GraphQL持久查询的默认AEM Dispatcher配置，可能会中断此类查询的GraphQL内容交付。 此问题将在我们的下一个维护版本中修复。

### 修复的问题 {#fixed-issues}

#### Sites {#sites-issues}

- SITES-11584修复了无法为带有批注的页面创建活动副本的问题
- SITES-11683禁用的MSM活动副本，继承部分中断

#### Assets {#assets-issues}

- ASSETS-20879固定回归导致“资产报表”UI无法正常工作，并导致生成的报表中出现错误结果。
- ASSETS-21020修复了资产下载中断的问题 — 移动资产后，图像配置文件不存在
- ASSETS-21023修复了Dynamic Media中的图像呈现版本阻止通过API访问的问题

#### Forms {#forms-issues}

- 无

#### 平台 {#platform-issues}

- GRANITE-44467 — 修复了在更新现有节点时，某些实例下的Filevault不保留mixin类型和子节点时导致导入失败的问题

### 嵌套的技术 {#embedded-tech}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 版本 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本1.4.20 - 1.4.0 | [HTML模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.21.2 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
