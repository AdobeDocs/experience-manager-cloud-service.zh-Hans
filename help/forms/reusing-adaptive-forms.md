---
title: 重用自适应表单的元数据属性
seo-title: Reuse metadata properties of an Adaptive Form
description: 您可以重用现有的自适应表单来创建新的自适应Forms。
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: ca0c9f102488c38dbe8c969b54be7404748cbc00
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---

# 重用自适应表单的元数据属性 {#reusing-adaptive-forms}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/creating-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/reusing-adaptive-forms.html) |
| AEM as a Cloud Service | 本文 |

如果要使用现有自适应表单的某些属性来生成新表单，则只需使用复制粘贴功能即可。 此外，您还可以将新的自适应表单粘贴到所需的文件夹路径。 将复制所有元数据属性，并复制基于XFA和XSD的自适应Forms的XFA和XSD。

>[!NOTE]
>
>不会复制状态和审阅详细信息。 例如，如果自适应表单已发布，然后复制，则粘贴的自适应表单处于未发布状态。 同样，如果复制的资产正在审核中，则粘贴的资产不在同一审核中。

## 复制自适应表单 {#copy-an-adaptive-form}

使用以下任一方法复制自适应表单：

1. 单击复制 ![aem6forms_copy](assets/aem6forms_copy.png) 图标。

   >[!NOTE]
   >
   >快速操作是在鼠标悬停时显示在缩略图上的操作项。

1. 选择自适应表单。 对于不同的视图，选择过程各不相同。

   如果您在卡片视图中，请单击选定内容以转到选定模式 ![aem6forms_check-circle](assets/aem6forms_check-circle.png) 图标，然后单击要复制的所有自适应Forms。

   如果您在列表视图中，请单击所有自适应Forms的复选框以选择它们。

   >[!NOTE]
   >
   >所有选定的资源都必须是自适应Forms，因为仅自适应Forms支持复制粘贴功能，并且所有选定的资源都必须存在于同一文件夹中。

   选择资源后，单击副本 ![aem6forms_copy](assets/aem6forms_copy.png) 工具栏中显示的图标以复制选定的自适应表单。

## 粘贴自适应表单 {#paste-an-adaptive-form}

单击复制操作将自动退出选择模式并进行粘贴 ![粘贴](assets/Smock_Paste_18_N.svg) 图标可见。 现在，转到所需的文件夹路径并单击粘贴 ![粘贴](assets/Smock_Paste_18_N.svg) 图标以粘贴复制的自适应表单。

如果在同一文件夹中粘贴或此目标文件夹中存在另一个具有相同节点名称（存储在CRX存储库中）的文件，则会在后缀后附加1(例如，myaf将变为myaf1，如果myaf1存在于同一位置，则myaf将变为myaf2。 所有其他属性与原始自适应表单相同。

单击粘贴后 ![粘贴](assets/Smock_Paste_18_N.svg) 图标，则它会再次隐藏。 同时，您只能粘贴一次。 要再次创建同一资产的副本，请再次复制该副本。

## 更改新自适应表单的内容 {#change-contents-of-new-adaptive-form}

可以使用以下方法更改粘贴的自适应Forms的内容，以使其与复制的表单不同：

1. **更改元数据属性：**

   您可以更改自适应表单的元数据属性，例如标题和描述。 有关元数据属性及其更改方式的更多详细信息，请参阅 [管理表单元数据](manage-form-metadata.md)

1. **更改基于XFA/XSD的自适应Forms的XFA/XSD：**

   您可以更改自适应Forms中使用的XFA/XSD。 要了解如何更改这些自适应Forms，请参阅 [管理表单元数据](manage-form-metadata.md)

1. **重新发布:**

   粘贴的资产与复制的资产不同。 您可以将其发布为新资源，以供最终用户使用。 要了解如何发布资产， <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->
