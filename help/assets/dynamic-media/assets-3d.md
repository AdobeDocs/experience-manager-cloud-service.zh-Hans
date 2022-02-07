---
title: Work with 3D assets in Dynamic Media
description: Learn how to work with 3D assets in Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: 347da5edf4c8ad2ae72284f4e1a4003493596194
workflow-type: tm+mt
source-wordcount: '2260'
ht-degree: 5%

---

# Work with 3D assets in Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media lets you upload, manage, view, and deliver 3D assets as immersive experiences.

* ****
* Optimized support for viewing 3D assets with the high-quality, interactive Dimensional viewer preset powered by Adobe Dimension.
* [!DNL Adobe Experience Manager Sites]

There is no additional installation required to use 3D assets in Dynamic Media.

![](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## 3D formats supported in Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media supports the following 3D file formats.

[](/help/assets/file-format-support.md#support-3d-formats)

| 3D file extension | File format | MIME type | 注释 |
|---|---|---|---|
| GLB | Binary GL Transmission | model/gltf-binary | Includes the materials and textures as a single asset. |
| OBJ | WaveFront 3D Object File | application/x-tgif |  |
| STL | Stereolithography | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Description Zip archive | model/vnd.usdz+zip | ** |

The 3D Media WCM component and 3D preview on an asset&#39;s Details page is not compatible with the latest version of Chrome (97.x). Instead, to work with 3D assets, use Firefox or Safari, or use an earlier version of Chrome (96.x).

## Quick Start: 3D assets in Dynamic Media {#quick-start-three-d}

The following step-by-step workflow description is designed to help you get up and running quickly with 3D assets in Dynamic Media.

[!DNL Experience Manager]

[](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

1. ****

   * [Upload your 3D assets for use in Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Supported 3D file formats for upload in Dynamic Media](#supported-three-d-file-formats-in-dm)

1. ****

   * Organize and search 3D assets

      * [Organizing digital assets](/help/assets/organize-assets.md)
      * [Search 3D assets](/help/assets/search-assets.md)
   * View 3D assets

      * [View and interact with 3D assets](#viewing-three-d-assets)
      * [Manage the Dimensional viewer preset](/help/assets/dynamic-media/managing-viewer-presets.md)
   * Work with 3D asset metadata

      * [Manage metadata for digital assets](/help/assets/manage-digital-assets.md#editing-properties)
      * [元数据架构](/help/assets/metadata-schemas.md)



1. ****

   * [Publish static Dynamic Media 3D assets](#publishing-three-d-assets)
   * [Alternate methods for publishing Dynamic Media 3D assets using the Dimensional viewer](#alternate-publish-methods)

## About viewing and interacting with 3D assets {#viewing-three-d-assets}

This section describes how to view and interact with 3D assets two different ways: from within the asset details page and from within the 3D Media component in Sites.

The interactive 3D viewer includes, among other things, a collection of interactive camera controls that let you orbit, zoom, and pan the 3D asset.

The time it takes to open a 3D asset in the Asset Details page view depends on several factors. 这些因素包括如下几项：

* Bandwidth to the server.
* Latencies to the server
* Complexity of the image.

In addition, the capabilities of the client computer-such as a workstation, notebook, or mobile touch device-are also important to consider when you manipulate the camera interactively. 具备良好图形功能的相当强大的系统可以使交互式 3D 查看体验更流畅、更舒适。

>[!TIP]
>
>You can open the Dimensional viewer preset in the Viewer Preset Editor to practice navigating a 3D asset without the need to first upload any 3D files. The Dimensional viewer preset has a built-in 3D asset for you to interact with.
>
>[](/help/assets/dynamic-media/managing-viewer-presets.md)

## View and interact with a 3D asset from the asset details page {#viewing-three-d-assets-from-asset-details-page}

[](/help/assets/dynamic-media/previewing-assets.md)

****

1. 确保您已将 3D 资产上传到 [!DNL Experience Manager].

   [](/help/assets/add-assets.md#upload-assets)

1. [!DNL Experience Manager]********
1. ********
1. 导航到要查看的 3D 资产。
1. To open the asset in the Details page, select the card of the 3D asset.
1. On the Details page for the 3D asset, do any of the following:

   | 查看 | 描述 | Mouse action | Touch screen action |
   | --- | --- | --- | --- |
   | **** | 围绕 3D 场景和对象旋转视图。 | Left click + drag. | Single-finger press + drag. |
   | **** | Pan your view left, right, up, or down. | Right click + drag. | Two-finger press + drag. |
   | **** | Move in and out of areas in the 3D scene. | Scroll wheel. | Two-finger pinch. |
   | **** | Recenter your camera to a point on an object in the 3D scene. | 双击. | Double-tap. |
   | **重置** | Near the lower-right corner of the page, select the Reset icon to restore the view target point to the center of the 3D asset. Reset also moves the camera closer or further away to show the asset in its entirety and at a reasonable viewing size. |  |  |
   | **全屏模式** | To enter full screen mode, in the lower-right corner of the page, select the Fullscreen icon. |  |  |

1. ****

## View and interact with a 3D asset inside a 3D Media component {#interacting-with-asset-inside-three-d-media-component}

********

>[!IMPORTANT]
>
>You can accomplish this task only after you have added a 3D Media component to a web page and assigned a 3D asset to the component. [](#adding-the-three-d-media-component-to-a-web-page)[](#assigning-a-three-d-asset-to-the-component)

[](/help/assets/dynamic-media/previewing-assets.md)

****

1. ****

   * ********
   * `/editor.html`

A fully interactive 3D asset as displayed in    ![](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)****

1. ****

   | 查看 | 描述 | Mouse action | Touch screen action |
   | --- | --- | --- | --- |
   | **** | 围绕 3D 场景和对象旋转视图。 | Left click + drag. | Single-finger press + drag. |
   | **** | Pan your view left, right, up, or down. | Right click + drag. | Two-finger press + drag. |
   | **** | Move in and out of areas in the 3D scene. | Scroll wheel. | Two-finger pinch. |
   | **** | Recenter your camera to a point on an object in the 3D scene. | 双击. | Double-tap. |
   | **重置** | Near the lower-right corner of the page, select the Reset icon to restore the view target point to the center of the 3D asset. Reset also moves the camera closer or further away to show the asset in its entirety and at a reasonable viewing size. |  |  |
   | **全屏模式** | To enter full screen mode, in the lower-right corner of the page, select the Fullscreen icon. |  |  |

## About working with the 3D Media component {#working-with-three-d-media-component}

[!DNL Experience Manager Sites]

* [Add the 3D Media component to the page template](#adding-three-d-media-component-to-page-template)
* [Add the 3D Media component to a web page](#adding-the-three-d-media-component-to-a-web-page)
   * [Optional - Configuring the 3D Media component](#configuring-the-three-d-component)
* [Assign a 3D asset to the 3D Media component](#assigning-a-three-d-asset-to-the-component)

## Add the 3D Media component to the page template {#adding-three-d-media-component-to-page-template}

1. ************
1. Navigate to the page template that you want to enable the 3D component in and select the template.
1. ****
1. ****

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. ****
1. ********
1. ****************
1. ********

   You can now place the Dynamic Media 3D Media component on all pages that use this template.

## Add the 3D Media component to a web page {#adding-the-three-d-media-component-to-a-web-page}

[!DNL Experience Manager]

[](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

1. [!DNL Experience Manager Sites]
1. ********

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. On the toolbar, select the Side Panel icon to toggle or &quot;turn on&quot; the display of the panel.

1. ****

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. ********

You are now ready to assign a 3D asset to the component.

[](#assigning-a-three-d-asset-to-the-component)

### Optional - Configuring the 3D Media component {#configuring-the-three-d-component}

1. [!DNL Experience Manager Sites]****
1. ****

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. ****

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. In the upper-right corner, select the check mark to save your changes.

## Assign a 3D asset to the 3D Media component {#assigning-a-three-d-asset-to-the-component}

After you have added a 3D Media component to a web page, you can assign a 3D asset to it.

[](#adding-the-three-d-media-component-to-a-web-page)

1. [!DNL Experience Manager Sites]********
1. ****
1. In the side panel, search for or scroll to the 3D asset that you want to view on the page being edited.
1. ****

   ![](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>[!DNL Experience Manager Sites]********

## Publish static Dynamic Media 3D assets {#publishing-three-d-assets}

**** The reason is because Dynamic Media Imaging Server does not recognize 3D formats. As such, after you publish a 3D asset in Dynamic Media, you have an instant URL that you can copy. The URL for the 3D asset follows the usual Dynamic Media URL structure. However, you cannot edit any parameters in the asset&#39;s URL, unlike traditional image assets in Dynamic Media.

[](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)

****&#x200B;在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

[!DNL Experience Manager]

[](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

[](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

****

1. Open a 3D asset (GLB, OBJ, or STL file format).
1. ****

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. ****
1. ****

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. ********
   * The 3D asset is a supported format (GLB, OBJ, STL, and USDZ).
   * The 3D asset was ingested into the Dynamic Media Image Production System (IPS).
   * The 3D asset is published.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. ****

### Alternate methods for publishing Dynamic Media 3D assets using the Dimensional viewer {#alternate-publish-methods}

**[!DNL Experience Manager]

* ********

   [](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)

* ********&#x200B;将嵌入代码复制到剪贴板，以便将其粘贴到网页中。 ****

   [](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)
