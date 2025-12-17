---
title: 将 [!DNL AEM Assets] 与 [!DNL Figma]集成。
description: 了解如何将 [!DNL AEM Assets] 与 [!DNL Figma] 集成，以在 [!DNL Figma] 设计工作流程中访问和使用您组织的资产。
hide: false
role: User
exl-id: 530561ca-497b-4331-a014-72c561e1ca84
source-git-commit: a9c1f5472092b3b9fa7a5e5570feb92f32e9ef6c
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 1%

---


# 将[!DNL AEM Assets]与[!DNL Figma]集成{#integrate-aem-assets-with-figma}

[!DNL AEM Assets]与[!DNL Figma]本机集成，这允许设计人员从[!DNL AEM Assets]用户界面中直接访问[!DNL Figma]中存储的资产。 您可以将在[!DNL AEM Assets]中管理的内容放在[!DNL Figma]画布中，然后在[!DNL AEM Assets]存储库中保存新内容或编辑的内容。

## 开始之前{#prerequisites-for-aem-assets-and-figma-integration}

* 所需的最低AEM版本为`19149`。

* 您必须具有有效的[!DNL AEM Assets]和[!DNL Figma]许可证才能将[!DNL AEM Assets]与[!DNL Figma]集成。

## 支持的文件格式 {#supported-file-formats-integration-figma}


* 要将[!DNL AEM]资源导入Figma，支持的格式包括图像资源(JPEG、PNG)、视频文件(MP4、MOV、WebM)、动画文件(GIF)和矢量文件(SVG)。
* 要将设计从[!DNL Figma]导出到[!DNL AEM Assets]，支持的格式为&#x200B;**PNG**、**PDF**、**JPG**、**SVG**。

## 访问[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]{#access-aem-assets-connector}

执行以下步骤以访问[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]：

1. 在[!DNL Figma]主页上，单击画布底部工具栏中的&#x200B;**[!UICONTROL 操作]**，然后在对话框中提供的搜索栏中搜索[!DNL Adobe Experience Manager (AEM) Assets Connector]。
1. 选择[!DNL Adobe Experience Manager (AEM) Assets Connector]以显示[!DNL Adobe Experience Manager (AEM) Assets Connector]面板。 使用此面板[将 [!DNL AEM] 资源导入 [!DNL Figma] 画布](#import-aem-assets-into-figma-workflow)。
   ![操作](/help/assets/assets/actions-on-figma.png)
或者，访问[[!DNL Adobe Experience Manager (AEM) Assets Connector]社区上可用的](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector) [!DNL Figma]，单击&#x200B;**[!UICONTROL 打开方式……]**，选择最近的文件或创建新文件并单击&#x200B;**[!UICONTROL 运行]**&#x200B;以访问[!DNL Adobe Experience Manager (AEM) Assets Connector]面板。
   ![plugin-page-on-figma-community](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> 如果您在登录到[环境后看到](https://helpx.adobe.com/contact.html)网络错误&#x200B;**[!UICONTROL 消息，请]**&#x200B;联系Adobe支持[!DNL AEM]以获取帮助。

## 将[!DNL AEM]资源导入[!DNL Figma]画布{#import-aem-assets-into-figma-workflow}

在您的[设计界面中[!UICONTROL 访问]Adobe Experience Manager (AEM) Assets Connector](#access-aem-assets-connector)面板[!DNL Figma]，并执行以下操作：

1. 在[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]面板中搜索资源。 有关详细信息，请参阅[使用资产选择器](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector)。

1. 将资源拖放到画布上，或者选择资源并单击&#x200B;**[!UICONTROL 选择]**&#x200B;以将资源放到画布上。

1. 单击文件夹路径中的![三个点](/help/assets/assets/three-dots.svg)以显示当前层次结构中的所有父文件夹和子文件夹。 选择要导航到该位置的文件夹。
   ![三个点](/help/assets/assets/figma-v2-plugin.png)

1. [可选]单击&#x200B;**[!UICONTROL 检查更新]**。 当前Figma文档中使用的资源会与AEM中存在的资源进行比较。 任何更新都将在单独的窗口中列出。 单击&#x200B;**[!UICONTROL 更新]**&#x200B;以将更新后的资源从AEM导入您的Figma文档。

Figma设计就绪后，您可以[将资源导出到AEM Assets存储库](#export-figma-design-to-aem-assets-folder)。

## 将资源导出到[!DNL AEM Assets]存储库{#export-figma-design-to-aem-assets-folder}

在[设计界面中[!UICONTROL 访问]Adobe Experience Manager (AEM) Assets Connector](#access-aem-assets-connector)面板[!DNL Figma]，然后执行以下步骤以将设计导出到[!DNL AEM Assets]存储库：

1. 导航到要保存[!DNL Figma]设计的目标文件夹。 如果您已在文件夹中，请单击文件夹路径中的“更多”选项（![三个圆点](/help/assets/assets/three-dots.svg)）以选择其他目标文件夹。
1. 可选：将画布上的资产分组，以作为单个单元将其选择并上传到您的文件夹中。
1. 单击![文件上传](/help/assets/assets/upload-icon.svg) **[!UICONTROL 上传]**&#x200B;以显示&#x200B;**[!UICONTROL 上传资产]**&#x200B;对话框。
1. 在该对话框中，选择&#x200B;**[!UICONTROL 选定项]**&#x200B;或&#x200B;**[!UICONTROL 页面]**，指定文件或页面名称，定义导出配置并单击&#x200B;**[!UICONTROL 上传]**&#x200B;以将选定资源或整个设计上传到目标文件夹。

   导出配置包括文件格式、规模和质量。 例如，如果选择JPG作为文件格式，则还可以定义图像比例和质量。 同样，如果选择PNG作为文件格式，也可以定义图像比例。
   ![上载图形设计](/help/assets/assets/upload-figma-design.png)
