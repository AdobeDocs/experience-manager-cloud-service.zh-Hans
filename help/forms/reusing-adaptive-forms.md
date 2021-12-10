---
title: 重复使用自适应表单的元数据属性
seo-title: Reuse metadata properties of an Adaptive Form
description: 您可以重复使用现有的自适应表单来创建新的自适应Forms。
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 重复使用自适应表单的元数据属性 {#reusing-adaptive-forms}

如果要使用现有自适应表单的某些属性生成新属性，您只需使用复制粘贴功能即可。 此外，您还可以将新的自适应表单粘贴到所需的文件夹路径中。 将复制所有元数据属性，并且还会复制基于XFA和XSD的自适应Forms的XFA和XSD。

>[!NOTE]
>
>不会复制状态和审阅详细信息。 例如，如果您的自适应表单已发布，然后复制它，则粘贴的自适应表单将处于未发布状态。 同样，如果复制的资产正在审核中，则粘贴的资产也不会处于同一审核下。

## 复制自适应表单 {#copy-an-adaptive-form}

使用以下任一方法复制自适应表单：

1. 单击复制 ![aem6forms_copy](assets/aem6forms_copy.png) 图标。

   >[!NOTE]
   >
   >快速操作是指将鼠标悬停在缩略图上时显示的操作项目。

1. 选择自适应表单。 不同视图的选择过程不同。

   如果您处于卡片视图中，请通过单击选定内容进入选择模式 ![aem6forms_check_circle](assets/aem6forms_check-circle.png) 图标，然后单击要复制的所有自适应Forms。

   如果您处于列表视图中，请单击所有自适应Forms的复选框以选择它们。

   >[!NOTE]
   >
   >所有选定的资产都必须是自适应Forms，因为只有自适应Forms支持复制粘贴功能，并且选定的所有资产都必须位于同一文件夹中。

   选择资产后，单击 ![aem6forms_copy](assets/aem6forms_copy.png) 图标以复制所选的自适应表单。

## 粘贴自适应表单 {#paste-an-adaptive-form}

单击复制操作会自动退出选择模式并进行粘贴 ![粘贴](assets/Smock_Paste_18_N.svg) 图标。 现在转到所需的文件夹路径并单击粘贴 ![粘贴](assets/Smock_Paste_18_N.svg) 图标以粘贴复制的自适应表单。

如果您粘贴到同一文件夹中，或者此目标文件夹中存在具有相同节点名称（与该节点名称存储在CRX存储库中）的其他文件，则1会附加到后缀中(例如，myaf将变为myaf1，而myaf1存在于同一位置，则myaf将变为myaf2。 所有其他属性仍与原始自适应表单相同。

单击粘贴后 ![粘贴](assets/Smock_Paste_18_N.svg) 图标，该图标将再次隐藏。 一次只能粘贴一次。 要再次创建同一资产的副本，请再次复制。

## 更改新自适应表单的内容 {#change-contents-of-new-adaptive-form}

可以使用以下方法更改粘贴的自适应Forms的内容，使其与复制的表单不同：

1. **更改元数据属性：**

   您可以更改自适应表单的元数据属性，例如标题和描述。 有关元数据属性及其更改方式的更多详细信息，请参阅 [管理表单元数据](manage-form-metadata.md)

1. **为基于XFA/XSD的自适应Forms更改XFA/XSD:**

   您可以更改自适应Forms中使用的XFA/XSD。 要了解如何更改这些自适应Forms，请参阅 [管理表单元数据](manage-form-metadata.md)

1. **重新发布:**

   粘贴的资产与复制的资产不同。 您可以将其作为新资产发布，以使其可供最终用户使用。 要了解如何发布资产， <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->
