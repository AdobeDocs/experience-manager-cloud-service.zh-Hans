---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.10.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.10.0 版的发行说明。'
exl-id: ab584923-5f06-4b54-941b-e00bc1158b81
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 75%

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

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前版本(2021.10.0)為2021年11月4日。
以下版本(2021.11.0)將於2021年12月2日發行。

## 发布视频 {#release-video}

請檢視 [2021年10月版本總覽](https://video.tv.adobe.com/v/338253) 影片以瞭解新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 內容片段模型現在會在發佈後自動設定為唯讀狀態，以避免重新發佈已編輯的模型後意外中斷即時API查詢。 嘗試編輯已發佈的模型時，系統會提示使用者警告。 接受警告後即可進行編輯。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* [!DNL Experience Manager] 現在支援使用內建聯結器從支援的音訊和視訊資產自動產生文字記錄，用於 [!DNL Azure Media Services]. 此 [支援的檔案型別](/help/assets/file-format-support.md#audio-video-transcription-formats) 會自動轉譯，且文字會以WebVTT格式儲存。 WebVTT註解可用於更有效的搜尋、註解或翻譯。 此外，功能可改善資產的協助工具、可發現性和本地化。

### 中的新功能 [!DNL Assets] 發行前通道 {#assets-prerelease-features}

* [!DNL Dynamic Media] 图像智能裁切和色板功能现在由最新的 Sensei 服务提供支持，可生成改进的裁切和色板。还推出了一项增强功能，可生成宽高比相同但分辨率不同的各种裁切内容。此外，如果图像配置文件中的宽度和高度没有变化，则在重新处理时将保留任何手动编辑内容。

* 智慧標籤會自動套用至使用資產微服務的資產，而非智慧內容服務。 基礎模型已更新，以改善標籤結果並減少偏差。 <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**：您现在可以通过 Adobe Analytics for Adaptive Forms 捕获和跟踪已登录和未登录（匿名）的行为，从而收集最终用户洞察。这有助于根据数据做出明智的决策，从而改善最终用户体验。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms-oct-2021}

* **将 AEM Workflow 数据外部化以便安全处理**：您可以将包含敏感个人数据 (SPD) 的进程内 AEM Workflow 数据（AEM Workflow 变量数据）存储在客户管理的存储库中，以便安全处理。数据元素和工作流变量没有存储在 AEM 存储库中，而是在处理工作流时按需从客户管理的存储库中提取。

### [!DNL Forms] 的 Beta 版功能 {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=zh-Hans) 可帮助您组合模板和 XML 数据，以生成各种格式的打印文档。该服务允许您以同步模式和批处理模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：

   * 使用 XML 数据填充模板文件（PDF 和 XDP）来生成文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF附加元件支援最新的Commerce v2.4.3，其中包含新的GraphQL API和結構描述

* 作者可使用RTF編輯器(RTE)，在文字欄位中新增產品與目錄頁面的連結。 RTE工具列已新增CIF圖示，可開啟選擇器，以快速搜尋和選取產品或類別，而不需離開內容。

* 現有的彈出式購物車和結帳頁面已替換為專用的AEM購物車和結帳頁面。 這些頁面上的元件是使用Adobe Commerce的可擴充Peregrine元件所建置

* 商家可以使用Commerce後端在導覽中隱藏某些產品目錄類別。 CIF導覽核心元件遵循商務後端設定「包含在功能表中」以在導覽中顯示/隱藏類別

* 如果找不到類別或產品頁面，AEM Storefront Venia會傳回HTTP 404錯誤

## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.10.0 中的 Cloud Manager 的发行说明。

### 发布日期 {#release-date-cm-nov}

AEM as a Cloud Service 2021.11.0 中的 Cloud Manager 的发布日期是 2021 年 11 月 4 日。
下一个版本计划于 2021 年 12 月 9 日发布。

### 新增功能 {#what-is-new-cm-nov}

* 用户现在可以利用新的前端管道以加速方式专门部署前端代码。有关更多信息，请参阅 [Cloud Manager 前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)。

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

Best Practices Analyzer v2.1.20的發行日期為2021年10月5日。

### 新增功能 {#what-is-new}

* 能夠偵測並報告節點名稱長度。

* 能夠偵測及報告索引總大小。

* 能夠偵測並報告缺少原始轉譯的資產。
