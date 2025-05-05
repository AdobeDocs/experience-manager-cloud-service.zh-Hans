---
title: 从Content Hub下载资源
description: 了解如何从Content Hub门户下载资源
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: e108d25f3cdc025e0fbe8010854f245f62786baf
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 10%

---

# 从Content Hub下载资源 {#download-assets}

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

<!-- ![Download assets](assets/download-asset.jpg) -->
![下载资源](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>Content Hub 指南现以 PDF 格式提供。下载完整指南并使用 Adobe Acrobat AI 助手来回答您的疑问。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub允许您下载和共享资源。 Content Hub用户界面仅显示批准的资源。 这些资产可能包括图像、视频或任何其他数字内容。 Content Hub增强了可访问性和适应性，以实现有效的资源分发。

您可以使用Content Hub下载单个或多个资源及其可用演绎版。

查看Content Hub[&#128279;](#types-of-renditions)中可用的类型的演绎版。

## 下载资源及其演绎版 {#download-asset-renditions}

要下载资源及其演绎版，请执行以下步骤：

1. 单击资产可查看其属性。

1. 单击![下载](/help/assets/assets/download-icon.svg)开始下载过程。 “下载”面板列出了所有可用的资源演绎版。

   >[!NOTE]
   >
   >* 仅当使用[配置](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)用户界面启用呈现版本的可见性时，才会显示呈现版本。
   >* 您可以在下载资源时下载所有[静态、动态和智能裁剪演绎版](#types-of-renditions)。

1. 选择一个或多个呈现版本并单击&#x200B;**[!UICONTROL 下载]**。

   ![下载单个资源演绎版](/help/assets/assets/download-single-asset-renditions.png)


如果您正在下载许可资产，请选择&#x200B;**[!UICONTROL 我已阅读并接受上述条款和条件]**，然后单击&#x200B;**[!UICONTROL 下载]**。 您还可以单击&#x200B;**[!UICONTROL 条款和条件]**&#x200B;查看资产许可证。 仅当使用Assets as a Cloud Service创作环境批准了资源时，才会显示许可证预览。 如需了解更多信息，请参阅[管理 Content Hub 上的已授予许可资源](/help/assets/manage-licensed-assets-on-content-hub.md)。

>[!NOTE]
>
> 有权访问[具有开放API功能的Dynamic Media ](/help/assets/dynamic-media-open-apis-overview.md)的用户可以查看和下载动态和智能裁剪演绎版。

## 下载多个资产及其演绎版 {#download-multiple-assets-renditions}

要下载多个资源及其演绎版，请执行以下步骤：

1. 选择资源并单击![下载](/help/assets/assets/download-icon.svg) **[!UICONTROL 下载]**。 此时会显示[!UICONTROL 下载资源]屏幕，其中列出了所有选定的资源。
1. 单击&#x200B;**[!UICONTROL 下载]**&#x200B;从各种下载选项中进行选择，以开始下载：

   * **下载[!UICONTROL 原始资产]**：选择此选项可下载原始表单中的选定资产。
   * **仅下载[!UICONTROL 静态演绎版]**：选择此选项可下载除原始资源之外的所有可用资源静态演绎版。
   * **下载[!UICONTROL 原始和静态演绎版]**：选择此选项可下载所选资源的原始和静态演绎版。

     ![下载多个演绎版](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     >* 仅当使用[配置](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)用户界面启用呈现版本的可见性时，才会显示呈现版本。
     >* 下载多个资源时，只能下载[静态呈现版本](#types-of-renditions)。

   如果任何选定资产是已许可资产，请单击左窗格中的资产许可证以查看其预览，该预览可让您选择&#x200B;**[!UICONTROL 我已阅读并接受上述条款和条件]**，然后单击&#x200B;**[!UICONTROL 下载]**。 仅当使用Assets as a Cloud Service创作环境批准了资源时，才会显示许可证预览。 如需了解更多信息，请参阅[管理 Content Hub 上的已授予许可资源](/help/assets/manage-licensed-assets-on-content-hub.md)。

   <!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

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


## 演绎版类型 {#types-of-renditions}

资源演绎版是资源原始文件的不同表示形式。 这些内容可以包括缩略图、针对Web或移动设备的优化版本、加水印或受DRM保护的文件，甚至包括智能裁剪等动态元素。 它们不需要匹配原始文件类型，而是在各种用例中用于表示资源。

了解有关[在Experience Manager Assets](/help/assets/renditions.md)中查看和管理演绎版的更多信息。

[!DNL Experience Manager Assets]支持以下类型的演绎版：

* [静态演绎版](/help/assets/renditions.md#static-renditions)：静态演绎版是数字资源的预创建版本，通常在资源摄取或修改期间生成。 它们针对特定用途和平台进行了优化，例如Web缩略图、适用于响应式设计的移动友好格式，或适用于打印的高分辨率文件，从而提供简化且一致的体验。

* [动态演绎版](/help/assets/renditions.md#dynamic-renditions)：动态演绎版是资产的实时、自定义版本，可执行各种操作，例如根据不同的设备分辨率调整图像大小或裁剪以适合各种长宽比。 这些演绎版允许您提供个性化和优化的体验，以满足更广泛的需求。 已在[!DNL Adobe Experience Manager Assets]创作环境中创建资源的动态演绎版。 有关启用动态呈现所需的步骤的信息，请参阅[启用动态呈现](#enable-dynamic-media-renditions)。

* [智能裁切](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)：智能裁切在裁切过程中仅专注于资源的重要部分。 适用于的Dynamic Media智能裁剪利用由Adobe Sensei提供的人工智能来跟踪目标点，确保我们的资源在所有屏幕大小上都具有最佳外观。 [!DNL Adobe Experience Manager]智能裁剪显示资源演绎版的宽度和高度以及标题。 请参阅[在AEM Assets Dynamic Media中使用智能裁剪](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)以了解详情。

  智能裁剪呈现版本会显示，并且仅在您有权访问具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)时才可供下载。 智能裁剪演绎版仅适用于图像资源。

  ![节目类型](/help/assets/assets/renditions-types.png)

### 启用动态呈现版本 {#enable-dynamic-media-renditions}

要启用动态呈现版本，请执行以下操作：

1. 确保您有权访问具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)。

   一旦您有权访问具有OpenAPI功能的Dynamic Media，则所有标记为`Approved`的资源都可用于Dynamic Media的公开交付。

1. 将资源的[审批目标](/help/assets/approve-assets-content-hub.md#set-approval-target)设置为Content Hub以仅审批Content Hub的资源。

1. 启用[配置](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub)用户界面的&#x200B;**[!UICONTROL 呈现版本]**&#x200B;选项卡中提供的&#x200B;**[!UICONTROL 启用呈现版本可用性]**&#x200B;切换开关。

1. 重新保存现有的图像预设，以使其在Content Hub上可用。 它仅适用于通过OpenAPI新载入到Dynamic Media的情况。

   要重新保存现有的图像预设，请导航到“管理员”视图，然后选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 图像预设]**。 选择预设，单击&#x200B;**[!UICONTROL 编辑]**，然后单击&#x200B;**[!UICONTROL 保存]**。



   >[!NOTE]
   > 
   > 动态演绎版仅适用于图像资源。



