---
title: 的最新发行说明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新发行说明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 4efac10fe32ef0aa0ab5a4de3f16c3f0dbf91551
workflow-type: tm+mt
source-wordcount: '1619'
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

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新版本(2021.10.0)是2021年11月4日。
以下版本(2021.11.0)发布于2021年12月16日。

## 发行视频 {#release-video}

请查看 [2021年10月版概述](https://video.tv.adobe.com/v/338253) 视频，了解添加的功能摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新增功能 [!DNL Sites] {#sites-features}

* 现在，内容片段模型在发布后会自动设置为只读状态，以避免在重新发布已编辑的模型后无意中中断实时API查询。 尝试编辑已发布的模型时，系统会提示用户显示警告。 接受警告后，即可进行编辑。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 的新增功能 [!DNL Assets] {#assets-features}

* [!DNL Experience Manager] 现在，支持使用内置连接器从支持的音频和视频资产自动生成文本记录 [!DNL Azure Media Services]. 的 [支持的文件类型](/help/assets/file-format-support.md#audio-video-transcription-formats) 文本以WebVTT格式存储。 WebVTT字幕用于更有效的搜索、字幕或翻译。 此外，该功能还改进了资产的辅助功能、可发现性和本地化。

### 的新增功能 [!DNL Assets] 预发行渠道 {#assets-prerelease-features}

* [!DNL Dynamic Media] 图像智能裁剪和色板现在由最新的Sensei服务提供支持，该服务可生成经过改进的裁剪和色板。 此外，还推出了增强功能，以生成不同的裁剪内容，适用于相同的宽高比，但也适用于不同的分辨率。 此外，如果图像配置文件的宽度和高度没有变化，则在重新处理时将保留任何手动编辑。

* 智能标记会使用资产微服务而不是智能内容服务自动应用于资产。 更新基础模型以改进标记结果并减少偏差。 <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 的新增功能 [!DNL Forms] {#what-is-new-forms-oct-2021}

* **适用于自适应Forms的Analytics**:现在，您可以通过Adobe Analytics for Adaptive Forms捕获和跟踪已登录和未登录（匿名）的行为，以收集最终用户分析。 它有助于根据数据做出明智的决策，以改善最终用户体验。

### 的新增功能 [!DNL Forms] 预发行渠道 {#prerelease-features-forms-oct-2021}

* **将AEM工作流数据外部化以进行安全处理**:您可以在客户管理的存储库中存储包含敏感个人数据(SPD)元素的正在处理的AEM工作流数据(AEM工作流变量数据)，以便进行安全处理。 数据元素和工作流变量不存储在AEM存储库中，在处理工作流时，它们会根据需要从客户管理的存储库获取。

### 的测试版功能 [!DNL Forms] {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) 帮助您将模板和XML数据结合起来，以生成各种格式的打印文档。 该服务允许您以同步和批处理模式生成文档。 利用API，可创建应用程序，以便：

   * 使用XML数据填充模板文件(PDF和XDP)，以生成文档。
   * 以各种格式生成输出表单，包括非交互式PDF打印流。

您可以写入 [!DNL formscsbeta@adobe.com] 注册测试版计划。

## CIF附加组件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF附加组件支持最新的Commerce v2.4.3和新的GraphQL API和架构

* 作者可以使用富文本编辑器(RTE)在文本字段中添加指向产品和目录页面的链接。 CIF图标已添加到RTE工具栏中，该工具栏将打开选取器，以便快速搜索并选择产品或类别，而无需离开上下文。

* 现有的弹出式购物车和结帐已替换为专用的AEM购物车和结帐页面。 这些页面上的组件是使用Magento的可扩展Peregrine组件构建的

* 商户可以使用商务后端在导航中隐藏某些产品目录类别。 CIF导航核心组件遵循商务后端配置“包含在菜单中”来在导航中显示/隐藏类别

* AEM Storefront Venia在未找到类别或产品页面时返回HTTP 404错误

## Cloud Manager {#cloud-manager}

本节概述AEM as a Cloud Service 2021.10.0中Cloud Manager的发行说明。

### 发布日期 {#release-date-cm-nov}

AEMas a Cloud Service中Cloud Manager的发行日期为2021.11.0 2021年11月4日。
下一版本计划于2021年12月9日发布。

### 新增功能 {#what-is-new-cm-nov}

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

### 错误修复 {#bug-fixes-nov}

* 某些非正统的生成配置会导致不必要的文件存储在管道的Maven对象缓存中，这会在启动和停止生成容器时导致不重要的网络I/O。

* 如果部署阶段不存在，则管道PATCHAPI会失败。

* 的 `ClientlibProxyResourceCheck` 当存在具有通用基本路径的客户端库时，质量规则会产生误报问题。

* 达到最大存储库数时的错误消息未指定错误原因。

* 在极少数情况下，管道因某些响应代码的重试处理不当而失败。


## 发布日期 {#release-date-cm-oct}

AEMas a Cloud Service中Cloud Manager的发行日期为2021.10.0 2021年10月14日。

### 新增功能 {#what-is-new-cm-oct}

* 为了准备一些即将发生的更改，现在将在用户界面中引用现有部署管道，并将其标记为 **完全堆栈** 管道。

* 管道卡已刷新，现在可显示单个集成的表面，该表面既显示生产管道，也显示非生产管道，用户可以直接从与每个管道关联的操作菜单中选择“运行/暂停/恢复”。

* 具有部署管理器角色的用户现在可以通过UI以自助方式删除生产管道。

* 添加和编辑管道体验已刷新，现在可以使用熟悉的现代模型。

* Cloud Manager的用户现在可以通过 **反馈** 按钮。

* 现在可以从Cloud Manager的用户界面下载每年的SLA图表。

* 现在，代码质量和非生产管道执行将在构建步骤中使用更高效的浅层克隆过程，从而为具有特别大的git存储库的客户缩短构建时间。

* 现在，“添加IP允许列表”向导将通知用户是否已达到允许的最大IP允许列表数。

* Cloud Manager API文档现在包含一个交互式操场，允许已登录的用户从其浏览器中试用该API。 请参阅 [Cloud Manager API操场](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 以了解更多详细信息。

* 如果禁用了“导航到”下的选择选项，则程序卡上的工具提示更具描述性。 此时会显示“生产环境不存在”。

### 错误修复 {#bug-fixes-cm-oct}

* 在极少数情况下，当Adobe员工恢复客户的环境时，在环境完全运行之前，会认为恢复已完成。

* 在环境创建期间发出的某些内部请求未重试。

* 如果在域名验证后发生部署失败错误，则错误消息已被更正，以请求客户联系其Adobe代表。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的发布日期是2021年10月5日。

### 新增功能 {#what-is-new}

* 能够检测并报告节点名称长度。

* 能够检测并报告总索引大小。

* 能够检测并报告缺少其原始演绎版的资产。


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

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具v1.7.10的发布日期是2021年12月8日。

### 新增功能 {#what-is-new-ctt}

* 在内容传输工具的摄取阶段添加切换以允许用户禁用 [预拷贝](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 在摄取期间。 为了获得最佳摄取速度，对于较小的迁移集，或者自上次摄取后仅添加了几个Blob，应禁用摄取期间的预复制。
* 更新了用户映射，以使用经过改进的用户管理API，该API可以同时吸引2000个用户，从而显着提升性能。
