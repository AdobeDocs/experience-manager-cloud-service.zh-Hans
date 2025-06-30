---
title: 元数据架构定义元数据属性页面的布局
description: 元数据架构定义属性页面的布局以及为资源显示的元数据属性。 了解如何创建自定义元数据架构、编辑元数据架构以及如何将元数据架构应用于资源。
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 9e94afeb-1c54-4653-bf52-b0910c0cb6c1
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '2634'
ht-degree: 10%

---

# 元数据架构 {#metadata-schemas}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-schemas.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

组织可以提供一个元数据模型，用于增强资产发现、使用、互操作性等。 正确的元数据应用程序对于维护元数据驱动的工作流程和流程至关重要。 要遵循组织范围的元数据策略和标准，您可以使用帮助DAM用户一致的元数据架构。 [!DNL Adobe Experience Manager]允许使用简单灵活的方法创建、维护和应用元数据架构。

在[!DNL Adobe Experience Manager Assets]中，架构包含要填写的特定信息的特定字段。 它还包含布局信息，以便以用户友好的方式显示元数据字段。 元数据属性包括标题、描述、MIME类型、标记等。 您可以使用[!UICONTROL 元数据架构Forms]编辑器来修改现有架构或添加自定义元数据架构。

要查看和编辑资产的属性页面，请执行以下步骤：

1. 在卡片视图中单击资产拼贴上的快速操作中的&#x200B;**[!UICONTROL 查看属性]**&#x200B;选项。 或者，选择一个资产，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]** ![查看属性](assets/do-not-localize/info-circle-icon.png)。

1. 您可以在可用选项卡下编辑各种可编辑的元数据属性。 但是，您不能在属性页面的[!UICONTROL 基本]选项卡中修改资产[!UICONTROL 类型]。

   ![资源属性的“基本”选项卡，无法更改资源类型](assets/asset-properties-basic-tab.png)

   *图：资源[!UICONTROL 属性]上的“基本”选项卡。*

   要修改资源的MIME类型，请使用自定义元数据架构表单或修改现有表单。 有关详细信息，请参阅[编辑元数据架构Forms](#edit-metadata-schema-forms)。 如果修改MIME类型的元数据架构，则会修改资源和所有子类型的属性页面布局。 例如，修改`default/image`下的jpeg架构只会修改MIME类型为`image/jpeg`的资源的元数据布局（资源属性）。 但是，如果您编辑默认架构，则所做的更改会修改所有资源类型的元数据布局。

## 元数据架构表单 {#default-metadata-schema-forms}

要查看表单或模板列表，请在[!DNL Experience Manager]界面中导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。

[!DNL Experience Manager]提供了以下元数据架构表单模板。

| 模板 | | 描述 |
|---|---|---|
| [!UICONTROL 默认值] | | 资源的基本元数据架构表单。 |
| | 以下子表单继承[!UICONTROL 默认]表单的属性： | |
| | <ul><li>[!UICONTROL dm_video]</li></ul> | Dynamic Media视频的架构表单。 |
| | <ul><li>[!UICONTROL 图像]</li></ul> | 具有MIME类型（如`image/jpeg`和`image/png`）的图像的架构表单。 <br> [!UICONTROL 图像]表单具有以下子表单模板： <ul><li> [!UICONTROL jpeg]：子类型为[!UICONTROL jpeg]的资产的架构表单。</li> <li>[!UICONTROL tiff]：具有子类型TIFF的资源的架构表单。</li></ul> |
| | <ul><li>[!UICONTROL 应用程序]</li></ul> | MIME类型资产（如`application/pdf`和`application/zip`）的架构表单。 <br>[!UICONTROL pdf]：具有子类型PDF的资源架构表单。 |
| | <ul><li>[!UICONTROL 视频]</li></ul> | 具有MIME类型（如`video/avi`和`video/mp4`）的视频资产的架构表单。 |
| [!UICONTROL 收藏集] | | 收藏集的架构表单。 |
| [!UICONTROL contentfragment] | | 内容片段的架构表单。 |
| [!UICONTROL 表单] | | 此架构表单与[!DNL Adobe Experience Manager Forms]相关。 |
| [!UICONTROL ugc_contentfragment] | | 用户生成的内容片段和资产从社交媒体集成到Experience Manager的架构表单。 |

>[!NOTE]
>
>要查看架构表单的子表单，请单击架构表单名称。

## 添加元数据架构表单 {#add-a-metadata-schema-form}

要添加元数据架构表单，请执行以下步骤：

1. 若要向列表添加自定义模板，请在工具栏中单击&#x200B;**[!UICONTROL 创建]**。

   >[!NOTE]
   >
   >锁定符号随未编辑的模板一起显示。 如果自定义模板，则该模板未被锁定![锁定关闭](assets/do-not-localize/lock_closed_icon.svg)。

1. 在对话框中，提供架构表单的标题，然后单击&#x200B;**[!UICONTROL 创建]**&#x200B;以完成表单创建过程。

## 编辑元数据架构表单 {#edit-metadata-schema-forms}

您可以编辑新添加或现有的元数据架构表单。 元数据架构表单包括选项卡和选项卡中的表单项。 您可以将这些表单项目映射/配置到CRX存储库中元数据节点内的字段。 您可以将选项卡或表单项添加到元数据架构表单。 从父项派生的选项卡和表单项处于锁定状态。 不能在子级别更改它们。

1. 在[!UICONTROL 元数据架构Forms]页面上，选择一个表单，然后单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。

1. 在&#x200B;**[!UICONTROL 元数据架构表单编辑器]**&#x200B;页面上，自定义元数据表单。 将所需的组件从&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡拖动到其中一个选项卡。

   ![元数据架构编辑器以自定义资产属性页面](assets/metadata-schema-editor.png)

   *图：包含可用选项卡的[!UICONTROL 元数据架构表单编辑器]页面。*

1. 要配置组件，请选择该组件并在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中修改其属性。

### [!UICONTROL 构建表单]选项卡中的组件 {#components-within-the-build-form-tab}

**[!UICONTROL 构建表单]**&#x200B;选项卡列出了您在架构表单中使用的表单项。 **[!UICONTROL 设置]**&#x200B;选项卡提供您在&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡中选择的每个项目的属性。 下表列出了&#x200B;**[!UICONTROL 生成表单]**&#x200B;选项卡中可用的表单项：

| 组件名称 | 描述 |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL 节标题] | 为常用组件列表添加章节标题。 |
| [!UICONTROL 单行文本] | 添加单行文本属性。 它存储为字符串。 |
| [!UICONTROL 多值文本] | 添加多值文本属性。 它存储为字符串数组。 |
| [!UICONTROL 数字] | 添加一个数值组件。 |
| [!UICONTROL 日期] | 添加一个日期组件。 |
| [!UICONTROL 下拉列表] | 添加一个下拉列表。 |
| [!UICONTROL 标准标记] | 添加标记。 |
| [!UICONTROL 智能标记] | 通过自动添加元数据标记来增强搜索功能。 |
| [!UICONTROL 隐藏字段] | 添加隐藏字段。 保存资产时，此参数将作为POST参数发送。 |
| [!UICONTROL 由]引用的资产 | 添加此组件可查看资产引用的资产列表。 |
| [!UICONTROL 资源引用] | 添加以显示引用资产的资产列表。 |
| [!UICONTROL 产品引用] | 添加以显示与资产链接的产品列表。 |
| [!UICONTROL 上下文元数据] | 添加以控制其他元数据选项卡在资源属性页面中的显示。 |

<!-- TBD: Ratings are not available in Experience Manager as a Cloud Service. Removed via cqdoc-18089 ticket. 
| [!UICONTROL Asset Rating]        | Add to display options for rating the asset.                                       |
-->

#### 编辑元数据组件 {#edit-the-metadata-component}

要编辑表单上元数据组件的属性，请单击该组件以在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中编辑以下属性的全部或子集。 建议仅将一个字段映射到元数据架构中的给定属性。 否则，系统会选取映射到属性的最新添加字段。

**字段标签**：在资产的属性页面上显示的元数据属性的名称。

**映射到属性**：此属性指定资源节点的相对路径或名称，资源节点保存在CRX存储库中。 它以`./`开头，表示路径在资产的节点下。

以下是属性的有效值示例：

* `./jcr:content/metadata/dc:title`：将该值作为属性 `dc:title` 存储在资产的元数据节点中。

* `./jcr:created`：存储资源的创建日期和时间。 它是受保护的资产。 如果配置这些资产，Adobe建议将它们标记为“禁用编辑”。 否则，在保存资产的属性时，会出现“资产修改失败”错误。

为确保组件在元数据架构表单中正确显示，属性路径不应包含任何空格。

* **占位符**：使用此属性指定与元数据属性相关的占位符文本。
* **必需**：使用此属性在属性页面上将元数据属性标记为必需。
* **禁用编辑**：使用此属性不允许对属性页面上的属性进行任何编辑。
* **以只读方式显示空字段**：标记此属性以在属性页面上显示元数据属性，即使该属性没有值也是如此。 默认情况下，当元数据属性没有值时，它不会列在属性页面上。
* **显示排序列表**：使用此属性显示排序的选项列表。
* **选项**：使用此属性指定列表中的选项。
* **描述** ：使用此属性为元数据组件添加简短描述。
* **类**：与属性关联的对象类。
* **删除**：单击[!UICONTROL 删除]从架构表单中删除组件。

>[!NOTE]
>
>[!UICONTROL 隐藏字段]组件不包含这些属性。 相反，它包括属性，如属性“名称”、“值”、“字段标签”和“描述”。 每当保存资产时，隐藏字段组件的值都会作为POST参数发送。 它不会另存为资源的元数据。

如果选择&#x200B;**[!UICONTROL 必需]**&#x200B;选项，则可以搜索缺少必需元数据的资产。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，展开&#x200B;**[!UICONTROL 元数据验证]**&#x200B;谓词，然后选择&#x200B;**[!UICONTROL 无效]**&#x200B;选项。搜索结果中显示的资产缺少您通过架构表单配置的必需元数据。

如果将“上下文元数据”组件添加到任何架构表单的任意选项卡，则该组件将以列表形式显示在应用了特定架构的资产属性页中。 该列表包含所有其他选项卡，但不包括您向其中应用了上下文元数据组件的选项卡。 目前，此功能提供了基本功能，可基于上下文控制元数据的显示。

除了显示应用上下文元数据组件的选项卡外，要在属性页面中显示任何选项卡，请从列表中选择选项卡。 选项卡即会添加到属性页面。

### 在JSON文件中指定属性 {#specify-properties-in-json-file}

您还可以通过指定相应的键值对在 JSON 文件中定义选项，而不是为&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中的选项指定属性。在 **[!UICONTROL JSON 路径]**&#x200B;字段中指定 JSON 文件的路径。

#### 在架构表单中添加或删除选项卡 {#add-delete-a-tab-in-the-schema-form}

通过架构编辑器，可以添加或删除选项卡。默认架构表单包括&#x200B;**[!UICONTROL Basic]**、**[!UICONTROL Advanced]**、**[!UICONTROL IPTC]**&#x200B;和&#x200B;**[!UICONTROL IPTC扩展]**&#x200B;选项卡。

![元数据架构表单中的默认选项卡](assets/metadata-schema-form-tabs.png)

单击`+`在架构表单上添加选项卡。 默认情况下，新选项卡的名称为`Unnamed-1`。 您可以从&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡修改名称。 单击`X`可删除选项卡。

![使用元数据架构编辑器添加或删除选项卡](assets/metadata-schema-form-new-tab.png)

## 删除元数据架构表单 {#deleting-metadata-schema-forms}

Experience Manager仅允许您删除自定义架构表单。 不允许删除默认架构表单/模板。 但是，您可以删除这些表单中的任何自定义更改。

要删除表单，请选择一个表单并单击删除图标。

>[!NOTE]
>
>删除对默认表单的自定义更改后，在元数据架构界面上，锁图标会重新显示在该表单之前，以指示该表单已恢复到其默认状态。

>[!NOTE]
>
>* 删除对默认表单的自定义更改后，锁![锁已关闭](assets/do-not-localize/lock_closed_icon.svg)会重新出现在表单前。 它指示表单将恢复到其默认状态。
>* 您无法删除[!DNL Assets]中的默认元数据架构表单。

## MIME类型的架构表单 {#schema-forms-for-mime-types}

[!DNL Experience Manager]为各种现成的MIME类型提供默认表单。 但是，您可以为各种MIME类型的资产添加自定义表单。

### 为MIME类型添加新表单 {#adding-new-forms-for-mime-types}

在相应的表单类型下创建表单。 例如，要为`image/png`子类型添加模板，请在“图像”表单下创建表单。 架构表单的标题是子类型名称。在这种情况下，标题为`png`。

#### 为各种MIME类型使用现有架构模板 {#use-an-existing-schema-template-for-various-mime-types}

您可以为其他MIME类型使用现有模板。 例如，对MIME类型`image/png`的资源使用`image/jpeg`表单。

在这种情况下，请在CRX存储库中的`/etc/dam/metadataeditor/mimetypemappings`处创建一个节点。 指定节点的名称并定义以下属性：

| 名称 | 描述 | 类型 | 价值 |
|------|-------------|------|-------|
| `exposedmimetype` | 要映射的现有表单的名称 | `String` | `image/jpeg` |
| `mimetypes` | 使用`exposedmimetype`属性中定义的表单的MIME类型列表 | `String` | `image/png` |

[!DNL Assets]映射以下MIME类型和架构表单：

| 架构表单 | MIME类型 |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi， video/msvideo， video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## 授予对元数据架构的访问权限 {#grant-access-to-metadata-schemas}

元数据架构功能仅对管理员可用。 但是，管理员可以通过修改某些权限为非管理员提供访问权限。 为非管理员用户提供`/conf`文件夹的创建、修改和删除权限。

## 应用文件夹特定的元数据 {#applying-folder-specific-metadata}

[!DNL Assets]允许您定义元数据架构的变体并将其应用到特定文件夹。

例如，您可以定义默认元数据架构的变体并将其应用到文件夹。 应用修改后的架构时，将覆盖应用于文件夹中资源的原始默认元数据架构。

只有上传到应用此架构的文件夹的资产才符合变体元数据架构中定义的修改后的元数据。 应用了原始架构的其他文件夹中的[!DNL Assets]继续符合原始架构中定义的元数据。

按资产划分的元数据继承基于应用于层次结构中顶级文件夹的架构。 子文件夹应用或继承相同的架构。 如果在子文件夹级别应用了其他架构，则继承将停止。

1. 在[!DNL Experience Manager]界面中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。 此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 选中表单前面的复选框，例如默认元数据表单，然后单击&#x200B;**[!UICONTROL 复制]**&#x200B;并将其另存为自定义表单。 指定表单的自定义名称，例如，`my_default`。 或者，您也可以创建自定义表单。

1. 在&#x200B;**[!UICONTROL 元数据架构Forms]**&#x200B;页面中，选择`my_default`表单，然后单击&#x200B;**[!UICONTROL 编辑]**。
1. 在&#x200B;**[!UICONTROL 元数据架构编辑器]**&#x200B;页中，向架构表单添加文本字段。 例如，添加标签为&#x200B;**[!UICONTROL Category]**&#x200B;的字段。
1. 单击&#x200B;**[!UICONTROL 保存]**。修改后的表单列在&#x200B;**[!UICONTROL 元数据架构Forms]**&#x200B;页中。
1. 从工具栏中选择&#x200B;**[!UICONTROL 应用到文件夹]**&#x200B;以将自定义元数据应用到文件夹。
1. 选择要应用修改后的架构的文件夹，然后选择&#x200B;**[!UICONTROL 应用]**。
1. 如果文件夹应用了其他元数据架构，则会显示一条消息，警告您即将覆盖现有的元数据架构。 单击&#x200B;**覆盖**。
1. 单击&#x200B;**确定**&#x200B;关闭成功消息。
1. 导航到将修改后的元数据架构应用于的文件夹。

## 定义必需的元数据 {#defining-mandatory-metadata}

您可以在文件夹级别定义必填字段，这是在上传到文件夹的资产上强制实施的。 如果上传的资源缺少之前定义的必填字段的元数据，则卡片视图中的资源上会显示缺少元数据的视觉指示。

>[!NOTE]
>
>可根据其他字段的值将元数据字段定义为必填字段。 在“卡片”视图中，Experience Manager不显示有关此类必填元数据字段缺少元数据的警告消息。

1. 单击Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。 此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 将默认元数据表单另存为自定义表单。 例如，将其另存为`my_default`。
1. 编辑自定义表单。 添加必填字段。 例如，添加&#x200B;**[!UICONTROL 类别]**&#x200B;字段并将该字段设为必填字段。
1. 单击&#x200B;**[!UICONTROL 保存]**。修改后的表单列在&#x200B;**[!UICONTROL 元数据架构Forms]**&#x200B;页中。 选择表单，然后从工具栏中选择&#x200B;**[!UICONTROL 应用到文件夹]**&#x200B;以将自定义元数据应用到文件夹。
1. 导航到文件夹，然后上传一些缺少添加到自定义表单的必填字段元数据的资源。 资产的“卡片”视图上会显示一条消息，指出缺少必填字段的元数据。
1. （可选）访问`https://[server]:[port]/system/console/components/`。 配置并启用默认禁用的`com.day.cq.dam.core.impl.MissingMetadataNotificationJob`组件。 设置Experience Manager检查资源上元数据有效性的频率。

   此配置将属性`hasValidMetadata`添加到资源的`jcr:content`。 使用此属性，Experience Manager可以筛选搜索中的结果。

   >[!NOTE]
   >
   >如果在计划检查之后添加资产，则在下次计划检查之前不会使用`hasValidMetadata`标记该资产。 资产不会显示在中间搜索结果中。

   >[!CAUTION]
   >
   >元数据验证检查占用大量资源，可能会影响系统性能。 相应地安排检查。 如果服务器无法应对负载，请尝试禁用此作业

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)