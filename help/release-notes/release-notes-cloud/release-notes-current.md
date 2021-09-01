---
title: ' [!DNL Adobe Experience Manager] 作为Cloud Service的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] 作为Cloud Service的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: f2c0b3cca634b10b1b39532465968619d53b4e65
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作为Cloud Service的最新发行说明 {#release-notes}

以下部分概述了作为Cloud Service的[!DNL Experience Manager]当前（最新）版本的常规发行说明。

>[!NOTE]
>
>从此处，您可以导航到以前版本的发行说明；例如，2020年、2021年，等等。

>[!NOTE]
>
>请参阅[近期文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) ，以了解有关与版本不直接相关的文档更新的详细信息。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]的当前版本(2021.8.0)的发布日期是2021年8月26日。
以下版本(2021.9.0)发布于2021年9月30日。

## 发行视频 {#release-video}

请查看[2021年8月版概述](https://video.tv.adobe.com/v/336277)视频，了解所添加功能的摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]的新增功能 {#assets-features}

* 在将数字资产作为链接共享时，用户可以立即将URL复制到剪贴板。 通过增强功能，您可以更快、更方便地共享资产。 此功能允许更快、更方便地共享资产。

   ![将资产共享为链接时，复制URL选项](/help/assets/assets/link-share-copy-URL-option.png)
   *图：现在，在将资产作为链接共享时，您可以复制URL以单独共享资产。*

* 上传TXT文件时，资产微服务会自动生成缩略图。 PNG缩略图是TXT文件的演绎版，可帮助用户在一定程度上识别内容或文件，而无需打开文件。 此功能不需要任何配置，并且默认情况下可正常工作。

   ![TXT文件的呈现版本由以PNG格 [!DNL Assets] 式自动生成](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *图：将自动生成TXT文件的呈现版本，以帮助您识别文件，而无需打开。*

### [!DNL Assets]预发行渠道中的新功能 {#assets-prerelease-features}

* 用户现在可以对列视图和卡片视图中搜索结果中显示的资产进行排序。 排序适用于“名称”、“已创建”、“已修改”或“无”列。

   ![在列视图和卡片视 [!DNL Assets] 图中对搜索结果排序](/help/assets/assets/sort-searched-assets.png)
   *图：在列视图和卡片视 [!DNL Assets] 图中对搜索结果排序。*

### [!DNL Assets]中修复的错误 {#assets-bugs-fixed}

* 当参与者组的成员导航到[!DNL Assets]控制台时，将生成一个额外的`POST`请求以尝试和创建收藏集。 此请求不是必需的，因权限问题而失败，并在日志中创建大量错误。 (CQ-4328856)
* 当用户查看资产并从左侧面板的弹出菜单中选择[!UICONTROL 时间轴]时，会显示错误。 在日志中，由于查询错误，记录了许多警告。 (CQ-4328919)

## [!DNL Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

* 用于Forms as aCloud Service的AEM原型项目现在包含[Canvas 3.0主题，并且表单数据模型适用于Microsoft Dynamics和Salesforce.com](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?#forms-cloud-service-local-development-environment)。

* **基于Acroform的记录文档**:AEM Forms as a Cloud Service支持将 [Adobe Acrobat表单PDF(Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 用作记录文档的模板，而不是基于XFA的表单模板。

* **Microsoft Azure数据存储连接器**:现在，您可 [以将表单数据模型连接到Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它允许您将自适应表单数据作为BLOB检索并存储到Microsoft Azure Storage中。

### [!DNL Forms]的测试版功能 {#aug-what-is-new-forms-prerelease}

* **统一存储连接器：** 使用统一存储连接器将客户管理的存储库中的进程中数据外部化。例如，您可以
   * 启用Forms Portal的保存和恢复功能，并将自适应表单草稿存储在客户管理的数据存储库中。
   * 将包含敏感个人数据(SPD)的正在处理的AEM工作流数据(AEM工作流变量数据)存储在客户管理的存储库中。

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) API您可以将XDP模板和XML数据组合在一起，以生成各种格式的打印文档。该服务允许您以同步模式生成文档。 利用API，可创建应用程序，以便：
   * 使用XML数据填充模板文件，以生成文档。
   * 以各种格式生成输出表单，包括非交互式PDF打印流。
   * 从XFA表单PDF和Adobe Acrobat表单生成打印PDF文件。

您可以写信给[!DNL formscsbeta@adobe.com]注册测试版程序。

### [!DNL Forms]预发行版渠道中提供的新增功能 {#prerelease-features-forms}

* **在自适应表单中使用Adobe Sign角色**:Adobe Sign的业务和企业服务级别可以选择扩展协议收件人的角色，而不仅仅是签名者，以更好地满足其工作流要求。现在，您可以使[的每个协议收件人都能够在自适应表单](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html?#addsignerstoanadaptiveform)中配置其角色，而签名者是默认角色。

* **用于自适应Forms的Analytics**:您现在可以通过Adobe Analytics for Adaptive Forms捕获和跟踪最终用户行为，以收集最终用户分析。它有助于根据数据做出明智的决策，以改善最终用户体验。

* **轻松连接AEM Forms与Microsoft Dynamics和Salesforce.com**:该服务为Microsoft Dynamics和Salesforce.com提供开箱即用的数据源配置和数据模型，使开发人 [员能够更快、更轻松地将Microsoft Dynamics和Salesforce.com配置为自适应表单的数据源](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html)。

## [!DNL Experience Manager Screens] as a  [!DNL Cloud Service] {#screens}

### 新增功能 {#what-is-new-screens}

* Screens作为Cloud Service现在支持基本的播放监控。 现在，播放器将报告各种播放量度，并且每次执行“ping”操作（默认为30秒）。 根据这些量度，它能够检测各种边缘情况（体验卡住、空白屏幕、计划问题等）。 此功能允许团队远程监控播放器是否正确播放了内容，提高对空白屏幕或现场中已损坏体验的反应性，并降低向最终用户显示已损坏体验的风险。
有关更多详细信息，请参阅[基本播放监控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring)。

* 在Screens中，现在支持将中的视频的缩略图支持作为Cloud Service。 内容作者可以为视频定义缩略图，以便图像可用作占位符，并在相应团队最终确定实际视频时，正确测试内容播放和定位。 在视频播放失败时，也可以使用图像。
有关更多详细信息，请参阅[视频的缩略图支持](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html?lang=en)。

### 错误修复 {#bug-fixes-screens}

* 播放器无法显示嵌入页面中的内容，此问题现已修复。

* 成功登录后，导航到默认页面（渠道）最终会出现“内部服务器错误”页面。

* 删除播放列表时，未删除关联的标记条目。


## CIF附加组件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新增了类别选取器UI，以改善用户体验、提高效率并更好地支持复杂的产品目录

   ![新建类别选取器](/help/assets/CIF/category-picker.png)

* 更好地A11Y持CIF核心组件

## Cloud Manager {#cloud-manager}

本部分概述了AEM as a 2021.8.0和2021.7.0Cloud Service中Cloud Manager的发行说明。

## 发布日期 {#release-date-cm-aug}

AEM as a Cloud Service2021.8.0中的Cloud Manager的发布日期是2021年8月12日。
下一版本计划于2021年9月9日发布。

### 新增功能 {#what-is-new-aug}

* Cloud Service客户现在可以在Cloud Manager中查看服务级别协议(SLA)报表。 这将在今后几个月逐步提供。
请参阅[SLA报告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html)以了解更多信息。

* IndexType和`IndexDamAssetLucene`质量规则的类型和严重性已更改。 这两个错误现在都是阻止程序&#x200B;*serverity*&#x200B;的错误。

* 新的Oak索引质量规则已引入，以涵盖异步和tika配置。

* 将每个程序的最大SSL证书数增加到50个。

* 允许用户通过Cloud Manager UI创建和管理多个存储库的自助服务功能。

* SonarQube不必要地读取Git历史数据。 在大型代码库中，这可能会导致不必要的内部版本性能损失。

* 现在有一个API可用于使每个管道的Maven依赖关系缓存失效。

* Cloud Manager使用的AEM项目原型版本已更新至版本29。

### 错误修复 {#bug-fixes-aug}

* 当最新版本小于当前版本时，不应显示“更新可用”状态。

* 对于名称很长的新组织，初始载入失败。

* 有时，当管道因某些原因触发两次时，会导致其中一次执行失败，并出现&#x200B;*无法更新管道执行状态*&#x200B;错误。

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具v1.5.6的发布日期是2021年8月11日。

### 错误修复 {#bug-fixes-ctt}

* 在某些情况下，并非所有用户都已迁移到目标实例。 要获取此修复，需要在目标AEM上作为Cloud Service实例使用aem-ethos-tools 1.2.354或更高版本以及CTT v1.5.6。

* 在将摄取到发布实例期间，**停止摄取**&#x200B;按钮处于禁用状态。 此操作不是必需的，因为在发布摄取期间没有执行任何一步恢复步骤。

* 成功提取后，CTT未清除`/tmp`目录。 这有时会导致磁盘空间问题。

