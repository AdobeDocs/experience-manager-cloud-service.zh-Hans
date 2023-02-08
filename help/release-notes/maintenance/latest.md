---
title: 的最新维护发行说明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新维护发行说明 [!DNL Adobe Experience Manager] as a Cloud Service。
source-git-commit: 76da86d31e2780c2d22419cb8a338cf37963fad8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 5%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述了Experience Manageras a Cloud Service最新维护版本的技术发行说明。

## 版本10912 {#release-10912}

以下是2023年2月3日公开发布的维护版本10912的持续改进。 此维护版本是以前维护版本9850的更新。

此维护版本的功能启用将为您提供完整的功能集。 请参阅 [最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md) 以了解完整详细信息。

### 已知问题 {#known-issues}

如果您使用的是CORS，请勿升级。 我们在此版本中发现了影响GraphQL内容交付部分的问题。 在默认AEM Dispatcher配置中，围绕GraphQL持久化查询的缓存方式进行更改，可能会破坏使用CORS配置的客户持久化查询的GraphQL内容交付。

### 嵌入式技术 {#embedded-tech}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM WCM核心组件 | 版本2.21.2 | [GitHub](https://github.com/adobe/aem-core-wcm-components) |
