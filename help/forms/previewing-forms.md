---
title: 如何预览自适应表单？
description: 用户可以在发布或激活表单之前预览表单，以确保表单符合预期。 预览选项可能因支持的表单类型而异。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 3%

---


# 预览表单 {#previewing-a-form}

## 概述 {#overview}

在 [!DNL AEM Forms]中，您可以预览存储库中存在的表单和文档。 预览有助于了解表单在发布给最终用户时的具体外观和行为。

在预览表单时，它们会在交互式界面中呈现，用户可以用数据填充表单。 预览文档时，它们以非交互模式呈现，用户只能查看文档。 对于表单，还提供了自定义预览的附加选项。 使用此选项，您可以使用XML文件中的数据预览表单。 数据会填充正在预览的表单的某些字段或所有字段。

下表列出了适用于不同类型受支持表单的预览选项：

<table>
 <tbody>
  <tr>
   <td><strong>资源类型</strong><br /> </td>
   <td><strong>可用的预览选项</strong><br /> </td>
  </tr>
  <tr>
   <td>文档</td>
   <td>PDF预览</td>
  </tr>
  <tr>
   <td>PDF表单</td>
   <td>使用数据预览和预览PDF<br /> </td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td>包含数据的HTML预览和HTML预览</td>
  </tr>
  <tr>
   <td>表单模板</td>
   <td>PDF预览、包含数据的PDF预览、HTML预览、包含数据的HTML预览<br /> </td>
  </tr>
 </tbody>
</table>

## 预览表单 {#previewing-a-form-1}

1. 选择要预览的资源，然后单击预览 ![aem6forms_preview](assets/aem6forms_preview.png) （在操作工具栏中）。

   >[!NOTE]
   >
   >要选择资产，请从默认信息卡视图切换到列表视图。 单击 ![aem6forms_viewlist](assets/aem6forms_viewlist.png) 或 ![aem6forms_viewcard](assets/aem6forms_viewcard.png) 以切换视图。

1. 单击预览会列出适用于所选资源类型的可能预览选项。 单击所需选项可在新选项卡中呈现所选资源。

   您的选项包括：

   * HTML预览
   * 使用数据预览
   * PDF预览（适用于表单模板）

## 使用数据预览 {#preview-with-data}

当您选择时 **使用数据预览**，您可以查看输入真实数据的表单的外观。 使用数据预览选项允许您上传包含示例用户数据的XML。 示例用户数据用于以您选择的格式填充预览表单。

1. 选择资源，单击预览 ![aem6forms_preview](assets/aem6forms_preview.png)，并选择 **使用数据预览**.
1. 在“预览表单”对话框中，将FormData作为XML文件提供。 单击预览以使用XML中的合并数据呈现表单。

