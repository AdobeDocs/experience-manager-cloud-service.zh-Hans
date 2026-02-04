---
title: 从Content Hub下载资源
description: 了解如何从Content Hub门户下载一个或多个资源及其演绎版。
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 655f84593adb1199bcfc21cb54071feb3c8523c5
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 1%

---

# 从Content Hub下载资源 {#download-assets}

[!DNL Content Hub]允许您下载并共享您的资产。 [!DNL Content Hub]用户界面仅显示批准的资源。 这些资产可能包括图像、视频或任何其他数字内容。 [!DNL Content Hub]增强了有效资产分配的可访问性和适应性。

>[!VIDEO](https://video.tv.adobe.com/v/3433135/?learn=on){transcript=true}

您可以使用[!DNL Content Hub]下载单个或多个资源及其可用演绎版。

查看Content Hub[中可用的](#types-of-renditions)类型的节目。

## 下载一个或多个资源及其演绎版 {#download-asset-renditions}

要下载一个或多个资源及其演绎版，请执行以下步骤：

* 要下载单个资源及其演绎版，请执行以下操作：
   1. 选择资产卡上可用的![下载](/help/assets/assets/download-icon.svg)以预览资产及其可用演绎版。
   1. 选择可用的格式副本，然后单击对话框中的&#x200B;**[!UICONTROL 下载]**&#x200B;选项以将所选格式副本下载为ZIP文件。 如果对话框显示资产许可证（用于许可资产），请接受许可条款和条件，然后单击&#x200B;**[!UICONTROL 下载]**。
      ![下载资源](/help/assets/assets/download-an-asset-CH-from-asset-card.png)
或者，单击资产缩略图，然后单击![下载](/help/assets/assets/download-icon.svg)以选择并查看对话框上的可用演绎版，然后再下载。

* 要下载多个资产及其演绎版，请执行以下操作：
   1. 选择资源，单击![下载](/help/assets/assets/download-icon.svg) **[!UICONTROL 下载]**，然后在&#x200B;**[!UICONTROL 下载资源]**&#x200B;对话框中查看选定资源的列表。 单击资产旁边的![取消选择](/help/assets/assets/Close.svg)以将其从列表中取消选择。
   1. 选择一个或多个演绎版以将它们下载为ZIP文件。 选择&#x200B;**[!UICONTROL 智能裁切]**&#x200B;和&#x200B;**[!UICONTROL 静态演绎版]**&#x200B;可下载每个所选资源的所有可用静态演绎版和智能裁切演绎版。
   1. 可选：取消选择&#x200B;**[!UICONTROL 为每个资源创建单独的文件夹]**，以将所选资源及其演绎版下载为zip文件中文件夹内的平面层次结构。 默认情况下，[!DNL Content Hub]会将所选资源及其演绎版下载到zip文件中的单独文件夹中。

      >[!NOTE]
      >
      > * Content Hub会将您的选择保存为首选项（**[!UICONTROL 为每个资源创建一个单独的文件夹]**），并保留它以供将来下载。
      > * **[!UICONTROL 为每个资产创建单独的文件夹]**&#x200B;选项仅适用于经过身份验证的[!DNL Content Hub]用户。 [!DNL Content Hub]允许公共用户将资源下载为单个资源。

   1. 单击&#x200B;**[!UICONTROL 下载]**&#x200B;可下载所选资源及其演绎版。
      ![下载多个资源](/help/assets/assets/bulk-asset-download-content-hub.png)

在下载过程中，您可以继续使用[!DNL Content Hub]。 在下载过程中，Content Hub不会中断您的工作流。
![下载多个资源](/help/assets/assets/download-assets-notification-ch.png)
如果&#x200B;**[!UICONTROL 下载资源]**&#x200B;对话框显示资源许可证，然后从左侧窗格（[!UICONTROL T&amp;C文档]部分）中选择每个许可证以预览该许可证并在对话框的中间窗格中显示与该许可证关联的选定资源。 查看每个许可证后，选择演绎版，单击&#x200B;**[!UICONTROL 我已阅读并接受上述条款和条件]**，然后选择&#x200B;**[!UICONTROL 下载]**&#x200B;以下载它们。
![下载多个资源](/help/assets/assets/download-multiple-licensed-assets-CH.png)

>[!NOTE]
>
>* 仅当使用[[!UICONTROL 配置]](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)用户界面启用呈现版本的可见性时，才会显示呈现版本。
>* 有权访问[[!DNL Dynamic Media with Open API capabilities]](/help/assets/dynamic-media-open-apis-overview.md)的用户可以查看和下载动态和智能裁剪演绎版。
>* 仅当使用[!DNL Assets as a Cloud Service]创作环境批准资产时，才会显示许可证预览。 如需了解更多信息，请参阅[管理 Content Hub 上的已授予许可资源](/help/assets/manage-licensed-assets-on-content-hub.md)。

<!--

## Download an asset and its renditions {#download-asset-renditions} 

To download an asset and its renditions, execute the following steps: 

1. Click the asset to view its properties.

1. Click ![download](/help/assets/assets/download-icon.svg) to see the list of available asset renditions in the **[!UICONTROL Download]** panel.

   >[!NOTE]
   >
   >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
   >* You can download all [static, dynamic, and smart crop renditions](#types-of-renditions) while downloading an asset.

1. Select one or more renditions and click **[!UICONTROL Download]** to download the selected renditions as a zip file. 
While downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** before clicking **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   ![Download single asset renditions](/help/assets/assets/download-single-asset-renditions.png)


If you are downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
> The users with access to [Dynamic Media with Open API capabilities](/help/assets/dynamic-media-open-apis-overview.md) can view and download dynamic and smart crop renditions.

## Download multiple assets and their renditions {#download-multiple-assets-renditions} 

To download multiple assets and their renditions, execute the following steps: 

1. Select the assets and click ![download](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]**. The [!UICONTROL Download assets] screen displays listing all the selected assets. 
1. Click **[!UICONTROL Download]** to select from the various download options to begin download:

    * **Download [!UICONTROL Originals]**: Select this option to download the selected assets in the original form.
    * **Download [!UICONTROL Static Renditions only]**: Select this option to download all available static renditions of assets except the original assets.
    * **Download [!UICONTROL Originals & Static Renditions]**: Select this option to download both original and static renditions of the selected assets. 

      ![Download multiple renditions](/help/assets/assets/download-multiple-renditions.png)

      >[!NOTE]
      >
      >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
      >* You can only download [static renditions](#types-of-renditions) while downloading multiple assets.

    If any of the selected asset is a licensed asset, click the license of the asset in left pane to see its preview, which enables you to select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

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

资源演绎版是资源原始文件的不同表示形式。 这些呈现版本可以包括缩略图、针对Web或移动设备的优化版本、加水印或受DRM保护的文件，甚至包括智能裁剪等动态元素。 它们不需要匹配原始文件类型，而是在各种用例中用于表示资源。

了解有关[在 [!DNL Experience Manager Assets]](/help/assets/renditions.md)中查看和管理演绎版的更多信息。

[!DNL Experience Manager Assets]支持以下类型的演绎版：

* [静态演绎版](/help/assets/renditions.md#static-renditions)：静态演绎版是数字资源的预创建版本，通常在资源摄取或修改期间生成。 它们针对特定用途和平台进行了优化，例如Web缩略图、适用于响应式设计的移动友好格式，或适用于打印的高分辨率文件，从而提供简化且一致的体验。

* [动态演绎版](/help/assets/renditions.md#dynamic-renditions)：动态演绎版是资产的实时、自定义版本，可执行各种操作，例如根据不同的设备分辨率调整图像大小或裁剪以适合各种长宽比。 这些演绎版允许您提供个性化和优化的体验，以满足更广泛的需求。 已在[!DNL Adobe Experience Manager Assets]创作环境中创建资源的动态演绎版。 有关启用动态呈现所需的步骤的信息，请参阅[启用动态呈现](#enable-dynamic-media-renditions)。

* [智能裁切](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)：智能裁切在裁切过程中仅专注于资源的重要部分。 Dynamic Media智能裁剪利用由Adobe AI提供的人工智能来跟踪目标点，确保我们的资源在所有屏幕大小上都具有最佳外观。 [!DNL Adobe Experience Manager]智能裁剪显示资源演绎版的宽度和高度以及标题。 请参阅[在AEM Assets Dynamic Media中使用智能裁剪](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)以了解详情。

  智能裁剪呈现版本会显示，并且仅在您有权访问具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)时才可供下载。 智能裁剪演绎版仅适用于图像资源。

  ![节目类型](/help/assets/assets/renditions-types.png)

  >[!NOTE]
  > 
  > “下载”面板仅显示自定义静态呈现版本。 默认`cq5dam.*`缩略图未显示在Content Hub中。

### 启用动态呈现版本 {#enable-dynamic-media-renditions}

要启用动态呈现版本，请执行以下操作：

1. 确保您有权访问具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)。

   一旦您有权访问具有OpenAPI功能的Dynamic Media，则所有标记为`Approved`的资源都可用于Dynamic Media的公开交付。

1. 将资源的[审批目标](/help/assets/approve-assets-content-hub.md#set-approval-target)设置为Content Hub以仅审批Content Hub的资源。

1. 启用&#x200B;**[!UICONTROL 配置]**&#x200B;用户界面的&#x200B;**[!UICONTROL 呈现版本]**&#x200B;选项卡中提供的[启用呈现版本可用性](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub)切换开关。

1. 重新保存现有的图像预设，以使其在Content Hub上可用。 它仅适用于通过OpenAPI新载入到Dynamic Media的情况。

   要重新保存现有的图像预设，请导航到“管理员”视图，然后选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 图像预设]**。 选择预设，单击&#x200B;**[!UICONTROL 编辑]**，然后单击&#x200B;**[!UICONTROL 保存]**。



   >[!NOTE]
   > 
   > 动态演绎版仅适用于图像资源。



