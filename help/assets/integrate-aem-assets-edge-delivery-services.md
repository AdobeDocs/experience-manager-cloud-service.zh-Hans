---
title: 在为 Edge Delivery Services 创作内容时集成 AEM Assets
description: 了解如何将AEM Assets与Edge Delivery Services集成。 通过此集成，您可以将AEM Assets与Microsoft Word和Google文档集成，将AEM Assets与通用编辑器集成，将Dynamic Media与OpenAPI功能与通用编辑器集成，并将Dynamic Media与Microsoft Word和Google文档中的OpenAPI功能集成。
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: e6fd7b1d16aac5e7021a8c309f6483f98746e85e
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 3%

---

# 在为 Edge Delivery Services 创作内容时集成 AEM Assets {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

![EDS2](/help/assets/assets/EDS2.png)

[Edge Delivery Services](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/overview)是一组可组合的服务，允许您高度灵活地在网站上创作和交付内容。 您可以使用通用编辑器和基于文档的创作](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)，同时使用[AEM内容管理](/help/sites-cloud/authoring/author-publish.md)和[WYSIWYG创作。

您可以在以下位置编辑内容：

* [Microsoft Word或Google文档](#integrate-aem-assets-with-document-based-authoring-tools)

* [通用编辑器](#integrate-aem-assets-with-universal-editor)

编辑内容后，您可以将其发布到Edge Delivery Services。

## 将AEM Assets与Edge Delivery Services的基于文档的创作流集成 {#integrate-aem-assets-with-document-based-authoring-tools}

AEM Assets与基于文档的创作工具(如Microsoft Word或Google Docs)集成，可在您的编辑器中直接提供资产选择器。 使用此资源选择器可访问AEM Assets，并将批准的资源插入到您的文档中。

如果您已有Edge Delivery Services网站，请参阅[AEM Assets插件](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)将AEM Assets与您现有的AEM项目集成。 如果您没有Edge Delivery Services网站，请参阅下面的[先决条件](#integrate-aem-assets-with-microsoft-word-and-google-docs)和[将AEM Assets与基于文档的创作环境集成](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs)部分。

### 先决条件{#integrate-aem-assets-with-microsoft-word-and-google-docs}

在开始之前，请确保您的基于文档的创作环境已准备就绪：

* 将AEM与基于文档的创作工具集成以设置创作环境。 请参阅[快速入门 — 开发人员教程](https://www.aem.live/developer/tutorial)以设置创作环境。

### 将AEM Assets与基于文档的创作环境集成{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

配置AEM AssetsSidekick插件以在Microsoft Word或Google文档中创作内容时使用资源。

* 请参阅[Adobe Experience Manager AssetsSidekick插件](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors)，了解如何在Microsoft Word或Google文档中访问和使用AEM Assets。
* 有关配置详细信息，请参阅[配置Adobe Experience Manager AssetsSidekick插件](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin)。
  ![my-assets-sidebar](/help/assets/assets/my-assets-sidebar.png)

## 使用具有OpenAPI功能的Dynamic Media交付资源 {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

您还可以使用通过DM和OpenAPI功能提供的资产。 它提供了许多好处，例如：

* 只能从AEM AssetsCloud Service访问品牌批准的资源(图像、视频、PDF和其他资源类型)。
* 管理（引用与资产的副本），这有助于自动传播资产生命周期事件，如到期、删除和更新。
* 动态图像演绎版和智能裁剪。
* 富媒体优化和交付，例如现成的自适应视频流以及针对PDF的原始资源交付。
* 资产级别的展示次数报表（[有限可用性](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)）。

有关这些功能的更多详细信息，请参阅具有OpenAPI功能的[Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview)文档。

### 先决条件 {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

要使用资源引用，您必须具有：

* 有权访问启用了带开放API功能的Dynamic Media的AssetsCloud Service环境。
* Dynamic Media许可证。
* 启用了AEM Assets sidekick插件，并为图像资源启用了复制引用。 有关更多详细信息，请参阅基于文档的创作的[this](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode)和基于通用编辑器的创作的[this](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)。
* 已批准的Assets。 批准的资源通过AssetsCloud Service后端或UI操作具有`dam:status=Approved`。

### 使用通过Dynamic Media提供的具有OpenAPI功能的资源{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

要在创作内容时使用通过具有OpenAPI功能的Dynamic Media交付的资源，请参阅：

* [使用图像引用](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [使用视频引用](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [对非图像和视频资源(如PDF、Zip文件等)使用资源引用](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

观看此视频，了解如何使用具有OpenAPI功能的Dynamic Media交付资源。

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## 示例Edge Delivery Services站点{#example-of-an-Edge-Delivery-Services-site}

请参阅[WKND旅游](https://aem-dynamicmedia-demo--dm--hlxsites.aem.live/travel-hospitality/wknd-trvl-home)。 此站点是使用Edge Delivery Services的基于文档的创作功能构建的。 网站内容是在[Google文档](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT)中创作的，使用Dynamic Media的OpenAPI功能进行资源交付。 创作后，将直接从文档发布内容。 对于此基于文档的创作设置，所有必需的文件、文件夹、配置、网站样式和功能代码都存储在此[Git存储库](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks)中。

## 将AEM Assets与基于Universal Editor的Edge Delivery Services创作流集成 {#integrate-aem-assets-with-universal-editor}

设置通用编辑器以与AEM Assets集成。 通过这种集成，您可以使用具有OpenAPI功能的Dynamic Media来交付资源。

* 请参阅Edge Delivery站点中的[配置](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)以在Universal Editor中添加自定义资产选取器函数。 通过自定义资产选取器，可将资产直接插入通用编辑器内容。
* 请参阅[扩展概述](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)，了解如何在Universal Editor中进行创作时访问AEM Assets和插入资源。
