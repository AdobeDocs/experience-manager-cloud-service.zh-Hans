---
title: 的最新发行说明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新发行说明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 53dd1d2a3b42e25a1da96ab8d06f05c05a36deab
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 2%

---


# 的最新发行说明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下部分概述了当前（最新）版本的常规发行说明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>从此处，您可以导航到以前版本的发行说明；例如，2020年、2021年，等等。

>[!NOTE]
>
>请参阅 [近期文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 有关与版本不直接相关的文档更新的详细信息。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新版本(2021.11.0)是2021年12月16日。
以下版本(2022.1.0)发布于2022年1月27日。

## 发行视频 {#release-video}

请查看 [2021年12月版概述](https://video.tv.adobe.com/v/339278) 视频，了解2021.11.0（2021年11月）版本中添加的功能摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 的新增功能 [!DNL Assets] {#assets-features}

* Dynamic Media Image Smart Crop and Swatch现在由最新的Sensei服务提供支持，可生成经过改进的作物和色板。 此外，还推出了增强功能，以生成不同的裁剪内容，适用于相同的宽高比，但也适用于不同的分辨率。 此外，如果图像配置文件的宽度和高度没有变化，则在重新处理时将保留任何手动编辑。

### 的新增功能 [!DNL Assets] 预发行渠道 {#assets-prerelease-features}

* [!DNL Dynamic Media]  — 您现在可以使用AEM Dynamic Media界面配置“常规设置”和“发布设置”，而不必再经过Dynamic Media Classic桌面应用程序。

* [!DNL Dynamic Media] 现在支持MXF视频的摄取、预览、播放和发布。 尚不支持MXF视频的注释和购物视频。

* 在远程DAM与Sites部署之间配置连接后，远程DAM上的资产将在Sites部署中可用。 您现在可以对远程DAM资产或文件夹执行更新、删除、重命名和移动操作。 更新（如果延迟）将在站点部署中自动提供。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 的新增功能 [!DNL Forms] {#what-is-new-forms}

* **Forms门户**:您可以使用 [Forms门户](/help/forms/configure-forms-portal.md) 可在AEM Sites页面上列出已发布的自适应表单。 它有助于网站访客发现所有可用的表单。 此外，访客还可以使用表单门户保存和访问自适应表单的草稿，并查看已提交的自适应表单的PDF版本。

* **将AEM工作流数据外部化以进行安全处理**:您可以在客户管理的存储库中存储包含敏感个人数据(SPD)元素的正在处理的AEM工作流数据(AEM工作流变量数据)，以便进行安全处理。 数据元素和工作流变量不存储在AEM存储库中，在处理工作流时，它们会根据需要从客户管理的存储库获取。

### 的新增功能 [!DNL Forms] 预发行渠道 {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 帮助您将模板和XML数据结合起来，以生成各种格式的打印文档。 该服务允许您以同步和批处理模式生成文档。 利用API，可创建应用程序，以便：

   * 使用XML数据填充模板文件(PDF和XDP)，以生成文档。
   * 以各种格式生成输出表单，包括非交互式PDF打印流。

* **为使用通信API创建的记录文档和PDF文档自定义字体**:现在，您可以在使用通信API生成的PDF文档中使用品牌批准的字体，以符合您的组织要求。

## CIF附加组件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 扩展了myAccount组件，这些组件基于Commerce的可扩展Peregrine组件

![扩展的myAccount组件](/help/assets/CIF/extended-myAccount-components.png)

* 作者可以使用其他推荐类型创建临时商务产品Recommendations

* 在AEM Storefront中支持礼品卡

## Cloud Manager {#cloud-manager}

本节概述AEM as a Cloud Service 2021.11.0中Cloud Manager的发行说明。

### 发布日期 {#release-date-cm-nov}

AEMas a Cloud Service中Cloud Manager的发行日期为2021.11.0 2021年11月4日。
下一版本计划于2021年12月9日发布。

### 新增功能 {#what-is-new-cm-nov}

* 用户现在可以利用新的前端管道以加速的方式专门部署前端代码。 请参阅 [Cloud Manager前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 以了解更多。

   >[!IMPORTANT]
   >您必须使用AEM版本 `2021.10.5933.20211012T154732Z` 或更高版本，以利用新的前端管道。

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

### 错误修复 {#bug-fixes-nov}

* 某些非正统的生成配置会导致不必要的文件存储在管道的Maven对象缓存中，这会在启动和停止生成容器时导致不重要的网络I/O。

* 如果部署阶段不存在，则管道PATCHAPI会失败。

* 的 `ClientlibProxyResourceCheck` 当存在具有通用基本路径的客户端库时，质量规则会产生误报问题。

* 达到最大存储库数时的错误消息未指定错误原因。

* 在极少数情况下，管道因某些响应代码的重试处理不当而失败。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.22的发布日期是2021年12月1日。

### 新增功能 {#what-is-new-bpa}

* 能够检测并报告所使用的ACS Commons版本。
* 能够检测并报告群组中的用户和子群组的数量。
* 能够检测并报告MongoDB中超过16MB的节点属性值。

### 错误修复 {#bug-fixes-bpa}

* 对基础组件的检测进行了细化，以减少漏报。
* 对于AEM Forms客户，与 `EMAIL_PDF_SUBMIT_ACTION` 已修复在AEMas a Cloud Service上不可用的问题。
