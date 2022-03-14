---
title: 文件夹元数据架构
description: 了解如何在中为资产文件夹创建元数据架构 [!DNL Experience Manager Assets]
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: 7ea0e6c2d277199fc5216aab70e587bd23ac6baa
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 17%

---

# 文件夹元数据架构 {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] 允许您为资产文件夹创建元数据架构，这些架构定义了文件夹属性页面中显示的布局和元数据。

## 添加文件夹元数据架构表单 {#add-a-folder-metadata-schema-form}

使用文件夹元数据架构Forms编辑器为文件夹创建和编辑元数据架构。

1. 点按/单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 文件夹元数据架构]**.
1. 在文件夹元数据架构Forms页面中，点按/单击 **[!UICONTROL 创建]**.
1. 指定表单的名称，然后点按/单击 **[!UICONTROL 创建]**. 新架构表单列在架构Forms页面中。

## 编辑文件夹元数据架构表单 {#edit-folder-metadata-schema-forms}

您可以编辑新添加的或现有的元数据架构表单，其中包括：

* 选项卡
* 选项卡中的表单项目

您可以将这些表单项目映射/配置到CRX存储库元数据节点中的字段。 可以向元数据架构表单中添加新的选项卡或表单项目。

1. 在架构Forms页面中，选择您创建的表单，然后点按/单击 **[!UICONTROL 编辑]** 图标。
1. 在文件夹元数据架构编辑器页面中，点按/单击 **[!UICONTROL +]** 图标向表单中添加选项卡。 要重命名选项卡，请点按/单击默认名称，然后在下指定新名称 **[!UICONTROL 设置]**.

   ![custom_tab](assets/custom_tab.png)

   要添加更多选项卡，请点按/单击 **[!UICONTROL +]** 图标。 点按/单击 **[!UICONTROL X]** 删除选项卡。

1. 在活动选项卡中，从 **[!UICONTROL 构建表单]** 选项卡。

   ![adding_components](assets/adding_components.png)

   如果创建多个选项卡，请点按/单击某个特定选项卡以添加组件。

1. 要配置组件，请选择该组件，然后在 **[!UICONTROL 设置]** 选项卡。

   如果需要，请从 **[!UICONTROL 设置]** 选项卡。

   ![configure_properties](assets/configure_properties.png)

1. 点按/单击 **[!UICONTROL 保存]** 来保存更改。

### 用于构建表单的组件 {#components-to-build-forms}

的 **[!UICONTROL 构建表单]** 选项卡列出了您在文件夹元数据架构表单中使用的表单项目。 的 **[!UICONTROL 设置]** 选项卡会显示您在 **[!UICONTROL 构建表单]** 选项卡。 以下是 **[!UICONTROL 构建表单]** 选项卡：

<table>
 <tbody>
  <tr>
   <td><p><strong>组件名称</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>章节标题</p> </td>
   <td><p> 添加一系列常用组件的章节标题。</p> </td>
  </tr>
  <tr>
   <td><p>单行文本</p> </td>
   <td><p> 添加单行文本属性。 它将作为字符串存储。</p> </td>
  </tr>
  <tr>
   <td><p>多值文本</p> </td>
   <td><p> 添加多值文本属性。它将作为字符串数组存储。</p> </td>
  </tr>
  <tr>
   <td><p>数值</p> </td>
   <td><p> 添加数字组件。</p> </td>
  </tr>
  <tr>
   <td><p>日期</p> </td>
   <td><p> 添加日期组件。</p> </td>
  </tr>
  <tr>
   <td><p>下拉列表</p> </td>
   <td><p> 添加下拉列表。</p> </td>
  </tr>
  <tr>
   <td><p>标准标记</p> </td>
   <td><p> 添加标记。 </p> </td>
  </tr>
  <tr>
   <td><p>隐藏字段</p> </td>
   <td><p> 添加隐藏字段。在保存资产时，该字段将作为 POST 参数发送。</p> </td>
  </tr>
 </tbody>
</table>

### 编辑表单项目 {#editing-form-items}

要编辑表单项的属性，请点按/单击组件，然后在 **[!UICONTROL 设置]** 选项卡。 建议仅将一个字段映射到元数据架构中的给定属性。 否则，系统会选取映射到属性的最新添加字段。

**[!UICONTROL 字段标签]**:文件夹的属性页面上显示的元数据属性的名称。

**[!UICONTROL 映射到属性]**:此属性指定保存文件夹节点的CRX存储库中文件夹节点的相对路径。 它以“**./**&quot; ，表示路径位于文件夹的节点下。

以下是属性的有效值示例：

* `./jcr:content/metadata/dc:title`:将该值作为属性存储在文件夹的元数据节点中 `dc:title`.

* `./jcr:created`:存储资产的创建日期和时间。 它是受保护的属性。 如果配置这些属性，Adobe建议您将其标记为 [!UICONTROL 禁用编辑].

要确保组件在元数据架构表单中正确显示，请勿在属性路径中包含空格。

**[!UICONTROL JSON路径]**:使用它可指定JSON文件的路径，您可以在该路径中为选项指定键值对。

**[!UICONTROL 占位符]**:使用此属性可指定与元数据属性相关的占位符文本。

**[!UICONTROL 选择]**:使用此属性可在列表中指定选项。

**[!UICONTROL 描述]**：使用此属性可添加对元数据组件的简短描述。

**[!UICONTROL 类]**:属性与关联的对象类。

## 删除文件夹元数据架构表单 {#delete-folder-metadata-schema-forms}

您可以从文件夹元数据架构Forms页面中删除文件夹元数据架构表单。 要删除某个表单，请将其选中，然后点按/单击工具栏中的删除图标。

![delete_form](assets/delete_form.png)

## 分配文件夹元数据架构 {#assign-a-folder-metadata-schema}

您可以从文件夹元数据架构Forms页面或在创建文件夹时，将文件夹元数据架构分配给文件夹。

如果为文件夹配置元数据架构，则架构表单的路径存储在 `folderMetadataSchema` 下文件夹节点的属性。*/jcr:content*.

### 从“文件夹元数据架构”页面中分配给架构 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 点按/单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]**> **[!UICONTROL 文件夹元数据架构]**.
1. 从文件夹元数据架构Forms页面中，选择要应用于文件夹的架构表单。
1. 在工具栏中，点按/单击 **[!UICONTROL 应用到文件夹]**.

1. 选择要应用架构的文件夹，然后单击/点按 **[!UICONTROL 应用]**. 如果已在文件夹上应用元数据架构，则会出现一条警告消息，告知您将要覆盖现有元数据架构。 点按/单击 **[!UICONTROL 覆盖]**.
1. 打开应用元数据架构的文件夹的元数据属性。

   ![folder_properties](assets/folder_properties.png)

   要查看文件夹元数据字段，请点按/单击&#x200B;**[!UICONTROL 文件夹元数据]**&#x200B;选项卡。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### 创建文件夹时分配架构 {#assign-a-schema-when-creating-a-folder}

在创建文件夹时，您可以分配文件夹元数据架构。 如果系统中至少存在一个文件夹元数据架构，则会在 **[!UICONTROL 创建文件夹]** 对话框。 您可以选择所需的架构。 默认情况下，未选择架构。

1. 从 [!DNL Experience Manager Assets] 用户界面，点按/单击 **[!UICONTROL 创建]** 中。
1. 指定文件夹的标题和名称。
1. 从文件夹元数据架构列表中，选择所需的架构。 然后，点按/单击 **[!UICONTROL 创建]**.

   ![select_schema](assets/select_schema.png)

1. 打开应用元数据架构的文件夹的元数据属性。
1. 要查看文件夹元数据字段，请点按/单击&#x200B;**[!UICONTROL 文件夹元数据]**&#x200B;选项卡。

## 使用文件夹元数据架构 {#use-the-folder-metadata-schema}

打开使用文件夹元数据架构配置的文件夹属性。文件夹属性页面中将显示&#x200B;**[!UICONTROL 文件夹元数据]**。要查看文件夹元数据架构表单，请选择此选项卡。

在各个字段中输入元数据值，然后点按/单击 **[!UICONTROL 保存]** 来存储值。 您指定的值存储在CRX存储库的文件夹节点中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)
