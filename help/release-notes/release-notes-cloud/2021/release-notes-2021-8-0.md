---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 版的发行说明。'
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 30%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager][!DNL Cloud Service] 当前版本 (2021.8.0) 的发布日期为 2021 年 26 月 8 日。以下版本(2021.9.0)将于2021年10月6日发布。

## 发布视频 {#release-video}

请查看 [2021年8月版概述](https://video.tv.adobe.com/v/336277) 视频，了解添加的功能摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 在将数字资产作为链接共享时，用户可以立即将URL复制到剪贴板。 通过增强功能，您可以更快、更方便地共享资产。 此功能允许更快、更方便地共享资产。

   ![将资产共享为链接时，复制URL选项](/help/assets/assets/link-share-copy-URL-option.png)
   *图：现在，在将资产作为链接共享时，您可以复制URL以单独共享资产。*

* 上传TXT文件时，资产微服务会自动生成缩略图。 PNG缩略图是TXT文件的演绎版，可帮助用户在一定程度上识别内容或文件，而无需打开文件。 此功能不需要任何配置，并且默认情况下可正常工作。

   ![TXT文件的呈现版本由 [!DNL Assets] 格式](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *图：将自动生成TXT文件的呈现版本，以帮助您识别文件，而无需打开。*

### 的新增功能 [!DNL Assets] 预发行渠道 {#assets-prerelease-features}

* 用户现在可以对列视图和卡片视图中搜索结果中显示的资产进行排序。 排序适用于“名称”、“已创建”、“已修改”或“无”列。

   ![在中对搜索结果排序 [!DNL Assets] 在列视图和卡片视图中](/help/assets/assets/sort-searched-assets.png)
   *图：在中对搜索结果排序 [!DNL Assets] 列视图和卡片视图中。*

### [!DNL Assets] 中修复的错误 {#assets-bugs-fixed}

* 当参与者组的成员导航到 [!DNL Assets] 控制台， `POST` 将生成请求以尝试和创建收藏集。 此请求不是必需的，因权限问题而失败，并在日志中创建大量错误。 (CQ-4328856)
* 当用户查看资产并选择 [!UICONTROL 时间轴] 从左侧面板的弹出菜单中，显示错误。 在日志中，由于查询错误，记录了许多警告。 (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* automated forms conversion服务可以 [用意大利语和葡萄牙语转换PDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) 适应Forms。

* **基于 Acroform 的记录文档**：除了基于 XFA 的表单模板，AEM Forms as a Cloud Service 还支持使用 [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作为记录文档的模板。

* **Microsoft Azure 数据存储连接器**：您现在可以[将表单数据模型连接到 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可让您检索自适应表单数据并将这些数据作为 BLOB 存储到 Microsoft Azure Storage。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* **在自适应表单中使用 Adobe Sign 角色**：用于商业和企业服务级别的 Adobe Sign 可让您选择扩展协议接收者的角色（不仅限于签名者），以便更好地匹配他们的工作流要求。您现在可以允许每个协议接收者在自适应表单中配置自己的角色，签名者是默认角色。

* **Analytics for Adaptive Forms**：您现在可以通过 Adobe Analytics for Adaptive Forms 捕获和跟踪最终用户行为，从而收集最终用户洞察。这有助于根据数据做出明智的决策，从而改善最终用户体验。

* **轻松将AEM Forms与Microsoft Dynamics和Salesforce.com连接**:该服务为Microsoft Dynamics和Salesforce.com提供开箱即用的数据源配置和数据模型，使开发人员能够更快、更轻松地将Microsoft Dynamics和Salesforce.com配置为自适应表单的数据源。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新增了类别选取器UI，以改善用户体验、提高效率并更好地支持复杂的产品目录

   ![新建类别选取器](/help/assets/CIF/category-picker.png)

* 更好地A11Y持CIF核心组件

## Cloud Manager {#cloud-manager}

本部分概述了AEM 2021.8.0和2021.7.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date-cm-aug}

AEM 2021.8.0版中Cloud Manager的发布日期是2021年8月12日。
下一版本计划于2021年9月9日发布。

### 新增功能 {#what-is-new-aug}

* Cloud Service客户现在可以在Cloud Manager中查看服务级别协议(SLA)报表。 这将在今后几个月逐步提供。
请参阅 [SLA报告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) 以了解更多。

* IndexType和的类型和严重性 `IndexDamAssetLucene` 质量规则已更改。 这两个都是拦截器的错误 *服务器*.

* 新的Oak索引质量规则已引入，以涵盖异步和tika配置。

* 将每个程序的最大SSL证书数增加到50个。

* 允许用户通过Cloud Manager UI创建和管理多个存储库的自助服务功能。

* SonarQube不必要地读取Git历史数据。 在大型代码库中，这可能会导致不必要的内部版本性能损失。

* 现在有一个API可用于使每个管道的Maven依赖关系缓存失效。

* Cloud Manager使用的AEM项目原型版本已更新至版本29。

### 错误修复 {#bug-fixes-aug}

* 当最新版本小于当前版本时，不应显示“更新可用”状态。

* 对于名称很长的新组织，初始载入失败。

* 有时，当由于某些原因触发管道两次时，会导致其中一次执行失败 *无法更新管道执行状态* 错误。

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具v1.5.6的发布日期是2021年8月11日。

### 错误修复 {#bug-fixes-ctt}

* 在某些情况下，并非所有用户都已迁移到目标实例。 要获取此修复，需要在target AEMas a Cloud Service实例上连同aem-ethos-tools 1.2.354或更高版本一起使用CTT v1.5.6。

* 的 **停止摄取** 按钮在摄取到发布实例时被禁用。 此操作不是必需的，因为在发布摄取期间没有执行任何一步恢复步骤。

* CTT没有清理 `/tmp` 目录。 这有时会导致磁盘空间问题。
