---
title: 如何管理 [!DNL Dynamic Media] 模板？
description: 了解如何使用WYSIWYG模板编辑器创建 [!DNL Dynamic Media] 模板并包含多个图像、文本和形状图层，以快速创建横幅和传单，并在下游应用程序中使用它们。
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: 97be1d044ae23859e263756116c8bac8701178b4
workflow-type: tm+mt
source-wordcount: '3779'
ht-degree: 1%

---


# [!DNL Dynamic Media]模板{#dynamic-media-templates}

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

使用[!DNL Dynamic Media]模板(WYSIWYG模板编辑器)为您的横幅和传单创建实时可自定义的模板。 发布[!DNL Dynamic Media]模板并将其用于下游应用程序。 [!DNL Dynamic Media]模板包含图像和文本图层。 向模板的图像和文本图层添加参数，并使用[[!DNL Dynamic Media] URL](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media)重新定位图层并调整其大小以及实时更新其内容。

一些主要功能包括：

* **[!DNL Dynamic Media]WYSIWYG模板编辑器：**&#x200B;创建带有图像和文本图层的可自定义横幅。
* **层参数化：**&#x200B;为层定义动态键值对以启用实时更新。
* **[!DNL Dynamic Media]URL支持：**&#x200B;为模板使用[!DNL Dynamic Media] URL，集成来自第一方或第三方应用程序的个性化值。
* **图层可见性控件：**&#x200B;根据需要动态隐藏或显示图层。
* **智能文本调整大小：**&#x200B;自动调整文本大小以适合指定的区域。

[!DNL Dynamic Media]模板的一些主要优势包括：

* **优化1:1 Personalization：**&#x200B;根据实时客户信号定制内容。
* **减少手动工作：**&#x200B;自动化并加快内容创建和管理。
* **确保一致的全渠道体验：**&#x200B;保持跨渠道的品牌一致性。
* **有效地重用内容：**&#x200B;避免使用单次的内容，并通过动态的参数化模板进行缩放。
* **降低风险：**&#x200B;实时更新定价、折扣和链接。
* **增强客户参与度：**&#x200B;推动交互式、与上下文相关的体验。

>[!NOTE]
>
>订阅增强安全性SKU的客户无法在该云服务计划中使用任何[!DNL Dynamic Media]功能，包括[!DNL Dynamic Media]模板。

在此视频中了解如何分步创建[!DNL Dynamic Media]模板。

>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## 开始之前{#prerequisites-for-dynamic-media-wysiwyg-template}

满足以下要求以创建[!DNL Dynamic Media]模板并生成其投放URL：

1. 访问[!DNL Dynamic Media]。
1. 在[!DNL Assets View]主页上，您有一个文件夹位于&#x200B;**[!UICONTROL Dynamic Media Assets]**&#x200B;中以保存您的模板。 [在](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view)Assets![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL 中创建文件夹&#x200B;]**&#x200B;以在&#x200B;**[!UICONTROL &#x200B; Dynamic Media Assets &#x200B;]**&#x200B;中复制该文件夹。
1. [将 [!DNL AEM Assets] 实例中可用的图像与 [!DNL Dynamic Media] 同步，以将其用于创建模板](/help/assets/dynamic-media/config-dm.md)。
1. 发布要在创建模板时使用的图像，以便在创建模板后生成模板的投放URL。 投放URL可用于下游应用程序。
1. 若要在模板的文本图层中使用默认[!UICONTROL Adobe Sans F2]字体以外的字体，请[同时将该字体文件上载并发布到AEM和Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation)。 [支持的字体文件格式为：AFM、OTF、PFB、PFM、PhotoFont、TTC、TTF](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats)。 另外，请确保[重新处理](/help/assets/reprocessing-assets-view.md)要使用的现有字体。 有关详细信息，请参阅[字体](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/support-files/fonts)。<!--(On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**)-->
1. 在触屏UI中验证以下内容：
   * 在&#x200B;**[!UICONTROL 编辑[!DNL Dynamic Media]配置页面]**&#x200B;上，默认情况下设置为&#x200B;**[!UICONTROL [!DNL Dynamic Media]禁用的]**&#x200B;同步模式&#x200B;**[!UICONTROL 未应用于所有AEM文件夹（]**&#x200B;同步所有内容&#x200B;**[!UICONTROL 未选中）。]**&#x200B;有关详细信息，请参阅[配置Dynamic Media Cloud Service](/help/assets/dynamic-media/config-dm.md)。
   * **[!UICONTROL [!DNL Dynamic Media]同步模式]**&#x200B;设置为目标文件夹或子文件夹的子文件夹&#x200B;**[!UICONTROL 启用]**&#x200B;创建后保存模板。 有关详细信息，请参阅[配置 [!DNL Dynamic Media] Cloud Service](/help/assets/dynamic-media/config-dm.md)。

## 创建[!DNL Dynamic Media]模板{#how-to-create-dynamic-media-template}

执行以下步骤以创建[!DNL Dynamic Media]模板：

<!--
1. Navigate to your [!DNL Assets View] and [create a folder](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**. The folder tree in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** replicates in **[!UICONTROL Dynamic Media Assets]**. Save your [!DNL Dynamic Media] template in this [!UICONTROL Dynamic Media Assets] folder.
1. Select ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** and [upload and publish your images to [!DNL AEM] and [!DNL Dynamic Media] simultaneously](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm#dynamic-media-publish-mode-set-to-upon-activation) to use them in creating the template. Publishing images is required to generate the template's delivery URL, after creating the template. The delivery URL can be used in downstream applications.
1. [Execute these asset uploading and publishing steps](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation) to upload and publish a font file to AEM and Dynamic Media simultaneously to use it in creating the template. [!UICONTROL Adobe Sans F2] is the only default font available in the text layer. [The supported font file formats are, AFM, OTF, PFB, PFM, PhotoFont, TTC, TTF](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats). Ensure to [reprocess](/help/assets/reprocessing-assets-view.md) the existing fonts to use them in creating the template (On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**). See [Fonts](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/support-files/fonts) to know more about fonts.
-->

1. [创建空白画布](#create-a-canvas)
1. [将图像添加到画布](#add-images-to-the-canvas)
1. [在画布中添加文本图层](#add-text-to-the-canvas)
1. [将形状添加到画布](#add-shapes-to-the-canvas)
1. [编辑或删除图层](#edit-or-delete-a-layer)
1. [参数化图层](#parameterise-a-layer)

### 创建空白画布{#create-a-canvas}

执行以下步骤可创建空白画布：

1. 导航到[!DNL Assets View]，选择左侧面板中可用的&#x200B;**[!UICONTROL Dynamic Media Assets]**，然后导航到您的文件夹以将您的模板保存在该文件夹中。

   ![Dynamic Media 模板](/help/assets/assets/DM-Assets1.png)

1. 选择&#x200B;**[!UICONTROL 创建模板]**。 此时将显示&#x200B;**[!UICONTROL 新模板]**&#x200B;对话框。

   ![如何创建可实时自定义的动态模板](/help/assets/assets/new-template.png)

   >[!NOTE]
   >
   >  模板将保存在创建该模板的位置。 在[!DNL Assets View]主页上，选择&#x200B;**[!UICONTROL Dynamic Media Assets]**，然后单击&#x200B;**[!UICONTROL 创建模板]**&#x200B;以将模板保存在&#x200B;**[!UICONTROL Dynamic Media Assets]**&#x200B;根文件夹中。

1. 指定模板名称，定义画布宽度和高度，然后单击&#x200B;**[!UICONTROL 创建]**。 屏幕上会显示一个空白画布，画布的两侧都有用于创建模板的菜单选项。 将鼠标悬停在菜单选项上可查看其工具提示。
   ![实时可自定义模板](/help/assets/assets/blank-canvas-page.png)

   >[!NOTE]
   >
   > 允许的宽度和高度范围是50到5000。

**右窗格中的菜单选项：**&#x200B;使用这些选项将必要的图像和文本图层添加到画布中。

* ![DM模板](/help/assets/assets/add-image.svg)：单击以将图像添加到画布。
* ![可自定义的模板](/help/assets/assets/add-text.svg)：单击以将文本添加到画布。
* ![可自定义的模板](/help/assets/assets/show-layers-list.svg)：单击可查看画布上所有图层（图像和文本）的列表。 添加到画布的每个图像和文本都表示为一个单独的图层。

**左窗格中的菜单选项：**&#x200B;请将这些选项用于以下常用编辑器操作。

* ![DM模板](/help/assets/assets/layer-selector.svg)：选择![DM模板](/help/assets/assets/layer-selector.svg)，然后单击画布上的某个图层将其选定。
* ![支持自定义的模板](/help/assets/assets/bring-forward.svg)：单击![支持自定义的模板](/help/assets/assets/bring-forward.svg)或使用键盘快捷键、**Ctrl** + **`]`** (Windows)或&#x200B;**Cmd** + **`]`** (Mac)以转发选定的层。
* ![如何创建可轻松自定义的模板](/help/assets/assets/send-backward.svg)：单击![如何创建可轻松自定义的模板](/help/assets/assets/send-backward.svg)或使用键盘快捷键、**Ctrl** + **`[`** (Windows)或&#x200B;**Cmd** + **`[`** (Mac)以向后发送选定的图层。
* ![创建可立即自定义的模板](/help/assets/assets/undo.svg)：单击![创建可立即自定义的模板](/help/assets/assets/undo.svg)或使用键盘快捷键、**Ctrl** + **Z** (Windows)或&#x200B;**Cmd** + **Z** (Mac)以撤消上一个操作。
* ![用于快速创建横幅的模板](/help/assets/assets/redo.svg)：单击![用于快速创建横幅的模板](/help/assets/assets/redo.svg)，或者使用键盘快捷键、**Ctrl** + **Y** (Windows)或&#x200B;**Cmd** + **Y** (Mac)用于重做上一个操作。
* ![用于快速创建传单的模板](/help/assets/assets/zoom-in.svg)：单击![用于快速创建传单的模板](/help/assets/assets/zoom-in.svg)，或者使用键盘快捷键、**Ctrl** + **+** (Windows)或&#x200B;**Cmd** + **+** (Mac)来放大画布。
* ![用于快速创建横幅的模板](/help/assets/assets/Zoom-out.svg)：单击![用于快速创建横幅的模板](/help/assets/assets/Zoom-out.svg)或使用键盘快捷键、**Ctrl** + **-** (Windows)或&#x200B;**Cmd** + **-** (Mac)以缩小画布。
* 如果没有正在编辑文本或属性，请按&#x200B;**Backspace**&#x200B;或&#x200B;**Delete**&#x200B;删除选定的图层。

单击![模板可快速创建传单](/help/assets/assets/show-layers-list.svg)，并在画布层上选择更多选项(![](/help/assets/assets/three-dots.svg))以在创建模板时随时编辑画布维度。
![](/help/assets/assets/edit-canvas1.png)

>[!NOTE]
>
> 模板最多允许20层，包括画布。

### 将图像添加到画布{#add-images-to-the-canvas}

执行以下步骤以将图像添加到画布：

1. 单击![立即创建横幅](/help/assets/assets/add-image.svg)以打开[资产选择器](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)面板。 该面板显示AEM Assets实例中已同步到[!DNL Dynamic Media]的图像。
1. 浏览面板或使用搜索栏中的关键字查找特定图像。
1. 将图像拖放到画布上以使用。 查看[**[!UICONTROL 属性面板]**](#reposition-resize-delete-a-layer)以调整画布上的图层大小或重新定位图层。
   ![在秒内创建横幅](/help/assets/assets/add-image-to-canvas.png)
1. 启用&#x200B;**[!UICONTROL 均匀半径]**&#x200B;切换开关并使用&#x200B;**[!UICONTROL 圆角半径]**&#x200B;滑块均匀调整图像所有四个角的圆度。 禁用切换功能，以通过为每个拐角指定特定半径值来自定义拐角圆度。
   ![调整图像的角圆度](/help/assets/assets/enable-uniform-radius-image.png)

### 在画布中添加文本图层{#add-text-to-the-canvas}

执行以下步骤以将文本图层添加到画布：

1. 单击![创建新横幅fastly](/help/assets/assets/add-text.svg)以将文本图层添加到画布并打开“属性”面板。
1. 选择图层并单击文本进行更新。
1. 在“属性”面板中选择&#x200B;**[!UICONTROL 智能文本调整大小]**&#x200B;以自动调整文本长度和字体大小，使其以最佳方式适应指定区域。
   ![最佳可自定义横幅](/help/assets/assets/add-text-layer.png)

查看[**[!UICONTROL 属性面板]**](#reposition-resize-delete-a-layer)以重新定位、调整大小、旋转或删除图层。 通过更改面板&#x200B;**[!UICONTROL 文本]**&#x200B;部分下相应字段中的值，将文本格式设置为所需的字体、大小、颜色、样式、对齐方式（在图层中）。 **[!UICONTROL 字体系列]**&#x200B;字段显示[!UICONTROL Adobe Sans F2]默认字体、重新处理的现有字体以及新上载和发布的字体。 有关详细信息，请参阅上面[开始之前](#prerequisites-for-dynamic-media-wysiwyg-template)部分中的第5点。

[对子字符串应用格式以单独设置文本特定部分的样式并控制它们。](#apply-formatting-to-substring)

#### 设置选择性文本格式{#apply-formatting-to-substring}

执行以下步骤来格式化字符串的特定部分：

1. 在字符串中选择一个或多个字符设置格式。
1. 使用[属性面板](#properties-panel)将格式设置应用于选定内容。 以下格式选项适用于子字符串及其部分：
   * **字体样式**：使用&#x200B;**[!UICONTROL 字体样式]**&#x200B;选项的粗体、斜体、下划线、下标和上标。
   * **字体属性**：使用相应的面板选项更改字体系列、颜色和大小。
     ![format-substring](/help/assets/assets/format-substring.png)

[每个带格式的字符串部分在子字符串选择器中显示为子字符串，可在参数面板中使用。 向这些格式化部分添加参数，以使用模板的投放URL](#substring-parameterisation)动态格式化它们。

### 将形状添加到画布 {#add-shapes-to-the-canvas}

执行以下步骤将形状添加到画布：

1. 单击![创建形状](/help/assets/assets/Shapes.svg)，选择一个形状（矩形或圆形）以将其添加到画布中。 使用形状的[[!UICONTROL 属性面板]](#reposition-resize-delete-a-layer)重新定位、调整大小、旋转或删除图层。
1. 滚动到面板的&#x200B;**[!UICONTROL 样式]**&#x200B;部分，在&#x200B;**[!UICONTROL 形状颜色]**&#x200B;字段中定义十六进制代码，或者使用拾色器填充所选形状中的颜色。
1. 启用&#x200B;**[!UICONTROL 统一半径]**&#x200B;切换功能，并使用&#x200B;**[!UICONTROL 圆角半径]**&#x200B;滑块来统一调整矩形所有四个角的圆度。 禁用切换功能，以通过为每个拐角指定特定半径值来自定义拐角圆度。
   ![调整形状的圆角度](/help/assets/assets/enable-uniform-radius-shape.png)
1. [将&#x200B;**[!UICONTROL 隐藏]**&#x200B;参数添加到选定的图层](#parameterise-a-layer)以使用模板URL实时显示或隐藏模板中的图层。
1. 选择图层以[向其中添加[!UICONTROL CTA]链接](#add-CTA-in-dynamic-media-templates)，允许用户在实时模板中单击形状作为超链接。

### 编辑或删除图层 {#edit-or-delete-a-layer}

执行以下步骤以编辑或删除画布层：

1. 单击支持动态更新的![模板](/help/assets/assets/show-layers-list.svg)，然后在画布上或从“图层”列表中选择该图层。
1. 单击&#x200B;**[!UICONTROL 更多选项]** （![支持实时更新的模板](/help/assets/assets/three-dots.svg)）以编辑或删除层。
1. 单击&#x200B;**[!UICONTROL 删除]**&#x200B;以删除图层。
1. 单击&#x200B;**[!UICONTROL 编辑]**&#x200B;以使用[**[!UICONTROL 属性面板]**](#reposition-resize-delete-a-layer)编辑图层。
   ![快速横幅创建](/help/assets/assets/dm-templates/edit-delete-layer.png)

### 属性面板{#properties-panel}

[!UICONTROL 属性]面板包含要[重新定位](#reposition-resize-delete-a-layer)、[调整大小](#reposition-resize-delete-a-layer)和[旋转图层](#reposition-resize-delete-a-layer)的部分。  它还为[形状图层](#add-shapes-to-the-canvas)提供颜色填充选项，为[文本图层](#text-formatting-options-on-properties-panel)提供[文本格式设置选项](#add-text-to-the-canvas)，并提供[将[!UICONTROL CTA]链接](#add-CTA-in-dynamic-media-templates)添加到任何选定图层的选项。
要导航到图层的属性面板，请单击![快速内容创建](/help/assets/assets/show-layers-list.svg)，然后从列表中选择该图层以显示其[!UICONTROL 属性]面板。

![快速内容创建](/help/assets/assets/properties-panel.png)

从图层的[!UICONTROL 属性]面板中，选择画布上的另一个图层以导航到其[!UICONTROL 属性]面板。

#### 重新定位、调整大小、旋转或删除图层{#reposition-resize-delete-a-layer}

请参阅这些常见的图层编辑操作以编辑文本或图像图层：

* **重新定位图层：**&#x200B;拖动图层可将其移动到画布上的任意位置。 此操作将更新属性面板中的X和Y值。 X和Y是画布平面上图层中心的坐标。
* **调整图层大小：**&#x200B;选择图层并拖动其边缘手柄以调整其大小。 此操作更新属性面板中的W（宽度）和H（高度）值。
* **旋转图层：**&#x200B;拖动垂直放置在图层上方的方形手柄，使其绕其中心旋转。 此操作将更新属性面板中的角度值。
* **删除层：**&#x200B;按&#x200B;**Backspace**&#x200B;或&#x200B;**删除**，然后单击&#x200B;**[!UICONTROL 确认]**&#x200B;以删除选定的层。

#### 文本格式设置选项{#text-formatting-options-on-properties-panel}

通过更改面板&#x200B;**[!UICONTROL 文本]**&#x200B;部分下相应字段中的值，将文本格式设置为所需的字体、大小、颜色、样式、对齐方式（在图层内）。
确保包括&#x200B;**[!UICONTROL 智能文本大小调整]**。 [!UICONTROL 智能文本大小调整]适用于[Copyfitting](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting)算法，可在文本区域中以最佳方式填充文本，防止文本溢出，并最大程度地减少文本底部的额外空间。

![立即创建内容](/help/assets/assets/smart-text-resize.png)

### 参数化图层 {#parameterise-a-layer}

创建包含多个图像、文本和形状层的模板后，将选定图层参数化。 将图层或其属性参数化后，它将获得一个键值对（也称为参数）。 此参数可以包含在模板URL中，以实时更新图层的位置、大小或内容，从而实时自定义模板。

要参数化图层，请执行以下操作：

1. 单击![即时内容创建](/help/assets/assets/show-layers-list.svg)，选择一个图层，然后单击&#x200B;**[!UICONTROL 参数]**。 显示&#x200B;**[!UICONTROL 参数]**&#x200B;面板。
1. 切换&#x200B;**[!UICONTROL 包含参数]**&#x200B;以参数化属性。 请参阅[参数面板选项](#parameterisation-options-or-allowed-parameters)，了解属性在参数化后的行为。
1. **可选：**&#x200B;重命名参数名称。 参数名称具有层名称后跟一个后缀。 对于选定层，其所有参数化属性共享相同的层名称，后跟一个变化的后缀。 按照语义命名约定重命名层名称，以便在URL中包含参数时，参数名称本身可以说明层的内容或其用途。
1. 单击&#x200B;**[!UICONTROL 保存]**。
   ![即时内容创建](/help/assets/assets/parameterise-a-layer.png)
若要在图像和文本图层的“参数”面板之间进行切换，请选择画布上的图层，然后单击&#x200B;**[!UICONTROL 参数]**。

#### “参数”面板选项 {#parameterisation-options-or-allowed-parameters}

参数化的属性可以作为URL参数包含在模板URL中，以使用URL实时编辑模板。

##### 图层参数{#layer-parameters}

下面是适用于图像和文本图层的图层参数。

**[!UICONTROL X]：** Include可通过更改URL中的参数值，沿图层中心线水平移动图层，平行于模板平面的X轴。
**[!UICONTROL Y]：**&#x200B;包含可通过更改URL中的参数值，沿图层中心线垂直移动图层，平行于模板平面的Y轴。
**[!UICONTROL 宽度]：**&#x200B;包含可通过更改URL中的参数值来调整图层的宽度。
**[!UICONTROL 高度]：**&#x200B;包含可通过更改URL中的参数值来调整图层的高度。
**[!UICONTROL 隐藏]：**&#x200B;包含以使用0（显示）和1（隐藏）来隐藏或显示模板中的图层。

##### 图像参数{#image-parameter}

包含&#x200B;**[!UICONTROL Source]**&#x200B;参数，以通过更改URL中参数值中的图像路径来使用新图像替换图层的图像。
![图像源参数](/help/assets/assets/image-parameter.png)

##### 文本格式设置参数{#text-formatting-parameters}

包括以下参数，以便通过更新URL中的参数值来编辑投放URL中的文本、其字体、颜色和大小：

**[!UICONTROL 文本]：**&#x200B;包含以从URL更新文本。
**[!UICONTROL 字体系列]：**&#x200B;包含以从URL更新文本的字体。
**[!UICONTROL 字体大小]：**&#x200B;包含以从URL更新文本的字体大小。
**[!UICONTROL 文本颜色]：**&#x200B;包含以从URL更新文本的字体颜色。

##### 参数化子字符串{#substring-parameterisation}

在&#x200B;**[!UICONTROL 参数]**&#x200B;面板中，滚动到&#x200B;**[!UICONTROL 子字符串参数]**&#x200B;部分。 此部分包含一个&#x200B;**子字符串选择器**，该选择器将格式一致的完整字符串（选定文本图层）或其格式化部分显示为单独的子字符串。 选择一个子字符串以[参数化其文本、字体系列、字体大小和颜色](#text-formatting-parameters)。
使用子字符串选择器[拆分子字符串](#split-substring)以参数化其各个部分，或者使用[合并子字符串](#merge-substring)以应用统一的参数。

###### 拆分子字符串{#split-substring}

要参数化子字符串的一部分，请将其拉出以使其成为单独的子字符串以供单独选择和参数化。
执行以下步骤，将子字符串拆分为单独的子字符串：

1. 在子字符串选择器中，选择子字符串中的字符以将其分开。
1. 单击![拆分子字符串](/help/assets/assets/unmerge.svg)以将其拉出，并使其成为&#x200B;**子字符串选择器**&#x200B;中的单独子字符串。
   ![拆分子字符串](/help/assets/assets/split-a-substring.png)
您可以选择所需的子字符串以[参数化其文本、字体系列、字体大小和颜色](#text-formatting-parameters)。

###### 合并子字符串{#merge-substring}

合并子字符串会删除其现有的单个参数，并允许您在新形成的子字符串中应用一致的参数。
执行以下步骤以合并两个相邻的子字符串，将统一的参数应用于生成的子字符串：

1. 在子字符串选择器中，跨两个具有相同格式的相邻子字符串选择字符。
1. 单击![合并子字符串](/help/assets/assets/merge.svg)以合并子字符串。
   ![合并相同的子字符串](/help/assets/assets/merge-two-substrings.png)
可以将统一参数应用到新形成的子字符串。
   >[!NOTE]
   >
   >只能合并具有相同格式的子字符串。

### 将层分组以同时控制其可见性{#group-layers}

保持模板灵活性的另一种方法是使用单个参数名称控制多个层。 此策略有助于显示可见性（隐藏或显示层）参数，以更新单个模板的设计或图形。

按照以下步骤为多个图层的[!UICONTROL 隐藏]参数（![快速内容创建](/help/assets/assets/Visibility-icon.svg)）指定相同的名称，从而允许您同时隐藏或显示它们。

1. 导航到图层的[**[!UICONTROL 属性面板]**](#parameterise-a-layer)。
1. 如果之前未设置参数，请切换&#x200B;**[!UICONTROL 隐藏]**&#x200B;参数。
1. **可选：**&#x200B;重命名&#x200B;**[!UICONTROL 隐藏]**&#x200B;参数。
1. 复制&#x200B;**[!UICONTROL 隐藏]**&#x200B;参数名称。
1. 从画布中选择其他图层以转到这些图层的“参数”面板，并切换其&#x200B;**[!UICONTROL 隐藏]**&#x200B;参数（如果未设置参数）。
1. 将他们的&#x200B;**[!UICONTROL 隐藏参数]**&#x200B;名称替换为复制的名称。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;将图层分组。
1. 执行[**[!UICONTROL 预览和发布]**](#preview-and-publish-template-and-copy-template-deliver-url)部分中的步骤3，然后执行步骤4，以查看所做的更改。

## 预览并发布模板以复制投放URL{#preview-and-publish-template-and-copy-template-deliver-url}

执行以下步骤以预览和发布模板并复制投放URL：

1. 在画布页面上，单击&#x200B;**[!UICONTROL 预览]**。 您还可以导航到&#x200B;**[!UICONTROL Assets视图]** **>** **[!UICONTROL Dynamic Media Assets]** **>**&#x200B;查找并选择您的模板&#x200B;**>**&#x200B;单击&#x200B;**[!UICONTROL 编辑模板]** **>**&#x200B;单击&#x200B;**[!UICONTROL 预览]**。 预览页面显示模板、其参数（参数化层和属性）、发布状态以及&#x200B;**[!UICONTROL 发布]**&#x200B;选项。
1. 从&#x200B;**[!UICONTROL 模板参数]**&#x200B;面板中选择参数以编辑其值，并立即更新预览中相应模板图层的内容、大小、位置或文本格式。 例如：
   1. 选择文本图层并编辑其文本或
   1. 选择图像图层，单击![即时创建内容](/help/assets/assets/add-image.svg)，从资产选择器中选择图像，然后单击&#x200B;**[!UICONTROL 刷新]**。

   模板会立即更新，显示编辑过的文本并将以前的图像替换为新图像。 此外，图像参数值反映了新的图像路径。 同样，可以通过调整图层的值来调整其大小，所做的更改将实时应用于模板。
1. 从列表中选择&#x200B;**[!UICONTROL 分组图层]**&#x200B;的[隐藏](#group-layers)参数，以便在模板中显示或隐藏这些图层。
1. **可选：**&#x200B;将&#x200B;**[!UICONTROL 隐藏]**&#x200B;参数值在0和1之间更改，然后单击&#x200B;**[!UICONTROL 刷新]**&#x200B;以查看更改内容。 具有相同&#x200B;**[!UICONTROL Hide]**&#x200B;参数的图层会一起隐藏或显示。 同样，您可以从URL控制图层的可见性。

   ![即时创建内容](/help/assets/assets/dm-templates-publish-status.png)
您还可以切换&#x200B;**[!UICONTROL 包含所有参数]**&#x200B;以编辑所有显示的参数值，并在模板预览中查看更新。
   <br>
1. 要从预览页面发布模板，请单击&#x200B;**[!UICONTROL 发布]**&#x200B;并确认发布。 显示&#x200B;**[!UICONTROL 发布完成]**&#x200B;消息，发布状态更新为&#x200B;**[!UICONTROL 已发布]**。

### 复制投放URL

**[!UICONTROL 预览]**&#x200B;页面上选定的参数将成为模板URL中的URL参数。

确保模板中的图像已发布到AEM和Dynamic Media以生成模板的投放URL。

执行以下步骤以复制模板的投放URL：

1. 单击&#x200B;**[!UICONTROL 复制URL]**。 将显示&#x200B;**[!UICONTROL 复制URL]**&#x200B;对话框。 选择并复制显示的URL。 URL中的第一个参数在问号&#x200B;**([!UICONTROL ？])**&#x200B;和一个键值对以&#x200B;**[!UICONTROL $]**&#x200B;开头，以&#x200B;**[!UICONTROL &amp;]**&#x200B;结尾。 键和值用等号&#x200B;**([!UICONTROL =])**&#x200B;分隔，键在左侧，值在右侧。
1. 将此URL粘贴到浏览器选项卡中，并查看您的实时模板。 通过直接更新URL中所需参数的值（键值）实时自定义模板，如[预览和发布](#preview-and-publish-template-and-copy-template-deliver-url)部分的&#x200B;**步骤2**&#x200B;所示。
1. 使用此URL快速推销您的产品或服务。 您可以与客户共享此URL，或将其集成到您的网站或任何下游第三方应用程序，以显示横幅并实时更新以反映持续优惠。

## 从URL实时更新模板{#update-the-template-from-the-url}

直接在URL中编辑参数可能比较繁琐。 要简化：

1. 复制URL并将其粘贴到记事本中。
1. 使用Cmd+F (Mac)或Ctrl+F (Windows)查找并编辑参数值。 例如：
   * 查找和替换图像图层的图像路径。
   * 查找图层的[参数化的](#parameterise-a-layer)坐标（宽度和高度）以调整其值。
   * 编辑文本图层的文本、字体、颜色、大小或对齐方式。
   * 将可见性值更改为0和1。

将此更新的URL粘贴到浏览器中以查看更改。

## 编辑模板{#edit-the-template}

按以下这些步骤编辑模板：

1. 在[!DNL Assets view]上，单击&#x200B;**[!UICONTROL Dynamic Media Assets]**。
2. 导航到模板位置。
3. 选择模板。
4. 单击&#x200B;**[!UICONTROL 编辑模板]**。 模板画布在“图层”面板中显示模板及其所有图层的列表。 根据您的要求开始编辑模板。

## 将Call to action (CTA)链接添加到模板层{#add-CTA-in-dynamic-media-templates}

通过添加CTA链接将[!DNL Dynamic Media]模板的任何图像、文本或形状图层转换为超链接，该链接可将用户引导至目标页面。

执行以下步骤以将CTA链接添加到层：

1. 导航到模板位置，选择模板并单击![编辑](/help/assets/assets/edit-pen-icon.svg) **[!UICONTROL 编辑模板]**。 模板显示在画布上。
1. 选择模板图层并[导航到其属性面板](#edit-or-delete-a-layer)以向其添加CTA链接。
1. 在属性面板上，选择&#x200B;**[!UICONTROL 添加CTA]**，在&#x200B;**[!UICONTROL URL]**&#x200B;字段中指定目标URL，然后单击&#x200B;**[!UICONTROL 保存]**。

   ![添加CTA](/help/assets/assets/add-cta.png)

1. 单击&#x200B;**[!UICONTROL 预览]**，然后选择&#x200B;**[!UICONTROL 发布]**&#x200B;以发布您的模板（如果之前未发布）。
1. 导航到保存此模板的文件夹，选择该模板并单击![详细信息页面](/help/assets/assets/details-page-icon.svg) **[!UICONTROL 详细信息]**。
1. 单击&#x200B;**[!UICONTROL 复制选项]**&#x200B;并选择&#x200B;**[!UICONTROL 复制嵌入代码]**。 确保将模板图像发布到[!DNL AEM and Dynamic Media]以复制嵌入代码。

   ![复制嵌入代码](/help/assets/assets/copy-options1.png)

   以下是嵌入代码的示例：

   ```json
    <div class="adobe-dynamicmedia-template-embed-container">
    <img id="<Image ID>>" src="<Image Source>>" alt="adobe dynamicmedia template" usemap="#adobe-dynamicmedia-template-map" width="800" height="300">
    <map name="adobe-dynamicmedia-template-map">
    <area shape="rect" coords="417,-60,817,340" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    <area shape="rect" coords="6,206.57,129,231.43" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    </map>
    </div>
   ```

1. 将复制的嵌入代码添加到网站的HTML文件，并在浏览器中运行该代码以显示模板。

单击模板上的CTA元素以导航到目标页面。

观看此分步视频，了解如何将CTA链接添加到模板图层。

>[!VIDEO](https://video.tv.adobe.com/v/3457616)

## 要注意的重要事项 {#important-points-to-note}

* 在创建具有用于动态更新的参数化图像层的模板后，请确保打算用于将来更新的图像共享与参数化图像相同的尺寸。 这确保图像完全适合在层内，而不会溢出或留下空隙。 目前，模板不支持自动调整尺寸以将图像适合图层。
* 文本图层不支持子字符串。 用户无法对文本图层的子字符串应用不同的字体属性。
* [!DNL Dynamic Media]模板当前不支持多个[!DNL Dynamic Media]公司。
* 如果进行复制或移动，目标选择器会显示所有文件夹（包括非[!DNL Dynamic Media]同步文件夹）。 此外，当前它不显示[!DNL Dynamic Media]模板资产（两者都是目标选择器的限制）。
* 从Assets部分对文件夹执行的任何更新操作（例如，发布或删除）都会影响该文件夹中可用的[!DNL Dynamic Media]模板。
* 垃圾桶对[!DNL Dynamic Media]模板无效。 如果将某个资源移至垃圾桶并恢复，则该资源将在AEM中恢复，但在[!DNL Dynamic Media]中无法恢复。 这同样适用于[!DNL Dynamic Media]模板。

## 另请参阅

1. 探索[[!DNL Dynamic Media] 及其功能](/help/assets/dynamic-media/dynamic-media.md)
1. 使用OpenAPI功能浏览[[!DNL Dynamic Media] ](/help/assets/dynamic-media-open-apis-overview.md)