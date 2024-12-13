---
title: 在Assets视图中批量编辑元数据
description: 了解如何在Assets视图中同时编辑多个可用资源的元数据。
source-git-commit: 5778d0dac141174c1b950625057f920af0301a8b
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 在Assets视图中批量编辑元数据{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

通过使用Assets视图UI中的&#x200B;**批量元数据编辑**，您可以同时修改多个资源文件的元数据。 您无需单独编辑每个资源的元数据，而是一次将更改应用于大量资源。 此功能提高了跨大量资产集的元数据属性的效率、一致性和准确性，从而提高资产的可搜索性和组织性。

## 批量编辑资源元数据 {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

执行以下步骤可一次批量编辑多个资源的元数据：

1. 在Assets视图中，单击&#x200B;**Assets**。
1. 浏览资源或在搜索栏中输入相关关键字以查找特定资源。
1. 选择多个资源并单击顶部菜单中的&#x200B;**批量元数据编辑**。
   ![bulk-metadata-edit](/help/assets/assets/bulk-metadata-edit.png)
1. 在“编辑元数据”页上，编辑&#x200B;**属性**&#x200B;面板中的以下字段：
   * **状态：**&#x200B;选择一个状态以定义所选资源的可用性。
   * **到期日期：**&#x200B;设置一个日期，在此日期之后资源不再有效或不再需要。
   * **作者：**&#x200B;指定作者的姓名。
   * **关键字：**添加提供有关资产的高级信息的术语或文本字符串以增强其可发现性。 添加关键字，然后按Enter键或返回键将另一个关键字添加到列表中。
     <!-- * **Tags:** Click ![tags icon](/help/assets/assets/tags-icon.svg) to select tags from the available options. Tags provide more specific information about the assets and enhances their discoverability. Tags already applied to the selected assets are only displayed in the **Properties** panel. If you cannot find the relevant tags, create the tags and assign them to the selected assets. See [Manage tags in Assets view](/help/assets/tagging-management-assets-view.md) for details.-->
   * 单击&#x200B;**保存**&#x200B;可附加关键字，<!-- Tags while-->将覆盖状态、过期日期和作者的现有详细信息。
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties1.png)

     >[!NOTE]
     >
     >您可以一次编辑100个资源的元数据。

要查看对资源应用的元数据更改，请导航到资源详细信息页面（选择资源，然后单击&#x200B;**详细信息**），然后单击![](/help/assets/assets/info-icon-solid-black.svg)，在&#x200B;**信息**&#x200B;面板中查看资源的元数据。

>[!NOTE]
>
>状态、过期日期、作者和关键字<!-- and Tags-->是可用于批量编辑元数据的标准元数据属性，而不考虑文件夹特定的元数据。 仅当这些元数据属性包含在应用于资源文件夹的元数据表单中时，它们才会显示在资源详细信息页面上。  如果在资源详细信息页面上看不到这些元数据属性，请编辑资源文件夹的元数据表单以包含它们。 请参阅Assets视图中的[元数据](/help/assets/metadata-assets-view.md)，了解如何创建或编辑元数据表单并将其应用到文件夹。


