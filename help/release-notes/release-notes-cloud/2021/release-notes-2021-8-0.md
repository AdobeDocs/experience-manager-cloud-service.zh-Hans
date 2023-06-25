---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 版的发行说明。'
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 51%

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

[!DNL Adobe Experience Manager][!DNL Cloud Service] 当前版本 (2021.8.0) 的发布日期为 2021 年 26 月 8 日。以下版本(2021.9.0)的发布日期为2021年10月6日。

## 发布视频 {#release-video}

请查看 [2021年8月发行版概述](https://video.tv.adobe.com/v/336277) 视频，以了解新增功能的摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 在将数字资产作为链接共享时，用户可以立即将URL复制到剪贴板。 增强功能可让您以更快、更方便的方式共享资产。 此功能允许更快、更方便地共享资产。

  ![将资产作为链接共享时，复制URL选项](/help/assets/assets/link-share-copy-URL-option.png)
  *图：将资产作为链接共享时，您现在可以复制URL以单独共享它。*

* 上传TXT文件时，资源微服务会自动生成缩略图。 PNG缩略图是TXT文件的演绎版，可帮助用户在一定程度上标识内容或文件，而无需打开文件。 此功能不需要任何配置，默认可以使用。

  ![TXT文件的演绎版由自动生成 [!DNL Assets] PNG格式](/help/assets/assets/thumbnail-rendition-txt-file.png)
  *图：将自动生成TXT文件的演绎版，以帮助您识别文件而无需打开。*

### 的新增功能 [!DNL Assets] 预发行渠道 {#assets-prerelease-features}

* 用户现在可以对列视图和卡片视图的搜索结果中显示的资源进行排序。 排序仅对名称、创建、修改或无列起作用。

  ![将搜索结果排序于 [!DNL Assets] 在“列”和“卡片”视图中](/help/assets/assets/sort-searched-assets.png)
  *图：将搜索结果排序于 [!DNL Assets] 在“列”和“卡片”视图中。*

### [!DNL Assets] 中修复的错误 {#assets-bugs-fixed}

* 当投稿人组的成员导航到 [!DNL Assets] 控制台，额外的 `POST` 将生成请求以创建收藏集。 此请求不是必需的；由于权限问题而失败，并在日志中创建许多错误。 (CQ-4328856)
* 当用户查看资源并选择 [!UICONTROL 时间线] 从左侧面板的弹出菜单中，会显示错误。 在日志中，由于查询错误，将记录许多警告。 (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* automated forms conversion服务可以 [用意大利语和葡萄牙语转换PDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) 到自适应Forms。

* **基于 Acroform 的记录文档**：除了基于 XFA 的表单模板，AEM Forms as a Cloud Service 还支持使用 [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作为记录文档的模板。

* **Microsoft Azure 数据存储连接器**：您现在可以[将表单数据模型连接到 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可让您检索自适应表单数据并将这些数据作为 BLOB 存储到 Microsoft Azure Storage。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* **在自适应表单中使用 Adobe Sign 角色**：用于商业和企业服务级别的 Adobe Sign 可让您选择扩展协议接收者的角色（不仅限于签名者），以便更好地匹配他们的工作流要求。您现在可以允许每个协议接收者在自适应表单中配置自己的角色，签名者是默认角色。

* **Analytics for Adaptive Forms**：您现在可以通过 Adobe Analytics for Adaptive Forms 捕获和跟踪最终用户行为，从而收集最终用户洞察。这有助于根据数据做出明智的决策，从而改善最终用户体验。

* **轻松地将AEM Forms与Microsoft Dynamics和Salesforce.com连接**：该服务为Microsoft Dynamics和Salesforce.com提供现成的数据源配置和数据模型，使得开发人员可以更快、更轻松地配置Microsoft Dynamics和Salesforce.com作为自适应表单的数据源。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新的类别选择器UI改善了用户体验、提高了效率并更好地支持复杂的产品目录

  ![新建类别选取器](/help/assets/CIF/category-picker.png)

* 对CIF核心组件的更佳A11Y支持

## Cloud Manager {#cloud-manager}

本部分概述了AEMas a Cloud Service2021.8.0和2021.7.0中的Cloud Manager发行说明。

## 发布日期 {#release-date-cm-aug}

AEM as a Cloud Service 2021.8.0 中的 Cloud Manager 的发布日期是 2021 年 8 月 12 日。下一个版本计划于2021年9月9日发布。

### 新增功能 {#what-is-new-aug}

* Cloud Service 客户现在可以在 Cloud Manager 中查看服务水平协议 (SLA) 报告。 该功能将在未来几个月逐步推出。
请参阅 [SLA 报告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html)了解详情。

* IndexType 和 `IndexDamAssetLucene` 质量规则的类型和严重性已更改。 两者均为 Blocker *级别*&#x200B;错误。

* 引入新的 Oak 索引质量规则以涵盖异步和 Tika 配置。

* 将每个程序的最大 SSL 证书数增加到 50。

* 借助自助服务功能，用户可通过 Cloud Manager UI 创建和管理多个存储库。

* SonarQube 未成功读取 Git 历史数据。 在大代码库情况下，这可能会导致出现不必要的构建性能损失。

* 现在有一个 API 可用于使每个管道的 Maven 依赖项缓存失效。

* Cloud Manager 使用的 AEM 项目原型的版本已更新到版本 29。

### 错误修复 {#bug-fixes-aug}

* 当最新版本低于当前版本时，不应显示“更新可用”状态。

* 对于名字很长的新组织，初始登录失败。

* 有时，当管道由于某种原因被触发两次时，会导致其中一个执行失败，并出现&#x200B;*无法更新管道执行状态*&#x200B;错误。

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具版本1.5.6的发布日期为2021年8月11日。

### 错误修复 {#bug-fixes-ctt}

* 在某些情况下，并非所有用户都迁移到目标实例。 要获取此修补程序，需要在目标AEMas a Cloud Service实例上安装CTT v1.5.6以及aem-ethos-tools 1.2.354或更高版本。

* 此 **停止引入** 在将按钮摄取到发布实例期间禁用了该按钮。 没有必要执行此操作，因为在发布引入期间没有mongo restore步骤。

* CTT未清理 `/tmp` 成功提取后的目录。 这有时会导致磁盘空间问题。
