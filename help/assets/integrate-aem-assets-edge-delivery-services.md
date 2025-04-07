---
title: '在为 [!DNL Edge Delivery Services]创作内容时集成 [!DNL AEM Assets] '
description: 了解如何将 [!DNL AEM Assets] 与 [!DNL Edge Delivery Services]. This integration enables you to integrate [!DNL AEM Assets] 与 [!DNL Microsoft Word] 集成，将 [!DNL Google Docs], integrate [!DNL AEM Assets] 与 [!DNL Universal Editor], integrate [!DNL Dynamic Media] 与 [!DNL Edge Delivery Services], integrate [!DNL Dynamic Media with OpenAPI capabilities] 与 [!DNL Universal Editor] 集成，以及如何将 [!DNL Dynamic Media with OpenAPI capabilities] 与 [!DNL Microsoft Word] 和 [!DNL Google Docs]集成。
tags: AEM Assets, Edge Delivery Services, Dynamic Media, Dynamic Media with OpenAPI capabilities, Universal Editor, Edge Delivery Services with Universal Editor
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: fecaefbb6a02e944be38c3dfaa3baea5691219cd
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 6%

---


# 在为[!DNL Edge Delivery Services]创作内容时集成[!DNL AEM Assets] {#integrate-aem-assets-with-edge-delivery-services}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 和 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用 Dynamic Media Prime 和 Ultimate</b></a>
        </td>
         <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
    </tr>
    <tr>
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

![AEM资源与通用编辑器的集成](/help/assets/assets/EDS2.png)

[[!DNL Edge Delivery Services]](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/overview)是一组可组合的服务，允许您高度灵活地在网站上创作和交付内容。 您可以使用[AEM内容管理](/help/sites-cloud/authoring/author-publish.md)和[WYSIWYG创作（使用 [!DNL Universal Editor] 以及基于文档的创作](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)）。

您可以在以下位置编辑内容：

* [[!DNL Microsoft Word]或 [!DNL Google Docs]](#integrate-dynamic-media-with-edge-delivery-services)
* [[!DNL Universal Editor]](#integrate-aem-assets-with-universal-editor-UE)

编辑内容后，您可以将其发布到Edge Delivery Services。

## 将[!DNL AEM Assets]与[!DNL Edge Delivery Services]的基于文档的创作流集成 {#integrate-dynamic-media-with-edge-delivery-services}

当[!DNL AEM Assets]与您的基于文档的创作工具（如[!DNL Microsoft Word]或[!DNL Google Docs]）集成时，它会在您的创作工具中提供资产选择器。 使用此资产选择器访问[!DNL AEM Assets]，并将批准的资产插入您的内容。
如果您已经拥有[!DNL Edge Delivery Services]网站，请参阅[[!DNL AEM Assets] 插件](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)文档，以了解如何将[!DNL AEM Assets]与您现有的[!DNL AEM]项目集成。
如果您没有[!DNL Edge Delivery Services]网站来发布在基于文档的创作工具中创作的[!DNL AEM Assets]包含内容，请遵循以下[先决条件](#integrate-aem-assets-with-microsoft-word-and-google-docs)和[集成 [!DNL AEM Assets] 与基于文档的创作环境](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs)部分。

### 先决条件{#integrate-aem-assets-with-microsoft-word-and-google-docs}

在开始之前，请确保您的基于文档的创作环境已准备就绪：

* 将[!DNL AEM]与基于文档的创作工具集成以设置创作环境。 请参阅[快速入门 — 开发人员教程](https://www.aem.live/developer/tutorial)，了解如何设置创作环境。

### 将[!DNL AEM Assets]与基于文档的创作环境集成{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

在[!DNL Microsoft Word]或[!DNL Google Docs]中创作内容时，将[!DNL AEM Assets] Sidekick插件配置为使用资源。

* 请参阅[[!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors)以了解如何在Microsoft Word或Google Docs中访问和使用AEM Assets。
* 有关配置详细信息，请参阅[配置 [!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin)。
  ![在ms word和google文档中使用具有openAPI功能的Dynamic Media](/help/assets/assets/my-assets-sidebar.png)

## 使用[!DNL Dynamic Media with OpenAPI capabilities]交付资源 {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

您还可以使用通过[!DNL Dynamic Media with OpenAPI capabilities]交付的资产。 它提供了许多好处，例如：

* 仅从[!DNL AEM Assets Cloud Services]访问品牌批准的资产（图像、视频、PDF和其他资产类型）。
* 管理（引用与资产的副本），这有助于自动传播资产生命周期事件，如到期、删除和更新。
* 动态图像演绎版和智能裁剪。
* 富媒体优化和交付，例如现成的自适应视频流以及PDF的原始资产交付。
* 资产级别的展示次数报表（[有限可用性](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)）。

有关功能的更多详细信息，请参阅[[!DNL Dynamic Media with OpenAPI capabilities]](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview)文档。

### 先决条件 {#dynamic-media-with-universal-editor-and-edge-delivery-services}

要使用资源引用，您必须具有：

* 有权访问已启用[!DNL Dynamic Media with Open API capabilities]的Assets Cloud Service环境。
* [!DNL Dynamic Media]许可证。
* [!DNL AEM Assets sidekick plugin]已启用，并启用了图像资源的复制引用。 有关更多详细信息，请参阅[此文档](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode)以进行基于文档的创作，并参阅[此文档](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)以进行基于通用编辑器的创作。
* 已批准的Assets。 批准的资源通过Assets Cloud Services后端或UI操作具有`dam:status=Approved`。

### 使用通过[!DNL Dynamic Media with OpenAPI capabilities]交付的资产{#Using-Dynamic-Media-with-edge-delivery-services}

选择以下链接，了解如何使用[!DNL Dynamic Media with OpenAPI capabilities]在内容中传递图像、视频和其他资源类型：

* [将图像添加到您的内容](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [将视频添加到您的内容](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [将非图像和视频资源(如PDF、Zip文件等)添加到您的内容中](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

观看本视频，了解如何使用带OpenAPI功能的Dynamic Media在您的内容中投放资产。

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## 示例[!DNL Edge Delivery Services]站点{#dynamic-media-with-google-docs-and-ms-word}

请参阅[WKND Travel](http://bit.ly/3DExLnf)，该网站是使用[!DNL Edge Delivery Services]的基于文档的创作功能生成的。 网站内容是在[Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT)中创作的，而[!DNL Dynamic Media with OpenAPI capabilities]用于交付内容中的资源。 创作后，内容将直接从文档发布。 浏览此[Git存储库](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks)以了解用于为此[!DNL Edge Delivery Services (EDS)]站点创建基于文档的创作设置的所有基本文件、文件夹、配置、网站样式和功能代码。

## 将[!DNL AEM Assets]与[!DNL Edge Delivery Services]的基于[!DNL Universal Editor]的创作流集成 {#integrate-aem-assets-with-universal-editor-UE}

设置[!DNL Universal Editor]以与[!DNL AEM Assets]集成。 此集成允许您使用[!DNL Dynamic Media with OpenAPI capabilities]交付资产。

* 查看 [!DNL Edge Delivery] 站点](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)中的[配置，了解如何在[!DNL Universal Editor]中添加自定义资产选取器函数。 自定义资产选取器允许您将资产直接插入到[!DNL Universal Editor]内容中。
* 请参阅[扩展概述](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)，了解如何在[!DNL Universal Editor]中创作时访问[!DNL AEM Assets]并插入资产。
