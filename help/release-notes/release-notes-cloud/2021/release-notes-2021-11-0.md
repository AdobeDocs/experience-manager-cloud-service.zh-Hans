---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.11.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.11.0 版的发行说明。'
source-git-commit: 16c4b6b694ddad7854906c0d18880dd72159c02a
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 99%

---


# [!DNL Adobe Experience Manager]as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hans)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新版本 (2021.11.0) 的发布日期为 2021 年 12 月 16 日。
以下版本(2022.1.0)发布于2022年2月3日。

## 发布视频 {#release-video}

观看 [2021 年 12 月版概述](https://video.tv.adobe.com/v/339278)视频，大致了解 2021.11.0（2021 年 11 月）版的新增功能。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* Dynamic Media 图像智能裁切和色板功能现在由最新的 Sensei 服务提供支持，可生成改进的裁切和色板。还推出了一项增强功能，可生成宽高比相同但分辨率不同的各种裁切内容。此外，如果图像配置文件中的宽度和高度没有变化，则在重新处理时将保留任何手动编辑内容。

### [!DNL Assets] 预发行渠道中的新功能 {#assets-prerelease-features}

* [!DNL Dynamic Media] - 您现在可以使用 AEM Dynamic Media 界面配置常规设置和发布设置，而不必使用 Dynamic Media Classic 桌面应用程序。

* [!DNL Dynamic Media] 现在支持 MXF 视频的提取、预览、播放和发布。尚不支持 MXF 视频的注释和可购买视频。

* 在配置远程 DAM 和 Sites 部署之间的连接后，远程 DAM 上的资源即可用于 Sites 部署。您现在可以对远程 DAM 资源或文件夹执行[更新、删除、重命名和移动操作](/help/assets/use-assets-across-connected-assets-instances.md)。更新会在 Sites 部署中自动提供，但会有一些延迟。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **将 AEM 工作流数据外部化以便安全处理**：对于包含敏感个人数据 (SPD) 元素的进程内 AEM 工作流数据（AEM 工作流变量数据），您可以存储在客户管理的存储库中以便安全处理。数据元素和工作流变量没有存储在 AEM 存储库中，而是在处理工作流时按需从客户管理的存储库中提取。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[Communication API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=zh-Hans) 可帮助您组合模板和 XML 数据，以生成各种格式的打印文档。该服务允许您以同步模式和批处理模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：

   * 使用 XML 数据填充模板文件（PDF 和 XDP）来生成文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。

* **使用 Communications API 创建的记录文档和 PDF 文档的自定义字体**：您现在可以在使用 Communications API 生成的 PDF 文档中使用品牌批准的字体，以满足贵企业的要求。

* **Forms Portal**：您可以使用 [Forms Portal](/help/forms/configure-forms-portal.md) 在 AEM Sites 页面上列出发布的自适应表单。它可以帮助网站访客发现所有可用表单。此外，访客可以使用 Forms Portal 保存和访问自适应表单的草稿，并查看提交的自适应表单的 PDF 版本。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 基于 Commerce 的可扩展 Peregrine 组件的扩展 myAccount 组件

![扩展 myAccount 组件](/help/assets/CIF/extended-myAccount-components.png)

* 作者可以使用其他推荐类型来创建临时 Commerce 产品推荐

* 支持 AEM Storefront 中的礼品卡

## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.11.0 中的 Cloud Manager 的发行说明。

### 发布日期 {#release-date-cm-nov}

AEM as a Cloud Service 2021.11.0 中的 Cloud Manager 的发布日期是 2021 年 11 月 4 日。
下一个版本计划于 2021 年 12 月 9 日发布。

### 新增功能 {#what-is-new-cm-nov}

* 用户现在可以利用新的前端管道以加速方式专门部署前端代码。有关更多信息，请参阅 [Cloud Manager 前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)。

   >[!IMPORTANT]
   >您必须使用 AEM 版本 `2021.10.5933.20211012T154732Z` 或更高版本才能使用新的前端管道。

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

### 错误修复 {#bug-fixes-nov}

* 某些非正统的生成配置会导致在管道的 Maven 构件缓存中存储不必要的文件，这会在启动和停止生成容器时导致产生无关的网络 I/O。

* 如果部署阶段不存在，则管道 PATCH API 将失败。

* 如果存在带公共基本路径的客户端库，则 `ClientlibProxyResourceCheck` 质量规则会产生误报问题。

* 达到最大存储库数时显示的错误消息未指定错误原因。

* 在极少数情况下，管道因某些响应代码的重试处理不当而失败。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.22 的发布日期是 2021 年 12 月 1 日。

### 新增功能 {#what-is-new-bpa}

* 能够检测和报告所使用的 ACS Commons 版本。
* 能够检测和报告一个组中用户和子组的数量。
* 能够检测和报告 MongoDB 中超过 16MB 的节点属性值。

### 错误修复 {#bug-fixes-bpa}

* 已改进对 Foundation 组件的检测来减少误报。
* 对于 AEM Forms 客户，已修复有关 `EMAIL_PDF_SUBMIT_ACTION` 在 AEM as a Cloud Service 中不可用的 BPA 消息。
