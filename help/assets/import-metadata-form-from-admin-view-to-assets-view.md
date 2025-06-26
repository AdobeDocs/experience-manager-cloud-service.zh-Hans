---
title: 将 [!DNL Admin View] 元数据表单导入 [!DNL Assets View]
description: 本文介绍如何导入 [!DNL Admin View] 到 [!DNL Assets View]中可用的元数据表单
contentOwner: AG
feature: Metadata
role: User, Admin
source-git-commit: 1ee93bee379ba48a9b42b13b5d11ff89f705b298
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 8%

---


# 将[!DNL Admin View]元数据表单导入[!DNL Assets View] {#import-admin-view-metadata-forms-to-assets-view}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 和 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 与 Edge Delivery Services 集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用 Dynamic Media Prime 和 Ultimate</b></a>
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

[!DNL Adobe Experience Manager Assets]允许您将元数据表单及其文件夹关联从[!DNL Admin View]导入到[!DNL Assets View]。

## 开始之前{#prerequisites-for-importing-metadata-forms-to-assets-view}

确保您具有管理员权限，可以将元数据表单及其文件夹关联从[!DNL Admin View]导入到[!DNL Assets View]。

## 将元数据表单导入[!DNL Assets View]{#import-metadata-forms-to-assets-view}

作为管理员，执行以下步骤以将[!DNL Admin View]中可用的元数据表单导入[!DNL Assets View]：

1. 导航到[!DNL Assets View]主页，然后单击&#x200B;**[!UICONTROL 设置]**&#x200B;下的&#x200B;**[!UICONTROL 元数据Forms]**&#x200B;以打开&#x200B;**[!UICONTROL 元数据Forms]**&#x200B;页面，该页面显示[!DNL Assets View]中可用的元数据表单列表。
   ![元数据表单页面](/help/assets/assets/metadata-forms-page.png)
1. 选择&#x200B;**[!UICONTROL 导入]**，此时将显示一条正在处理的消息(例如，*正在处理2个元数据表单……请稍候。*)。 处理完成后，将显示&#x200B;**[!UICONTROL 导入元数据表单]**&#x200B;表，其中包括[!DNL Admin View]中可用的元数据表单列表。 该表行包括：元数据表单名称（**[!UICONTROL 名称]**&#x200B;下）、与该表单关联的文件夹（**[!UICONTROL 文件夹关联]**&#x200B;下）以及在导入表单之前预览![该表单的选项](/help/assets/assets/Preview.svg)。
   ![导入元数据Forms页面](/help/assets/assets/import-metadata-forms-page.png)

   >[!NOTE]
   > 
   > 在&#x200B;**[!UICONTROL 导入元数据Forms]**&#x200B;中，表单名称旁边的&#x200B;**[!UICONTROL 重复]**&#x200B;标签显示该表单已应用于[!DNL Assets View]中的文件夹。 导入该重复表单会覆盖应用于文件夹的现有表单。 要避免此覆盖，请在导入表单之前重命名表单。 单击表单名称可对其进行重命名。
1. 单击文件夹名称（位于[!UICONTROL 文件夹关联]下）旁边的![选择文件夹](/help/assets/assets/x.svg)以删除与表单的文件夹关联。
1. 单击![选择文件夹](/help/assets/assets/add-to-folder.svg)以选择一个文件夹，为其分配相应的元数据表单。
1. 单击红色圆圈可查看有关不支持的元数据组件或表单中从导入中排除的映射的详细信息。
   ![导入元数据Forms页面](/help/assets/assets/unsupported-import-elements.png)
1. 选择表中的一个或多个表单，然后单击&#x200B;**[!UICONTROL 开始导入]**&#x200B;以将元数据表单及其关联的文件夹导入[!DNL Assets View]。 显示处理消息(例如，*正在导入3个元数据表单。 请稍候！*)。 导入完成后，将显示一条成功消息，确认表单已成功导入，并且&#x200B;**[!UICONTROL 元数据Forms]**&#x200B;页面（共[!DNL Assets View]页）会显示最近导入的表单以及[!DNL Assets View]中可用的现有表单。 您可以在此页面上执行以下操作：
   * 单击列标题可按[!UICONTROL 名称]、[!UICONTROL 修改时间]或[!UICONTROL 作者]对表进行排序。
   * 选择导入的表单并单击&#x200B;**[!UICONTROL 从文件夹删除]**，然后验证文件夹路径中的文件夹名称以确认文件夹已正确移植。
     ![验证元数据表单页面](/help/assets/assets/confirm-ported-folder.png)
   * 选择导入的表单，然后单击&#x200B;**[!UICONTROL 编辑]**&#x200B;查看元数据表单的所有受支持配置。 有关元数据表单、其组件和字段的更多信息，请参阅[设置元数据Forms](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/metadata#metadata-forms)。
     ![验证元数据表单页面](/help/assets/assets/verify-metadata-forms-page.png)

## 验证导入的元数据表单{#Verify-the-imported-metadata-forms}

将元数据表单从[!DNL Admin View]导入到[!DNL Assets View]后，请按照以下步骤验证导入：

1. 导航到导入的元数据表单的任何关联文件夹。
1. 导航到[资源的详细信息页面](/help/assets/navigate-assets-view.md#preview-assets)，并验证支持的元数据组件、组件字段和字段值是否已从[!DNL Admin View]同步。 有关元数据组件、组件字段和字段值的更多信息，请参阅Assets Essentials中的[元数据](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/metadata)文章。

   >[!NOTE]
   >
   > 在[[!DNL Assets View] 详细信息页面](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/metadata-assets-view#metadata-forms)或[[!DNL Admin View] 属性页面](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/administer/metadata-schemas)中，对元数据属性值的更改将在两个界面之间自动同步。 但是，表单中的结构更改（如添加或删除字段或其他修改）不会同步。