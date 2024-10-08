---
title: 文件夹元数据架构
description: 了解如何在 [!DNL Experience Manager Assets]中为资源文件夹创建元数据架构
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 10%

---

# 文件夹元数据架构 {#folder-metadata-schema}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

[!DNL Adobe Experience Manager Assets]允许您为资源文件夹创建元数据架构，这些文件夹定义文件夹属性页面中显示的布局和元数据。

## 添加文件夹元数据架构表单 {#add-a-folder-metadata-schema-form}

使用文件夹元数据架构Forms编辑器创建和编辑文件夹的元数据架构。

1. 选择[!DNL Experience Manager]徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 文件夹元数据架构]**。
1. 在“文件夹元数据架构Forms”页面中，选择&#x200B;**[!UICONTROL 创建]**。
1. 指定表单的名称，然后选择&#x200B;**[!UICONTROL 创建]**。 新的架构表单列在架构Forms页面中。

## 编辑文件夹元数据架构表单 {#edit-folder-metadata-schema-forms}

您可以编辑新添加或现有元数据架构表单，其中包含以下内容：

* 选项卡
* 选项卡中的表单项目。

您可以将这些表单项目映射/配置到CRX存储库中元数据节点内的字段。 您可以将新选项卡或表单项添加到元数据架构表单。

1. 在“架构Forms”页面中，选择您创建的表单，然后从工具栏中选择&#x200B;**[!UICONTROL 编辑]**&#x200B;图标。
1. 在“文件夹元数据架构编辑器”页中，选择&#x200B;**[!UICONTROL +]**&#x200B;图标以向表单添加选项卡。 要重命名选项卡，请选择默认名称，并在&#x200B;**[!UICONTROL 设置]**&#x200B;下指定新名称。

   ![自定义选项卡](assets/custom_tab.png)

   要添加更多选项卡，请选择&#x200B;**[!UICONTROL +]**&#x200B;图标。 选择&#x200B;**[!UICONTROL X]**&#x200B;以删除选项卡。

1. 在活动选项卡中，从&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡添加一个或多个组件。

   ![正在添加_组件](assets/adding_components.png)

   如果创建多个选项卡，请选择特定选项卡以添加组件。

1. 要配置组件，请选择该组件并在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中修改其属性。

   如有必要，请从&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中删除组件。

   ![配置_属性](assets/configure_properties.png)

1. 从工具栏中选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改。

### 用于构建表单的组件 {#components-to-build-forms}

**[!UICONTROL 构建表单]**&#x200B;选项卡列出了您在文件夹元数据架构表单中使用的表单项。 **[!UICONTROL 设置]**&#x200B;选项卡显示您在&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡中选择的每个项目的属性。 以下是&#x200B;**[!UICONTROL 生成表单]**&#x200B;选项卡中可用的表单项列表：

<table>
 <tbody>
  <tr>
   <td><p><strong>组件名称</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>章节标题</p> </td>
   <td><p> 为常用组件列表添加章节标题。</p> </td>
  </tr>
  <tr>
   <td><p>单行文本</p> </td>
   <td><p> 添加单行文本属性。 它存储为字符串。</p> </td>
  </tr>
  <tr>
   <td><p>多值文本</p> </td>
   <td><p> 添加多值文本属性。 它存储为字符串数组。</p> </td>
  </tr>
  <tr>
   <td><p>数字</p> </td>
   <td><p> 添加一个数值组件。</p> </td>
  </tr>
  <tr>
   <td><p>日期</p> </td>
   <td><p> 添加一个日期组件。</p> </td>
  </tr>
  <tr>
   <td><p>下拉列表</p> </td>
   <td><p> 添加一个下拉列表。</p> </td>
  </tr>
  <tr>
   <td><p>标准标记</p> </td>
   <td><p> 添加标记。 </p> </td>
  </tr>
  <tr>
   <td><p>隐藏字段</p> </td>
   <td><p> 添加隐藏字段。 在保存资源时，它将作为POST参数发送。</p> </td>
  </tr>
 </tbody>
</table>

### 编辑表单项目 {#editing-form-items}

要编辑表单项的属性，请选择该组件并在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中编辑以下所有属性或属性子集。 建议仅将一个字段映射到元数据架构中的给定属性。 否则，系统会选取映射到属性的最新添加字段。

**[!UICONTROL 字段标签]**：在文件夹的属性页面上显示的元数据属性的名称。

**[!UICONTROL 映射到属性]**：此属性指定保存它的CRX存储库中文件夹节点的相对路径。 它以“**”开头。/**”，这表示路径在文件夹的节点下。

以下是属性的有效值示例：

* `./jcr:content/metadata/dc:title`：将该值作为属性`dc:title`存储在文件夹的元数据节点中。

* `./jcr:created`：存储资源的创建日期和时间。 它是受保护的资产。 如果配置这些属性，Adobe建议将它们标记为[!UICONTROL 禁用编辑]。

要确保组件在元数据架构表单中正确显示，请不要在属性路径中包含空格。

**[!UICONTROL JSON路径]**：使用它指定JSON文件的路径，在该路径中为选项指定键值对。

**[!UICONTROL 占位符]**：使用此属性指定与元数据属性相关的占位符文本。

**[!UICONTROL 选项]**：使用此属性指定列表中的选项。

**[!UICONTROL 描述]**：使用此属性为元数据组件添加简短描述。

**[!UICONTROL 类]**：与属性关联的对象类。

## 删除文件夹元数据架构表单 {#delete-folder-metadata-schema-forms}

您可以从“文件夹元数据架构Forms”页面中删除文件夹元数据架构表单。 要删除表单，请选择该表单并从工具栏中选择删除图标。

![delete_form](assets/delete_form.png)

## 分配文件夹元数据架构 {#assign-a-folder-metadata-schema}

您可以从文件夹元数据架构Forms页面或在创建文件夹时，将文件夹元数据架构分配给文件夹。

如果为文件夹配置元数据架构，则架构表单的路径将存储在下的文件夹节点的`folderMetadataSchema`属性中。*/jcr：content*。

### 从“文件夹元数据架构”页分配给架构 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 选择[!DNL Experience Manager]徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]**> **[!UICONTROL 文件夹元数据架构]**。
1. 从文件夹元数据架构Forms页面中，选择要应用于文件夹的架构表单。
1. 从工具栏中选择&#x200B;**[!UICONTROL 应用到文件夹]**。

1. 选择要应用架构的文件夹，然后选择&#x200B;**[!UICONTROL 应用]**。 如果元数据架构已应用于文件夹，则会显示一条警告消息，告知您即将覆盖现有的元数据架构。 选择&#x200B;**[!UICONTROL 覆盖]**。
1. 打开将元数据架构应用到的文件夹的元数据属性。

   ![folder_properties](assets/folder_properties.png)

   要查看文件夹元数据字段，请选择&#x200B;**[!UICONTROL 文件夹元数据]**&#x200B;选项卡。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### 创建文件夹时分配架构 {#assign-a-schema-when-creating-a-folder}

您可以在创建文件夹时分配文件夹元数据架构。 如果系统中至少存在一个文件夹元数据架构，则&#x200B;**[!UICONTROL 创建文件夹]**&#x200B;对话框中会显示一个额外的列表。 您可以选择所需的架构。 默认情况下，未选择架构。

1. 从[!DNL Experience Manager Assets]用户界面中，从工具栏中选择&#x200B;**[!UICONTROL 创建]**。
1. 指定文件夹的标题和名称。
1. 从文件夹元数据架构列表中，选择所需的架构。 然后选择&#x200B;**[!UICONTROL 创建]**。

   ![select_schema](assets/select_schema.png)

1. 打开将元数据架构应用到的文件夹的元数据属性。
1. 要查看文件夹元数据字段，请选择&#x200B;**[!UICONTROL 文件夹元数据]**&#x200B;选项卡。

## 使用文件夹元数据架构 {#use-the-folder-metadata-schema}

打开使用文件夹元数据架构配置的文件夹属性。文件夹属性页面中将显示&#x200B;**[!UICONTROL 文件夹元数据]**。要查看文件夹元数据架构表单，请选择此选项卡。

在各个字段中输入元数据值，然后选择&#x200B;**[!UICONTROL 保存]**&#x200B;以存储这些值。 您指定的值存储在CRX存储库的文件夹节点中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
