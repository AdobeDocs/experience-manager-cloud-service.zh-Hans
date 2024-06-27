---
title: 编辑图像
description: 使用由 [!DNL Adobe Express] 提供支持的选项编辑图像并将更新后的图像另存为版本。
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: 9a21c9218e45bb6ce91263c9798e3b1c99f369b4
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 33%

---

# 在 [!DNL Assets view] 中编辑图像 {#edit-images-in-assets-view}

“资源视图”支持基本的图像编辑，包括调整大小、删除背景、裁剪以及在JPEG格式和PNG格式之间进行转换。 此外，它还允许通过与Adobe Express集成进行高级编辑。 在编辑图像之后，您可以将新图像另存为新版本。版本控制可帮助您以后在需要时还原为原始资源。 若要编辑图像，请[打开其预览](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/navigate-view#preview-assets)，然后单击&#x200B;**“编辑图像”。**

>[!NOTE]
>
>您可以使用 [!DNL Adobe Express] 编辑 PNG 和 JPEG 文件类型的图像。

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## 编辑图像 {#edit-image}

登陆资产视图，使用链接 —  [资产视图](https://experience.adobe.com/#/assets) 并选择正确的存储库。 要获得访问权限，请联系贵组织的管理员。
有关任何其他参考信息，请参阅 —  [开始使用Adobe Experience Manager Assets视图](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view)， [了解Assets视图用户界面](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/navigate-assets-view#understand-interface-navigation)、和 [Assets查看用例](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view#use-cases).
<!--
>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express Integration"
>abstract="Easy and intuitive image-editing tools powered by Adobe Express available directly within AEM Assets to increase content reuse and accelerate content velocity."-->

### 在Assets视图上使用Adobe Express编辑图像 {#edit-image-on-assets-view-using-adobe-express}

登录Assets视图后，单击 **Assets**，选择图像，然后单击 **编辑** 从顶部边栏上。 新屏幕显示了可用的编辑选项，包括调整大小、删除背景、裁剪以及在JPEG格式和PNG格式之间进行转换。

#### 调整图像大小 {#resize-image-using-express}

将图像大小调整为热门用例中的特定大小。Assets视图通过提供针对特定照片大小预先计算的新分辨率，可让您快速调整图像大小以适合常见的照片大小。 要使用Assets视图调整图像大小，请执行以下步骤：

1. 单击 **调整图像大小** 左窗格中的。
1. 从调整大小下拉列表中选择相应的社交媒体平台，然后从显示的选项中选择图像大小。
1. 如果需要，使用&#x200B;**“图像比例”**&#x200B;字段缩放图像。
1. 单击&#x200B;**[!UICONTROL 应用]**以应用您的更改。
   ![使用 Adobe Express 进行图像编辑](assets/adobe-express-resize-image.png)

   您编辑的图像可供下载。您可以将编辑后的资源另存为同一资源的新版本，也可以将其另存为新资源。
   ![使用 Adobe Express 保存图像](assets/adobe-express-resize-save.png)

#### 删除背景 {#remove-background-using-express}

您可以按照以下所述步骤从图像中删除背景：

1. 单击 **删除背景** 左窗格中的。 Experience Manager Assets 不含背景地显示该图像。
1. 单击&#x200B;**[!UICONTROL 应用]**以应用您的更改。
   ![使用 Adobe Express 保存图像](assets/adobe-express-remove-background.png)

   您编辑的图像可供下载。您可以将编辑后的资源另存为同一资源的新版本，也可以将其另存为新资源。

#### 裁切图像 {#crop-image-using-express}

将图像转换为完美大小非常简单，只需使用嵌入即可 [!DNL Adobe Express] 快速操作。

1. 单击 **[!UICONTROL 裁切图像]** 左窗格中的。
2. 拖动该图像四角的手柄以创建您想要的裁切效果。
3. 单击&#x200B;**[!UICONTROL 应用]**。
   ![使用 Adobe Express 保存图像](assets/adobe-express-crop-image.png)
裁剪后的图像可供下载。您可以将编辑后的资源另存为同一资源的新版本，也可以将其另存为新资源。

#### 在图像文件类型之间转换 {#convert-image-types-using-express}

您可以使用Adobe Express在JPEG和PNG图像格式之间快速转换。 执行以下步骤：

1. 单击 **JPEG到PNG** 或 **PNG到JPEG** 左窗格中的。
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
1. 单击&#x200B;**[!UICONTROL “下载”。]**

#### 限制 {#limitations-adobe-express}

* 支持的图像分辨率：最小 - 50 像素，最大 - 每维 6000 像素。

* 支持的最大文件大小：17 MB。

### 在Adobe Express嵌入式编辑器中编辑图像 {#edit-images-in-adobe-express-embedded-editor}

拥有Express权利的用户可以从Assets视图中使用嵌入的Express编辑器，轻松地在Adobe Firefly中使用GenAI编辑内容和创建新内容。 这提高了内容重用率并加快了内容速度。 您还可以使用预定义元素让您的资产外观引人注目，或执行快速操作以只需单击几下即可编辑图像。
![在Essentials UI中表达](/help/assets/assets/express-in-essentials-ui.jpg)
要使用编辑图像，请执行以下操作 [!DNL Adobe Express] 嵌入式编辑器，请执行以下步骤：

1. 使用以下链接登录到AEM Assets视图 —  [AEM资源视图](https://experience.adobe.com/#/assets) 并选择正确的存储库。
1. 单击 **Assets**，输入文件夹，然后选择图像。
1. 单击 **在Adobe Express中打开**. 图像在快速画布上打开。
1. 对图像进行所需的编辑。
1. 如果您的项目要求您添加更多页面，请单击 **添加**，选择Assets，输入文件夹，选择要放到画布页面上的图像，然后对图像执行所需的编辑。
1. 要保存图像，请单击 **保存**. 此时将显示保存对话框。

   >[!NOTE]
   >
   > **1. 对于单页**
   >
   > **另存为版本：** 此功能仅支持保存单个资源。 选择此选项可将图像导出为新版本（保留原始格式），并将其保存在同一文件夹中。
   > **另存为新资产：** 选择此选项可将资源以与原始资源不同的格式导出，并将其另存到任意文件夹中作为新资源。
   >  
   > **2. 对于多页**
   >
   > **另存为版本：** 此功能仅支持保存单个资源。 如果要从多个页面中保存单个页面，请选择此选项，以原始格式和位置保存资产。\
   > **另存为新资产：** 利用此选项，您可以将多个资源或单个资源导出到任意文件夹，并将它们另存为新资源，其文件格式为原始文件或其他文件。

1. 在“保存”对话框中：
   1. 在中输入文件的名称 **另存为** 字段。
   1. 选择目标文件夹。
   1. 可选：提供项目或营销策划名称、关键字、渠道、时间范围和区域等详细信息。
1. 单击 **另存为版本** 或 **另存为新资源** 以保存资产。

#### 在Express编辑器中编辑图像的限制 {#limitations-of-editing-images-in-the-express-editor}

* 支持的文件类型：JPEG或PNG。
* 支持的最大文件大小：40 MB。
* 支持的宽度和高度范围：介于50到8000像素之间。
* 重新加载页面以查看源文件夹中最新保存的新资源。

### 使用 Adobe Express 创建新资源 {#create-new-embedded-editor}

[!DNL Assets view] 使您能够使用 [!DNL Adobe Express] 嵌入式编辑器从头开始创建新模板。若要使用 [!DNL Adobe Express] 创建新资源，请执行以下步骤：

1. 导航到 **[!UICONTROL 我的Workspace]** 并单击 **[!UICONTROL 创建]** 顶部显示的Adobe Express横幅中。 [!DNL Adobe Express] 空白画布显示在 [!DNL Assets view] 用户界面中。
1. 使用[模板](https://helpx.adobe.com/cn/express/using/work-with-templates.html)创建您的内容。否则，导航至&#x200B;**[!UICONTROL 您的内容]**&#x200B;来修改现有内容。
1. 完成编辑后，单击 **[!UICONTROL 保存]**.
1. 为创建的资源指定目标路径，然后单击 **[!UICONTROL 另存为新资源]**.

#### 限制 {#limitations}

* 您只能修改 `JPEG` 和 `PNG` 格式类型的图像。
* 资源大小必须小于 40 MB。
* 您可以将图像保存为 `PDF`, `JPEG` 或者 `PNG` 格式。

<!--
## Edit images using [!DNL Adobe Photoshop Express] {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->
<!--
### Touch up images {#spot-heal-images-using-photoshop-express}

If there are minor spots or small objects on an image, you can edit and remove the spots using the spot healing feature provided by Adobe Photoshop.

The brush samples the retouched area and makes the repaired pixels blend seamlessly into the rest of the image. Use a brush size that is only slightly larger than the spot you want to fix.

![Spot healing edit option](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->
<!-- 
### Crop and straighten images {#crop-straighten-images-using-photoshop-express}

Using the crop and straighten option that you can do basic cropping, rotate image, flip it horizontally or vertically, and crop it to dimensions suitable for popular social media websites.

To save your edits, click **[!UICONTROL Crop Image]**. After editing, you can save the new image as a version.

![Option to crop and straighten](assets/edit-crop-straighten.png)

Many default options let you crop your image to the best proportions that fit various social media profiles and posts.

### Resize image {#resize-image-using-photoshop-express}

You can view the common photo sizes in centimeters or inches to know the dimensions. By default, the resizing method retains the aspect ratio. To manually override the aspect ratio, click ![](assets/do-not-localize/lock-closed-icon.png).

Enter the dimensions and click **[!UICONTROL Resize Image]** to resize the image. Before you save the changes as a version, you can either undo all the changes done before saving by clicking [!UICONTROL Undo] or you can change the specific step in the editing process by clicking [!UICONTROL Revert].

![Options when resizing an image](assets/resize-image.png)

### Adjust image {#adjust-image-using-photoshop-express}

[!DNL Assets view] lets you adjust the color, tone, contrast, and more, with just a few clicks. Click **[!UICONTROL Adjust image]** in the edit window. The following options are available in the right sidebar:

* **Popular**: [!UICONTROL High Contrast & Detail], [!UICONTROL Desaturated Contrast], [!UICONTROL Aged Photo], [!UICONTROL B&W Soft], and [!UICONTROL B&W Sepia Tone].
* **Color**: [!UICONTROL Natural], [!UICONTROL Bright], [!UICONTROL High Contrast], [!UICONTROL High Contrast & Detail], [!UICONTROL Vivid], and [!UICONTROL Matte].
* **Creative**: [!UICONTROL Desaturated Contrast], [!UICONTROL Cool Light], [!UICONTROL Turquoise & Red], [!UICONTROL Soft Mist], [!UICONTROL Vintage Instant], [!UICONTROL Warm Contrast], [!UICONTROL Flat & Green], [!UICONTROL Red Lift Matte], [!UICONTROL Warm Shadows], and [!UICONTROL Aged Photo].
* **B&W**: [!UICONTROL B&W Landscape], [!UICONTROL B&W High Contrast], [!UICONTROL B&W Punch], [!UICONTROL B&W Low Contrast], [!UICONTROL B&W Flat], [!UICONTROL B&W Soft], [!UICONTROL B&W Infrared], [!UICONTROL B&W Selenium Tone], [!UICONTROL B&W Sepia Tone], and [!UICONTROL B&W Split Tone].
* **Vignetting**: [!UICONTROL None], [!UICONTROL Light], [!UICONTROL Medium], and [!UICONTROL Heavy].

![Adjust image by editing](assets/adjust-image.png)

<!--
TBD: Insert a video of the available social media options.
-->

### 后续步骤 {#next-steps}

* 使用提供产品反馈 [!UICONTROL 反馈] 选项，该选项位于Assets视图用户界面上。

* 通过右侧边栏中的[!UICONTROL 编辑此页面]![编辑页面](assets/do-not-localize/edit-page.png)或[!UICONTROL 记录问题]![创建 GitHub 问题](assets/do-not-localize/github-issue.png)来提供文档反馈

* 联系[客户关怀团队](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Adobe Express中的快速操作](https://helpx.adobe.com/cn/express/using/resize-image.html)
>* [查看资源的版本历史记录](navigate-assets-view.md)
