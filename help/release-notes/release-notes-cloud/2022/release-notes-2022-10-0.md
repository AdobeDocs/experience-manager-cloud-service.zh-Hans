---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.10.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.10.0 版的发行说明。'
exl-id: 8fce7c50-f322-4bcf-bd76-390faedfd5b7
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 80%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2022.10.0 版的发行说明 {#release-notes}

以下部分概述了2022.10.0版的功能发行说明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前月度版本 (2022.10.0) 的发布日期为 2022 年 11 月 10 日。 
下一月度版本 (2023.1.0) 计划于 2023 年 9 月 2 日发布。

## 发布视频 {#release-video}

观看 2022 年 10 月版概述视频，大致了解 2022.10.0 版的新增功能：

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### [!DNL Sites] 中的新增功能 {#sites-features}

* 此 [体验片段的个性化选项卡](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) 允许体验片段编辑器进行分段详述，并灵活创建嵌套体验片段，从而可以为多个片段创建页眉和页脚变化。 在此功能推出之前，AEM 提供的个性化仅适用于网站页面，不适用于体验片段。

* [内容片段控制台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)现在使用户能够有效地管理翻译的内容片段。 还提供一键访问以查看所有语言副本。用户还可按其感兴趣的区域设置筛选表格视图。

![内容片段语言](/help/release-notes/assets/cfconsole-languages.png)

* 通过优化模板中的图像大小设置，进一步减少访问者的页面加载时间。 在[核心 WCM 组件](https://github.com/adobe/aem-core-wcm-components)查找有关图像组件的更多信息

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* Experience Manager Assets现在允许您上传其他受支持格式类型的文档，并且[使用包含的Document Cloud查看器预览文档](/help/assets/manage-pdf-documents.md). 支持的格式类型包括 TXT、RTF、DOC、DOCX、PPT、PPTX、XLS 和 XLSX。

  ![其他格式的 PDF 演绎版](/help/release-notes/assets/multi-page-other-formats.png)


### [!DNL Assets] 预发布中的新增功能 {#prerelease-features-assets}

* Experience Manager Assets 现在为图像智能标记使用改进的人工智能框架。 这种内容智能化可提高智能标记的相关性和准确性，可用于摄取的所有图像资产。 此外，方向信息填充在 `cq:tags` 中，这样可以使用“方向”过滤器获得更准确的搜索结果。

  如果您有兴趣参与 Beta 测试，请在 11 月 14 日之前[填写这张表格](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u)。

* 除了用于身份验证的 Access 密钥外，Experience Manager Assets 现在还[支持 SAS 令牌](/help/assets/add-assets.md#asset-bulk-ingestor)，同时还连接到 Azure Blob 存储数据源，从而使用“批量导入”工具摄取资产。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* **自适应Forms模板编辑器**：模板编辑器可让您预定义组织自适应Forms的基本结构和外观。 此版本的模板编辑器有以下改进：
   * **[模板编辑器中的表单数据模型](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**：您可以在模板编辑器中将表单数据模型架构关联到自适应表单模板。 这样有助于减少创建自适应表单所需的时间。该选项也已添加到自适应表单编辑器中，用户可选择或更改现有表单的表单数据模型。
   * **[模板编辑器中的记录文档](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**：您现在可以为使用模板创建的所有表单标准化记录文档生成的过程。这有助于增强组织要求的合规性和标准化。

* **[从 AEM Sites 页面启动“自适应表单”向导](/help/forms/embed-adaptive-form-aem-sites.md)**：AEM Sites 页面已增强对自适应表单的支持。 您现在可以创建新的“自适应表单”或嵌入现有的“自适应表单”，同时保留在 AEM Sites 页面上。
* **[更改 DoR 中复选框和单选按钮的显示对齐方式](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**：您现在可以为记录文档上的复选框和单选按钮设置所需的对齐方式（水平、垂直、与自适应表单相同）。此选项确定记录文档中复选框和单选按钮选项的位置。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 作者可以使用体验片段动态丰富产品列表（例如：在产品列表之间放置横幅）。
* 列表组件现在支持关联产品/类别页面，可动态显示相关页面。
* 添加了对 Peregrine 12.5 组件的支持。
* 添加了对产品 Teaser 和轮播中客户端价格加载的支持。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* AEM as a Cloud Service （创作服务）现与 Unified Shell 集成，可改进用户体验并将其与所有其他 Experience Cloud 应用程序相统一。 请参阅AEM as a [Unified Shell上的Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) 以了解更多详细信息。

* 如先前在发行说明中所述，使用复制代理管理屏幕或复制API分发大于10 MB的内容包（具有属性的节点，不包括二进制文件）现在已弃用和强制使用。 请参阅 [管理发布](/help/operations/replication.md#manage-publication) 或 [发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow) 了解复制这些大型内容包的建议方法。

* Dispatcher 配置现在引用了一个文件，其中列出了常见的营销活动查询参数。客户可以选择取消注释与其相关的参数，从而实现更好的缓存。 请参阅 [营销活动参数](/help/implementing/dispatcher/caching.md#marketing-parameters) 以了解更多详细信息。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
