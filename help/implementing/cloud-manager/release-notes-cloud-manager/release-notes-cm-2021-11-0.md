---
title: AEMas a Cloud Service版本2021.11.0中的Cloud Manager发行说明
description: 以下是AEMas a Cloud Service版本2021.11.0中Cloud Manager的发行说明
feature: Release Information
exl-id: 98fd6d8a-ddc2-4f53-9dfc-d8e21af0c14d
source-git-commit: 4505f703754fa46cd746ae4794a3cab65cb19976
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2021.11.0 {#release-notes}

本页概述了AEM as a Cloud Service 2021.11.0中Cloud Manager的发行说明。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEM Manager在as a Cloud Service中的发布日期为2021.11.0 2021年11月4日。
下一版本计划于2021年12月16日发布。

## 新增功能 {#what-is-new}

* 用户现在可以利用新的前端管道以加速方式专门部署前端代码。有关更多信息，请参阅 [Cloud Manager 前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)。

   >[!IMPORTANT]
   >您必须使用AEM版本 `2021.10.5933.20211012T154732Z` 利用新的前端管道。

* 通过以更有效的方式执行代码分析而无需构建整个 AEM 映像，大大缩短了代码质量管道持续时间。此更改将在版本发布后的几周内逐步推出。

* Git Commit ID 现在将显示在管道执行详细信息中，以便更轻松地跟踪已生成的代码。

* 现在可通过公开的 API 创建程序。

* 现在可通过公开的 API 创建环境。

* `x-request-id` 响应标头现已在 [www.adobe.io](https://www.adobe.io/) 上的 API Playground 中可见。在提交客户关怀问题以进行疑难解答时，此标头很有用。

* 作为用户，我发现不带管道的管道信息卡为我提供了适当的指导。

* 现在软件提供了一个新的活动页面，可以在其中查看管道和代码执行等活动及其相关详细信息。随着时间的推移，此页面中列出的活动的范围将随着提供的详细信息而扩大。

* 现在提供了带悬停弹出框的新管道页面，以便轻松查看详细信息摘要。可以查看管道执行及其相关详细信息。

* Edit Pipeline API 现在支持更改部署阶段使用的环境。

* 已针对大型包在 OakPal 扫描过程中引入了优化。

* 质量问题 CSV 文件现在将包含每个质量问题的时间戳。

## 错误修复 {#bug-fixes}

* 某些非正统的生成配置会导致在管道的 Maven 构件缓存中存储不必要的文件，这会在启动和停止生成容器时导致产生无关的网络 I/O。

* 如果部署阶段不存在，则管道 PATCH API 将失败。

* 如果存在带公共基本路径的客户端库，则 `ClientlibProxyResourceCheck` 质量规则会产生误报问题。

* 达到最大存储库数时显示的错误消息未指定错误原因。

* 在极少数情况下，管道因某些响应代码的重试处理不当而失败。
