---
title: Dynamic Media 图像配置文件
description: 了解如何创建Dynamic Media图像配置文件，其中包含USM锐化设置、智能裁切或智能色板设置，或者同时包含这两项设置。 然后，将配置文件应用到图像资产的文件夹。
feature: Asset Management,Image Profiles,Renditions
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: a2bbc64051214efa83d74d414e2e5f1407433127
workflow-type: tm+mt
source-wordcount: '3277'
ht-degree: 10%

---

# Dynamic Media 图像配置文件 {#image-profiles}

上传图像时，您可以通过将图像配置文件应用到文件夹，在上传时自动裁剪图像。

>[!IMPORTANT]
>
>图像配置文件不适用于PDF、动画GIF或INDD(Adobe InDesign)文件。

## 钝化蒙版选项 {#unsharp-mask}

创建图像配置文件时，您可以使用 **[!UICONTROL 钝化蒙版]** 选项，对最终的缩减采样图像微调锐化滤镜效果。 您可以控制效果的强度、效果的半径（以像素为单位）以及被忽略的对比度阈值。 此效果使用与 Adobe Photoshop 的“钝化蒙蔽”滤镜相同的选项。

>[!NOTE]
>
>USM锐化仅应用于PTIFF（金字塔tiff）中缩减采样率超过50%的缩小演绎版。 这意味着ptiff中最大大小的演绎版不会受到USM锐化的影响。 但是，大小较小的演绎版（如缩略图）会发生更改（并显示USM锐化）。

在 **[!UICONTROL 钝化蒙版]**，则具有以下筛选选项：

<table>
 <tbody>
  <tr>
   <td><strong>选项</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>数量</td>
   <td>控制应用于边缘像素的对比度量。 默认值为1.75。对于高分辨率图像，最高可将其增加到5。 可以考虑使用数量来衡量滤镜强度。范围为0-5。</td>
  </tr>
  <tr>
   <td>半径</td>
   <td>确定边缘像素周围影响锐化的像素数量。对于高分辨率图像，输入 1 到 2。低值仅锐化边缘像素；高值锐化较宽范围的像素。正确的值取决于图像大小。默认值为0.2。范围为0-250。</td>
  </tr>
  <tr>
   <td>阈值</td>
   <td><p>确定在应用USM锐化滤镜时要忽略的对比度范围。换句话说，此选项确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素并进行锐化。 为避免引入杂色，请尝试使用0到255之间的值。</p> </td>
  </tr>
 </tbody>
</table>

有关“锐化”的信息，请参阅[锐化图像](/help/assets/dynamic-media/assets/sharpening_images.pdf)。

## 裁切选项 {#crop-options}

在图像上实施智能裁剪时，Adobe建议采用以下最佳实践并强制实施以下限制：

| 限制类型 | 最佳实践 | 规定的限制 | 2022年12月31日的上限变更 |
| --- | --- | --- | --- |
| 每个图像的智能作物数量 | 5 | 100 | 20 |

另请参阅 [Dynamic Media限制](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

智能裁切坐标取决于宽高比。 对于图像配置文件中的智能裁剪设置，如果图像配置文件中添加的维度的宽高比相同，则会将相同的宽高比发送到Dynamic Media。 Adobe建议您使用相同的裁剪区域。 这样做可确保对图像配置文件中使用的不同维度不会产生任何影响。

您创建的每个智能裁剪生成都需要额外的处理。 例如，添加五个以上智能裁剪长宽比可能会导致资产摄取速度缓慢。 它还可能增加系统的负载。 由于您可以在文件夹级别应用智能裁剪，因此Adobe建议您在文件夹上使用智能裁剪 *仅* 需要的地方。

您有两个图像裁剪选项可供您选择。 您还可以选择自动创建颜色和图像色板，或跨目标分辨率保留裁剪内容。

>[!IMPORTANT]
>
>Adobe建议您查看生成的任何作物和色板，以确保它们与您的品牌和价值相关且适当。

| 选项 | 何时使用 | 描述 |
| --- | --- | --- |
| **[!UICONTROL 像素裁剪]** | 仅基于维度批量裁剪图像。 | 从 **[!UICONTROL 裁剪选项]** 下拉列表中，选择 **[!UICONTROL 像素裁剪]**.<br>要从图像的侧边进行裁剪，请输入要从图像的任意侧边或每侧进行裁剪的像素数。裁剪图像的多少取决于图像文件中的ppi（像素/英寸）设置。<br>图像配置文件像素裁切按以下方式呈现：<br>·值包括顶部、底部、左侧和右侧。<br>·考虑左上角 `0,0` 像素裁切就从此计算。<br>·裁剪起点：左为X，上为Y<br>·水平计算：原始图像的水平像素大小减去“左”，然后减去“右”。<br>·垂直计算：垂直像素高度减去“顶部”，然后减去“底部”。<br>例如，假定您的图像为4000 x 3000像素。 您使用以下值：顶=250，底=500，左=300，右=700。<br>从左上角(300,250)使用填充空间(4000-300-700、3000-250-500或3000,2250)进行裁剪。 |
| **[!UICONTROL 智能裁剪]** | 根据图像的可视焦点批量裁剪图像。 | Smart Crop利用Adobe Sensei中人工智能的强大功能，快速批量自动裁剪图像。 智能裁剪可自动检测并裁剪到任何图像中的焦点以获取预期的目标点，而不管屏幕大小。<br>从 **[!UICONTROL 裁剪选项]** 下拉列表中，选择 **[!UICONTROL 智能裁剪]**，则位于的右侧 **[!UICONTROL 响应式图像裁剪]**，启用（打开）该功能。<br>默认断点大小(**[!UICONTROL 大]**, **[!UICONTROL 中]**, **[!UICONTROL 小]**)涵盖大多数图像在移动和平板电脑设备、台式机和横幅上使用的所有大小。 如果需要，您可以编辑默认名称“大”、“中”和“小”。<br>要添加更多断点，请选择 **[!UICONTROL 添加裁剪]**;要删除裁剪，请选择垃圾箱图标。 |
| **[!UICONTROL 颜色和图像样本]** | 批量会为每个图像生成一个图像样本。 | **注意**:Dynamic Media Classic不支持智能色板。<br>自动从显示颜色或纹理的产品图像中定位并生成高质量样本。<br>从 **[!UICONTROL 裁剪选项]** 下拉列表中，选择 **[!UICONTROL 智能裁剪]**. 在右侧 **[!UICONTROL 颜色和图像色板]**，启用（打开）该功能。 在 **[!UICONTROL 宽度]** 和 **[!UICONTROL 高度]** 框中。<br>虽然所有图像裁剪都可以从演绎版边栏中获取，但样本仅通过 **[!UICONTROL 复制URL]** 功能。 使用您自己的查看组件在网站上渲染色板。 此规则的例外是传送横幅。 Dynamic Media为轮播横幅中使用的色板提供查看组件。<br><br>**使用图像色板**<br>&#x200B;图像样本的URL非常简单：<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>其中 `:Swatch` 会附加到资产请求中。<br><br>**使用颜色色板**<br>&#x200B;要使用颜色色板，请 `req=userdata` 请求，其中包含以下内容：<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>例如，以下是Dynamic Media Classic中的色板资产：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>下面是样本资产的对应 `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>的 `req=userdata` 响应如下：<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>您还可以请求 `req=userdata` XML或JSON格式的响应，如以下各个URL示例所示：<br>·`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>·`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**注意**:您必须创建自己的WCM组件才能请求颜色样本并解析 `SmartSwatchColor` 属性，由24位RGB十六进制值表示。<br>另请参阅 [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) （在查看器参考指南中）。 |
| **[!UICONTROL 在目标分辨率间保留裁切内容]** | 在相同的宽高比中维护裁剪内容 | 在创建智能裁剪配置文件时使用。<br>取消选中此选项，可针对不同分辨率的给定宽高比生成新的裁剪内容（同时仍保持焦点）。<br>如果决定取消勾选此框，请确保原始图像分辨率大于您为智能裁剪配置文件定义的分辨率。<br><br>例如，假定您已将宽高比设置为600 x 600（大）、400 x 400（中）和300 x 300（小）。<br>When **[!UICONTROL 跨目标分辨率保留裁剪内容]** 选项 *已检查*，则所有三种分辨率中都会看到相同的裁剪，这与以下图像示例输出类似（仅供说明用途）：<br>![选中选项](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>When **[!UICONTROL 跨目标分辨率保留裁剪内容]** 选项 *未选中*，则所有三种分辨率的裁剪内容都是新的，与以下图像示例输出类似（仅供说明用途）：<br>![未选中选项](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### 智能裁切和颜色色板支持的图像文件格式

支持的最大输入文件大小分辨率为16K。

| 图像格式 | 文件扩展名不区分大小写 | MIME类型 | 支持的输入色彩空间 | 支持的最大输入文件大小 | 是否支持图像格式？ |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | 是 |
| EPS |  |  |  |  | 否 |
| GIF | `.gif` | image/gif | sRGB | 15 GB | 是；动画GIF的第一帧用于演绎版。 不能配置或更改第一帧。 |
| JPEG | `.jpg` 和 `.jpeg` | image/jpeg | sRGB | 15 GB | 是 |
| PNG | `.png` | image/png | sRGB | 15 GB | 是 |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | 是 |
| SVG |  |  |  |  | 否 |
| TIFF | `.tif` 和 `.tiff` | image/tiff | sRGB<br>CMYK | 4 GB | 是 |
| WebP/动画WebP |  |  |  |  | 否 |

## 创建Dynamic Media图像配置文件 {#creating-image-profiles}

要为其他资产类型定义高级处理参数，请参阅 [配置资产处理](config-dm.md#configuring-asset-processing).

请参阅 [关于Dynamic Media图像配置文件和视频配置文件](/help/assets/dynamic-media/about-image-video-profiles.md).

另请参阅[组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md)。

**要创建Dynamic Media图像配置文件，请执行以下操作：**

1. 选择Adobe Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 要添加图像配置文件，请选择 **[!UICONTROL 创建]**.
1. 输入USM锐化、裁切或色板的配置文件名称和值，或同时输入两者。

   提示：使用特定于其预期目的的配置文件名称。 例如，假定您要创建仅生成色板的配置文件。 即，禁用（关闭）智能裁剪，启用（打开）颜色和图像色板。 在这些情况下，您可以使用配置文件名称“Smart Swatches”。

   另请参阅[智能裁切和智能色板选项](#crop-options)和[钝化蒙版](#unsharp-mask)。

   ![农作物](assets/crop.png)

1. 选择&#x200B;**[!UICONTROL “保存”]**。此时新创建的配置文件会显示在可用配置文件列表中。

## 编辑或删除Dynamic Media图像配置文件 {#editing-or-deleting-image-profiles}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要编辑或删除的图像配置文件。要编辑它，请选择 **[!UICONTROL 编辑图像处理配置文件]**. 要删除它，请选择 **[!UICONTROL 删除图像处理配置文件]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果是进行编辑操作，请保存更改。如果是进行删除操作，请确认您要删除配置文件。

## 将Dynamic Media图像配置文件应用到文件夹 {#applying-an-image-profile-to-folders}

当您将图像配置文件分配给文件夹后，该文件夹中的所有子文件夹都会自动继承父文件夹的配置文件。 因此，您只能为一个文件夹分配一个图像配置文件。 因此，您在上传、存储、使用资产以及将资产存档的过程中，请妥善安排文件夹结构。

如果您为文件夹分配了其他图像配置文件，则新配置文件会覆盖之前的配置文件。以前存在的文件夹资产将保持不变。新配置文件会应用于稍后添加到文件夹的资产。

用户界面中会指示为其分配了配置文件的文件夹，卡片中会显示配置文件的名称。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以将图像配置文件应用到特定文件夹或全局应用到所有资产。

您可以重新处理文件夹中的资产，该文件夹中已有您稍后更改的图像配置文件。 请参阅 [编辑文件夹中的资产处理配置文件后，会重新处理该文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### 将Dynamic Media图像配置文件应用到特定文件夹 {#applying-image-profiles-to-specific-folders}

您可以在 **[!UICONTROL 工具]** 菜单，或者如果您在文件夹中， **[!UICONTROL 属性]**.

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

您可以重新处理文件夹中已有视频配置文件且稍后进行了更改的资产。 请参阅 [编辑文件夹中的资产处理配置文件后，会重新处理该文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### 将Dynamic Media图像配置文件从配置文件用户界面应用到文件夹 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要应用于一个或多个文件夹的图像配置文件。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 选择 **[!UICONTROL 将处理配置文件应用到文件夹]** ，然后选择一个或多个用于接收新上传资产的文件夹，然后选择 **[!UICONTROL 应用]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

#### 将Dynamic Media图像配置文件从属性应用到文件夹 {#applying-image-profiles-to-folders-from-properties}

1. 点按Experience Manager徽标，然后导航到 **[!UICONTROL 资产]**.
1. 导航到 *文件夹* （不是资产）。
1. 根据您所在的视图，执行以下操作之一：
   * 在“卡片视图”中，将指针悬停在文件夹上，然后选择复选标记以将其选中。
   * 在列视图或列表视图中，选中文件夹名称左侧的复选框。
1. 在工具栏中，选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL Dynamic Media处理]** 选项卡。
1. 在 **[!UICONTROL 图像配置文件]**，从 **[!UICONTROL 配置文件名称]** 下拉列表中，选择要应用的用户档案。
1. 在页面的右上角附近，选择 **[!UICONTROL 保存并关闭]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全局应用Dynamic Media图像配置文件 {#applying-an-image-profile-globally}

除了将配置文件应用到文件夹之外，您还可以全局应用一个配置文件。 任何文件夹中上传到Experience Manager Assets的任何内容都会应用选定的配置文件。

您可以重新处理文件夹中已有视频配置文件且稍后进行了更改的资产。 请参阅 [编辑文件夹中的资产处理配置文件后，会重新处理该文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**要全局应用Dynamic Media图像配置文件，请执行以下操作：**

1. 执行下列操作之一：

   * 导航到 `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` ，然后应用相应的用户档案并选择 **[!UICONTROL 保存]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 导航到CRXDE Lite到以下节点： `/content/dam/jcr:content`.

      添加属性 `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` 选择 **[!UICONTROL 全部保存]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 编辑单个图像的智能裁剪或智能色板 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>Adobe建议您查看生成的任何智能作物和智能色板，以确保它们与您的品牌和价值相关且适当。

您可以手动重新调整图像的智能裁剪窗口大小或调整其大小，以进一步优化其焦点。

编辑智能裁剪并保存后，所做的更改会传播到您对特定图像使用裁剪的所有位置。

>[!IMPORTANT]
>
>手动重新调整资产的智能裁剪窗口大小或调整其大小时，即使您稍后决定重新处理资产，也会维护并保留该编辑。 但是，如果您在 **[!UICONTROL 响应式图像裁剪]** ，则会重新处理该资产。
>请参阅 [在文件夹中重新处理Dynamic Media资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

如有必要，您可以重新运行智能裁剪以再次生成其他裁剪。

另请参阅 [编辑多幅图像的智能裁切或智能色板](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**要编辑单个图像的智能裁切或智能色板，请执行以下操作：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]**，然后转到应用了智能裁剪或智能色板图像配置文件的文件夹。
1. 要打开其内容，请选择文件夹。
1. 选择要调整其智能裁剪或智能色板的图像。
1. 在工具栏中，选择 **[!UICONTROL 智能裁剪]**.

1. 执行以下操作之一：

   * 在页面的右上角附近，向左或向右拖动滑块条以分别增加或减少图像显示。
   * 在图像上，拖动角手柄以调整裁剪或色板可查看区域的大小。
   * 在图像上，将框/色板拖到新位置。 您只能编辑图像色板；颜色色板是静态的。
   * 在图像上方，选择  **[!UICONTROL 还原]** 撤消所有编辑并恢复原始裁剪或色板。
   * 使用键盘箭头键裁剪帧大小，或调整图像位置，或者同时调整两者。

1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 关闭]** ，以返回到资产文件夹。

## 编辑多幅图像的智能裁切或智能色板 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

将包含智能裁剪的图像配置文件应用到文件夹后，该文件夹中的所有图像都会对其应用裁剪。 如果需要，您可以 *手动* 重新调整多幅图像中智能裁剪窗口的大小或调整其大小，以进一步优化其焦点。

编辑智能裁剪并保存后，所做的更改会传播到您对特定图像使用裁剪的所有位置。

>[!IMPORTANT]
>
>手动重新调整多个资产的智能裁剪窗口大小或调整其大小时，即使您稍后决定重新处理这些资产，也会维护并保留这些编辑。 不过，如果您在图像配置文件的&#x200B;**[!UICONTROL 响应式图像裁切]**区域中编辑宽度和/或高度，则这些资源需要重新处理。
>请参阅 [在文件夹中重新处理Dynamic Media资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

如有必要，您可以重新运行智能裁剪以再次生成其他裁剪。

**要编辑多幅图像的智能裁切或智能色板，请执行以下操作：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]**，然后转到应用了智能裁剪或智能色板图像配置文件的文件夹。
1. 在文件夹中，选择 **[!UICONTROL 更多操作]** (...)图标，然后选择 **[!UICONTROL 智能裁剪]**.

1. 在 **[!UICONTROL 编辑智能裁剪]** ，请执行以下任一操作：

   * 调整页面上图像的查看大小。

      在断点名称下拉列表的右侧，向左或向右拖动滑块以更改可查看图像显示的大小。

      ![edit_smart_crobs_sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根据断点名称过滤可查看图像的列表。 在以下示例中，图像是在断点名称“Medium”上过滤的。

      在页面的右上角附近，从下拉列表中，选择一个断点名称以过滤您看到的图像。 （请参阅上图。）

      ![edit_smart_crobs_dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 调整智能裁剪框的大小。 执行以下任一操作：

      * 如果图像仅具有智能裁剪或智能色板，请在图像上拖动裁剪框的角手柄。 调整裁剪可查看区域的大小。
      * 如果图像同时具有智能裁切和智能色板，请在图像上拖动裁剪框的角手柄。 调整裁剪可查看区域的大小。 或者，选择图像下方的智能色板（颜色色板为静态色板），然后拖动裁剪框的角手柄。 调整样本可查看区域的大小。

      ![调整图像的智能裁剪大小](assets/edit_smart_crops-resize.png).

   * 移动智能裁剪框。 执行以下任一操作：

      * 如果图像仅具有智能裁剪或智能色板，则在图像上将裁剪框拖到新位置。
      * 如果图像同时具有智能裁切和智能色板，则在图像上，将智能裁切框拖到新位置。 或者，选择图像下方的智能色板（颜色色板为静态色板），然后将智能色板裁剪框拖到新位置。

      ![edit_smart_crobs_move](assets/edit_smart_crops-move.png)

   * 撤消所有编辑并恢复原始智能裁剪或智能色板（仅适用于当前编辑会话）。

      选择 **[!UICONTROL 还原]** 图像上方。

      ![edit_smart_crobs_revert](assets/edit_smart_crops-revert.png)



1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 关闭]** ，以返回到资产文件夹。

## 将图像配置文件从文件夹删除 {#removing-an-image-profile-from-folders}

当您将图像配置文件从文件夹删除后，该文件夹中的所有子文件夹都会自动删除从父文件夹继承的配置文件。但是，对文件夹中已发生的文件的任何处理均将保持不变。

您可以从 **[!UICONTROL 工具]** 菜单，或者如果您在文件夹中， **[!UICONTROL 属性]**.

### 通过Profiles用户界面将Dynamic Media图像配置文件从文件夹删除 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要从一个或多个文件夹中删除的图像配置文件。
1. 选择 **[!UICONTROL 从文件夹删除处理配置文件]** ，然后选择一个或多个要从中删除配置文件的文件夹，然后选择 **[!UICONTROL 删除]**.

   您可以确认图像配置文件不再应用于文件夹，因为文件夹名称的下方不再显示该名称。

### 通过属性将Dynamic Media图像配置文件从文件夹删除 {#removing-image-profiles-from-folders-via-properties}

1. 选择Experience Manager徽标并导航 **[!UICONTROL 资产]** ，然后转到要从中删除图像配置文件的文件夹。
1. 在文件夹中，选择复选标记以将其选中，然后选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL 图像配置文件]** 选项卡。
1. 从 **[!UICONTROL 配置文件名称]** 下拉列表中，选择 **[!UICONTROL 无]**，然后选择 **[!UICONTROL 保存并关闭]**.

   如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。
