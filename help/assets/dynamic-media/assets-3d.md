---
title: 在Dynamic Media中使用3D资产
description: 了解如何在Dynamic Media中使用3D资产。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '2298'
ht-degree: 3%

---

# 在Dynamic Media中使用3D资产 {#working-with-three-d-assets-dm}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
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

您可以利用Dynamic Media上传、管理、查看和交付3D资产，尽享沉浸式体验。

* 一键发布（使用工具栏上的&#x200B;**[!UICONTROL 快速发布]**）来生成URL。
* 优化支持使用由Adobe Dimension提供支持的高质量交互式Dimensional查看器预设查看3D资源。
* 通过3D媒体WCM组件，您可以轻松将3D资产添加到[!DNL Adobe Experience Manager Sites]页面。

在Dynamic Media中使用3D资产无需额外安装。

3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)中的![鞋

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media支持的3D格式 {#supported-three-d-file-formats-in-dm}

Dynamic Media支持以下3D文件格式。

另请参阅Experience Manager Assets支持的[3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary | 将材料和纹理作为单个资产包含在内。 |
| 对象 | WaveFront 3D对象文件 | application/x-tgif |  |
| STL | 立体成形 | application/vnd.ms-pki.stl |  |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | *仅支持摄取；不可查看或交互。* USDZ是一种专有的3D格式，可由Safari或iOS以本机方式查看。 |

资产详细信息页面上的3D Media WCM组件和3D预览与最新版本的Chrome (97.x)不兼容。 要处理3D资产，请使用Firefox或Safari，或者使用早期版本的Chrome (96.x)。

## 快速入门：Dynamic Media中的3D资源 {#quick-start-three-d}

以下分步工作流描述旨在帮助您在Dynamic Media中快速启动和运行3D资产。

在Dynamic Media中使用3D资产之前，请确保您的[!DNL Experience Manager]管理员已启用并配置了Dynamic Media云服务。

请参阅[配置Dynamic Media云服务](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)。

1. **上传3D资源**

   * [上传要在Dynamic Media中使用的3D资产](/help/assets/add-assets.md#upload-assets)
   * [在Dynamic Media中上传时支持的3D文件格式](#supported-three-d-file-formats-in-dm)

1. **管理3D资源**

   * 组织和搜索3D资产

      * [组织数字资产](/help/assets/organize-assets.md)
      * [搜索3D资产](/help/assets/search-assets.md)

   * 查看3D资产

      * [查看3D资源并与之交互](#viewing-three-d-assets)
      * [管理维查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)

   * 使用3D资源元数据

      * [管理数字资源的元数据](/help/assets/manage-digital-assets.md#editing-properties)
      * [元数据架构](/help/assets/metadata-schemas.md)

1. **发布3D资源**

   * [发布静态Dynamic Media 3D资产](#publishing-three-d-assets)
   * [使用维度查看器发布Dynamic Media 3D资产的替代方法](#alternate-publish-methods)

## 关于查看和与3D资产交互 {#viewing-three-d-assets}

本节将介绍如何通过两种不同的方式查看3D资源并与之交互：在资源详细信息页面中查看，以及在Sites的3D媒体组件中查看3D资源并与之交互。

交互式3D查看器包括一组交互式相机控件等，可让您环绕、缩放和平移3D资产。

在“资产详细信息”页面视图中打开3D资产所需的时间取决于多个因素。 这些因素包括：

* 到服务器的带宽。
* 服务器的延迟
* 图像的复杂性。

此外，当以交互方式操作摄像头时，客户端计算机的功能（如工作站、笔记本或移动触控设备）也非常重要。 功能相当强大、图形功能良好的系统可使交互式3D观看体验更加流畅和更加有利。

>[!TIP]
>
>您可以在查看器预设编辑器中打开维查看器预设，以练习导航3D资产，而无需首先上传任何3D文件。 维查看器预设提供了一个内置的3D资产供您与交互。
>
>请参阅[管理查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md)。

## 从资源详细信息页面查看并与3D资源交互 {#viewing-three-d-assets-from-asset-details-page}

另请参阅[使用软件界面](/help/assets/dynamic-media/previewing-assets.md)预览资源。

**要从资产详细信息页面查看和交互3D资产：**

1. 确保您已将3D资产上传到[!DNL Experience Manager]。

   查看[上传3D资产以在Dynamic Media中使用](/help/assets/add-assets.md#upload-assets)。

1. 从[!DNL Experience Manager]，在&#x200B;**[!UICONTROL 导航]**&#x200B;页面上，选择&#x200B;**[!UICONTROL Assets >文件]**。
1. 在页面的右上角附近，从&#x200B;**[!UICONTROL 视图]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 卡片视图]**。
1. 导航到要查看的3D资产。
1. 要在详细信息页面中打开资产，请选择3D资产的卡。
1. 在3D资产的“详细信息”页面上，执行以下任一操作：

   | 查看 | 描述 | 鼠标操作 | 触摸屏操作 |
   | --- | --- | --- | --- |
   | **转动相机** | 围绕 3D 场景和对象旋转视图。 | 左键单击+拖动。 | 单指按下+拖动。 |
   | **平移相机** | 向左、向右、向上或向下平移视图。 | 右键单击+拖动。 | 双指按下+拖动。 |
   | **缩放相机** | 在3D场景中移入和移出区域。 | 滚轮。 | 两指捏合。 |
   | **重新居中相机** | 将相机重新居中到3D场景中对象上的某个点。 | 双击。 | 双击。 |
   | **重置** | 在页面的右下角附近，选择“重置”图标以将视图目标点恢复到3D资产的中心。 重置还会将相机靠近或远离其他位置，以便以合理的观看大小完整地显示资产。 |   |   |
   | **全屏模式** | 要进入全屏模式，请选择页面右下角的全屏图标。 |   |   |

1. 在页面的右上角，选择&#x200B;**[!UICONTROL 关闭]**&#x200B;以返回Assets页面。

## 在3D媒体组件中查看3D资产并与之交互 {#interacting-with-asset-inside-three-d-media-component}

当网页处于&#x200B;**[!UICONTROL 编辑]**&#x200B;模式时，无法与3D资产进行交互。 要使资产具有交互性，您可以使用&#x200B;**[!UICONTROL 预览]**&#x200B;功能在页面编辑器中查看网页，从而完全访问3D媒体组件的功能。

>[!IMPORTANT]
>
>只有在将3D媒体组件添加到网页并为其分配了3D资产后，您才能完成此任务。 请参阅[将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page)和[将3D资产分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component)。

另请参阅[使用软件界面](/help/assets/dynamic-media/previewing-assets.md)预览资源。

**要在3D媒体组件中查看和交互3D资产：**

1. 当网页处于&#x200B;**[!UICONTROL 编辑]**&#x200B;模式时，请执行下列任一操作：

   * 在页面的右上角附近，单击&#x200B;**[!UICONTROL 预览]**&#x200B;以进入&#x200B;**[!UICONTROL 预览]**&#x200B;模式。
   * 从浏览器中的页面URL中删除`/editor.html`。

   ![3D资产显示在3D媒体组件内](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
以**[!UICONTROL 预览]**&#x200B;模式显示的完全交互式3D资产。

1. 在&#x200B;**[!UICONTROL 预览]**&#x200B;模式下，执行以下任一操作：

   | 查看 | 描述 | 鼠标操作 | 触摸屏操作 |
   | --- | --- | --- | --- |
   | **转动相机** | 围绕 3D 场景和对象旋转视图。 | 左键单击+拖动。 | 单指按下+拖动。 |
   | **平移相机** | 向左、向右、向上或向下平移视图。 | 右键单击+拖动。 | 双指按下+拖动。 |
   | **缩放相机** | 在3D场景中移入和移出区域。 | 滚轮。 | 两指捏合。 |
   | **重新居中相机** | 将相机重新居中到3D场景中对象上的某个点。 | 双击。 | 双击。 |
   | **重置** | 在页面的右下角附近，选择“重置”图标以将视图目标点恢复到3D资产的中心。 重置还会将相机靠近或远离其他位置，以便以合理的观看大小完整地显示资产。 |   |   |
   | **全屏模式** | 要进入全屏模式，请选择页面右下角的全屏图标。 |   |   |

## 关于使用3D媒体组件 {#working-with-three-d-media-component}

Dynamic Media包含一个Dynamic Media 3D Media组件，您可以在[!DNL Experience Manager Sites]中使用它来启用在网页上交互查看3D模型的功能。

* [将3D媒体组件添加到页面模板](#adding-three-d-media-component-to-page-template)
* [将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page)
   * [可选 — 配置3D媒体组件](#configuring-the-three-d-component)
* [将3D资产分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component)

## 将3D媒体组件添加到页面模板 {#adding-three-d-media-component-to-page-template}

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 模板]**。
1. 导航到要在其中启用3D组件的页面模板，然后选择该模板。
1. 要打开模板，请选择&#x200B;**[!UICONTROL 编辑]**。
1. 在页面的右上角附近，在下拉菜单中选择&#x200B;**[!UICONTROL 结构]**&#x200B;模式（如果尚未处于活动状态）。

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. 要选择空白区域并打开其关联的工具栏，请在&#x200B;**[!UICONTROL 布局容器]**&#x200B;区域中选择空白区域。
1. 在工具栏上，选择&#x200B;**[!UICONTROL 策略]**&#x200B;图标以打开&#x200B;**[!UICONTROL 策略编辑器]**。
1. 在&#x200B;**[!UICONTROL 属性]**&#x200B;部分的&#x200B;**[!UICONTROL 允许的组件]**&#x200B;选项卡下，滚动到&#x200B;**[!UICONTROL 动态媒体]**，然后展开列表并检查&#x200B;**[!UICONTROL 3D媒体]**。
1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存更改并关闭&#x200B;**[!UICONTROL 策略编辑器]**。

   现在，您可以将Dynamic Media 3D Media组件放在使用此模板的所有页面上。

## 将3D媒体组件添加到网页 {#adding-the-three-d-media-component-to-a-web-page}

如果您将[!DNL Experience Manager]用作Web内容管理系统，则可以通过3D媒体组件将3D资产添加到网页。

另请参阅[将Dynamic Media资源添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

1. 打开[!DNL Experience Manager Sites]并选择要将Dynamic Media 3D Media组件添加到其中的网页。
1. 要在页面编辑器中打开页面，请选择&#x200B;**[!UICONTROL 编辑]** （铅笔）图标。 确保在页面右上角附近选择&#x200B;**[!UICONTROL 编辑]**&#x200B;模式。

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. 在工具栏上，选择侧面板图标以切换或“打开”面板的显示。

1. 在侧面板中，选择加号图标以打开&#x200B;**[!UICONTROL 组件]**&#x200B;列表。

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. 将&#x200B;**[!UICONTROL 3D媒体]**&#x200B;组件从&#x200B;**[!UICONTROL 组件]**&#x200B;列表拖到页面上要显示3D查看器的位置。

现在，您可以为该组件分配3D资产了。

请参阅[将3D资产分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component)

### 可选 — 配置3D媒体组件 {#configuring-the-three-d-component}

1. 在[!DNL Experience Manager Sites]页面编辑器中，选择您之前添加到页面的&#x200B;**[!UICONTROL 3D媒体查看器]**&#x200B;组件。
1. 要打开组件配置对话框，请选择&#x200B;**[!UICONTROL 配置]**&#x200B;图标（扳手）。

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. 在“3D媒体”对话框中，从“查看器预设”下拉列表中选择&#x200B;**[!UICONTROL 维度]**&#x200B;以将维度查看器预设分配给组件。

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. 选择右上角的复选标记以保存更改。

## 将3D资产分配给3D媒体组件 {#assigning-a-three-d-asset-to-the-component}

将3D媒体组件添加到网页后，即可为其分配3D资产。

请参阅将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page)。[

1. 在[!DNL Experience Manager Sites]页面编辑器中，单击&#x200B;**[!UICONTROL Assets]**&#x200B;图标以打开侧面板中的&#x200B;**[!UICONTROL Assets]**。
1. 在下拉列表中，选择&#x200B;**[!UICONTROL 3D]**&#x200B;以仅显示3D资源文件类型。
1. 在侧面板中，搜索或滚动到要在编辑的页面上查看的3D资产。
1. 将3D资源从Assets侧面板拖放到您之前添加到页面的&#x200B;**[!UICONTROL 3D Media]**&#x200B;组件上。

   ![将3d资产分配给3d媒体组件](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>当网页处于[!DNL Experience Manager Sites] **[!UICONTROL 编辑]**&#x200B;模式时，3D媒体组件会显示3D资产，但无法与资产交互。 要使资产具有交互性，您可以使用&#x200B;**[!UICONTROL 预览]**&#x200B;功能在页面编辑器中查看网页，从而完全访问3D媒体组件的功能。

## 发布静态Dynamic Media 3D资产 {#publishing-three-d-assets}

Dynamic Media接受Dynamic Media中作为&#x200B;*静态内容*&#x200B;支持的各种3D文件格式。 静态内容表示您可以上传和发布3D资产，但不支持与该3D资产关联的&#x200B;*动态*&#x200B;图像或重新调整图像。 原因是Dynamic Media图像服务器无法识别3D格式。 因此，在Dynamic Media中发布3D资产后，您就可以复制一个即时URL。 3D资产的URL遵循常规的Dynamic Media URL结构。 但是，与Dynamic Media中的传统图像资产不同，您无法编辑资产URL中的任何参数。

另请参阅[获取静态资源的URL](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)。

在&#x200B;**[!UICONTROL 卡片视图]**&#x200B;中，资产名称的正下方及其日期和时间的左侧会显示一个小地球图标，指示资产已发布。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

如果您将[!DNL Experience Manager]用作WCM，请使用此发布方法直接在网页上添加Dynamic Media 3D资产。

另请参阅[发布Dynamic Media资源](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

另请参阅[发布页面](/help/sites-cloud/authoring/sites-console/publishing-pages.md)。

**要发布静态Dynamic Media 3D资源：**

1. 打开3D资产（GLB、OBJ或STL文件格式）。
1. 在详细信息页面的工具栏上，选择&#x200B;**[!UICONTROL 快速发布]**。

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. 选择&#x200B;**[!UICONTROL 关闭]**&#x200B;以退出对话框并返回到资源详细信息页面。
1. 从3D资产文件名左侧的下拉列表中，选择&#x200B;**[!UICONTROL 呈现版本]**。

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. 选择&#x200B;**[!UICONTROL 原始]**。 发布（或“激活”）3D资产时，如果满足以下所有3D资产条件，则页面左下角附近将显示&#x200B;**[!UICONTROL URL]**&#x200B;按钮：
   * 3D资产是受支持的格式（GLB、OBJ、STL和USDZ）。
   * 已将3D资产摄取到Dynamic Media图像生产系统(IPS)。
   * 发布3D资产。

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. 要显示可在网页上复制和使用的3D资产的直接生产URL，请选择&#x200B;**[!UICONTROL URL]**。

### 使用维度查看器发布Dynamic Media 3D资产的替代方法 {#alternate-publish-methods}

如果您&#x200B;*不是*，且使用[!DNL Experience Manager]作为WCM，请使用以下两种方法发布Dynamic Media 3D资产。

* **[!UICONTROL URL]** — 如果您使用的是第三方Web内容管理系统，并且希望使用维度查看器将Dynamic Media 3D资产链接到您的网页，请使用&#x200B;**[!UICONTROL URL]**。

  查看[将URL链接到您的Web应用程序](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)。

* **[!UICONTROL 嵌入]** — 当您想要使用维度查看器查看嵌入到网页上的Dynamic Media 3D资产时，请使用&#x200B;**[!UICONTROL 嵌入]**。 将嵌入代码复制到剪贴板，以便将其粘贴到网页中。 不允许在&#x200B;**[!UICONTROL 嵌入]**&#x200B;对话框中编辑代码。

  请参阅[将Dynamic Media视频、图像查看器或维度查看器嵌入网页](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)。
