---
title: Dynamic Media 图像配置文件
description: 了解如何创建包含钝化蒙版和/或智能裁切或智能色板设置的Dynamic Media图像配置文件。 然后，将配置文件应用到图像资源的文件夹。
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Renditions
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: 59392c3a3dd7481d63ed0a79a018a4d6878011ed
workflow-type: tm+mt
source-wordcount: '3490'
ht-degree: 9%

---

# Dynamic Media 图像配置文件 {#image-profiles}

上传图像时，您可以通过将图像配置文件应用到文件夹来在上传时自动裁切图像。

>[!IMPORTANT]
>
>图像配置文件不适用于PDF、动画GIF或INDD (Adobe InDesign)文件。

## “钝化蒙版”选项 {#unsharp-mask}

创建图像配置文件时，您可以使用 **[!UICONTROL 钝化蒙版]** 用于微调最终缩减取样图像的锐化滤镜效果的选项。 您可以控制效果的强度、效果的半径（以像素为单位）以及忽略的对比度阈值。 此效果使用与Adobe Photoshop的“钝化蒙版”滤镜相同的选项。

>[!NOTE]
>
>USM锐化只应用于PTIFF（金字塔tiff）内缩减像素采样率超过50%的缩减格式副本。 这意味着ptiff中最大大小的演绎版不受钝化蒙版的影响。 而较小大小的演绎版（例如缩略图）会被更改（并显示钝化蒙版）。

In **[!UICONTROL 钝化蒙版]**，则可以使用以下筛选选项：

<table>
 <tbody>
  <tr>
   <td><strong>选项</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>数量</td>
   <td>控制应用于边缘像素的对比度数量。 默认值为1.75。对于高分辨率图像，最多可将其增加到5。 可以考虑使用数量来衡量滤镜强度。范围是0-5。</td>
  </tr>
  <tr>
   <td>半径</td>
   <td>确定边缘像素周围影响锐化的像素数量。对于高分辨率图像，输入 1 到 2。低值仅锐化边缘像素；高值锐化较宽范围的像素。正确的值取决于图像大小。默认值为0.2。范围是0-250。</td>
  </tr>
  <tr>
   <td>阈值</td>
   <td><p>确定在应用钝化蒙版滤镜时要忽略的对比度范围。换句话说，此选项确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素并进行锐化。 为避免引入噪声，请尝试使用0-255之间的值。</p> </td>
  </tr>
 </tbody>
</table>

有关“锐化”的信息，请参阅[锐化图像](/help/assets/dynamic-media/assets/sharpening_images.pdf)。

## 裁切选项 {#crop-options}

当您对图像实施智能裁剪时，Adobe建议采用以下最佳实践并强制实施以下限制：

| 资源 — 限制类型 | 最佳实践 | 施加的限制 |
| --- | --- | --- |
| **图像**  — 每个图像的智能裁剪数 | 5 | 100 |

另请参阅 [Dynamic Media限制](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

智能裁剪坐标与纵横比相关。 对于图像配置文件中的智能裁剪设置，如果图像配置文件中添加的维度的宽高比相同，则会将相同的宽高比发送到Dynamic Media。 Adobe建议您使用相同的裁切区域。 这样做可确保对图像配置文件中使用的不同尺寸不产生任何影响。

您创建的每个智能裁剪生成都需要额外的处理。 例如，添加五个以上的智能裁切长宽比可能会导致资源摄取速度缓慢。 它还可能导致系统负载增加。 由于您可以在文件夹级别应用智能裁切，因此Adobe建议您在文件夹上使用它 *仅限* 在需要的地方。

**定义图像配置文件中智能裁剪的准则**
为了控制智能裁切的使用，并优化裁切的处理时间和存储，Adobe建议以下准则和提示：

* 避免创建具有相同宽度和高度值的重复智能裁剪配置文件。
* 根据裁切维度而不是最终用途命名智能裁切。 这样做有助于优化在多个页面上使用单个维度的重复项。
* 为特定文件夹和子文件夹创建基于页面/资源类型的图像配置文件，而不是创建应用于所有文件夹或所有资源的通用智能裁剪配置文件。
* 应用于子文件夹的图像配置文件将覆盖应用于该文件夹的图像配置文件。
* 理想情况下，每个图像应有10-15个智能裁剪，以优化屏幕比例和处理时间。

您有两个图像裁切选项可供选择。 您还可以选择自动创建颜色和图像样本，或保留所有目标分辨率的裁切内容。

>[!IMPORTANT]
>
>Adobe建议您查看任何生成的裁切和色板，以确保它们合适且与您的品牌和价值观相关。

| 选项 | 何时使用 | 描述 |
| --- | --- | --- |
| **[!UICONTROL 像素裁剪]** | 仅基于尺寸批量裁切图像。 | 从 **[!UICONTROL 裁切选项]** 下拉列表，选择 **[!UICONTROL 像素裁切]**.<br>若要从图像的侧面裁切，请输入要从图像的任意侧面或每侧面裁切的像素数。裁切图像的量取决于图像文件中的ppi（像素/英寸）设置。<br>图像配置文件像素裁剪通过以下方式渲染：<br>·值为Top、Bottom、Left和Right。<br>·考虑左上角 `0,0` 像素裁切是从此处计算的。<br>·裁切起点：左为X，上为Y<br>·水平计算：原始图像的水平像素大小减去“左”，然后减去“右”。<br>·垂直计算：垂直像素高度减“顶部”，然后减“底部”。<br>例如，假设您有一个4000 x 3000像素的图像。 可使用以下值：Top=250、Bottom=500、Left=300、Right=700。<br>从左上角(300,250)裁切，使用填充空间（4000-300-700、3000-250-500或3000,2250）。 |
| **[!UICONTROL 智能裁剪]** | 根据视觉焦点批量裁切图像。 | 智能裁剪利用Adobe Sensei中人工智能的强大功能快速批量自动裁剪图像。 智能裁切会自动检测并裁切到任何图像中的焦点，以获得预期的目标点，而不管屏幕大小如何。<br>从 **[!UICONTROL 裁切选项]** 下拉列表，选择 **[!UICONTROL 智能裁剪]**，然后在的右侧 **[!UICONTROL 响应式图像裁切]**，启用（打开）该功能。<br>默认断点大小(**[!UICONTROL 大]**， **[!UICONTROL 中]**， **[!UICONTROL 小]**)涵盖大部分图像在移动设备和平板电脑设备、台式机和横幅上使用的各种尺寸。 如果需要，可以编辑“大”、“中”和“小”的缺省名称。<br>要添加更多断点，请选择 **[!UICONTROL 添加裁切]**；要删除裁切，请选择垃圾桶图标。 |
| **[!UICONTROL 颜色和图像样本]** | 批量生成每个图像的图像样本。 | **注释**：Dynamic Media Classic不支持智能色板。<br>从显示颜色或纹理的产品图像自动定位并生成高质量色板。<br>从 **[!UICONTROL 裁切选项]** 下拉列表，选择 **[!UICONTROL 智能裁剪]**. 然后在右侧 **[!UICONTROL 颜色和图像样本]**，启用（打开）该功能。 输入像素值 **[!UICONTROL 宽度]** 和 **[!UICONTROL 高度]** 文本框。<br>虽然所有图像裁剪都可以从“演绎版”边栏中使用，但样本只能通过 **[!UICONTROL 复制URL]** 功能。 使用您自己的查看组件渲染网站上的色板。 此规则的例外是轮播横幅。 Dynamic Media为轮播横幅中使用的样本提供查看组件。<br><br>**使用图像样本**<br>&#x200B;图像样本的URL很简单：<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>位置 `:Swatch` 会附加到资产请求中。<br><br>**使用色板**<br>&#x200B;要使用色板，请制作 `req=userdata` 请求包含以下内容：<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>例如，以下是Dynamic Media Classic中的样本资源：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>下面是样本资产的对应项 `req=userdata` URL：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>此 `req=userdata` 响应如下：<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>您还可以请求 `req=userdata` XML或JSON格式的响应，如以下相应的URL示例所示：<br>·`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>·`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**注释**：您必须创建自己的WCM组件以请求颜色样本并解析 `SmartSwatchColor` 属性，由24位RGB的十六进制值表示。<br>另请参阅 [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) 在查看器参考指南中。 |
| **[!UICONTROL 在目标分辨率间保留裁切内容]** | 要保持相同纵横比的裁切内容，请执行以下操作 | 在创建智能裁剪配置文件时使用。<br>取消选中此选项可在保持焦点的同时，跨不同分辨率为给定的纵横比生成新的裁切内容。<br>如果决定取消选中此框，请确保原始图像分辨率大于为智能裁剪配置文件定义的分辨率。<br><br>例如，假设您已将长宽比设置为600 x 600（大）、400 x 400（中）和300 x 300（小）。<br>时间 **[!UICONTROL 跨目标分辨率保留裁切内容]** 选项为 *已选中*，您会在所有三个分辨率上看到相同的裁切，类似于以下图像输出示例（仅用于说明目的）：<br>![已勾选选项](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>时间 **[!UICONTROL 跨目标分辨率保留裁切内容]** 选项为 *未选中*，裁切内容是所有三个分辨率中的新增内容，类似于以下图像输出示例（仅用于说明目的）：<br>![已取消选中选项](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### 智能裁切和色板支持的图像文件格式

支持的最大输入文件大小分辨率为16K。

>[!NOTE]
>
>16K分辨率是一种水平显示分辨率，约为16,000像素。 最常讨论的16K分辨率是15360 × 8640，它将8K UHD的像素数增加了一倍，总像素数是四倍。 该分辨率为132.7百万像素，是4K分辨率的16倍，是1080p分辨率的64倍。

| 图像格式 | 不区分大小写的文件扩展名 | MIME类型 | 支持的输入颜色空间 | 支持的最大输入文件大小 | 支持的图像格式？ |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | 是 |
| CMYK |  |  |  |  | 是 |
| EPS |  |  |  |  | 否 |
| GIF | `.gif` | image/gif | sRGB | 15 GB | 是；动画GIF的第一帧用于演绎版。 不能配置或更改第一帧。 |
| JPEG | `.jpg` 和 `.jpeg` | image/jpeg | sRGB | 15 GB | 是 |
| PNG | `.png` | image/png | sRGB | 15 GB | 是 |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | 是 |
| SVG |  |  |  |  | 否 |
| TIFF | `.tif` 和 `.tiff` | image/tiff | sRGB<br>CMYK | 4 GB | 是 |
| WebP/动画WebP |  |  |  |  | 否 |

## 创建Dynamic Media图像配置文件 {#creating-image-profiles}

要为其它资产类型定义高级处理参数，请参阅 [配置资源处理](config-dm.md#configuring-asset-processing).

参见 [关于Dynamic Media图像配置文件和视频配置文件](/help/assets/dynamic-media/about-image-video-profiles.md).

另请参阅[组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md)。

**要创建Dynamic Media图像配置文件，请执行以下操作：**

1. 选择Adobe Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 要添加图像配置文件，请选择 **[!UICONTROL 创建]**.
1. 输入配置文件名称，以及钝化蒙版、裁切或色板（或两者）的值。

   提示：使用特定于其预期用途的配置文件名称。 例如，假设您要创建一个仅生成样本的配置文件。 即，禁用（关闭）智能裁切，启用（打开）颜色和图像色板。 在这种情况下，您可以使用配置文件名称“智能色板”。

   另请参阅[智能裁切和智能色板选项](#crop-options)和[钝化蒙版](#unsharp-mask)。

   ![裁切](assets/crop.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。此时新创建的配置文件会显示在可用配置文件列表中。

## 编辑或删除Dynamic Media图像配置文件 {#editing-or-deleting-image-profiles}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要编辑或删除的图像配置文件。 要编辑图像配置文件，请选择&#x200B;**[!UICONTROL 编辑图像处理配置文件]**。要删除它，请选择 **[!UICONTROL 删除图像处理配置文件]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果是进行编辑操作，请保存更改。如果是进行删除操作，请确认您要删除配置文件。

## 将Dynamic Media图像配置文件应用到文件夹 {#applying-an-image-profile-to-folders}

将图像配置文件分配给文件夹时，任何子文件夹都会自动从其父文件夹继承配置文件。 因此，您只能将一个图像配置文件分配给文件夹。 因此，您在上传、存储、使用资产以及将资产存档的过程中，请妥善安排文件夹结构。

如果为文件夹分配了不同的图像配置文件，则新配置文件将覆盖以前的配置文件。以前现有的文件夹资产保持不变。新配置文件将应用于稍后添加到此文件夹的资产。

为其分配了配置文件的文件夹在用户界面中指示，卡片中显示配置文件的名称。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以将图像配置文件应用到特定文件夹，也可以全局应用到所有资产。

如果文件夹中已有您后来更改的现有图像配置文件，您可以重新处理该文件夹中的资产。 参见 [编辑文件夹的处理配置文件后，重新处理文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### 将Dynamic Media图像配置文件应用到特定文件夹 {#applying-image-profiles-to-specific-folders}

您可以将图像配置文件应用到中的文件夹 **[!UICONTROL 工具]** 菜单，或者如果您在文件夹中，则从 **[!UICONTROL 属性]**.

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

如果文件夹中已有您后来更改的现有视频配置文件，您可以重新处理该文件夹中的资产。 参见 [编辑文件夹的处理配置文件后，重新处理文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### 从“配置文件”用户界面将Dynamic Media图像配置文件应用到文件夹 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要应用于一个或多个文件夹的图像配置文件。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 选择 **[!UICONTROL 将处理配置文件应用到文件夹]** 并选择一个或多个用于接收新上传资源的文件夹，然后选择 **[!UICONTROL 应用]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

#### 将Dynamic Media图像配置文件从“属性”应用到文件夹 {#applying-image-profiles-to-folders-from-properties}

1. 点按Experience Manager徽标并导航到 **[!UICONTROL 资产]**.
1. 导航到 *文件夹* 要应用图像配置文件的（非资产）。
1. 根据您所在的视图，执行以下操作之一：
   * 在“卡片视图”中，将指针悬停在文件夹上，然后选择复选标记以将其选中。
   * 在“列视图”或“列表视图”中，选中文件夹名称左侧的复选框。
1. 在工具栏上，选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL Dynamic Media处理]** 选项卡。
1. 下 **[!UICONTROL 图像配置文件]**，来自 **[!UICONTROL 配置文件名称]** 从下拉列表中，选择要应用的配置文件。
1. 在页面的右上角附近，选择 **[!UICONTROL 保存并关闭]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全局应用Dynamic Media图像配置文件 {#applying-an-image-profile-globally}

除了将配置文件应用到文件夹外，您还可以全局应用配置文件。 任何文件夹中上传到Experience Manager Assets的任何内容均已应用选定的配置文件。

如果文件夹中已有您后来更改的现有视频配置文件，您可以重新处理该文件夹中的资产。 参见 [编辑文件夹的处理配置文件后，重新处理文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**要全局应用Dynamic Media图像配置文件，请执行以下操作：**

1. 执行下列操作之一：

   * 导航到 `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 并应用相应的配置文件，然后选择 **[!UICONTROL 保存]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 导航到CRXDE Lite以下节点： `/content/dam/jcr:content`.

      添加属性 `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` 并选择 **[!UICONTROL 全部保存]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 编辑单个图像的智能裁切或智能色板 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>Adobe建议您查看任何生成的智能裁切和智能色板，以确保它们正确且与您的品牌和价值观相关。

您可以手动重新对齐图像的智能裁切窗口或调整其大小，以进一步细化其焦点。

编辑智能裁切并保存后，所做的更改会传播到您对特定图像使用该裁切的任何位置。

>[!IMPORTANT]
>
>当您手动重新对齐资源的智能裁剪窗口或调整其大小时，即使您稍后决定重新处理资源，也会保留并维护该编辑。 但是，如果您在中编辑宽度和/或高度， **[!UICONTROL 响应式图像裁切]** 区域，则该资产需要进行重新处理。
>参见 [重新处理文件夹中的Dynamic Media资源](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

如有必要，您可以重新运行智能裁剪以再次生成其他裁剪。

另请参阅 [编辑多个图像的智能裁剪或智能色板](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**要编辑单个图像的智能裁切或智能色板，请执行以下操作：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]**，然后转到应用了智能裁切或智能色板图像配置文件的文件夹。
1. 要打开其内容，请选择文件夹。
1. 选择要调整其智能裁剪或智能色板的图像。
1. 在工具栏中，选择 **[!UICONTROL 智能裁剪]**.

1. 执行以下操作之一：

   * 在页面的右上角附近，向左或向右拖动滑块可分别增加或减少图像显示。
   * 在图像上，拖动角手柄以调整裁切或色板的可查看区域的大小。
   * 在图像上，将框/样本拖动到新位置。 只能编辑图像样本；颜色样本是静态的。
   * 在图像上方，选择  **[!UICONTROL 还原]** 撤消所有编辑并恢复原始裁切或色板。
   * 使用键盘箭头键裁切框架大小、重新定位图像或同时使用两者。

1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 关闭]** 以返回到资产的文件夹。

## 编辑多个图像的智能裁剪或智能色板 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>Adobe建议您查看任何生成的智能裁切和智能色板，以确保它们正确且与您的品牌和价值观相关。

将包含智能裁切的图像配置文件应用到文件夹后，该文件夹中的所有图像都会应用裁切。 如果需要，您可以 *手动* 在多个图像中重新对齐智能裁剪窗口或调整其大小，以进一步细化其焦点。

编辑智能裁切并保存后，所做的更改会传播到您对特定图像使用该裁切的任何位置。

>[!IMPORTANT]
>
>当您手动重新对齐多个资源的智能裁切窗口或调整其大小时，即使您稍后决定重新处理这些资源，也会维护并保留所做的这些编辑。 不过，如果您在图像配置文件的&#x200B;**[!UICONTROL 响应式图像裁切]**区域中编辑宽度和/或高度，则这些资源需要重新处理。
>参见 [重新处理文件夹中的Dynamic Media资源](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

如有必要，您可以重新运行智能裁剪以再次生成其他裁剪。

**要编辑多个图像的智能裁剪或智能色板，请执行以下操作：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]**，然后转到应用了智能裁切或智能色板图像配置文件的文件夹。
1. 在文件夹中，选择 **[!UICONTROL 更多操作]** (...)图标，然后选择 **[!UICONTROL 智能裁剪]**.

1. 在 **[!UICONTROL 编辑智能裁剪]** 页面，执行以下任一操作：

   * 调整页面上图像的查看大小。

      在断点名称下拉列表的右侧，向左或向右拖动滑块栏以更改可视图像显示的大小。

      ![edit_smart_ranks-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根据断点名称筛选可见图像的列表。 在以下示例中，图像是根据断点名称“Medium”进行筛选的。

      在页面的右上角附近，从下拉列表中选择一个断点名称，以筛选您看到的图像。 （请参阅上图。）

      ![edit_smart_rances-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 调整智能裁剪框的大小。 执行以下任一操作：

      * 如果图像仅具有智能裁切或智能色板，请在图像上拖动裁切框的角手柄。 调整裁切可视区域的大小。
      * 如果图像同时具有智能裁切和智能色板，请在图像上拖动裁切框的角手柄。 调整裁切可视区域的大小。 或者，选择图像下方的智能色板（颜色色板是静态的），然后拖动裁切框的角手柄。 调整色板的可查看区域的大小。

      ![调整图像的智能裁剪大小](assets/edit_smart_crops-resize.png).

   * 移动智能裁剪框。 执行以下任一操作：

      * 如果图像具有智能裁剪或仅具有智能色板，请在图像上将裁剪框拖动到新位置。
      * 如果图像同时具有智能裁切和智能色板，请在图像上将智能裁切框拖动到新位置。 或者，选择图像下方的智能色板（颜色色板是静态的），然后将智能色板裁剪框拖动到新位置。

      ![edit_smart_compets-move](assets/edit_smart_crops-move.png)

   * 撤消所有编辑并恢复原始智能裁剪或智能色板（仅适用于当前编辑会话）。

      选择 **[!UICONTROL 还原]** 在图像上方。

      ![edit_smart_compets-revert](assets/edit_smart_crops-revert.png)



1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 关闭]** 以返回到资产的文件夹。

## 从文件夹中删除图像配置文件 {#removing-an-image-profile-from-folders}

当您从文件夹中删除图像配置文件时，任何子文件夹都会自动继承从其父文件夹中删除的配置文件的操作。但是，在文件夹内发生的任何文件处理都保持不变。

您可以从中的文件夹删除图像配置文件 **[!UICONTROL 工具]** 菜单，或者如果您在文件夹中，则从 **[!UICONTROL 属性]**.

### 通过“配置文件”用户界面从文件夹中删除Dynamic Media图像配置文件 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要从一个或多个文件夹中删除的图像配置文件。
1. 选择 **[!UICONTROL 从文件夹中删除处理配置文件]** 并选择一个或多个要从中删除配置文件的文件夹，然后选择 **[!UICONTROL 移除]**.

   您可以确认图像配置文件不再应用于文件夹，因为该名称不再显示在文件夹名称下方。

### 通过属性从文件夹中删除Dynamic Media图像配置文件 {#removing-image-profiles-from-folders-via-properties}

1. 选择Experience Manager徽标并导航 **[!UICONTROL 资产]** 然后转到要删除图像配置文件的文件夹。
1. 在文件夹中，选中复选标记以将其选中，然后选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL 图像配置文件]** 选项卡。
1. 从 **[!UICONTROL 配置文件名称]** 下拉列表，选择 **[!UICONTROL 无]**，然后选择 **[!UICONTROL 保存并关闭]**.

   如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。
