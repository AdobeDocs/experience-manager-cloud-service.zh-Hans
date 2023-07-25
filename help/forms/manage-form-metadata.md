---
title: 管理元数据
seo-title: Manage [!DNL AEM Forms] metadata
description: 元数据允许更轻松地分类和组织资源，并帮助正在查找特定资源的用户。
seo-description: Metadata allows for easier categorization and organization of assets and helps users who are looking for a specific asset.
exl-id: 8527246a-37f0-4d43-a49e-1c76c265514e
source-git-commit: ca0c9f102488c38dbe8c969b54be7404748cbc00
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 3%

---

# 添加、删除或编辑自适应表单的元数据 {#manage-form-metadata}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/creating-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/manage-form-metadata.html) |
| AEM as a Cloud Service | 本文 |

元数据允许更轻松地分类和组织资源，并帮助正在查找特定资源的用户。

[!DNL AEM Forms]默认情况下，会为每个资源类型提供一组定义的元数据。 除了默认元数据之外，您还可以将自定义元数据添加到每个资源类型。 [!DNL AEM Forms] 还为您提供了正确的方法，以便有效地为表单创建、管理和交换所有这些元数据。

<!-- If you are a developer or a site owner, you can customize Forms Portal, the end-user interface for [!DNL AEM Forms] to reflect the metadata you are using in your organization. For more information abouts Forms Portal, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md). -->

## [!DNL AEM Forms] 中的元数据 {#metadata-in-aem-forms}

In [!DNL AEM Forms]，则与资源关联的元数据属性列表取决于其类型。 此外，如果添加任何自定义元数据属性，则会将该属性添加到添加了自定义元数据的类型的所有资产中。

### 资源类型 {#asset-types}

中支持以下资源类型 [!DNL AEM Forms]：

* 表单模板（XFA表单）
* PDF forms
* 文档(平面PDF)
* 自适应表单
* Forms数据模型
* XFS

#### 广泛的元数据列表 {#extensive-list-of-metadata}

以下是中支持的元数据属性的详尽列表 [!DNL AEM Forms]：

<table>
 <tbody> 
  <tr> 
   <td><strong>属性名称</strong></td> 
   <td><strong>资源类型</strong></td> 
   <td><strong>描述</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>标题</td> 
   <td>除资源外的所有其他资源</td> 
   <td>资源的显示名称。<br /> </td> 
  </tr> 
  <tr> 
   <td>描述</td> 
   <td>除资源外的所有其他资源</td> 
   <td>资源的描述。 用户可以指定此值。<br /> </td> 
  </tr> 
  <tr> 
   <td>类型</td> 
   <td>所有</td> 
   <td><p>指定资源类型的只读值。 它可以具有以下值之一：</p> 
    <ul> 
     <li>表单模板</li> 
     <li>PDF表单、PDF表单(Acroform)或PDF表单（签名）</li> 
     <li>文档，文档（已签署）</li> 
     <li>自适应表单</li> 
     <li>表单数据模型</li>
     <li>资源</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>创建时间</td> 
   <td>所有</td> 
   <td>指定资源创建时间的只读值。</td> 
  </tr> 
  <tr> 
   <td>上次修改日期</td> 
   <td>所有</td> 
   <td>指定上次修改资源的时间的只读值。</td> 
  </tr> 
  <tr> 
   <td>创作</td> 
   <td>除资源外的所有其他资源</td> 
   <td><p>根据表单类型自动计算的只读值。</p> 
    <ul> 
     <li>PDF/表单模板/文档 — 从上传的二进制文件获取。</li> 
     <li>自适应表单 — 创建表单时登录用户。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>状态</td> 
   <td>除资源外的所有其他资源</td> 
   <td><p> 只读值，定义表单的以下状态之一：</p> 
    <ul> 
     <li>无值：表示从未发布过表单。</li> 
     <li>已发布：发布表单时。</li> 
     <li>修改时间：表单发布一次后进行修改的时间。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>上次发布日期</td> 
   <td>除资源外的所有其他资源</td> 
   <td>指定上次发布表单时间的只读值。</td> 
  </tr> 
  <tr> 
   <td>发布开启/关闭时间</td> 
   <td>除资源外的所有其他资源</td> 
   <td><p>计划自动发布/取消发布表单的时间。 用户在编辑元数据时设置此值。</p> 
    <ul> 
     <li>发布开始时间和发布结束时间均应在当前日期之后。 </li> 
     <li>发布关闭时间应晚于发布开启时间。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>提交URL</td> 
   <td><p>表单模板</p> <p>PDF表单</p> </td> 
   <td><p>配置用户指定的URL以将表单数据提交到servlet。</p> <p>可以使用以下任意一种方法配置提交URL，按优先顺序排列：</p> 
    <ul> 
     <li>在AEM Forms Designer中创建XFA表单时，通过使用HTTP提交按钮，直接在表单模板中指定提交URL。</li> 
     <li>在AEM Forms UI中，选择表单并在编辑元数据属性时指定提交URL。</li> 
     <!-- <li>In Forms Portal, edit the Search &amp; Lister component and specify a submit URL under the Form Link tab.</li> -->
    </ul> </td> 
  </tr> 
  <tr> 
   <td>HTML渲染配置文件</td> 
   <td>表单模板</td> 
   <td>以HTML格式呈现表单HTML时使用的模板渲染配置文件。</td> 
  </tr> 
  <tr> 
   <td>渲染格式</td> 
   <td><p>表单模板</p> <p>自适应表单</p> </td> 
   <td><p>此选项允许用户指定发布表单时的表单渲染格式：</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li> 双向</li> 
    </ul> <p>此选项仅用于限制表单在最终用户可见的表单门户上的呈现格式。</p> </td> 
  </tr> 
  <tr> 
   <td>标记</td> 
   <td>除资源外的所有其他资源</td> 
   <td>与表单关联的标签有助于快速轻松搜索。</td> 
  </tr> 
  <tr> 
   <td>引用</td> 
   <td><p>自适应表单</p> <p>表单模板</p> <p>资源</p> </td> 
   <td><p>与此表单相关的资产（其他表单或资源）列表。 这些资产可以分为以下两类：</p> 
    <ul> 
     <li>引用：当前表单引用的资产。</li> 
     <li>引用者：引用当前资产的资产。</li> 
    </ul> <p>这些资源显示为链接，可以通过单击它们直接访问其元数据。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>表单模型(XDP/XSD)选择</td> 
   <td>自适应表单</td> 
   <td><p>指定在创作自适应表单时使用的表单模型。 此属性可以具有以下值：</p> 
    <ul> 
      <li>表单数据模型 </li>
      <li>架构： JSON架构的XML</li>
     <!-- <li>Form template: A form template is selected from the ones existing in the repository. This value can be updated.</li> 
     <li>XML schema: An XSD file is uploaded. This value can be updated.</li> -->
     <li>无</li> 
    </ul> 
    <div>
      表单模型一旦选定便可以更新，但不能删除。 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## 查看表单元数据 {#view-form-metadata}

资产具有现有的属性值，可以在只读模式下查看这些值。 此元数据源自表单上传或表单创建时。

1. 导航到要查看其元数据的资源的位置。

1. 使用以下方式之一打开属性页面：

   * 单击 **[!UICONTROL 属性]** ![属性](assets/Smock_Info_18_N.svg) 图标。

     >[!NOTE]
     >
     >快速操作是在鼠标悬停时显示在缩略图上的操作项。

   * 选择表单并单击 **[!UICONTROL 属性]** ![属性](assets/Smock_Info_18_N.svg) 工具栏中显示的图标。
   * 在不处于选择模式时，通过单击表单缩略图导航到表单详细信息页面。 现在，单击 ![属性](assets/Smock_Info_18_N.svg) 右上角的眼睛图标，然后单击其下方列表中的“属性”。

1. 打开的属性页显示一个方案，其中仅包含那些保存某些值的元数据属性。

   <!-- The properties page has a toolbar containing two action icons:

    * Edit: ![Edit](assets/Smock_Edit_18_N.svg) Edit the metadata property values
    * View: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navigate to the form details page, which opens the form in the preview mode. -->

   内容部分分为两部分：

   * 左侧面板包含表单的缩略图
   * 右侧面板以只读模式包含元数据属性，这些属性分布在不同的选项卡中。

## 添加/更新表单元数据值 {#add-update-form-metadata-values}

您可以编辑现有元数据属性的值或向现有元数据属性字段添加新值（例如，当元数据字段为空时）。

<!-- ### Update metadata property values {#update-metadata-property-values}

1. Follow the steps mentioned in the previous section to open the properties page where existing metadata of the selected form can be viewed.  

1. From the toolbar, click the Edit icon ![Edit](assets/Smock_Edit_18_N.svg) to change the mode of the page from read-only to read/write.  

1. The properties page that opens holds a schema that contains a mix of editable input fields and static text.  

1. The properties displayed in static text are the ones that you cannot edit.  

1. You can navigate to other tabs to find input fields for metadata properties placed under them.

   This page has a toolbar containing two action icons different from those in view mode:

    * Cancel: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Cancel any changes made to metadata property values so far
    * Done: ![aem6forms_check](assets/aem6forms_check.png) Save all the changes made to metadata property values so far

   Both these actions direct the user back to read-only mode of the properties page containing the updated values.-->

### 更新表单缩略图 {#update-the-form-thumbnail}

属性页面中的左侧面板显示表单的缩略图。 默认情况下，显示的缩略图是创建表单（自适应表单）时或上传表单时生成的缩略图。

对于所有表单类型，您可以选择通过单击 **[!UICONTROL 上传图像]** 和从本地目录浏览图像文件。 所选图像用作缩略图，而不是默认图像。

对于自适应Forms，还提供了附加功能，允许用户生成缩略图作为当前自适应表单预览的快照。 从 [!DNL AEM Forms] 还支持自适应Forms的创作，每次更改自适应表单时，自适应表单的预览可能会更改。 此功能可生成缩略图，以帮助您根据当前预览状态获取自适应表单的新缩略图。 单击 **[!UICONTROL 生成预览]** 执行这项操作。

>[!NOTE]
>
>* 缩略图使用正方形图像。 当您使用非正方形图像并在列表视图中查看缩略图时，缩略图显示为已剪切。
>* 上传或生成新图像后，缩略图将被此图像替换，并且无法重置为上一个图像。
>

## 添加自定义元数据 {#add-custom-metadata}

除了开箱即用的元数据之外， [!DNL AEM Forms] 支持新的自定义元数据。

提供了一个工具（元数据架构编辑器）来定义元数据布局的架构；即， **[!UICONTROL 属性]** 表单的页面。 元数据架构编辑器允许您添加或修改资源的自定义架构。

[!DNL AEM Forms] 公开此工具中支持的表单类型的元数据架构。 通过这种方式，您可以访问这些架构，并使用元数据架构编辑器中提供的功能来添加自定义属性。

### 在元数据架构编辑器中导航 {#navigate-the-metadata-schema-editor}

1. 导航到 **[!UICONTROL 工具>资产>元数据架构]**.

1. 单击 **[!UICONTROL 表单]** 从列出的架构表单中。

1. 在打开的列表中，单击要添加自定义元数据的资源类型。

   >[!NOTE]
   >
   >这些架构包含现成提供的元数据属性，不得更改/编辑（选中复选框并单击工具栏中的编辑）以避免功能问题。

1. 单击的任何资源类型都会打开一个列表，其中包含 `extendedmetadata` 选项。 编辑此架构。

1. 选中旁边的复选框 `extendedmetadata` 然后单击“编辑” ![编辑](assets/Smock_Edit_18_N.svg) 工具栏中显示的图标。

1. [!DNL AEM Forms] 打开所选资源类型的元数据架构编辑器/表单生成器（在本例中为“自适应表单”）。

   元数据编辑器

   1. 左侧面板包含放置字段的选项卡部分，右侧面板显示所有可用的UI组件以及从左侧面板中选择的字段的属性。

   1. 锁定的部分不可编辑，并包含现成提供的所有元数据属性的字段。

   1. 单击+符号可添加其他选项卡。

   1. 您可以通过从以下位置拖动字段组件来添加所需类型的自定义字段： **[!UICONTROL 构建表单]** 部分。
   1. 此字段的规范可在 **[!UICONTROL 设置]** 字段后的区域。

### 在架构编辑器中添加自定义元数据属性 {#add-custom-metadata-property-in-schema-editor}

1. 导航到要在其中添加自定义属性的选项卡（现有或新）。

1. 将所需类型的组件从 **[!UICONTROL 构建表单]** 部分到左侧面板，并放置在方便的位置。

   >[!NOTE]
   >
   >不能移动锁定的部分，但可以将组件放在任何空格中。

1. 单击刚刚拖动的组件。 在右侧面板中打开的“设置”选项卡中，填写以下字段的信息：

   1. 指定字段标签，以用作位于架构中的字段上方的显示名称（例如：Department）
   1. 在映射到属性字段下，您可以看到预填充的值 **&#39;./jcr：content/metadata/default&#39;**. 更改&#39;**默认**”到所需的属性名称，该名称用于在crx存储库中存储属性(例如： &#39;。/jcr：content/metadata/department&#39;)

      >[!NOTE]
      >
      >请勿更改前缀&#39;。/jcr：content/metadata/&#39;，因为它定义存储属性的路径。
      >
      >此外，属性名称必须是唯一的，以避免在存储库中的同一位置写入两个或多个属性的值。 因此，建议您更改“default”值。

   1. 根据需要填写其他设置。 例如：如果要使字段成为必填字段，请选择必填选项。
   1. 要删除添加的字段，请选择该字段，然后单击删除 ![删除](assets/Smock_Delete_18_N.svg) 图标。

1. 如有必要，请按照步骤1-3添加其他资产。
1. 单击 **[!UICONTROL 保存]** 完成所有更改之后。

   您已成功添加自定义元数据属性。

中的所有自适应Forms [!DNL AEM Forms] 现在包含此额外的元数据属性。 您可以从属性页面中编辑它。
