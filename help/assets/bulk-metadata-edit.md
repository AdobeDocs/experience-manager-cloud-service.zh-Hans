---
title: 在资产视图中批量元数据编辑
description: 了解如何在Assets视图中同时更新多个可用资源的预定义标准元数据字段集。
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 5%

---

# 在资产视图中批量元数据编辑{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

Assets视图中的&#x200B;**批量元数据编辑**&#x200B;功能允许用户同时为多个资源文件编辑预定义的标准元数据字段集。 选择多个资源并一次批量更新其预定义的标准元数据集，而不是为每个资源单独更新这些标准元数据。 此功能提高了标准元数据属性在大量资产中的效率、一致性和准确性，从而提高资产的可搜索性和组织性。

## 批量编辑资源元数据 {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

执行以下步骤可一次批量编辑多个资源的元数据：

1. 在Assets视图中，单击&#x200B;**Assets**。
1. 浏览特定资源或使用搜索栏中的关键词搜索它们。
1. 选择资源并单击顶部菜单中的&#x200B;**批量元数据编辑**。
   ![bulk-metadata-edit](/help/assets/assets/bulk-metadata-edit1.png)
1. 在“编辑元数据”页上，编辑&#x200B;**属性**&#x200B;面板中的以下字段：
   * **状态：**&#x200B;为所选资源选择状态。
   * **到期日期：**&#x200B;设置一个日期，在此日期之后资源不再有效或不再需要。
   * **作者：**&#x200B;指定作者的姓名。
   * **关键字：**&#x200B;添加提供有关资源的高层信息的特定术语或文本字符串，以增强资源的可发现性。 添加关键字，然后按Enter键或返回键将另一个关键字添加到列表中。
   * **标记：**&#x200B;单击![标记图标](/help/assets/assets/tags-icon.svg)从可用选项中选择标记。 标记提供了有关资产的更具体信息并增强了它们的可发现性。 已应用于所选资源的标记会显示在&#x200B;**属性**&#x200B;面板中。 如果找不到相关标记，请创建这些标记并将其分配给选定的资源。 有关创建标记并将其分配给资源的详细信息，请参阅[在Assets视图中管理标记](/help/assets/tagging-management-assets-view.md)。
   * 单击&#x200B;**保存**以将上述元数据更新应用于所选资源。 保存后，将附加关键字和标记，而状态、过期日期和作者的更新详细信息将覆盖其现有详细信息。
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >您可以一次编辑100个资源的元数据。

要查看对某个资源应用的元数据更新，请导航到资源详细信息页面（选择资源，然后单击&#x200B;**详细信息**），然后单击![](/help/assets/assets/info-icon-solid-black.svg)，在&#x200B;**信息**&#x200B;面板中查看该资源的元数据。

>[!NOTE]
>
>**状态**、**到期日期**、**作者**、**关键字**&#x200B;和&#x200B;**标记**&#x200B;是可用于批量元数据编辑的标准元数据属性，而不考虑文件夹特定的元数据。 仅当这些元数据属性包含在应用于资源文件夹的元数据表单中时，它们才会显示在资源详细信息页面上。 如果在资源详细信息页面上找不到这些标准元数据属性，请编辑资源文件夹的元数据表单以包含它们。 请参阅Assets视图中的[元数据](/help/assets/metadata-assets-view.md)，了解如何创建或编辑元数据表单并将其应用到文件夹。
