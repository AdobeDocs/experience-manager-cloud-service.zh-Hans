---
title: AEMas a Cloud Service版本2021.11.0中的Cloud Manager发行说明
description: AEMas a Cloud Service版本2021.11.0中的Cloud Manager发行说明
feature: Release Information
exl-id: null
source-git-commit: e8ceeb0eb4fb26553683ced74a2e20628fc2952e
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2021.11.0 {#release-notes}

本页概述了AEM as a Cloud Service 2021.11.0中Cloud Manager的发行说明。

>[!NOTE]
>要查看最新的Adobe Experience Manager as a Cloud Service发行说明，请单击 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hans).

## 发布日期 {#release-date}

AEMas a Cloud Service中Cloud Manager的发行日期为2021.11.0 2021年11月4日。
下一版本计划于2021年12月9日发布。

### 新增功能 {#what-is-new}

* 用户现在可以利用新的前端管道以加速的方式专门部署前端代码。 请参阅 [Cloud Manager前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 以了解更多。

   >[!IMPORTANT]
   >您必须使用AEM版本 `2021.10.5933.20211012T154732Z` 利用新的前端管道。

* 通过以更有效的方式执行代码分析，无需构建整个AEM图像，代码质量管道持续时间显着缩短。 此更改将在发布后的几周内逐步推出。

* Git提交ID现在将显示在管道执行详细信息中，从而更便于跟踪已构建的代码。

* 现在，可通过公开的API创建项目。

* 现在，可通过公开的API创建环境。

* 的 `x-request-id` 响应标头现在在API操场上可见 [www.adobe.io](https://www.adobe.io/). 提交客户关怀问题以进行疑难解答时，此标题非常有用。

* 作为用户，我看到带零管道的管道卡为我提供了适当的指导。

* 现在提供了新的活动页面，可在其中查看管道和代码执行等活动及其关联的详细信息。 随着时间的推移，此页面中列出的活动范围将会扩展，并且还会扩展提供的详细信息。

* 现在提供了一个新的“管道”页面，该页面上提供了悬停时的状态弹出窗口，以便轻松查看详细信息摘要。 可以查看管道执行及其关联的详细信息。

* 编辑管道API现在支持更改部署阶段中使用的环境。

* OakPal扫描过程中对大型包进行了优化。

* 质量问题CSV文件现在将包含每个质量问题的时间戳。

### 错误修复 {#bug-fixes}

* 某些非正统的生成配置会导致不必要的文件存储在管道的Maven对象缓存中，这会在启动和停止生成容器时导致不重要的网络I/O。

* 如果部署阶段不存在，则管道PATCHAPI会失败。

* 的 `ClientlibProxyResourceCheck` 当存在具有通用基本路径的客户端库时，质量规则会产生误报问题。

* 达到最大存储库数时的错误消息未指定错误原因。

* 在极少数情况下，管道因某些响应代码的重试处理不当而失败。

