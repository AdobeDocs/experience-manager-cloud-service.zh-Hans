---
title: 编辑图像
description: 使用由 [!DNL Adobe Express] 提供支持的选项编辑图像并将更新后的图像另存为版本。
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
source-git-commit: 42d3751a4a29149f3b31dbc28555b81aa7ed43cc
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 70%

---

# 在 [!DNL Assets view] 中编辑图像 {#edit-images}

[!DNL Assets view] 提供了简单易用的编辑选项，由 [!DNL Adobe Express] 支持。可用的编辑操作，使用 [!DNL Adobe Express] 是“调整图像大小”、“删除背景”、“裁切图像”和“将JPEG转换为PNG”，反之亦然。

在编辑图像之后，您可以将新图像另存为新版本。版本控制可帮助您以后在需要时还原为原始资源。此外，版本控制仅适用于PNG文件类型，这意味着当您尝试从JPG文件类型中删除背景时，JPG会自动转换为PNG。 若要编辑图像，请[打开其预览](navigate-assets-view.md)，然后单击&#x200B;**[!UICONTROL “编辑图像”。]**

>[!NOTE]
>
>您可以使用 [!DNL Adobe Express] 编辑 PNG 和 JPEG 文件类型的图像。

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## 使用 Adobe Express 编辑图像 {#edit-using-express}

>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express 集成"
>abstract="可直接在 AEM Assets 中使用简单而直观的受 Adobe Express 支持的图像编辑工具，以提高内容重用率并加快内容速度。"

### 调整图像大小 {#resize-image-using-express}

将图像大小调整为热门用例中的特定大小。[!DNL Assets view] 提供针对特定照片大小预先计算的新分辨率，让您可以快速地调整图像大小以适合常见的照片尺寸。要使用 [!DNL Assets view] 调整图像大小，请按照以下步骤操作：

1. 从中选择图像 [!DNL Experience Manager] 资产存储库，然后单击 **编辑**.
2. 从可在左侧窗格中找到的快速操作中单击&#x200B;**[!UICONTROL 调整图像大小]**。
3. 从&#x200B;**[!UICONTROL “调整大小对象”]**&#x200B;下拉列表中选择适当的社交媒体平台，并从显示的选项中选择图像大小。
4. 如果需要，使用&#x200B;**[!UICONTROL “图像比例”]**&#x200B;字段缩放图像。
5. 单击&#x200B;**[!UICONTROL 应用]**以应用您的更改。
   ![使用 Adobe Express 进行图像编辑](assets/adobe-express-resize-image.png)

   您编辑的图像可供下载。您可以将编辑后的资源另存为同一资源的新版本，也可以将其另存为新资源。
   ![使用 Adobe Express 保存图像](assets/adobe-express-resize-save.png)

### 删除背景 {#remove-background-using-express}

您可以通过几个简单的步骤从图像中删除背景，如下所述：

1. 从中选择图像 [!DNL Experience Manager] 资产存储库，然后单击 **编辑**.
2. 从可在左侧窗格中找到的快速操作中单击&#x200B;**[!UICONTROL 去除背景]**。Experience Manager Assets 不含背景地显示该图像。
3. 单击&#x200B;**[!UICONTROL 应用]**以应用您的更改。
   ![使用 Adobe Express 保存图像](assets/adobe-express-remove-background.png)

### 裁切图像 {#crop-image-using-express}

使用嵌入的 [!DNL Adobe Express] 快速操作可以轻松地将图像转换为完美尺寸。

1. 从中选择图像 [!DNL Experience Manager] 资产存储库，然后单击 **编辑**.
2. 从可在左侧窗格中找到的快速操作中单击&#x200B;**[!UICONTROL 裁切图像]**。
3. 拖动该图像四角的手柄以创建您想要的裁切效果。
4. 单击&#x200B;**[!UICONTROL 应用]**。
   ![使用 Adobe Express 保存图像](assets/adobe-express-crop-image.png)
裁剪后的图像可供下载。您可以将编辑后的资源另存为同一资源的新版本，也可以将其另存为新资源。

### 将 JPEG 转化为 PNG {#convert-jpeg-to-png-using-express}

您可以使用 Adobe Express 将 JPEG 图像快速转换为 PNG 格式。执行以下步骤：

1. 从中选择图像 [!DNL Experience Manager] 资产存储库，然后单击 **编辑**.
2. 单击 **[!UICONTROL 转换为PNG]** 从左侧窗格中可用的快速操作删除。
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
3. 单击&#x200B;**[!UICONTROL 应用]**。
4. 导航到 **[!UICONTROL 在右上角另存为]** 并单击 **[!UICONTROL 另存为新资源]**.

### 将PNG转换为JPEG {#convert-png-to-jpeg-using-express}

您可以使用Adobe Express快速将PNG图像转换为JPEG格式。 执行以下步骤：

1. 从中选择图像 [!DNL Experience Manager] 资产存储库，然后单击 **编辑**.
2. 单击 **[!UICONTROL 转换为JPEG]** 从左侧窗格中可用的快速操作删除。
3. 单击&#x200B;**[!UICONTROL 应用]**。
4. 导航到 **[!UICONTROL 在右上角另存为]** 并单击 **[!UICONTROL 另存为新资源]**.

### 限制 {#limitations-adobe-express}

* 支持的图像分辨率：最小 — 50像素，最大 — 6000像素/维度。

* 支持的最大文件大小：17 MB。

## 使用 Adobe Express 嵌入式编辑器编辑图像 {#edit-using-embedded-editor}

有权访问Assets的组织可以使用集成的图像编辑和创建工具(直接在Assets视图中提供的Adobe Express和Adobe Firefly)，以提高Adobe Express重用并加快内容速度。 您还可以使用预定义的元素使您的资源看起来令人惊叹，或者只需单击几下即可执行快速操作来编辑图像。

若要使用 [!DNL Adobe Express] 嵌入式编辑器编辑图像，请按照以下步骤操作：

1. 从您的 [!DNL Experience Manager] Assets 存储库中选择一张图像。
1. 单击&#x200B;**[!UICONTROL 在 Adobe Express 中打开]**。

   ![Adobe Express 嵌入式编辑器](assets/embedded-editor.png)

   您可以利用 [!DNL Adobe Express] 功能来执行所有与图像编辑相关的操作，例如[调整图像大小](https://helpx.adobe.com/cn/express/using/resize-image.html)、[删除或更改背景颜色](https://helpx.adobe.com/cn/express/using/remove-background.html)、[裁剪图像](https://helpx.adobe.com/cn/express/using/crop-image.html)以及更多。

1. 完成图像编辑后，您可以将资源下载为新资源或将资源另存为新版本。

## 使用 Adobe Express 创建新资源 {#create-new-embedded-editor}

[!DNL Assets view] 使您能够使用 [!DNL Adobe Express] 嵌入式编辑器从头开始创建新模板。若要使用 [!DNL Adobe Express] 创建新资源，请执行以下步骤：

1. 导航到 **[!UICONTROL 我的工作区]** 并单击 **[!UICONTROL 创建]** 顶部显示的Adobe Express横幅中。 [!DNL Adobe Express] 空白画布显示在 [!DNL Assets view] 用户界面中。
1. 使用[模板](https://helpx.adobe.com/cn/express/using/work-with-templates.html)创建您的内容。否则，导航至&#x200B;**[!UICONTROL 您的内容]**&#x200B;来修改现有内容。
1. 完成编辑后，单击&#x200B;**[!UICONTROL 另存为新资源]**。
1. 指定创建资源的目标路径，然后单击&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>* 您只能修改 `JPEG` 和 `PNG` 格式类型的图像。
>* 资源大小必须小于 17 MB。
>* 您可以将图像保存在 `PDF`， `JPEG`，或 `PNG` 格式；但是，当存在多个页面时，可以将它们另存为 `PDF`.

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

* 利用资源视图用户界面上的[!UICONTROL 反馈]选项提供产品反馈

* 通过右侧边栏中的[!UICONTROL 编辑此页面]![编辑页面](assets/do-not-localize/edit-page.png)或[!UICONTROL 记录问题]![创建 GitHub 问题](assets/do-not-localize/github-issue.png)来提供文档反馈

* 联系[客户关怀团队](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Adobe Express中的快速操作](https://helpx.adobe.com/cn/express/using/resize-image.html)
>* [查看资源的版本历史记录](navigate-assets-view.md)
