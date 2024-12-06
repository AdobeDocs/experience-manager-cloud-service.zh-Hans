---
title: 从Content Hub下载资源
description: 了解如何从Content Hub门户下载资源
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 28424cb184d0378669498c78e571961227f6539a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 从Content Hub下载资源 {#download-assets}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![下载资源](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>Content Hub指南现在提供了PDF格式。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE Content Hub指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub允许您下载和共享资源。 Content Hub用户界面仅显示批准的资源。 这些资产可能包括图像、视频或任何其他数字内容。 Content Hub增强了可访问性和适应性，以实现有效的资源分发。

您可以使用Content Hub下载单个或多个资源及其可用演绎版。

## 下载资源及其演绎版 {#download-asset-renditions}

要下载资源及其演绎版，请执行以下步骤：

1. 单击资产可查看其属性。

1. 单击![下载](/help/assets/assets/download-icon.svg)开始下载过程。 “下载”面板列出了所有可用的资源演绎版（原始+其他演绎版）。

   >[!NOTE]
   >
   仅当使用[配置](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)用户界面启用呈现版本的可见性时，才会显示呈现版本。

1. 选择演绎版并单击&#x200B;**[!UICONTROL 下载]**。

   ![下载单个资源演绎版](/help/assets/assets/download-single-asset-renditions.png)


如果您正在下载许可资产，请选择&#x200B;**[!UICONTROL 我已阅读并接受上述条款和条件]**，然后单击&#x200B;**[!UICONTROL 下载]**。 您还可以单击&#x200B;**[!UICONTROL 条款和条件]**&#x200B;查看资产许可证。 仅当使用Assetsas a Cloud Service创作环境批准了资源时，才会显示许可证预览。 如需了解更多信息，请参阅[管理 Content Hub 上的已授予许可资源](/help/assets/manage-licensed-assets-on-content-hub.md)。

## 下载多个资产及其演绎版 {#download-multiple-assets-renditions}

要下载多个资源及其演绎版，请执行以下步骤：

1. 选择资源并单击![下载](/help/assets/assets/download-icon.svg) **[!UICONTROL 下载]**。 此时会显示[!UICONTROL 下载资源]屏幕，其中列出了所有选定的资源。
1. 单击&#x200B;**[!UICONTROL 下载]**&#x200B;从各种下载选项中进行选择，以开始下载：

   * **下载[!UICONTROL 原始资产]**：选择此选项可下载原始表单中的选定资产。
   * **仅下载[!UICONTROL 演绎版]**：选择此选项可下载除原始资源之外资源的所有可用演绎版。
   * **下载[!UICONTROL 原始和全部格式副本]**：选择此选项可下载所选资源的原始和格式副本。

     ![下载多个演绎版](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     仅当使用[配置](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)用户界面启用呈现版本的可见性时，才会显示呈现版本。

   如果任何选定资产是已许可资产，请单击左窗格中的资产许可证以查看其预览，该预览可让您选择&#x200B;**[!UICONTROL 我已阅读并接受上述条款和条件]**，然后单击&#x200B;**[!UICONTROL 下载]**。 仅当使用Assetsas a Cloud Service创作环境批准了资源时，才会显示许可证预览。 如需了解更多信息，请参阅[管理 Content Hub 上的已授予许可资源](/help/assets/manage-licensed-assets-on-content-hub.md)。

   ![download-multiple-license](/help/assets/assets/download-multiple-license.png)

<!--1. On the Content Hub homepage, select the asset and click **Download**. The **Download assets** dialog box displays a license or list of licenses associated with the selected assets in the left pane. 
1. Click a license in the left pane to see its PDF in the middle pane and the associated assets with it in the right pane. The license PDF preview is displayed only if the license is approved in your Assets as a Cloud Service environment. [Approve the license PDFs](/help/assets/approve-assets-content-hub.md) of the selected assets to see their previews.
1. Optional: Click ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the dialog box.
1. Select **I have read and accept all the terms and conditions mentioned above.** 
1. Click **Download** to download the selected assets.-->

<!---This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the preview of the associated assets to the license in the right. Reviewed licenses are highlighted in light blue.


The dialog box that displays depends on whether the download list includes expired assets or only non-expired assets. <br/>
**Download expired assets dialog box:** This dialog box displays the expired assets' preview along with their expiry date in the left pane. The expired assets' count out of total selected displays in the right pane. Click **Proceed with all assets** to download expired assets with other assets (if present). The Download assets dialog box displays. See the [Download assets dialog box](#Download-asset-dialog-box) to proceed further.
    
    >[!NOTE]
    >
    >[Enable the download option for expired assets](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) to download them. Only expired assets that have enabled downloading are available for download.

   <a id="Download-asset-dialog-box"></a> **Download assets dialog box:** This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the associated assets' preview and their count in the right pane. Reviewed licenses are highlighted in light blue.

    >[!NOTE]
    >
    > The **Download Asset dialog box** previews licensing terms and conditions only for approved licenses. [Approve the assets' licenses](/help/assets/approve-assets-content-hub.md) before downloading them to preview their licensing terms in the **Download Asset dialog box**.

1. Click  ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the download dialog box. 

1. Accept the terms and conditions and then click **Download** to download assets associated with the available licenses in the left pane.-->
<!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

<!---
### Download non-licensed Assets {#download-non-licensed-assets}

 To download non-licensed assets, select the assets and click ![download](/help/assets/assets/download-icon.svg) from the top rail.-->







