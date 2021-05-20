---
title: 已知问题
description: 特定于 Adobe Experience Manager as a Cloud Service 已知问题的发行说明
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 100%

---

# 已知问题 {#known-issues}

本文列出了 Adobe Experience Manager as a Cloud Service 产品的已知问题。该列表会随每次连续发行的 Experience Manager 进行修订和更新。

有关已知问题的详细信息，请[联系支持人员](https://helpx.adobe.com/cn/support/experience-manager.html)。

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## 资产 {#assets}

<!-- Jira label: assets-cloud-known-issues -->

一些已知问题包括：

* **元数据架构**：资产评级小部件曾导致 JSP 编译错误。已从元数据架构将其删除。<!-- CQ-4282865, CQ-4284633 -->

### 即将推出的资产功能 {#upcoming-assets-capabilities}

Adobe Experience Manager Assets 中有一些依赖于基础功能的功能在 Experience Manager as a Cloud Service 部署架构尚不可用，这些功能预计将在稍后的阶段中启用：

* 由于依赖于商务集成框架 API，当前未启用以下功能：
   * 照片拍摄工作流模型。
   * 未填充资产属性用户界面中的“产品信息”选项卡。
* 由于依赖于 InDesign 服务器集成，当前未启用以下功能：
   * 资产模板和资产目录。
   * Adobe InDesign 文件的多页预览。

>[!MORELIKETHIS]
>
>* [AEM 中的主要更改](aem-cloud-changes.md)
* [已弃用和已删除的功能](deprecated-removed-features.md)
* [发行说明](home.md)

