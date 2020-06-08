---
title: 元数据架构
description: 元数据模式定义属性页面的布局以及为资产显示的元数据属性。 了解如何创建自定义元数据模式、编辑元数据模式，以及如何将元数据模式应用于资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 24%

---


# 元数据架构 {#metadata-schemas}

在Adobe Experience Manager(AEM)资产中，元数据模式定义属性页面的布局以及为使用特定模式的资产显示的元数据属性。 元数据属性包括标题、描述、MIME类型、标记等。

您可以使用元数据模式表单编辑器修改现有模式或添加自定义元数据模式。

1. 要视图资产的属性页面，请单击或点按卡片视图 **[!UICONTROL 中资产拼贴]** 上快速操作中的视图属性图标。 或者，在UI中选择资产，然后单击或点按工 **[!UICONTROL 具栏]** 中的属性图标。
1. 编辑各个选项卡下的各种元数据属性。 但是，您无法在属性页面中修改资产类型。
要修改资产的MIME类型，请使用自定义元数据模式表单或修改现有表单。 有关详 [细信息，请参阅编辑元模式](#edit-metadata-schema-forms) “表单”。 如果您修改某些MIME类型的元数据模式，则将修改当前MIME类型和所有资产子类型的资产的属性页面布局。 例如，修改jpeg模式时，只 `default/image` 会修改MIME类型资产的元数据布局（资产属性） `image/jpeg`。 但是，如果您编辑默认模式，则所做的更改将修改所有类型资产的元数据布局。

1. 要查看表单/模板列表，请单击 AEM 徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。AEM提供了以下现成模板：

   * **默认**: 资产的基本元数据模式表单。
   以下子表单继承默认表单的属性：
我。 **图像**: 模式MIME类型为“image”的资产的表单， `image/jpeg`如 `image/png`、等等。
“图像”表单具有以下子表单模板：
a. **jpeg**: 模式子类型资产的表单 `jpeg`。
b. **tiff**: Schema form for the assets with sub type `tiff`.

   ii. **应用程序**: 模式具有MIME类 `application`型的资产 `application/pdf`的 `application/zip`表单，如等。
a. **pdf**: Schema form for assets with sub type `pdf`.

   iii. **视频**: 模式具有MIME类型 `video`的资产 `video/avi`的 `video/mp4`表单，如、等。

   * **集合**: 集合的模式表单。
   * **contentfragment:** 内容片段的模式表单。


>[!NOTE]
>
>要视图模式表单的子表单，请单击／点按模式表单名称。

## Add a metadata schema form {#add-a-metadata-schema-form}

1. 要向列表添加自定义模板，请单击工 **[!UICONTROL 具栏]** 中的创建。

   >[!NOTE]
   >
   >未编辑的模板前面会有一个锁图标。 如果自定义任何模板，则模板前面的锁图标会消失。

1. In the dialog, enter the title of the Schema form, and then click **[!UICONTROL Create]** to complete the form creation process.

## 编辑元数据模式表单 {#edit-metadata-schema-forms}

可以编辑新添加的或现有的元数据架构表单。元数据模式表包括：

* 选项卡
* 选项卡中的表单项目

您可以将这些表单项映射到／配置到CRX存储库中元数据节点内的字段。

可以向元数据架构表单中添加新的选项卡或表单项目。从父级派生的选项卡和表单项目处于锁定状态。 无法从子级别更改它们。

1. 在“架构表单”页面中，选中表单前面的复选框，然后单击工具栏上的&#x200B;**编辑图标**。
1. 在元数 **[!UICONTROL 据架构编辑器页中]** ，通过将“构建表单”选项卡中的组件类型列表中的一个或多个组件拖至“基本”选项卡，自定义资产的属性页 ******** 。
1. To configure a component, select it and modify its properties in the **Settings** tab.

### “构建表单”选项卡内的组件{#components-within-the-build-form-tab}

The **[!UICONTROL Build Form]** tab lists form items that you use in your schema form. The **[!UICONTROL Settings]** tab provides the attributes of each item that you select in the **[!UICONTROL Build Form]** tab. The following table lists the form items available in the **[!UICONTROL Build Form]** tab:

<table>
 <tbody>
  <tr>
   <td><strong>组件名称</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>章节标题</td>
   <td>添加一列表常用组件的章节标题。</td>
  </tr>
  <tr>
   <td>单行文本</td>
   <td>添加单行文本属性。 它存储为字符串。</td>
  </tr>
  <tr>
   <td>多值文本</td>
   <td>添加多值文本属性。 它存储为字符串数组。</td>
  </tr>
  <tr>
   <td>数字</td>
   <td>添加数字组件。</td>
  </tr>
  <tr>
   <td>日期</td>
   <td>添加日期组件。</td>
  </tr>
  <tr>
   <td>下拉列表</td>
   <td>添加下拉列表。</td>
  </tr>
  <tr>
   <td>标准标记</td>
   <td>添加标记. </td>
  </tr>
  <tr>
   <td>智能标记</td>
   <td>通过自动添加元数据标记来增强搜索功能。<br /> </td>
  </tr>
  <tr>
   <td>隐藏字段</td>
   <td>添加隐藏字段。 在保存资产时，它将作为POST参数发送。</td>
  </tr>
  <tr>
   <td>资产引用对象</td>
   <td>将此组件添加到资产引用的资产的视图列表。</td>
  </tr>
  <tr>
   <td>资产引用</td>
   <td>添加以显示引用资产的资产列表。</td>
  </tr>
  <tr>
   <td>产品引用</td>
   <td>添加以显示与资产链接的产品的列表。</td>
  </tr>
  <tr>
   <td>资产评级</td>
   <td>添加以显示资产评级选项。</td>
  </tr>
  <tr>
   <td>上下文元数据</td>
   <td>添加以控制资产属性页面中其他元数据选项卡的显示。</td>
  </tr>
 </tbody>
</table>

#### 编辑元数据组件 {#edit-the-metadata-component}

To edit the properties of a metadata component on the form, click the component and edit all or a subset of the following properties in the **[!UICONTROL Settings]** tab.

**字段标签**: 资产的属性页面上显示的元数据属性的名称。

**映射到属性**: 此属性指定资产节点在CRX存储库中保存的相对路径／名称。 It starts with `./` because indicating that the path is under the asset&#39;s node.

以下是此属性的有效值：

* . `/jcr:content/metadata/dc:title`：将该值作为属性 `dc:title` 存储在资产的元数据节点中。

* . `/jcr:created`：在资产的节点上显示 jcr 属性。如果您在视图属性上配置这些属性，我们建议您将这些属性标记为“禁用编辑”，因为它们是受保护属性。否则，在保存资产的属性时，会出现“资产修改失败”错误。

要确保在元数据模式表单中正确显示组件，属性路径不应包含任何空格。

**占位符**: 使用此属性可指定与元数据属性相关的占位符文本。

**必需**: 使用此属性可在属性页面上将元数据属性标记为必需。

**禁用编辑**: 使用此属性可使元数据属性在“属性”页面上不可编辑。

**在只读模式下显示空字段**: 标记此属性可在属性页面上显示元数据属性，即使其没有值也是如此。 默认情况下，当元数据属性没有值时，不会在属性页面中列出该属性。

**显示订购列表**: 使用此属性可显示选项的有序列表

**选择**: 使用此属性指定列表中的选项

**描述**：使用此属性可添加对元数据组件的简短描述。

**类**: 属性关联的对象类。

**删除**: 单击以从模式表单中删除组件。

>[!NOTE]
>
>隐藏字段组件不包含这些属性。 而是包括属性，如名称、值、字段标签和说明。 无论何时保存资产，都会将“隐藏字段”组件的值作为 POST 参数进行发送。该组件的值不会作为资产的元数据进行保存。

如果选择&#x200B;**[!UICONTROL 必需]**&#x200B;选项，则可以搜索缺少必需元数据的资产。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，展开&#x200B;**[!UICONTROL 元数据验证]**&#x200B;谓词，然后选择&#x200B;**[!UICONTROL 无效]**&#x200B;选项。搜索结果中显示的资产缺少您通过架构表单配置的必需元数据。

如果您将上下文元数据组件添加到任何模式表单的任何选项卡，该组件将作为列表显示在应用特定模式的资产的属性页面中。 该列表包括除您应用了上下文元数据组件的选项卡外的所有其他选项卡。 目前，此功能提供基本功能，用于根据上下文控制元数据的显示。

要在属性页面中除应用上下文元数据组件的选项卡外，还包括任何选项卡，请从列表中选择该选项卡。 该选项卡会添加到属性页面。

### 在JSON文件中指定属性 {#specify-properties-in-json-file}

您还可以通过指定相应的键值对在 JSON 文件中定义选项，而不是为&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中的选项指定属性。在 **[!UICONTROL JSON 路径]**&#x200B;字段中指定 JSON 文件的路径。

#### 添加和删除模式表单中的选项卡 {#add-delete-a-tab-in-the-schema-form}

通过架构编辑器，可以添加或删除选项卡。默认架构表单包括&#x200B;**[!UICONTROL 基本]**、**[!UICONTROL 高级]**、**[!UICONTROL IPTC]** 和 **[!UICONTROL IPTC 扩展]**&#x200B;选项卡（默认情况下）。

Click `+` to add a new tab on a schema form. By default, the new tab has the name `Unnamed-1`. You can modify the name from the **[!UICONTROL Settings]** tab. Click `X` to delete a tab.

## Deleting metadata schema forms {#deleting-metadata-schema-forms}

AEM允许您仅删除自定义模式表单。 您无法删除默认的架构表单/模板。但是，您可以删除对这些表单所做的任何自定义更改。

要删除表单，请选择一个表单，然后单击删除图标。

>[!NOTE]
>
>删除对默认表单的自定义更改后，在元数据模式界面上，表单前面会重新显示锁图标，以指示表单已恢复为默认状态。

>[!NOTE]
>
>您无法删除AEM资产中开箱即用的元数据模式表单。

## Schema forms for MIME types {#schema-forms-for-mime-types}

AEM资产为各种现成MIME类型提供默认表单。 但是，您可以为各种MIME类型的资产添加自定义表单。

### 为 MIME 类型添加新表单 {#adding-new-forms-for-mime-types}

在相应的表单类型下创建新表单。例如，要为 **image/png** 子类型添加新模板，请在“image”表单下创建表单。架构表单的标题是子类型名称。在这种情况下，标题为“png.**”**

#### 为各种 MIME 类型使用现有架构模板 {#using-an-existing-schema-template-for-various-mime-types}

您可以为不同的 MIME 类型使用现有模板。For example, use the `image/jpeg` form for assets of MIME type `image/png`.

In this case, create a new node at `/etc/dam/metadataeditor/mimetypemappings` in the CRX repository. 指定节点的名称并定义以下属性：

| **名称** | **描述** | **类型** | **值** |
|---|---|---|---|
| `exposedmimetype` | 要映射的现有表单的名称 | 字符串 | `image/jpeg` |
| `mimetypes` | List of MIME types that use the form defined in the `exposedmimetype` attribute | 字符串 | `image/png` |

AEM 资产映射以下 MIME 类型和架构表单：

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
| video/avi | video/avi、video/msvideo、video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Granting access to metadata schemas {#granting-access-to-metadata-schemas}

元数据架构功能仅适用于管理员。不过，管理员可以通过修改一些权限，向非管理员用户提供访问权限。The non administrator should have create, modify, and delete permissions on the `/conf` folder.

## 应用特定于文件夹的元数据 {#applying-folder-specific-metadata}

AEM资产允许您定义元数据模式的变体，并将其应用到特定文件夹。

例如，您可以定义默认元数据模式的变体并将其应用到文件夹。 应用修改后的模式时，该模式将覆盖应用于文件夹内资产的原始默认元数据区域。

只有上传到应用此模式的文件夹的资产才会与变体元数据模式中定义的修改后的元数据相符。

应用原始模式的其他文件夹中的资产会继续与原始模式中定义的元数据保持一致。

资产的元数据继承基于应用于层次结构中第一级文件夹的模式。 换言之，如果文件夹不包含子文件夹，则文件夹内的资产会继承应用于该文件夹的模式的元数据。

如果文件夹有子文件夹，则子文件夹内的资产会继承子文件夹级别所应用模式的元数据(如果子文件夹级别应用了其他模式)。 但是，如果子文件夹级别未应用模式或同一模式，则子文件夹资产将继承父文件夹级别所应用模式的元数据。

1. 单击 AEM 徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 选中表单前面的复选框（例如默认元数据表单），单击或点按复制图标，然后将其另存为自定义表单。 指定表单的自定义名称，例如 `my_default`。 或者，您也可以创建自定义表单。

1. 在元数 **[!UICONTROL 据模式表单]** ，选择表 `my_default` 单，然后单击编 **[!UICONTROL 辑图]** 标。
1. 在元数 **[!UICONTROL 据模式编辑]** 器页面中，向模式表单添加一个文本字段。 例如，添加带有标签类别的 **[!UICONTROL 字段]**。
1. 单击&#x200B;**[!UICONTROL 保存]**。修改后的表单列在元数据 **[!UICONTROL 模式表单页]** 。
1. 单击／点 **[!UICONTROL 按工具栏中的应用到文件夹]** ，以将自定义元数据应用到文件夹。
1. 选择要应用已修改模式的文件夹，然后单击／点按应 **[!UICONTROL 用]**。
1. 如果该文件夹应用了其他元数据模式，则会显示一条消息，警告您将覆盖现有元数据模式。 单击“ **覆盖**”。
1. Click **OK** to close the success message.
1. 导览至应用已修改元数据模式的文件夹。

## 定义强制元数据 {#defining-mandatory-metadata}

您可以在文件夹级别定义必填字段，这将强制执行于上传到该文件夹的资产。 如果您上传的资产上传之前定义的必填字段缺少元数据，则卡视图的资产上会显示缺少元数据的可视指示。

>[!NOTE]
>
>可以根据其他字段的值将元数据字段定义为强制字段。 在“卡”视图中，AEM不显示有关此类强制元数据字段缺失元数据的警告消息。

1. 单击 AEM 徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 将默认元数据表单另存为自定义表单。 例如，将其另存为 `my_default`。
1. 编辑自定义表单。 添加必填字段。 例如，添加一个 **[!UICONTROL 类别]** 字段，并将该字段设为必填。
1. 单击&#x200B;**[!UICONTROL 保存]**。修改后的表单列在元数据 **[!UICONTROL 模式表单页]** 。 选择表单，然后单击或点 **[!UICONTROL 按工具栏中的应用到文]** 件夹，以将自定义元数据应用到文件夹。
1. 导航到文件夹，然后上传某些资产，其中缺少您添加到自定义表单的必填字段的元数据。 资产的卡片视图上会显示必填字段中缺少的元数据的消息。
1. （可选）访 `https://[server]:[port]/system/console/components/`问。 配置并启 `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` 用默认禁用的组件。 设置AEM检查资产上元数据有效性的频率。

   此配置向资产 `hasValidMetadata` 添加 `jcr:content` 属性。 使用此属性，AEM可以筛选搜索结果。

   >[!NOTE]
   >
   >如果资产是在计划检查后添加的，则直到下一个计划检查 `hasValidMetadata` 后，才会将资产标记为。 资产不会显示在中间搜索结果中。

   >[!CAUTION]
   >
   >元数据验证检查会占用大量资源，并且可能会影响系统性能。 计划相应的检查。 如果服务器无法处理加载，请尝试禁用此作业
