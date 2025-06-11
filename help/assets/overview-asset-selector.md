---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资产选择器'
description: 使用资产选择器在您的应用程序中搜索、查找和检索资产的元数据和演绎版。
role: Admin, User
exl-id: 62b0b857-068f-45b7-9018-9c59fde01dc3
source-git-commit: fb1e73b24e0717998a69132cc8f196193c87bab4
workflow-type: ht
source-wordcount: '1598'
ht-degree: 100%

---

# 微前端资产选择器 {#Overview}

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

微前端资产选择器提供了一个用户界面，它可以轻松地与 [!DNL Experience Manager Assets] 存储库集成，以便您能够浏览或搜索存储库中可用的数字资产，并在您的应用程序创作体验中使用它们。

微前端用户界面可用于采用了资产选择器包的应用程序体验。对该包的任何更新都会自动导入，并且最新部署的资产选择器会自动加载到您的应用程序中。

![概述](assets/overview.png)

资产选择器提供了许多好处，例如：

* 使用 Vanilla JavaScript 库，可轻松与任何 [Adobe](/help/assets/integrate-asset-selector-adobe-app.md) 或[非 Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md) 应用程序集成。
* 易于维护，因为对资产选择器包的更新将自动部署到可用于应用程序的资产选择器。您的应用程序中无需更新即可加载最新的修改。
* 易于定制，因为提供了用于控制应用程序中的资产选择器显示的属性。
* 全文搜索、开箱即用和自定义过滤器，可快速导航到资产以便在创作体验中使用。
* 能够在 IMS 组织内切换存储库以选择资产。
* 能够按名称、维度和大小对资产进行排序，并在列表、网格、库或瀑布视图中查看它们。

<!--Perform the following tasks to integrate and use Asset Selector with your [!DNL Experience Manager Assets] repository:

1. [Install Asset Selector](#installation)
2. [Integrate Asset Selector using Vanilla JS](#integration-using-vanilla-js)
3. [Use Asset Selector](#using-asset-selector)
-->

<!--
## Setting up Asset Selector {#asset-selector-setup}

![Asset Selector set up](assets/asset-selector-prereqs.png)
-->

## 先决条件{#prereqs}

您必须确保采用以下通信方式：

* 主机应用程序在 HTTPS 上运行。
* 您无法在 `localhost` 上运行此应用程序。如果您想在本地机器上集成资产选择器，则需要创建一个自定义域，例如 `[https://<your_campany>.localhost.com:<port_number>]`，并将此自定义域添加到 `redirectUrl list` 中。
* 您可以使用相应的 `imsClientId` 配置 clientID 并将其添加到 AEM Cloud Service 环境变量中。
<!--* You can configure and add `ADOBE_PROVIDED_CLIENT_ID` into the AEM Cloud Service environment variable with the respective `imsClientId`.
![Asset Selector IMS Client id environment](assets/asset-selector-ims-client-id-env.png)-->
* 需要在环境配置中定义 IMS 范围列表。
* 该应用程序的 URL 位于 IMS 客户端的重定向 URL 允许列表中。
* 使用 Web 浏览器上的弹出窗口配置和呈现 IMS 登录流。因此，应在目标浏览器上启用或允许弹出窗口。

如果您需要资产选择器的 IMS 身份验证工作流，请使用上述先决条件。或者，如果您已经通过 IMS 工作流程进行身份验证，那么您可以添加 IMS 信息。

**查看更多**

* [将资产选择器与 Adobe 应用程序集成](/help/assets/integrate-asset-selector-adobe-app.md)
* [将资产选择器与一个非 Adobe 应用程序集成](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [集成资产选择器 Dynamic Media 开放 API](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!IMPORTANT]
>
> 此存储库旨在作为补充文档，描述集成资产选择器的可用 API 和使用示例。在尝试安装或使用资产选择器之前，请确保您的组织已在 Experience Manager Assets as a Cloud Service 配置文件中被授予访问资产选择器的权限。如果您尚未进行配置，则无法集成或使用这些组件。要请求配置，您的程序管理员应该从 Admin Console 提交一个标记为 P2 的支持工单，并包含以下信息：
>
>* 托管集成应用程序的域名。
>* 配置后，您的组织将获得与配置资产选择器所需的环境相对应的 `imsClientId`、`imsScope` 和 `redirectUrl`。没有这些有效属性，您无法运行安装步骤。

## 安装 {#installation}

资产选择器可通过 ESM CDN（例如，[esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)）和 [UMD](https://github.com/umdjs/umd) 版本获得。

在使用 **UMD 版本**&#x200B;的浏览器中（推荐）：

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

在使用 **ESM CDN 版本**&#x200B;带有 `import maps` 支持的浏览器中：

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

在使用 **ESM CDN 版本**&#x200B;的 Deno/Webpack 模块联合中：

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

## 使用资产选择器 {#using-asset-selector}

在设置完资产选择器后，您可以通过身份验证将资产选择器与您的 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 应用程序结合使用，可以选择资产或执行各种其他操作以在存储库中搜索您的资产。

![using-asset-selector](assets/using-asset-selector.png)

* **A**：[隐藏/显示面板](#hide-show-panel)
* **B**：[存储库切换器](#repository-switcher)
* **C**：[资产](#repository)
* **D**：[过滤器](#filters)
* **E**：[搜索栏](#search-bar)
* **F**：[排序](#sorting)
* **G**：[按升序或降序排序](#sorting)
* **H**：[查看](#types-of-view)

### 隐藏/显示面板 {#hide-show-panel}

要隐藏左侧导航中的文件夹，请单击 **[!UICONTROL 隐藏文件夹]**&#x200B;图标。要撤消更改，请再次单击 **[!UICONTROL 隐藏文件夹]**&#x200B;图标。

### 存储库切换器 {#repository-switcher}

资产选择器还允许您切换存储库以进行资产选择。您可以从左侧面板中可用的下拉列表中选择所选存储库。下拉列表中可用的存储库选项基于 `repositoryId` 文件中定义的 `index.html` 属性。它基于登录用户访问的选定 IMS 组织的环境。消费者可以传递首选 `repositoryID`，在这种情况下，资产选择器将停止呈现存储库切换器，并且仅呈现给定存储库中的资产。

### 资产存储库

它是可用于执行操作的资产文件夹的集合。

### 开箱即用的过滤器 {#filters}

资产选择器还提供开箱即用的过滤器选项来细化您的搜索结果。可用过滤器如下：

* **[!UICONTROL 状态]：** 包括 `all`、`approved`、`rejected` 或 `no status` 中的当前资产状态。
* **[!UICONTROL 文件类型]：** 包括 `folder`、 `file`、 `images`、 `documents` 或 `video`。
* **[!UICONTROL 过期状态]：** 根据到期时间提及资产。您可以选中 `[!UICONTROL Expired]` 复选框来过滤过期的资产；或设置资产的 `[!UICONTROL Expiration Duration]`，以根据资产的到期持续时间显示资产。当资产已过期或即将过期时，就会出现一个徽章来表示该资产已过期或即将过期。此外，您可以控制是否允许使用（或拖放）过期资产。详细了解[自定义过期资产](/help/assets/asset-selector-customization.md#customize-expired-assets)。默认情况下，对于将在未来 30 天内到期的资产，会显示&#x200B;**即将到期**&#x200B;徽章。但是，您可以使用 `expirationDate` 属性配置有效期限。

  >[!TIP]
  >
  > 如果您想根据资产的未来到期日查看或筛选资产，请在 `[!UICONTROL Expiration Duration]` 字段中注明未来的日期范围。它显示了带有&#x200B;**即将到期**&#x200B;徽章的资产。

* **[!UICONTROL MIME 类型]：** 包括 `JPG`、`GIF`、`PPTX`、`PNG`、`MP4`、`DOCX`、`TIFF`、`PDF`、`XLSX`。
* **[!UICONTROL 图像大小]：** 包括图像的最小/最大宽度、最小/最大高度。

  ![rail-view-example](assets/filters-asset-selector.png)

### 自定义搜索

除了全文搜索外，资产选择器还允许您使用自定义搜索在文件中搜索资产。您可以在“模态”视图和“边栏”视图模式下使用自定义搜索过滤器。

![custom-search](assets/custom-search1.png)

您还可以创建默认搜索过滤器，以保存您经常搜索的字段，并在以后使用它们。要为资产创建自定义搜索，可以使用 `filterSchema` 属性。

### 搜索栏 {#search-bar}

资产选择器允许您对所选存储库中的资产进行全文搜索。例如，如果您在搜索栏中键入关键字 `wave`，则将显示任意元数据属性中提及的所有带 `wave` 关键字的资产。

### 排序 {#sorting}

您可以在资产选择器中按资产的名称、尺寸或大小对资产进行排序。您还可以按升序或降序对资产进行排序。

### 视图类型 {#types-of-view}

资产选择器允许您在四种不同的视图中查看资产：

* ![列表视图](assets/do-not-localize/list-view.png) [!UICONTROL **列表视图**]&#x200B;列表视图在单个列中显示可滚动的文件和文件夹。
* ![网格视图](assets/do-not-localize/grid-view.png) [!UICONTROL **网格视图**] 网格视图以行和列的网格显示可滚动的文件和文件夹。
* ![库视图](assets/do-not-localize/gallery-view.png) [!UICONTROL **库视图**] 库视图以居中锁定的水平列表显示文件或文件夹。
* ![瀑布视图](assets/do-not-localize/waterfall-view.png)[!UICONTROL **瀑布**&#x200B;视图]瀑布视图以桥的形式显示文件或文件夹。

### 资产详细信息和元数据 {#asset-details-and-metadata}

资产详情页面提供特定资产的全面视图，可将所有关键信息集中在一处。它包括带有名称、文件格式、状态和简要说明的概述，以及预览或缩略图，以便于视觉识别。它还包括资产的元数据，例如创建日期、作者、大小、配色方案等。这些属性有助于有效地搜索、过滤和分类资产。资产选择器的边栏视图和模态视图中均提供资产详细信息面板。在边栏视图中，需要启用并配置 `onDrop` 属性来返回资产。或者在模态视图中，`handleSelection` 属性会返回一项资产。请参阅[资产选择器属性](asset-selector-properties.md)。

要查看资产和元数据的详细信息，请执行以下步骤：

1. 打开资产选择器 MFE 并导航到资产。
1. 将鼠标悬停在资产上，然后点击![信息图标](/help/assets/assets/info-icon-solid-black.svg)。
1. 转到&#x200B;**[!UICONTROL 信息]**&#x200B;选项卡，以查看资产的详细信息。 <!--Otherwise, go to the **[Renditions](#asset-renditions)** tab to see renditions of an asset.-->

要自定义资产的详细信息视图面板，请参阅[自定义模态视图中的信息](asset-selector-customization.md#customize-info-in-modal-view)。

![资产详细信息](assets/asset-details.png)

<!--

#### Asset renditions {#asset-renditions}

Renditions in Adobe Experience Manager (AEM) are customized versions of digital assets, such as images, designed for different devices and platforms to ensure optimal performance. See [Dynamic Media renditions](/help/assets/renditions.md#dynamic-media-renditions).

>[!NOTE]
>
>* Prerequisites to [Dynamic Media with OpenAPI Capabilities renditions](/help/assets/renditions.md##prereqs-dm-with-openapi-renditions).
>* Renditions tab in the details panel of an asset shows up if `featureSet`  props is set to `['detail-panel', 'dm-renditions']`.
>* An asset should be approved to see Dynamic Media with OpenAPI renditions and/or ensure processing/publishing of the asset to Dynamic Media is complete (for images only).

![Asset details dynamic media renditions](assets/asset-details-dm-renditions.png)

For assets that are approved and have renditions enabled, you see the **Dynamic Media with Open API** badge. 

![Dynamic Media Open API stamp](assets/dm-open-api-stamp.png)

Additionally, see [Asset Selector user interface for Dynamic Media with OpenAPI capabilities](integrate-asset-selector-dynamic-media-open-api.md##interface-dynamic-media-open-api).

##### Add modifiers {#modifiers-dm-media-renditions}

Beyond the common image settings available in the UI, Dynamic Media supports numerous advanced image modifications that you can specify in the Image Modifiers field. See [Defining image preset options with Image Modifiers](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/assets/dynamic/managing-image-presets#defining-image-preset-options-with-image-modifiers).

-->

## 详细了解关键功能 {#key-capabilities-asset-selector}

<table>
<tr>
    <td>
        <img src="assets/integrate-asset-selector.gif" width="70px" height="70px" alt="集成资产选择器图形"><br/>
        <a href="integrate-asset-selector.md">集成资产选择器</a>
        <p>
        <em>了解将资产选择器与多个应用程序集成的各种功能。
        </p>
     </td>
    <td>
        <img src="assets/with-adobe-app.gif" width="70px" height="70px" alt="将资产选择器与 Adobe 应用程序图形集成"><br/>
        <a href="integrate-asset-selector-adobe-app.md">将资产选择器与 Adobe 应用程序集成</a>
        <p>
        <em>了解如何将资产选择器与各种 Adobe 应用程序集成。</em>
        </p>
    </td>
    <td>
        <img src="assets/third-party-app.gif" width="70px" height="70px" alt="集成资产选择器图形"><br/>
        <a href="integrate-asset-selector-non-adobe-app.md">将资产选择器与第三方应用程序集成</a>
        <p>
        <em>挖掘将资产选择器与非 Adobe 应用程序集成的功能。</em>
        </p>
    </td>
    <td>
        <img src="assets/with-dynamic-media-open-api.gif" width="70px" height="70px" alt="集成资产选择器图形"><br/>
        <a href="integrate-asset-selector-dynamic-media-open-api.md">将资产选择器与 Dynamic Media 开放 API 集成</a>
        <p>
        <em>了解如何将资产选择器与 Dynamic Media 开放 API 集成。</em>
        </p>
     </td>
     <td>
        <img src="assets/asset-selector-properties.gif" width="70px" height="70px" alt="资产选择器示例图形"><br/>
        <a href="asset-selector-properties.md">资产选择器属性</a>
        <p>
        <em>以实际的方式了解属性的使用。</em>
        </p>
    </td>
</tr>
<tr>
    <td>
        <img src="assets/asset-selector-examples.gif" width="70px" height="70px" alt="资产选择器属性图形"><br/>
        <a href="asset-selector-examples.md">资产选择器示例</a>
        <p>
        <em>了解自定义资产选择器各种组件的基础知识，如过滤器、资产选择、过期资产等。 </em>
        </p>
    </td>
    <td>
        <img src="assets/customize-asset-selector.gif" width="70px" height="70px" alt="自定义资产选择器图形"><br/>
        <a href="asset-selector-customization.md">资产选择器自定义</a>
        <p>
        <em>根据您的可用性配置和自定义资产选择器的各种组件。</em>
        </p>
    </td>
    <td>
        <img src="assets/asset-selector-upload.gif" width="70px" height="70px" alt="资产选择器上传图形"><br/>
        <a href="asset-selector-upload.md">资产选择器上传</a>
        <p>
        <em>了解如何从本地或第三方文件系统将文件或文件夹上传到资产选择器。</em>
        </p>
    </td>
     <td>
        <img src="assets/asset-selector-collections.gif" width="70px" height="70px" alt="资产选择器收藏集图形"><br/>
        <a href="asset-selector-collections.md">资产选择器收藏集</a>
        <p>
        <em>了解如何使用 Experience Manager 存储库在资产选择器中使用收藏集。</em>
        </p>
    </td>
    <td>
    </td>
</tr>
</table>

>[!MORELIKETHIS]
>
>* [资产选择器自定义](/help/assets/asset-selector-customization.md)
>* [将资产选择器与各种应用程序集成](/help/assets/integrate-asset-selector.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
>* [将资产选择器与具有 OpenAPI 功能的 Dynamic Media 集成](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
