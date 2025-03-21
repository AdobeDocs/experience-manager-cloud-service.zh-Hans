---
title: 在为 Edge Delivery Services 创作内容时集成 AEM Assets
description: 了解如何将AEM Assets与Edge Delivery Services集成。 通过此集成，您可以将AEM Assets与Microsoft Word和Google Docs集成，将AEM Assets与通用编辑器集成，将Dynamic Media与OpenAPI功能与通用编辑器集成，并将Dynamic Media与OpenAPI功能与Microsoft Word和Google Docs集成。
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: e4a71d1a513bebed67b9571a483871dc16c36daa
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 3%

---

# 在为 Edge Delivery Services 创作内容时集成 AEM Assets {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

具有UE的![AEM资源](/help/assets/assets/EDS2.png)

[Edge Delivery Services](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/overview)是一组可组合的服务，允许您高度灵活地在网站上创作和交付内容。 您可以使用通用编辑器和基于文档的创作来使用[AEM内容管理](/help/sites-cloud/authoring/author-publish.md)和[WYSIWYG创作](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)。

您可以在以下位置编辑内容：

* [Microsoft Word或Google Docs](#integrate-aem-assets-with-document-based-authoring-tools)
* [通用编辑器](#integrate-aem-assets-with-UE-universal-editor)

编辑内容后，您可以将其发布到Edge Delivery Services。

## 将AEM Assets与Edge Delivery Services的基于文档的创作流集成 {#integrate-aem-assets-with-document-based-authoring-tools}

当AEM Assets与基于文档的创作工具(如Microsoft Word或Google Docs)集成时，它会在您的编辑器中提供资产选择器。 使用此资源选择器可访问AEM Assets，并将批准的资源插入到您的文档中。
如果您已经拥有Edge Delivery Services网站，请参阅[AEM Assets插件](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)文档，了解如何将AEM Assets与现有AEM项目集成。
如果您没有AEM Assets网站来发布使用基于文档的创作工具创作的、包含AEM Assets的内容，请遵循以下[先决条件](#integrate-aem-assets-with-microsoft-word-and-google-docs)和[将Edge Delivery Services与基于文档的创作环境集成](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs)部分。

### 先决条件{#integrate-aem-assets-with-microsoft-word-and-google-docs}

在开始之前，请确保您的基于文档的创作环境已准备就绪：

* 将AEM与基于文档的创作工具集成以设置创作环境。 请参阅[快速入门 — 开发人员教程](https://www.aem.live/developer/tutorial)，了解如何设置创作环境。

### 将AEM Assets与基于文档的创作环境集成{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

配置AEM Assets Sidekick插件以在Microsoft Word或Google Docs中创作内容时使用资源。

* 请参阅[Adobe Experience Manager Assets Sidekick插件](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors)，了解如何在Microsoft Word或Google Docs中访问和使用AEM Assets。
* 有关配置详细信息，请参阅[配置Adobe Experience Manager Assets Sidekick插件](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin)。
  ![在ms word和google文档中使用具有openAPI功能的Dynamic Media](/help/assets/assets/my-assets-sidebar.png)

## 使用具有OpenAPI功能的Dynamic Media交付资源 {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

您还可以使用通过DM和OpenAPI功能提供的资产。 它提供了许多好处，例如：

* 从AEM Assets Cloud Services仅访问品牌批准的资源（图像、视频、PDF和其他资源类型）。
* 管理（引用与资产的副本），这有助于自动传播资产生命周期事件，如到期、删除和更新。
* 动态图像演绎版和智能裁剪。
* 富媒体优化和交付，例如现成的自适应视频流以及PDF的原始资产交付。
* 资产级别的展示次数报表（[有限可用性](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)）。

有关功能的更多详细信息，请参阅[具有OpenAPI功能的Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview)文档。

### 先决条件 {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

要使用资源引用，您必须具有：

* 有权访问启用了带开放API功能的Dynamic Media的Assets Cloud Service环境。
* Dynamic Media许可证。
* 启用了AEM Assets sidekick插件，并为图像资源启用了复制引用。 有关更多详细信息，请参阅基于文档的创作的[this](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode)和基于通用编辑器的创作的[this](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)。
* 已批准的Assets。 批准的资源通过Assets Cloud Services后端或UI操作具有`dam:status=Approved`。

### 使用具有OpenAPI功能的Dynamic Media交付的资源{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

选择以下链接，了解如何将Dynamic Media与OpenAPI功能结合使用，以在您的内容中交付图像、视频和其他资产类型：

* [将图像添加到您的内容](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [将视频添加到您的内容](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [将非图像和视频资源(如PDF、Zip文件等)添加到您的内容中](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

观看本视频，了解如何使用带OpenAPI功能的Dynamic Media在您的内容中投放资产。

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Edge Delivery Services站点示例{#example-of-an-Edge-Delivery-Services-site}

请参阅[WKND Travel](http://bit.ly/3DExLnf)，这是使用Edge Delivery Services的基于文档的创作功能构建的网站。 网站内容是在[Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT)中创作的，而具有OpenAPI功能的Dynamic Media用于在内容中投放资源。 创作后，内容将直接从文档发布。 浏览此[Git存储库](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks)，了解用于为此Edge Delivery Services (EDS)站点创建基于文档的创作设置的所有基本文件、文件夹、配置、网站样式和功能代码。

## 将AEM Assets与基于Universal Editor的Edge Delivery Services创作流集成 {#integrate-aem-assets-with-UE-universal-editor}

设置通用编辑器以与AEM Assets集成。 通过此集成，您可以使用具有OpenAPI功能的Dynamic Media来交付资产。

* 请参阅Edge Delivery站点中的[配置](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)，了解如何在通用编辑器中添加自定义资产选取器函数。 通过自定义资产选取器，可将资产直接插入通用编辑器内容。
* 请参阅[扩展概述](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)，了解如何在Universal Editor中进行创作时访问AEM Assets和插入资源。
