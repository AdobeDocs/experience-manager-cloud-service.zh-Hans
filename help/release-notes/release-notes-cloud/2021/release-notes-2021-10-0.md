---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.10.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.10.0 版的发行说明。'
exl-id: ab584923-5f06-4b54-941b-e00bc1158b81
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 71%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hans)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前版本(2021.10.0)为2021年11月4日。
以下版本(2021.11.0)的发布日期为2021年12月2日。

## 发布视频 {#release-video}

请查看 [2021年10月发行版概述](https://video.tv.adobe.com/v/338253) 视频以了解新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新增功能 [!DNL Sites] {#sites-features}

* 内容片段模型现在在发布后自动设置为只读状态，以避免在重新发布已编辑的模型后无意中中断实时API查询。 在尝试编辑已发布的模型时，系统会提示用户并显示警告。 接受警告时可以进行编辑。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* [!DNL Experience Manager] 现在支持使用内置连接器从支持的音频和视频资源自动生成文本转录，以 [!DNL Azure Media Services]. 此 [支持的文件类型](/help/assets/file-format-support.md#audio-video-transcription-formats) 将自动转录，文本以WebVTT格式存储。 WebVTT字幕用于更有效的搜索、字幕或翻译。 此外，该功能还提高了资源的可访问性、可发现性和本地化程度。

### 的新增功能 [!DNL Assets] 预发行渠道 {#assets-prerelease-features}

* [!DNL Dynamic Media] 图像智能裁切和色板功能现在由最新的 Sensei 服务提供支持，可生成改进的裁切和色板。还推出了一项增强功能，可生成宽高比相同但分辨率不同的各种裁切内容。此外，如果图像配置文件中的宽度和高度没有变化，则在重新处理时将保留任何手动编辑内容。

* 智能标记是使用资产微服务而不是智能内容服务自动应用于资产的。 更新底层模型以改善标记结果并减少偏差。 <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**：您现在可以通过Adobe Analytics for Adaptive Forms捕获和跟踪已登录和未登录（匿名）的行为，从而收集用户洞察。 这有助于根据数据做出明智的决策，从而改善用户体验。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms-oct-2021}

* **将 AEM Workflow 数据外部化以便安全处理**：您可以将包含敏感个人数据 (SPD) 的进程内 AEM Workflow 数据（AEM Workflow 变量数据）存储在客户管理的存储库中，以便安全处理。数据元素和工作流变量没有存储在 AEM 存储库中，而是在处理工作流时按需从客户管理的存储库中提取。

### [!DNL Forms] 的 Beta 版功能 {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=zh-Hans) 可帮助您组合模板和 XML 数据，以生成各种格式的打印文档。该服务让您能够以同步和批处理模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：

   * 使用 XML 数据填充模板文件（PDF 和 XDP）来生成文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF加载项支持带有新GraphQL API和架构的最新Commerce v2.4.3

* 作者可以使用富文本编辑器(RTE)在文本字段中添加指向产品和目录页面的链接。 RTE工具栏中添加了CIF图标，该图标会打开选取器，以便在不离开上下文的情况下快速搜索和选择产品或类别。

* 现有的弹出购物车和结帐已替换为专用的AEM购物车和结帐页面。 这些页面上的组件是使用Adobe Commerce的可扩展Peregrine组件构建的

* 商家可以使用Commerce后端在导航中隐藏某些产品目录类别。 CIF导航核心组件遵循Commerce后端配置“包含在菜单中”以在导航中显示/隐藏类别

* 如果找不到类别或产品页面，AEM Storefront Venia返回HTTP 404错误

## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.10.0 中的 Cloud Manager 的发行说明。

### 发布日期 {#release-date-cm-nov}

AEM as a Cloud Service 2021.11.0 中的 Cloud Manager 的发布日期是 2021 年 11 月 4 日。
下一个版本计划于 2021 年 12 月 9 日发布。

### 新增功能 {#what-is-new-cm-nov}

* 用户现在可以使用新的前端管道专门加速部署前端代码。有关更多信息，请参阅 [Cloud Manager 前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)。

  >[!IMPORTANT]
  >您必须使用 AEM 版本 `2021.10.5933.20211012T154732Z` 才能使用新的前端管道。

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


## 发布日期 {#release-date-cm-oct}

AEM as a Cloud Service 2021.10.0 中的 Cloud Manager 的发布日期是 2021 年 10 月 14 日。

### 新增功能 {#what-is-new-cm-oct}

* 为即将进行的更改做准备，现有部署管道现在将在用户界面中被引用并标记为&#x200B;**全栈**&#x200B;管道。

* 管道信息卡已刷新，现在显示单一的集成面，其中显示生产和非生产管道，用户可以直接从与每个管道关联的动作菜单中选择运行/暂停/恢复。

* “部署管理员”角色的用户现在可以通过 UI 以自助方式删除生产管道。

* 添加和编辑管道体验已经更新，现在可以使用熟悉的现代模式。

* Cloud Manager 用户现在可以通过登陆页面右上角的&#x200B;**反馈**&#x200B;按钮直接从用户界面提交反馈。

* 现在可以从 Cloud Manager 的用户界面下载年度 SLA 图表。

* 代码质量和非生产管道执行现在将在构建步骤中采用更高效的浅层克隆过程，从而为拥有特别大的 Git 存储库的客户缩短构建时间。

* 添加 IP 允许列表向导现在将通知用户是否已达到允许的最大 IP 允许列表数。

* Cloud Manager API 文档现在包括交互式游乐场，允许登录用户从浏览器中体验 API。有关更多详细信息，请参阅 [Cloud Manager API 游乐场](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/)。

* 如果“导航到”下的选择选项被禁用，“程序”信息卡上的工具提示将更具描述性。 它现在显示“生产环境不存在”。

### 错误修复 {#bug-fixes-cm-oct}

* 在极少数情况下，当 Adobe 员工恢复客户的环境时，恢复被认为是在环境完全运行之前完成的。

* 未重试在创建环境期间发出的某些内部请求。

* 如果在域名验证后发生部署失败错误，则已更正错误消息，请求客户联系其 Adobe 代表。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.20的发布日期是2021年10月5日。

### 新增功能 {#what-is-new}

* 能够检测和报告节点名称长度。

* 能够检测和报告索引总大小。

* 能够检测和报告缺少原始演绎版的资源。
