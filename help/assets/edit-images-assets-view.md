---
title: 编辑图像
description: 使用由 [!DNL Adobe Photoshop Express] 提供支持的选项编辑图像并将更新后的图像另存为版本。
role: User
exl-id: fc21a6ee-bf23-4dbf-86b0-74695a315b2a
source-git-commit: da54e996bad3e6dc8558cecd5bfd7eb99670b142
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 75%

---

# 在 [!DNL Assets view] 中编辑图像 {#edit-images}

[!DNL Assets view] 提供了简单易用的编辑选项，并由 [!DNL Adobe Express] 和 [!DNL Adobe Photoshop Express] 提供支持。使用 [!DNL Adobe Express] 可进行的编辑操作包括调整图像大小、删除背景、裁切图像和将 JPEG 转换为 PNG。

在编辑图像之后，您可以将新图像另存为新版本。版本控制可帮助您以后在需要时还原为原始资源。若要编辑图像，请[打开其预览](/help/assets/navigate-assets-view.md)，然后单击&#x200B;**[!UICONTROL “编辑图像”。]**

>[!NOTE]
>
>您可以使用 [!DNL Adobe Express] 编辑 PNG 和 JPEG 文件类型的图像。

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## 使用 Adob&#x200B;&#x200B;e Express 编辑图像 {#edit-using-express}

>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express 集成"
>abstract="由 Adobe Express 提供支持的简单直观的图像编辑工具可直接在 AEM Assets 中使用，以增加内容重用率并加快内容处理速度。"

### 调整图像大小 {#resize-image-using-express}

将图像大小调整为热门用例中的特定大小。[!DNL Assets view] 提供针对特定照片大小预先计算的新分辨率，让您可以快速地调整图像大小以适合常见的照片尺寸。要使用 [!DNL Assets view] 调整图像大小，请按照以下步骤操作：

1. 选择图像并单击&#x200B;**“编辑”。**
2. 单击可在左窗格中找到的快速操作内的 **[!DNL Resize Image]**。
3. 从&#x200B;**[!UICONTROL “调整大小对象”]**&#x200B;下拉列表中选择适当的社交媒体平台，并从显示的选项中选择图像大小。
4. 如有必要，使用 **[!UICONTROL 图像缩放]** 字段。
5. 单击 **[!DNL Apply]** 应用您的更改。
   ![使用 Adob&#x200B;&#x200B;e Express 进行图像编辑](assets/adobe-express-resize-image.png)

   您编辑的图像可供下载。您可以将编辑后的资源另存为同一资源的新版本，也可以将其另存为新资源。
   ![使用 Adob&#x200B;&#x200B;e Express 保存图像](assets/adobe-express-resize-save.png)

### 删除背景 {#remove-background-using-express}

您可以通过几个简单的步骤从图像中删除背景，如下所述：

1. 选择图像并单击&#x200B;**“编辑”。**
2. 单击可在左窗格中找到的快速操作内的 **[!DNL Remove Background]**。Experience Manager Assets 显示无背景的图像。
3. 单击 **[!DNL Apply]** 应用您的更改。
   ![使用 Adob&#x200B;&#x200B;e Express 保存图像](assets/adobe-express-remove-background.png)

   您编辑的图像可供下载。您可以将编辑后的资源另存为同一资源的新版本，也可以将其另存为新资源。

### 裁切图像 {#crop-image-using-express}

使用嵌入的 [!DNL Adobe Express] 快速操作可以轻松地将图像转换为完美尺寸。

1. 选择图像并单击&#x200B;**“编辑”。**
2. 单击可在左窗格中找到的快速操作内的 **[!DNL Crop Image]**。
3. 拖动图像角落上的手柄以创建所需的裁剪效果。
4. 单击 **[!DNL Apply]**。
   ![使用 Adob&#x200B;&#x200B;e Express 保存图像](assets/adobe-express-crop-image.png)
裁剪后的图像可供下载。您可以将编辑后的资源另存为同一资源的新版本，也可以将其另存为新资源。

### 将 JPEG 转化为 PNG {#convert-jpeg-to-png-using-express}

您可以使用 Adob&#x200B;&#x200B;e Express 将 JPEG 图像快速转换为 PNG 格式。执行以下步骤：

1. 选择图像并单击&#x200B;**“编辑”。**
2. 单击可在左窗格中找到的快速操作内的 **[!DNL JPEG to PNG]**。
   ![使用 Adob&#x200B;&#x200B;e Express 转换为 PNG](assets/adobe-express-convert-image.png)
3. 单击&#x200B;**[!UICONTROL “下载”。]**

### 限制 {#limitations-adobe-express}

* 支持的图像分辨率：最小 - 50 像素，最大 - 每维 6000 像素

* 支持的最大文件大小：17 MB

## 使用Adobe Express嵌入式编辑器编辑图像 {#edit-using-embedded-editor}

有权访问Express的用户现在可以直接在AEM Assets中使用Adobe Express和Adobe Firefly集成的图像编辑和创建工具，以改进内容重用并加快内容速度。 您还可以使用预定义元素让您的资产外观引人注目，或执行快速操作以只需单击几下即可编辑图像。

要使用编辑图像，请执行以下操作 [!DNL Adobe Express] 嵌入式编辑器，请执行以下步骤：

1. 从中选择图像 [!DNL Experience Manager] 资产存储库。
1. 单击 **[!UICONTROL 在Adobe Express中打开]**.

   ![Adobe Express嵌入式编辑器](assets/embedded-editor.png)

   您可以利用的功能 [!DNL Adobe Express] 执行所有与图像编辑相关的操作，例如 [调整图像大小](https://helpx.adobe.com/in/express/using/resize-image.html)， [删除或更改背景颜色](https://helpx.adobe.com/in/express/using/remove-background.html)， [裁切图像](https://helpx.adobe.com/in/express/using/crop-image.html)，等等。

1. 完成图像编辑后，您可以将资源下载为新资源或将资源另存为新版本。

## 使用Adobe Express创建新资源 {#create-new-embedded-editor}

[!DNL Assets view] 提供了使用从头开始创建新模板的功能 [!DNL Adobe Express] 嵌入式编辑器。 要使用创建新资源，请执行以下操作 [!DNL Adobe Express]，执行以下步骤：

1. 导航到 **[!UICONTROL 我的工作区]** 并单击 **[!UICONTROL 创建]** 在顶部显示的Adobe Express横幅中 [!UICONTROL 快速访问] 部分。 [!DNL Adobe Express] 空白画布会显示在 [!DNL Assets view] 用户界面。
1. 创建内容，使用 [模板](https://helpx.adobe.com/in/express/using/work-with-templates.html). 否则，导航到 **[!UICONTROL 你的东西]** 以修改现有内容。
1. 完成编辑后，单击 **[!UICONTROL 另存为新资源]**.
1. 为创建的资源指定目标路径，然后单击 **[!UICONTROL 保存]**.

>[!NOTE]
>
>* 您只能修改以下项的图像： `JPEG` 和 `PNG` 格式类型。
>* 资源大小必须小于14 MB。
>* 您可以将图像保存在 `PDF`， `JPEG`，或 `PNG` 格式。

## 使用 [!DNL Adobe Photoshop Express] 编辑图像 {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](//help/navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->

### 对图像进行污点修复 {#spot-heal-images-using-photoshop-express}

如果某个图像上有小污点或者小物体，您可以使用 Adobe Photoshop 提供的污点修复功能编辑和移除污点。

画笔在修饰后的区域中取样，并使修复的像素无缝地混入图像的其余部分。使用仅略大于所要修复污点的画笔大小。

![污点修复编辑选项](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->

### 裁切和拉直图像 {#crop-straighten-images-using-photoshop-express}

使用裁切和拉直选项，您可以执行基本的裁切、旋转图像、在水平或垂直方向上翻转图像，以及将其裁切为适合流行社交媒体网站的尺寸。

要保存您的编辑，请单击&#x200B;**[!UICONTROL 裁切图像]**。在编辑之后，您可以将新图像另存为版本。

![裁切和拉直图像的选项](assets/edit-crop-straighten.png)

许多默认选项可以让您将图像裁切为最佳比例，以适合各种社交媒体配置文件和帖子。

### 调整图像大小 {#resize-image-using-photoshop-express}

您可以按厘米或英寸查看常见照片大小来了解具体的尺寸。默认情况下，调整大小方法保留纵横比。要手动覆盖纵横比，请单击 ![](assets/do-not-localize/lock-closed-icon.png)。

输入尺寸，单击&#x200B;**[!UICONTROL 调整图像大小]**&#x200B;来调整图像大小。在将更改另存为版本之前，您可以在保存之前通过单击[!UICONTROL 还原]以撤销进行的所有更改，或者单击[!UICONTROL 恢复]来更改编辑过程中的特定步骤。

![调整图像大小时的选项](assets/resize-image.png)

### 调整图像 {#adjust-image-using-photoshop-express}

使用 [!DNL Assets view] 只需几次单击即可调整颜色、色调、对比度等等。在编辑窗口中单击&#x200B;**[!UICONTROL 调整图像]**。右侧边栏中提供了以下选项：

* **流行**：[!UICONTROL 高对比度和细节]、[!UICONTROL 去饱和对比度]、[!UICONTROL 老照片]、[!UICONTROL 黑白柔和]和[!UICONTROL 黑白棕褐色调]。 
* **颜色**：[!UICONTROL 自然]、[!UICONTROL 明亮]、[!UICONTROL 高对比度]、[!UICONTROL 高对比度和细节]、[!UICONTROL 鲜艳]和[!UICONTROL 哑光]。
* **创意**：[!UICONTROL 去饱和对比度]、[!UICONTROL 冷光]、[!UICONTROL 绿松石色和红色]、[!UICONTROL 柔和薄雾]、[!UICONTROL 复古瞬间]、[!UICONTROL 暖调对比度]、[!UICONTROL 平坦和绿色]、[!UICONTROL 红色提升哑光]、[!UICONTROL 暖调阴影]和[!UICONTROL 老照片]。
* **黑白**：[!UICONTROL 黑白风景]、[!UICONTROL 黑白高对比度]、[!UICONTROL 黑白打孔]、[!UICONTROL 黑白低对比度]、[!UICONTROL 黑白平坦]、[!UICONTROL 黑白柔和]、[!UICONTROL 黑白红外线]、[!UICONTROL 黑白硒色调]、[!UICONTROL 黑白棕褐色]和[!UICONTROL 黑白分离色调]。
* **渐晕**：[!UICONTROL 无]、[!UICONTROL 轻]、[!UICONTROL 中]和[!UICONTROL 重]。

![通过编辑调整图像](assets/adjust-image.png)

<!--
TBD: Insert a video of the available social media options.
-->

### 后续步骤 {#next-steps}

* 利用资源视图用户界面上的[!UICONTROL 反馈]选项提供产品反馈

* 通过右侧边栏中的[!UICONTROL 编辑此页面]![编辑页面](assets/do-not-localize/edit-page.png)或[!UICONTROL 记录问题]![创建 GitHub 问题](assets/do-not-localize/github-issue.png)来提供文档反馈

* 联系[客户关怀团队](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [查看资源的版本历史记录](/help/assets/navigate-assets-view.md)
