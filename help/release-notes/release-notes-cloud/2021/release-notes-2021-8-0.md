---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.8.0 版的发行说明。'
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 25%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此处导航到早期版本的发行说明。 例如，2020年和2021年的情况。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]当前版本(2021.8.0)的发布日期是2021年8月26日。
以下版本(2021.9.0)的发布日期为2021年10月6日。

## 发布视频 {#release-video}

观看[2021年8月版概述](https://video.tv.adobe.com/v/336277)视频，大致了解新增功能。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 在将数字资产作为链接共享时，用户可以立即将URL复制到剪贴板。 增强功能可让您以更快、更方便的方式共享资产。 此功能允许更快、更方便地共享资产。

  将资产作为链接共享时，![复制URL选项](/help/assets/assets/link-share-copy-URL-option.png)
  *图：将资产作为链接共享时，您现在可以复制URL以单独共享它。*

* 上传TXT文件时，资源微服务会自动生成缩略图。 PNG缩略图是TXT文件的演绎版，在不打开文件的情况下，在一定程度上帮助用户识别内容或文件。 此功能不需要进行任何配置，默认可以使用。

  ![TXT文件的格式副本由[!DNL Assets]以PNG格式自动生成](/help/assets/assets/thumbnail-rendition-txt-file.png)
  *图：将自动生成TXT文件的演绎版，以帮助您识别文件而无需打开。*

### [!DNL Assets]预发行渠道中的新功能 {#assets-prerelease-features}

* 用户现在可以对列视图和卡片视图的搜索结果中显示的资源进行排序。 排序仅对名称、创建、修改或无列起作用。

  ![在列视图和卡片视图的[!DNL Assets]中对搜索结果排序](/help/assets/assets/sort-searched-assets.png)
  *图：对列视图和卡片视图中的[!DNL Assets]中的搜索结果排序。*

### [!DNL Assets] 中修复的错误 {#assets-bugs-fixed}

* 当参与者组的成员导航到[!DNL Assets]控制台时，会生成额外的`POST`请求以创建收藏集。 此请求不是必需的；它由于权限问题而失败，并在日志中创建许多错误。 (CQ-4328856)
* 当用户查看资产并从左侧面板的弹出菜单中选择[!UICONTROL 时间轴]时，会显示错误。 在日志中，由于查询错误，将记录许多警告。 (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* automated forms conversion服务可以[将意大利语和葡萄牙语的PDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model)转换为自适应Forms。

* **基于 Acroform 的记录文档**：除了基于 XFA 的表单模板，AEM Forms as a Cloud Service 还支持使用 [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作为记录文档的模板。

* **Microsoft® Azure数据存储连接器**：您现在可以[将表单数据模型连接到Microsoft® Azure存储](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html)。 它可让您检索自适应表单数据并将其作为BLOB存储到Microsoft® Azure Storage。

### [!DNL Forms]预发行渠道中提供的新功能 {#prerelease-features-forms}

* **在自适应表单中使用Adobe Sign角色** — 用于商业和企业服务级别的Adobe Sign可以选择扩展协议接受者的角色，而不只是签名者角色，以便更好地匹配他们的工作流要求。 您现在可以在自适应表单中为每个协议接受者配置他们的角色，签名者是默认角色。

* **Analytics for Adaptive Forms** — 您现在可以通过Adobe Analytics for Adaptive Forms捕获和跟踪最终用户行为，从而收集最终用户洞察。 这有助于根据数据做出明智的决策，从而改善最终用户体验。

* **轻松将AEM Forms连接到Microsoft® Dynamics和Salesforce.com** — 该服务为Microsoft® Dynamics和Salesforce.com提供现成的数据源配置和数据模型。 这使得开发人员可以更快、更轻松地配置Microsoft®Dynamics和Salesforce.com作为自适应表单的数据源。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新的类别选取器UI，可改善用户体验、提高效率并更好地支持复杂的产品目录

  ![新类别选取器](/help/assets/CIF/category-picker.png)

* 更好地支持CIF核心组件的A11Y

## Cloud Manager {#cloud-manager}

本部分概述了AEM as a Cloud Service 2021.8.0和2021.7.0中的Cloud Manager发行说明。

## 发布日期 {#release-date-cm-aug}

AEM as a Cloud Service 2021.8.0中的Cloud Manager的发布日期是2021年8月12日。
下一个版本计划于2021年9月9日发布。

### 新增功能 {#what-is-new-aug}

* Cloud Service 客户现在可以在 Cloud Manager 中查看服务水平协议 (SLA) 报告。 该功能将在未来几个月逐步推出。
请参阅 [SLA 报告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/sla-reporting.html)。

* IndexType 和 `IndexDamAssetLucene` 质量规则的类型和严重性已更改。 这两个规则现在均为Blocker *严重性*&#x200B;的Bug。

* 引入新的 Oak 索引质量规则以涵盖异步和 Tika 配置。

* 将每个程序的最大 SSL 证书数增加到 50。

* 借助自助服务功能，用户可通过Cloud Manager UI创建和管理多个存储库。

* SonarQube 未成功读取 Git 历史数据。 在大代码库情况下，这可能会导致出现不必要的构建性能损失。

* 现在有一个 API 可用于使每个管道的 Maven 依赖项缓存失效。

* Cloud Manager 使用的 AEM 项目原型的版本已更新到版本 29。

### 错误修复 {#bug-fixes-aug}

* 当最新版本低于当前版本时，不应显示“更新可用”状态。

* 对于名字长的新组织，初始登录失败。

* 有时，当管道由于某种原因被触发两次时，会导致其中一个执行失败，并出现&#x200B;*`cannot update pipeline execution status`*&#x200B;错误。

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具版本1.5.6的发布日期为2021年8月11日。

### 错误修复 {#bug-fixes-ctt}

* 有时，并非所有用户都迁移到目标实例。 要获取此修复，目标AEM as a Cloud Service实例上需要安装CTT v1.5.6以及aem-ethos-tools 1.2.354或更高版本。

* 在摄取到Publish实例期间，**停止摄取**&#x200B;按钮被禁用。 没有必要执行此操作，因为Publish摄取期间没有蒙戈恢复步骤。

* 成功提取后，CTT未清理`/tmp`目录。 这有时会导致磁盘空间问题。
