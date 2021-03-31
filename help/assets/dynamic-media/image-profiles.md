---
title: Dynamic Media 图像配置文件
description: “了解如何创建包含USM锐化设置、智能裁切或智能色板，或同时包含这两个设置的Dynamic Media图像用户档案。 然后，将用户档案应用到图像资产的文件夹。”
feature: 资产管理，图像用户档案，演绎版
topic: 商务从业人员
role: 商务从业人员
translation-type: tm+mt
source-git-commit: 497952b1b6679eca301839d1435924e16a2e2438
workflow-type: tm+mt
source-wordcount: '2707'
ht-degree: 14%

---


# Dynamic Media 图像配置文件 {#image-profiles}

上传图像时，您可以通过将图像用户档案应用到文件夹，在上传时自动裁剪图像。

>[!IMPORTANT]
>
>图像用户档案不适用于PDF、动画GIF或INDD(Adobe InDesign)文件。

## 裁剪选项{#crop-options}

<!-- CQDOC-16069 for the paragraph directly below -->

智能裁剪坐标取决于长宽比。 对于图像用户档案中的智能裁剪设置，如果对于图像用户档案中添加的尺寸，宽高比相同，则会向Dynamic Media发送相同的宽高比。 Adobe建议您使用相同的裁剪区域。 这样做可确保不会影响在图像用户档案中使用的不同尺寸。

您创建的每个智能裁剪生成都需要额外处理。 例如，添加五个以上的智能裁剪长宽比会导致资产摄取速率降低。 它还可能增加系统的负载。 由于您可以在文件夹级别应用智能裁剪，因此Adobe建议您仅在需要智能裁剪的文件夹&#x200B;**&#x200B;中使用智能裁剪。

您有两个要从中选择的图像裁剪选项。 您还可以选择自动创建颜色和图像色板。

<table>
 <tbody>
  <tr>
   <td><strong>选项</strong></td>
   <td><strong>何时使用</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>像素裁剪</td>
   <td>仅根据尺寸批量裁切图像。</td>
   <td><p>要使用此选项，请从“裁剪选项”下拉列表中选择<strong>像素裁剪</strong>。</p> <p>要从图像的侧边进行裁剪，请输入要从图像的任一侧边或各个侧边裁剪的像素数。裁剪的图像多少取决于图像文件中的 ppi（每英寸像素数）设置。</p> <p>图像用户档案像素裁切按以下方式呈现：<br /> </p>
    <ul>
     <li>值为“顶”、“底”、“左”和“右”。</li>
     <li>左上角被视为0,0，并从那里计算像素裁剪。</li>
     <li>裁切起点：左为X，上为Y</li>
     <li>水平计算：原始图像的水平像素尺寸减去“左”，然后减去“右”。</li>
     <li>垂直计算：垂直像素高度减去“顶部”，然后减去“底部”。</li>
    </ul> <p>例如，假设您有一张4000 x 3000像素的图像。 您使用以下值：顶部=250，底部=500，左侧=300，右侧=700。</p> <p>使用(4000-300-700、3000-250-500或3000、2250)的填充空间从左上角(300,250)进行裁剪。</p> </td>
  </tr>
  <tr>
   <td>智能裁剪</td>
   <td>根据图像的可视焦点批量裁剪图像。</td>
   <td><p>Smart Crop利用Adobe Sensei中人工智能的强大功能快速实现图像批量裁剪的自动化。 Smart Crop可自动检测并裁切到任何图像的焦点，以捕获预期的目标点，而不管屏幕大小。</p> <p>要使用智能裁剪，请从“裁剪选项”下拉列表中选择<strong>智能裁剪</strong>，然后在响应式图像裁剪的右侧，启用（打开）该功能。</p> <p>默认的断点大小（大、中、小）涵盖大多数图像在移动和平板电脑设备、桌面和横幅上使用的所有大小。 如果需要，您可以编辑默认名称“大”、“中”和“小”。</p> <p>要添加更多断点，请单击<strong>添加裁剪</strong>;要删除裁剪，请单击垃圾桶图标。</p> </td>
  </tr>
  <tr>
   <td>颜色和图像样本</td>
   <td>批量为每个图像生成一个图像样本。</td>
   <td><p><strong>注意</strong>:Dynamic Media Classic中不支持智能色板。</p> <p>从显示颜色或纹理的产品图像自动定位和生成高质量色板。</p> <p>要使用颜色和图像色板，请从“裁剪选项”下拉列表中选择<strong>智能裁剪</strong>。 然后，在“颜色和图像色板”的右侧，启用（打开）该功能。 在"宽度"和"高度"文本框中输入像素值。</p> <p>虽然所有图像裁剪都可从演绎版边栏中使用，但只能通过复制URL功能使用色板。 使用您自己的查看组件在您的站点上呈现色板。 此规则的例外是传送横幅。 Dynamic Media为传送横幅中使用的色板提供了查看组件。</p> <p><strong>使用图像色板</strong></p> <p>图像色板的URL很简单：</p> <p><code>/is/image/company/&lt;asset_name&gt;:Swatch</code></p> <p>其中<code>:Swatch</code>会附加到资产请求。</p> <p><strong>使用色板</strong></p> <p>要使用色板，请使用以下命令发出<code>req=userdata</code>请求：</p> <p><code>/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata</code></p> <p>例如，以下是Dynamic Media Classic中的色板资源：</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch</code></p> <p>下面是色板资产的相应<code>req=userdata</code> URL:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata</code></p> <p><code>req=userdata</code>响应如下：</p> <p><code class="code">SmartCropDef=Swatch
       SmartCropHeight=200.0
       SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200
       SmartCropType=Swatch
       SmartCropWidth=200.0
       SmartSwatchColor=0xA56DB2</code></p> <p>您还可以以XML或JSON格式请求<code>req=userdata</code>响应，如以下各个URL示例所示：</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml</code></p><p><code>SmartSwatchColor</code></p><p></p></td></tr></tbody></table>

## USM 锐化 {#unsharp-mask}

使用&#x200B;**[!UICONTROL 钝化蒙版]**&#x200B;对最终取样缩小的图像微调锐化滤镜效果。您可以控制效果的强度、效果的半径（以像素为单位）以及被忽略的对比度阈值。 此效果使用与 Adobe Photoshop 的“钝化蒙蔽”滤镜相同的选项。

>[!NOTE]
>
>USM锐化仅应用于PTIFF（金字塔tiff）中缩减采样率超过50%的缩小演绎版。 这意味着ptiff中最大的演绎版不会受USM锐化的影响。 但是，缩略图等较小的演绎版会发生更改（并显示USM锐化）。

在&#x200B;**[!UICONTROL USM锐化]**&#x200B;中，您有以下筛选选项：

<table>
 <tbody>
  <tr>
   <td><strong>选项</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>数量</td>
   <td>控制应用于边缘像素的对比度量。 默认为1.75。对于高分辨率图像，最高可将其增加到5。 可以考虑使用数量来衡量滤镜强度。范围是0-5。</td>
  </tr>
  <tr>
   <td>半径</td>
   <td>确定边缘像素周围影响锐化的像素数量。对于高分辨率图像，输入 1 到 2。低值仅锐化边缘像素；高值锐化较宽范围的像素。正确的值取决于图像大小。默认值为0.2。范围为0-250。</td>
  </tr>
  <tr>
   <td>阈值</td>
   <td><p>确定应用USM锐化滤镜时要忽略的对比度范围。换句话说，此选项确定锐化的像素与周围区域必须有多大的不同，才能被视为边缘像素并进行锐化。 要避免引入杂色，请尝试使用0到255之间的值。</p> </td>
  </tr>
 </tbody>
</table>

有关“锐化”的说明，请参阅[锐化图像。](/help/assets/dynamic-media/assets/sharpening_images.pdf)

## 创建Dynamic Media Image用户档案{#creating-image-profiles}

要为其他资产类型定义高级处理参数，请参阅[配置资产处理](config-dm.md#configuring-asset-processing)。

请参阅[关于Dynamic Media图像用户档案和视频用户档案](/help/assets/dynamic-media/about-image-video-profiles.md)。

另请参阅[组织数字资产以使用处理配置文件的最佳实践](/help/assets/dynamic-media/best-practices-for-file-management.md)。

**创建Dynamic Media图像用户档案**

1. 点按AEM徽标，然后导航到&#x200B;**[!UICONTROL 工具>资产>图像用户档案]**。
1. 要添加图像用户档案，请点按&#x200B;**[!UICONTROL 创建]**。
1. 输入用户档案名称，以及USM锐化、裁剪或色板或两者的值。

   提示：使用特定于其预期目的的用户档案名称。 例如，假设您要创建只生成色板的用户档案。 即，禁用（关闭）“智能裁剪”，启用（打开）“颜色和图像色板”。 在这种情况下，您可以使用用户档案名称“智能色板”。

   另请参阅[智能裁切和智能色板选项](#crop-options)和[钝化蒙版](#unsharp-mask)。

   ![裁剪](assets/crop.png)

1. 点按&#x200B;**[!UICONTROL 保存]**。此时新创建的配置文件会显示在可用配置文件列表中。

## 编辑或删除Dynamic Media图像用户档案{#editing-or-deleting-image-profiles}

1. 点按AEM徽标，然后导航到&#x200B;**[!UICONTROL 工具>资产>图像用户档案]**。
1. 选择要编辑或删除的图像用户档案。要编辑图像，请选择&#x200B;**[!UICONTROL 编辑图像处理用户档案]**。 要删除图像，请选择&#x200B;**[!UICONTROL 删除图像处理用户档案]**。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果是进行编辑操作，请保存更改。如果是进行删除操作，请确认您要删除配置文件。

## 将Dynamic Media图像用户档案应用到文件夹{#applying-an-image-profile-to-folders}

当您将图像用户档案分配给文件夹后，该文件夹中的所有子文件夹都会自动继承父文件夹的用户档案。 因此，您只能为一个文件夹分配一个图像用户档案。 因此，您在上传、存储、使用资产以及将资产存档的过程中，请妥善安排文件夹结构。

如果为文件夹分配了其他图像用户档案，则新用户档案将覆盖之前的用户档案。此前存在的文件夹资产将保持不变。新用户档案将应用于稍后添加到该文件夹的资产。

在用户界面中，会指示为其分配了用户档案的文件夹，卡中会显示用户档案的名称。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以将图像用户档案应用到特定文件夹或全局应用到所有资产。

您可以重新处理文件夹中的资产，该文件夹已经有您稍后更改的现有图像用户档案。 请参阅[编辑文件夹的处理配置文件后重新处理该文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

### 将Dynamic Media图像用户档案应用到特定文件夹{#applying-image-profiles-to-specific-folders}

您可以在&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中将图像用户档案应用到文件夹；如果您在文件夹中，也可以从&#x200B;**[!UICONTROL 属性]**&#x200B;中应用。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

您可以重新处理文件夹中的资产，该文件夹已经有您稍后更改的现有视频用户档案。 请参阅[编辑文件夹的处理配置文件后重新处理该文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

#### 将Dynamic Media Image用户档案从用户档案用户界面{#applying-image-profiles-to-folders-from-profiles-user-interface}应用到文件夹

1. 点按AEM徽标，然后导航到&#x200B;**[!UICONTROL 工具>资产>图像用户档案]**。
1. 选择要应用到一个或多个文件夹的图像用户档案。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 点按&#x200B;**[!UICONTROL 将处理用户档案应用到文件夹]**，选择要用于接收新上传资产的一个或多个文件夹，然后点按/单击&#x200B;**[!UICONTROL 应用]**。 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

#### 从属性{#applying-image-profiles-to-folders-from-properties}将Dynamic Media图像用户档案应用到文件夹

1. 点按AEM徽标，然后导航到&#x200B;**[!UICONTROL 资产]**，然后导航到您要对其应用图像用户档案的文件夹。
1. 在文件夹中，点按复选标记以将其选中，然后点按&#x200B;**[!UICONTROL 属性]**。
1. 点按&#x200B;**[!UICONTROL 图像配置文件]**&#x200B;选项卡。从&#x200B;**[!UICONTROL 配置文件名称]**&#x200B;下拉列表中，选择配置文件，然后点按&#x200B;**[!UICONTROL 保存并关闭]**。如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全局应用Dynamic Media图像用户档案{#applying-an-image-profile-globally}

除了将用户档案应用到文件夹外，您还可以全局应用一个。 上传到任何文件夹中的Experience Manager资产的任何内容均已应用选定的用户档案。

您可以重新处理文件夹中的资产，该文件夹已经有您稍后更改的现有视频用户档案。 请参阅[编辑文件夹的处理配置文件后重新处理该文件夹中的资产](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。

**要全局应用Dynamic Media图像用户档案**:

1. 执行下列操作之一：

   * 导航到`https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam`并应用相应的用户档案，然后点按&#x200B;**[!UICONTROL 保存]**。

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 导航到CRXDE Lite到以下节点：`/content/dam/jcr:content`。

      添加属性`imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>`并点按&#x200B;**[!UICONTROL 保存全部]**。

      ![configure_image_用户档案](assets/configure_image_profiles.png)

## 编辑单个图像{#editing-the-smart-crop-or-smart-swatch-of-a-single-image}的智能裁剪或智能色板

您可以手动重新对齐图像的智能裁剪窗口或调整其大小以进一步调整其焦点。

在编辑智能裁剪并保存后，更改会传播到您对特定图像使用裁剪的所有位置。

如有必要，您可以重新运行智能裁剪以再次生成其他裁剪。

另请参阅[编辑多个图像的智能裁剪或智能色板](#editing-the-smart-crop-or-smart-swatch-of-multiple-images)。

**编辑单个图像的智能裁剪或智能色板**

1. 点按AEM徽标，然后导航到&#x200B;**[!UICONTROL 资产]**，然后导航到应用了智能裁剪或智能色板图像用户档案的文件夹。

1. 要打开其内容，请点按文件夹。
1. 点按要调整其智能裁剪或智能色板的图像。
1. 在工具栏中，点按&#x200B;**[!UICONTROL 智能裁剪]**。

1. 执行以下操作之一：

   * 在页面的右上角附近，向左或向右拖动滑块条以分别增加或减少图像显示。
   * 在图像上，拖动角手柄以调整裁剪或色板的可查看区域的大小。
   * 在图像上，将框/色板拖动到新位置。 只能编辑图像色板；色板是静态的。
   * 在图像上方，点按&#x200B;**[!UICONTROL 还原]**&#x200B;以撤消您所做的所有编辑并恢复原始裁剪或色板。
   * 使用键盘箭头键裁剪帧大小或重新定位图像，或同时裁剪两者。

1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 保存]**，然后点按&#x200B;**[!UICONTROL 关闭]**&#x200B;以返回到资产文件夹。

## 编辑多个图像的智能裁剪或智能色板{#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

将包含智能裁剪的图像用户档案应用到文件夹后，该文件夹中的所有图像都应用了裁剪。 如果需要，您可以手动&#x200B;**&#x200B;重新对齐或调整多个图像中的智能裁剪窗口的大小，以进一步调整其焦点。

在编辑智能裁剪并保存后，更改会传播到您对特定图像使用裁剪的所有位置。

如有必要，您可以重新运行智能裁剪以再次生成其他裁剪。

**编辑多个图像的智能裁剪或智能色板**

1. 点按AEM徽标，然后导航到&#x200B;**[!UICONTROL 资产]**，然后导航到应用了智能裁剪或智能色板图像用户档案的文件夹。
1. 在文件夹中，点按&#x200B;**[!UICONTROL 更多操作]**(...)图标，然后点按&#x200B;**[!UICONTROL 智能裁剪]**。

1. 在&#x200B;**[!UICONTROL 编辑智能裁切]**&#x200B;页面上，执行下列任一操作：

   * 调整页面上图像的查看大小。

      在断点名称下拉列表的右侧，向左或向右拖动滑块以更改可查看图像显示的大小。

      ![edit_smart_crobs_sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根据断点名称过滤可查看图像的列表。 在以下示例中，图像会在断点名称“Medium”上筛选。

      在页面右上角附近的下拉列表中，选择一个断点名称以筛选您看到的图像。 （请参阅上图。）

      ![edit_smart_crobs_dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 调整智能裁剪框的大小。 执行下列任一操作：

      * 如果图像仅包含智能裁剪或智能色板，请在图像上拖动裁剪框的角手柄。 调整裁剪的可视区域的大小。
      * 如果图像同时具有智能裁剪和智能色板，请在图像上拖动裁剪框的角手柄。 调整裁剪的可视区域的大小。 或者，点按图像下方的智能色板（色板是静态的），然后拖动裁剪框的角手柄。 调整色板可查看区域的大小。

      ![调整图像的智能裁剪大小。](assets/edit_smart_crops-resize.png)

   * 移动智能裁剪框。 执行下列任一操作：

      * 如果图像仅具有智能裁剪或智能色板，则在图像上将裁剪框拖动到新位置。
      * 如果图像同时具有智能裁剪和智能色板，则在图像上，将智能裁剪框拖动到新位置。 或者，点按或单击图像下方的智能色板（色板是静态的），然后将智能色板裁剪框拖到新位置。

      ![edit_smart_crobs_move](assets/edit_smart_crops-move.png)

   * 撤消所有编辑并恢复原始智能裁剪或智能色板（仅适用于当前编辑会话）。

      点按图像上方的&#x200B;**[!UICONTROL 还原]**。

      ![edit_smart_crobs_revert](assets/edit_smart_crops-revert.png)



1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 保存]**，然后点按&#x200B;**[!UICONTROL 关闭]**&#x200B;以返回到资产文件夹。

## 从文件夹{#removing-an-image-profile-from-folders}删除图像用户档案

当您将图像用户档案从文件夹删除后，该文件夹中的所有子文件夹都会自动删除从父文件夹继承的用户档案。但是，对文件夹中已发生的文件的任何处理都将保持不变。

您可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中的文件夹删除图像用户档案；如果您在文件夹中，也可以从&#x200B;**[!UICONTROL 属性]**&#x200B;中删除。

### 通过用户档案用户界面{#removing-image-profiles-from-folders-via-profiles-user-interface}将Dynamic Media Image用户档案从文件夹删除

1. 点按AEM徽标，然后导航到&#x200B;**[!UICONTROL 工具>资产>图像用户档案]**。
1. 选择要从一个或多个文件夹删除的图像用户档案。
1. 点按&#x200B;**[!UICONTROL 从文件夹]**&#x200B;中删除处理用户档案，然后选择一个或多个要用于从中删除用户档案的文件夹，然后点按&#x200B;**[!UICONTROL 删除]**。

   您可以确认图像用户档案不再应用于文件夹，因为文件夹名称下不再显示该名称。

### 通过属性{#removing-image-profiles-from-folders-via-properties}将Dynamic Media图像用户档案从文件夹删除

1. 点按AEM徽标，然后导航&#x200B;**[!UICONTROL 资产]**，然后导航到您要从中删除图像用户档案的文件夹。
1. 在文件夹中，点按复选标记以选择它，然后点按&#x200B;**[!UICONTROL 属性]**。
1. 选择&#x200B;**[!UICONTROL 图像用户档案]**&#x200B;选项卡。
1. 从&#x200B;**[!UICONTROL 用户档案名称]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 无]**，然后点按&#x200B;**[!UICONTROL 保存并关闭]**。

   如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。
