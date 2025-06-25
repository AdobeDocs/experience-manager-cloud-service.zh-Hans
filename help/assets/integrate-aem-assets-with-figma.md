---
title: 将 [!DNL AEM Assets] 与 [!DNL Figma]集成。
description: 了解如何将 [!DNL AEM Assets] 与 [!DNL Figma] 集成，以在 [!DNL Figma] 设计工作流程中访问和使用您组织的资产。
hide: false
role: User
exl-id: 530561ca-497b-4331-a014-72c561e1ca84
source-git-commit: 41fc6cc1c852c25215a804c2d1f9c5872a46e0a4
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 10%

---

# 将[!DNL AEM Assets]与[!DNL Figma]集成{#integrate-aem-assets-with-figma}

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

[!DNL AEM Assets]与[!DNL Figma]本机集成，这允许设计人员从[!DNL Figma]用户界面中直接访问[!DNL AEM Assets]中存储的资产。 您可以将在[!DNL AEM Assets]中管理的内容放在[!DNL Figma]画布中，然后在[!DNL AEM Assets]存储库中保存新内容或编辑的内容。

## 开始之前{#prerequisites-for-aem-assets-and-figma-integration}

* 所需的最低AEM版本为`19149`。

* 您必须具有有效的[!DNL AEM Assets]和[!DNL Figma]许可证才能将[!DNL AEM Assets]与[!DNL Figma]集成。

## 访问[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]{#access-aem-assets-connector}

执行以下步骤以访问[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]：

1. 在[!DNL Figma]主页上，单击画布底部工具栏中的&#x200B;**[!UICONTROL 操作]**，然后在对话框中提供的搜索栏中搜索[!DNL Adobe Experience Manager (AEM) Assets Connector]。
1. 选择[!DNL Adobe Experience Manager (AEM) Assets Connector]以显示[!DNL Adobe Experience Manager (AEM) Assets Connector]面板。 使用此面板[将 [!DNL AEM] 资源导入 [!DNL Figma] 画布](#import-aem-assets-into-figma-workflow)。
   ![操作](/help/assets/assets/actions-on-figma.png)
或者，访问[!DNL Figma]社区上可用的[[!DNL Adobe Experience Manager (AEM) Assets Connector]](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector)，单击&#x200B;**[!UICONTROL 打开方式……]**，选择最近的文件或创建新文件并单击&#x200B;**[!UICONTROL 运行]**&#x200B;以访问[!DNL Adobe Experience Manager (AEM) Assets Connector]面板。
   ![plugin-page-on-figma-community](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> 如果您在登录到[!DNL AEM]环境后看到&#x200B;**[!UICONTROL 网络错误]**&#x200B;消息，请[联系Adobe支持](https://helpx.adobe.com/contact.html)以获取帮助。

## 将[!DNL AEM]资源导入[!DNL Figma]画布{#import-aem-assets-into-figma-workflow}

在您的[!DNL Figma]设计界面中[访问[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]面板](#access-aem-assets-connector)，并执行以下操作：

1. 在[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]面板中搜索资源。 有关详细信息，请参阅[使用资产选择器](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector)。

1. 将资源拖放到画布上，或者选择资源并单击&#x200B;**[!UICONTROL 选择]**&#x200B;以将资源放到画布上。

1. 单击文件夹路径中的![三个点](/help/assets/assets/three-dots.svg)以显示当前层次结构中的所有父文件夹和子文件夹。 选择要导航到该位置的文件夹。
   ![三个点](/help/assets/assets/assets-folder-structure.png)

Figma设计就绪后，您可以[将资源导出到AEM Assets存储库](#export-figma-design-to-aem-assets-folder)。

## 将资源导出到[!DNL AEM Assets]存储库{#export-figma-design-to-aem-assets-folder}

在[!DNL Figma]设计界面中[访问[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]面板](#access-aem-assets-connector)，然后执行以下步骤以将设计导出到[!DNL AEM Assets]存储库：

1. 导航到要保存[!DNL Figma]设计的目标文件夹。 如果您已在文件夹中，请单击文件夹路径中的“更多”选项（![三个圆点](/help/assets/assets/three-dots.svg)）以选择其他目标文件夹。
1. 可选：将画布上的资产分组，以作为单个单元将其选择并上传到您的文件夹中。
1. 单击![文件上传](/help/assets/assets/upload-icon.svg) **[!UICONTROL 上传]**&#x200B;以显示&#x200B;**[!UICONTROL 上传资产]**&#x200B;对话框。
1. 在该对话框中，指定文件名，选择文件格式，选择&#x200B;**[!UICONTROL 选定项]**&#x200B;或&#x200B;**[!UICONTROL 页面]**，然后单击&#x200B;**[!UICONTROL 上传]**&#x200B;以将选定资源或整个设计上传到目标文件夹。
   ![上载图形设计](/help/assets/assets/upload-figma-design.png)

## 要注意的重要事项{#Limitations-of-using-aem-assets-into-figma}

此集成当前具有以下限制：

* 要将[!DNL AEM]资源导入Figma，支持的格式为&#x200B;**JPEG**、**PNG**。
* 要将设计从[!DNL Figma]导出到[!DNL AEM Assets]，支持的格式为&#x200B;**PNG**、**PDF**、**JPG**、**SVG**。

