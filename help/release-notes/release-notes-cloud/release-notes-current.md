---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 218dd65d1969f92317ae1d9877e2e37bb201ea6a
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 35%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

>[!CAUTION]
>
>**计划维护排除期**
>
> 在以下时间范围内（从午夜开始到午夜结束），不会执行自动AEMaCS维护(00:00):
>
>* 11月21日星期一至12月12日星期一
>* 12月19日星期一至1月3日星期二


## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前月度版本(2022.10.0)为2022年11月10日。 下一个月版本（2023.1.0版）计划于2023年1月26日发布。

## 发布视频 {#release-video}

请观看2022年10月版概述视频，以了解2022.10.0版本中添加的功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### [!DNL Sites] 中的新增功能 {#sites-features}

* 的 [体验片段的“个性化”选项卡](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) 允许对体验片段编辑器执行分段规范功能，并且还允许灵活地创建嵌套式体验片段，以便为多个区段创建页眉和页脚变量。 在启动此功能之前，AEM提供的个性化仅适用于网站页面，而不适用于体验片段

* 的 [内容片段控制台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 现在，用户可以高效管理翻译的内容片段。 还提供一键访问以查看所有语言副本。用户还可按其感兴趣的区域设置筛选表格视图。

![内容片段语言](/help/release-notes/assets/cfconsole-languages.png)

* 通过优化模板中的图像大小设置，进一步缩短访客的页面加载时间。 有关图像组件的更多信息，请访问 [核心WCM组件](https://github.com/adobe/aem-core-wcm-components)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* Experience Manager Assets现在允许您上传其他支持格式类型的文档，并且[ 使用包含的Document Cloud查看器预览受众](/help/assets/manage-pdf-documents.md). 支持的格式类型包括TXT、RTF、DOC、DOCX、PPT、PPTX、XLS和XLSX。

   ![PDF其他格式的呈现版本](/help/release-notes/assets/multi-page-other-formats.png)


### 的新增功能 [!DNL Assets] 预发行 {#prerelease-features-assets}

* Experience Manager Assets现在对图像智能标记使用改进的人工智能框架。 这种内容智能可在摄取时提高适用于所有图像资产的智能标记的相关性和准确性。 此外，方向信息填充在 `cq:tags`，可使用方向筛选器更好地搜索结果。

   如果您有兴趣参加测试版， [填写此表格](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) 到11月14日。

* Experience Manager Assets现在 [支持SAS令牌](/help/assets/add-assets.md#asset-bulk-ingestor) 除了用于在连接到Azure Blob Storage数据源时进行身份验证的访问密钥之外，还可用于使用批量导入工具摄取资产。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 的新增功能 [!DNL Forms] {#new-features-available-in-channel}


* [自适应表单向导](/help/forms/creating-adaptive-form.md)：AEM Forms 提供便于企业用户使用的向导以快速创作自适应表单。该向导可快速地在选项卡之间导航，从而轻松地选择预先配置的模板、样式、字段和提交选项以创建自适应表单。此版本的向导有以下改进：

   * 选择或取消选择字段：可在向导中创建基于 JSON 和表单数据模型架构的自适应表单。现在可选择架构中的一部分字段以包括在自适应表单中。所选的字段被转换为相应的自适应表单数据捕获组件以快速创建所需的自定义表单。

   * 使用静态模板：在传统静态模板中有长期投入的客户可通过在模板中使用静态模板创作自适应表单，继续其采用云的历程。这样使客户有更多时间可将旧有的静态模板迁移到现代的可编辑模板。

* [在服务器端处理时从记录文档 (DoR) 删除隐藏的字段](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)：您可为最终用户生成记录文档 PDF，其中仅包含在数据捕获体验期间对最终用户可见的那些字段。在提交表单时，服务器根据所提交的数据验证对最终用户隐藏了哪些字段，并从记录文档中排除以达到一致。

### [!DNL Forms]预发行渠道中提供的新功能 {#prerelease-features-forms}

* **自适应Forms模板编辑器**:利用模板编辑器，可预定义组织的自适应Forms的基本结构和外观。 此版本对模板编辑器进行了以下改进：
   * **[模板编辑器中的表单数据模型](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**:您可以在模板编辑器中将表单数据模型架构与自适应表单模板关联。 这有助于减少创建自适应表单所花费的时间。 自适应Forms编辑器中还会添加选项，以允许用户为现有表单选择或更改表单数据模型。
   * **[模板编辑器中的记录文档](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**:现在，您可以标准化使用模板创建的所有表单的记录文档生成。 这有助于增强组织要求的合规性和标准化。

* **[从AEM Sites页面启动“自适应表单”向导](/help/forms/embed-adaptive-form-aem-sites.md)**:AEM Sites页面扩展了对自适应Forms的支持。 您现在可以创建新的自适应表单或嵌入现有的自适应表单，同时保留在AEM Sites页面上。
* **[在DoR中更改复选框和单选按钮的显示对齐方式](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**:现在，您可以在“记录文档”中为复选框和单选按钮设置所需的对齐方式(“水平”、“垂直”、“与自适应Forms相同”)。 此选项确定“记录文档”中复选框和单选按钮选项的位置。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 作者可以使用体验片段动态扩充产品列表(示例：在产品列表之间放置横幅)。
* 列表组件现在支持关联的产品/类别页面来动态显示相关页面。
* 添加了对Peregrine 12.5组件的支持。
* 添加了对产品Teaser和轮播中客户端价格加载的支持。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* AEMas a Cloud Service（创作服务）现已与统一Shell集成，以改进用户体验并将其与所有其他Experience Cloud应用程序相统一。 请参阅AEM as a [Cloud Service统一外壳](/help/overview/aem-cloud-service-on-unified-shell.md) 以了解更多详细信息。

* 如发行说明中所述，将弃用使用复制代理管理屏幕或复制API来分发大于10 MB（具有属性的节点，不包括二进制文件）的内容包，并将在未来几天内强制执行。 请参阅 [管理发布](/help/operations/replication.md#manage-publication) 或 [发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow) 以了解复制这些大内容包的建议方法。

* 调度程序配置现在引用一个文件，其中列出了常见的营销活动查询参数。 客户可以选择取消对与其相关的参数的注释，从而改善缓存。 请参阅 [营销活动参数](/help/implementing/dispatcher/caching.md#marketing-parameters) 以了解更多详细信息。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
