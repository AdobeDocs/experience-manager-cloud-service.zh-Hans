---
title: 管理元数据
seo-title: Manage [!DNL AEM Forms] metadata
description: 元数据可以更轻松地对资产进行分类和组织，并帮助正在查找特定资产的用户。
seo-description: Metadata allows for easier categorization and organization of assets and helps users who are looking for a specific asset.
exl-id: 8527246a-37f0-4d43-a49e-1c76c265514e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 2%

---

# 添加、删除或编辑自适应表单的元数据 {#manage-form-metadata}

元数据可以更轻松地对资产进行分类和组织，并帮助正在查找特定资产的用户。

[!DNL AEM Forms]默认情况下，会为每个资产类型提供一组定义的元数据。 除了默认元数据之外，您还可以向每种资产类型添加自定义元数据。 [!DNL AEM Forms] 此外，还为您提供了有效创建、管理和交换所有这些元数据的正确方法。

<!-- If you're a developer or a site owner, you can customize Forms Portal, the end-user interface for [!DNL AEM Forms] to reflect the metadata you're using in your organization. For more information abouts Forms Portal, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md). -->

## 元数据(位于 [!DNL AEM Forms] {#metadata-in-aem-forms}

在 [!DNL AEM Forms]，则与资产关联的元数据属性列表取决于其类型。 此外，如果添加任何自定义元数据属性，则该属性会添加到添加了自定义元数据的类型的所有资产中。

### 资产类型 {#asset-types}

支持以下资产类型 [!DNL AEM Forms]:

* 表单模板（XFA表单）
* PDF forms
* 文档(平面PDF)
* 自适应表单
* Forms数据模型
* XFS

#### 元数据的广泛列表 {#extensive-list-of-metadata}

以下是 [!DNL AEM Forms]:

<table>
 <tbody> 
  <tr> 
   <td><strong>属性名称</strong></td> 
   <td><strong>资产类型</strong></td> 
   <td><strong>描述</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>标题</td> 
   <td>除资源外</td> 
   <td>资产的显示名称。<br /> </td> 
  </tr> 
  <tr> 
   <td>描述</td> 
   <td>除资源外</td> 
   <td>资产的描述。 用户可以指定此值。<br /> </td> 
  </tr> 
  <tr> 
   <td>类型</td> 
   <td>所有</td> 
   <td><p>指定资产类型的只读值。 它可以具有以下值之一：</p> 
    <ul> 
     <li>表单模板</li> 
     <li>PDF表单、PDF表单(Acroform)或PDF表单（签名）</li> 
     <li>文档，文档（签名）</li> 
     <li>自适应表单</li> 
     <li>表单数据模型</li>
     <li>资源</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>创建时间</td> 
   <td>所有</td> 
   <td>指定资产创建时间的只读值。</td> 
  </tr> 
  <tr> 
   <td>上次修改日期</td> 
   <td>所有</td> 
   <td>一个只读值，指定上次修改资产的时间。</td> 
  </tr> 
  <tr> 
   <td>创作</td> 
   <td>除资源外</td> 
   <td><p>基于表单类型自动计算的只读值。</p> 
    <ul> 
     <li>PDF/表单模板/文档 — 从上传的二进制文件中获取。</li> 
     <li>自适应表单 — 在表单创建时登录用户。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>状态</td> 
   <td>除资源外</td> 
   <td><p> 一个只读值，用于定义表单的以下状态之一：</p> 
    <ul> 
     <li>无值：如果表单从未发布。</li> 
     <li>已发布：发布表单时。</li> 
     <li>已修改：表单在发布后被修改一次的时间。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>上次发布日期</td> 
   <td>除资源外</td> 
   <td>一个只读值，指定上次发布表单的时间。</td> 
  </tr> 
  <tr> 
   <td>发布开/关时间</td> 
   <td>除资源外</td> 
   <td><p>表单计划自动发布/取消发布的时间。 用户在编辑元数据时会设置此值。</p> 
    <ul> 
     <li>“发布”和“关闭”时间都应超出当前日期。 </li> 
     <li>“发布结束”时间应该超出“发布正时”时间。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>提交URL</td> 
   <td><p>表单模板</p> <p>PDF表单</p> </td> 
   <td><p>配置用户指定的URL，以将表单数据提交到Servlet。</p> <p>可以使用以下任何方法配置提交URL，这些方法按优先顺序列出：</p> 
    <ul> 
     <li>在AEM Forms Designer中创建XFA表单时，使用HTTP提交按钮直接在表单模板中指定提交URL。</li> 
     <li>在AEM Forms UI中，选择一个表单，然后在编辑元数据属性时指定提交URL。</li> 
     <!-- <li>In Forms Portal, edit the Search &amp; Lister component and specify a submit URL under the Form Link tab.</li> -->
    </ul> </td> 
  </tr> 
  <tr> 
   <td>HTML渲染配置文件</td> 
   <td>表单模板</td> 
   <td>以HTML格式呈现表单模板时使用的HTML渲染配置文件。</td> 
  </tr> 
  <tr> 
   <td>呈现格式</td> 
   <td><p>表单模板</p> <p>自适应表单</p> </td> 
   <td><p>此选项允许用户在发布表单时指定表单的呈现格式：</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>两者</li> 
    </ul> <p>此选项用于限制仅在对最终用户可见的表单门户上呈现格式。</p> </td> 
  </tr> 
  <tr> 
   <td>标记</td> 
   <td>除资源外</td> 
   <td>与表单关联的标签，以便于快速、轻松地搜索。</td> 
  </tr> 
  <tr> 
   <td>引用</td> 
   <td><p>自适应表单</p> <p>表单模板</p> <p>资源</p> </td> 
   <td><p>此表单所关联的资产（其他表单或资源）列表。 这些资产可以分为以下两类：</p> 
    <ul> 
     <li>指：当前表单引用的资产。</li> 
     <li>引用者：指流动资产的资产。</li> 
    </ul> <p>这些资产会显示为链接，单击即可直接访问其元数据。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>表单模型(XDP/XSD)选择</td> 
   <td>自适应表单</td> 
   <td><p>指定创作自适应表单时使用的表单模型。 此属性可以具有以下值：</p> 
    <ul> 
      <li>表单数据模型 </li>
      <li>架构：JSON架构的XML</li>
     <!-- <li>Form template: A form template is selected from the ones existing in the repository. This value can be updated.</li> 
     <li>XML schema: An XSD file is uploaded. This value can be updated.</li> -->
     <li>无</li> 
    </ul> 
    <div>
      选择表单模型后，可以更新但不能删除该模型。 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## 查看表单元数据 {#view-form-metadata}

资产具有现有的属性值，这些属性值可在只读模式下查看。 此元数据在表单上传或表单创建时发起。

1. 导航到要查看其元数据的资产位置。

1. 使用以下方法之一打开属性页面：

   * 单击 **[!UICONTROL 属性]** ![属性](assets/Smock_Info_18_N.svg) 图标。

      >[!NOTE]
      >
      >快速操作是指将鼠标悬停在缩略图上时显示的操作项目。

   * 选择表单并单击 **[!UICONTROL 属性]** ![属性](assets/Smock_Info_18_N.svg) 图标。
   * 当不在选择模式下时，通过单击表单缩略图导航到表单详细信息页面。 现在，单击 ![属性](assets/Smock_Info_18_N.svg) 右上方的“眼睛”图标，然后单击该图标下方列表中的“属性”。

1. 打开的属性页面会显示一个架构，其中仅包含那些包含某些值的元数据属性。

   <!-- The properties page has a toolbar containing two action icons:

    * Edit: ![Edit](assets/Smock_Edit_18_N.svg) Edit the metadata property values
    * View: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navigate to the form details page, which opens the form in the preview mode. -->

   内容部分分为两部分：

   * 左侧面板包含表单的缩略图
   * 右侧面板包含只读模式下的元数据属性，这些属性分布于各种选项卡中。

## 添加/更新表单元数据值 {#add-update-form-metadata-values}

您可以编辑现有元数据属性的值，或向现有元数据属性字段添加新值（例如，当元数据字段为空时）。

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

属性页面中的左侧面板显示表单的缩略图。 默认情况下，显示的缩略图是在创建表单（自适应表单）或上传表单时生成的缩略图。

对于所有表单类型，您可以选择通过单击 **[!UICONTROL 上传图像]** 和从本地目录浏览图像文件。 选定的图像将用作缩略图，而不是默认的缩略图。

对于自适应Forms，提供了其他功能，该功能允许用户生成缩略图作为当前自适应表单预览的快照。 自 [!DNL AEM Forms] 此外，还支持创作自适应Forms，每当您更改自适应表单时，自适应表单的预览可能会发生更改。 生成缩略图的功能可帮助您根据当前预览状态为自适应表单获取新的缩略图。 单击 **[!UICONTROL 生成预览]** 来执行这项行动。

>[!NOTE]
>
>* 缩览图使用方形图像。 当您使用非方形图像并在列表视图中查看缩略图时，缩略图会被剪贴。
>* 上传或生成新图像后，缩略图将被此图像替换，无法重置为之前的图像。
>


## 添加自定义元数据 {#add-custom-metadata}

除了现成提供的元数据外， [!DNL AEM Forms] 支持新的自定义元数据。

提供了一种工具（元数据架构编辑器），用于定义元数据布局的架构；即， **[!UICONTROL 属性]** 页面。 利用元数据架构编辑器，可添加或修改资产的自定义架构。

[!DNL AEM Forms] 在此工具中公开了支持的表单类型的元数据架构。 这样，您就可以访问这些架构，并使用元数据架构编辑器中提供的功能来添加自定义属性。

### 导航元数据架构编辑器 {#navigate-the-metadata-schema-editor}

1. 导航到 **[!UICONTROL 工具> Assets >元数据架构]**.

1. 单击 **[!UICONTROL 表单]** 从列出的架构表单中。

1. 在打开的列表中，单击要为其添加自定义元数据的资产类型。

   >[!NOTE]
   >
   >这些架构包含现成提供的元数据属性，这些属性不得更改/编辑（选中复选框，然后单击工具栏中的编辑），以避免出现功能问题。

1. 单击的任何资产类型都会打开一个包含 `extendedmetadata` 选项。 编辑此架构。

1. 选中旁边的复选框 `extendedmetadata` ，然后单击“编辑” ![编辑](assets/Smock_Edit_18_N.svg) 图标。

1. [!DNL AEM Forms] 打开选定资产类型的元数据架构编辑器/表单生成器（在本例中为“自适应表单”）。

   元数据编辑器

   1. 左侧面板包含放置字段的选项卡部分，右侧面板显示所有可用的UI组件以及从左侧面板中选择的字段的属性。

   1. 锁定的部分不可编辑，其中包含现成提供的所有元数据属性的字段。

   1. 您可以通过单击+符号添加其他选项卡。

   1. 您可以通过从 **[!UICONTROL 构建表单]** 部分。
   1. 此字段的规范可在 **[!UICONTROL 设置]** 中，将会在页面上显示该对话框。

### 在架构编辑器中添加自定义元数据属性 {#add-custom-metadata-property-in-schema-editor}

1. 导航到要在其中添加自定义属性的选项卡（现有或新）。

1. 从 **[!UICONTROL 构建表单]** 区域，并放置在方便的位置。

   >[!NOTE]
   >
   >您无法移动锁定的部分，但可以将组件放置在任何空格中。

1. 单击之前拖动的组件。 在右侧面板中打开的设置选项卡中，填写以下字段的信息：

   1. 指定字段标签，该标签将用作架构中放置的字段上方的显示名称(例如：部门)
   1. 在映射到属性字段下，您可以看到一个预填充的值 **&#39;。/jcr:content/metadata/default`**. 更改“**默认**“ ”到所需的属性名称，该属性名称用于将属性存储在crx存储库中(例如：&#39;。/jcr:content/metadata/department&#39;)

      >[!NOTE]
      >
      >请勿更改前缀“。/jcr:content/metadata/&#39; ，它定义存储属性的路径。
      >
      >此外，属性名称必须是唯一的，以避免为存储库中同一位置的两个或多个属性写入值。 因此，建议您更改值“default”。

   1. 根据需要填写其他设置。 例如：如果要将字段设为必填字段，请选择“必填”选项。
   1. 要删除添加的字段，请选择该字段，然后单击删除 ![删除](assets/Smock_Delete_18_N.svg) 图标。

1. 如有必要，请按照步骤1-3添加其他属性。
1. 单击 **[!UICONTROL 保存]** 进行所有更改之后。

   您已成功添加自定义元数据属性。

中的所有自适应Forms [!DNL AEM Forms] 现在包含此附加的元数据属性。 您可以从属性页面中编辑该属性。
