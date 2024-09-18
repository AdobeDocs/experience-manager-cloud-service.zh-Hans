---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 使用资产选择器可在应用程序中搜索、查找和检索资产的元数据和演绎版。
role: Admin, User
exl-id: 62b0b857-068f-45b7-9018-9c59fde01dc3
source-git-commit: 027922c304be9c36b600b04b264d571ea8ed60d4
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 34%

---

# 微前端资源选择器 {#Overview}

微前端资源选择器提供了一个用户界面，它可以轻松地与 [!DNL Experience Manager Assets] 存储库集成，以便您能够浏览或搜索存储库中可用的数字资源，并在您的应用程序创作体验中使用它们。

微前端用户界面可用于采用了资源选择器包的应用程序体验。对该包的任何更新都会自动导入，并且最新部署的资源选择器会自动加载到您的应用程序中。

![概述](assets/overview.png)

资源选择器提供了许多好处，例如：

* 使用Vanilla JavaScript库轻松与任何[Adobe](/help/assets/integrate-asset-selector-adobe-app.md)或[非Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md)应用程序集成。
* 易于维护，因为对资源选择器包的更新将自动部署到可用于应用程序的资源选择器。您的应用程序中无需更新即可加载最新的修改。
* 易于定制，因为提供了用于控制应用程序中的资源选择器显示的属性。
* 全文搜索、开箱即用和自定义过滤器，可快速导航到资源以便在创作体验中使用。
* 能够在 IMS 组织内切换存储库以选择资源。
* 能够按名称、维度和大小对资源进行排序，并在列表、网格、库或瀑布图视图中查看这些资源。

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

必须确保以下通信方法：

* 应用程序正在HTTPS上运行。
* 应用程序的URL位于IMS客户端的重定向URL允许列表中。
* IMS登录流通过Web浏览器上的弹出窗口进行配置和渲染。 因此，应在目标浏览器上启用或允许弹出窗口。

如果您需要资产选择器的IMS身份验证工作流，请使用上述先决条件。 或者，如果您已通过IMS工作流身份验证，则可以改为添加IMS信息。

**查看更多**

* [将资源选择器与Adobe应用程序集成](/help/assets/integrate-asset-selector-adobe-app.md)
* [将资源选择器与非Adobe应用程序集成](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [集成资产选择器Dynamic Media打开API](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!IMPORTANT]
>
> 此存储库旨在作为补充文档，描述用于集成Asset Selector的可用API和使用示例。 在尝试安装或使用资产选择器之前，请确保贵组织已获得资产选择器的访问权限，且已作为Experience Manager Assetsas a Cloud Service配置文件的一部分进行配置。 如果您尚未配置，则无法集成或使用这些组件。 要请求配置，您的项目管理员应从Admin Console中提出标记为P2的支持票证并包含以下信息：
>
>* 托管集成应用程序的域名。
>* 配置之后，将为您的组织提供`imsClientId`、`imsScope`以及对应于所请求环境的`redirectUrl`，这些环境对于配置资产选择器至关重要。 如果没有这些有效属性，您将无法运行安装步骤。

## 安装 {#installation}

资产选择器可通过ESM CDN（例如，[esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)）和[UMD](https://github.com/umdjs/umd)版本使用。

在使用 **UMD 版本**&#x200B;的浏览器中（推荐）：

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

在使用 **ESM CDN 版本**&#x200B;并支持 `import maps` 的浏览器中：

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

在使用 **ESM CDN 版本**&#x200B;的 Deno/Webpack 模块联合中：

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

## 使用资源选择器 {#using-asset-selector}

在设置完资源选择器后，您可以通过身份验证将资源选择器与您的 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 应用程序结合使用，可以选择资源或执行各种其他操作以在存储库中搜索您的资源。

![using-asset-selector](assets/using-asset-selector.png)

* **A**：[隐藏/显示面板](#hide-show-panel)
* **B**：[存储库切换器](#repository-switcher)
* **C**：[资源](#repository)
* **D**：[过滤器](#filters)
* **E**：[搜索栏](#search-bar)
* **F**：[排序](#sorting)
* **G**：[按升序或降序排序](#sorting)
* **H**：[查看](#types-of-view)

### 隐藏/显示面板 {#hide-show-panel}

要在左侧导航中隐藏文件夹，请单击&#x200B;**[!UICONTROL 隐藏文件夹]**&#x200B;图标。 要撤消更改，请再次单击&#x200B;**[!UICONTROL 隐藏文件夹]**&#x200B;图标。

### 存储库切换器 {#repository-switcher}

通过资产选择器，您还可以切换存储库以进行资产选择。 您可以从左侧面板中可用的下拉列表中选择所选存储库。下拉列表中可用的存储库选项基于 `index.html` 文件中定义的 `repositoryId` 属性。它基于登录用户访问的选定IMS组织的环境。 消费者可以传递首选 `repositoryID`，在这种情况下，资源选择器将停止呈现存储库切换器，并且仅呈现给定存储库中的资源。

### 资源存储库

它是可用于执行操作的资源文件夹的集合。

### 开箱即用的过滤器 {#filters}

资源选择器还提供开箱即用的过滤器选项来细化您的搜索结果。可用过滤器如下：

* **[!UICONTROL 状态]：**&#x200B;包括`all`、`approved`、`rejected`或`no status`之间的资源的当前状态。
* **[!UICONTROL 文件类型]：**&#x200B;包括`folder`、`file`、`images`、`documents`或`video`。
* **[!UICONTROL 到期状态]：**&#x200B;根据资产的到期持续时间提及该资产。 您可以选中`[!UICONTROL Expired]`复选框以筛选已过期的资产；或将资产的`[!UICONTROL Expiration Duration]`设置为根据资产的到期持续时间显示资产。 当资产已过期或即将过期时，系统会显示一个描述该资产的徽章。 此外，您可以控制是否允许使用（或拖放）已过期的资源。 查看有关[自定义过期资产](/help/assets/asset-selector-customization.md#customize-expired-assets)的详细信息。 默认情况下，对于在未来30天内过期的资产，会显示&#x200B;**即将过期**&#x200B;徽章。 但是，您可以使用`expirationDate`属性配置到期时间。

  >[!TIP]
  >
  > 如果要根据资产的未来到期日期查看或筛选资产，请在`[!UICONTROL Expiration Duration]`字段中提及未来日期范围。 它显示具有&#x200B;**即将过期**&#x200B;徽章的资源。

* **[!UICONTROL MIME类型]：**&#x200B;包括`JPG`、`GIF`、`PPTX`、`PNG`、`MP4`、`DOCX`、`TIFF`、`PDF`、`XLSX`。
* **[!UICONTROL 图像大小]：**&#x200B;包括图像的最小值/最大宽度、最小值/最大高度。

  ![rail-view-example](assets/filters-asset-selector.png)

### 自定义搜索

除了全文搜索之外，资产选择器还允许您使用自定义搜索在文件中搜索资产。 您可以在“模态”视图和“边栏”视图模式下使用自定义搜索过滤器。

![custom-search](assets/custom-search1.png)

您还可以创建默认搜索过滤器，以保存您经常搜索的字段并在以后使用。 要为资源创建自定义搜索，可以使用 `filterSchema` 属性。

### 搜索栏 {#search-bar}

通过资源选择器，您可以对选定存储库中的资源执行全文搜索。 例如，如果您在搜索栏中键入关键字 `wave`，则将显示任意元数据属性中提及的所有带 `wave` 关键字的资源。

### 排序 {#sorting}

您可以在资源选择器中按资源的名称、尺寸或大小对资源进行排序。您还可以按升序或降序对资源进行排序。

### 视图类型 {#types-of-view}

通过资源选择器，您可以在四种不同的视图中查看资源：

* **![列表视图](assets/do-not-localize/list-view.png) [!UICONTROL 列表视图]**&#x200B;列表视图在单个列中显示了可滚动的文件和文件夹。
* **![网格视图](assets/do-not-localize/grid-view.png) [!UICONTROL 网格视图]**&#x200B;网格视图在行和列的网格中显示可滚动的文件和文件夹。
* **![图库视图](assets/do-not-localize/gallery-view.png) [!UICONTROL 图库视图]**&#x200B;图库视图在中心锁定的水平列表中显示文件或文件夹。
* **![瀑布视图](assets/do-not-localize/waterfall-view.png) [!UICONTROL 瀑布视图]**&#x200B;瀑布视图以Bridge的形式显示文件或文件夹。

**概览图形**


## 了解关于关键功能的更多信息 {#key-capabilities-asset-selector}

<table>
<tr>
    <td>
        <img src="assets/integrate-asset-selector.gif" width="70px" height="70px" alt="“集成资产选择器”图形"><br/>
        <a href="integrate-asset-selector.md">集成资源选择器</a>
        <p>
        <em>了解将资产选择器与多个应用程序集成的各种功能。
        </p>
     </td>
    <td>
        <img src="assets/with-adobe-app.gif" width="70px" height="70px" alt="将Asset Selector与Adobe应用程序集成图形"><br/>
        <a href="integrate-asset-selector.md">将资源选择器与Adobe应用程序集成</a>
        <p>
        <em>了解如何将资源选择器与各种Adobe应用程序集成。</em>
        </p>
    </td>
    <td>
        <img src="assets/third-party-app.gif" width="70px" height="70px" alt="“集成资产选择器”图形"><br/>
        <a href="integrate-asset-selector.md">将资产选择器与第三方应用程序集成</a>
        <p>
        <em>发掘功能以将Asset Selector与非Adobe应用程序集成。</em>
        </p>
    </td>
    <td>
        <img src="assets/with-dynamic-media-open-api.gif" width="70px" height="70px" alt="“集成资产选择器”图形"><br/>
        <a href="integrate-asset-selector.md">将资源选择器与Dynamic Media Open API集成</a>
        <p>
        <em>了解如何将Asset Selector与Dynamic Media Open API集成。</em>
        </p>
     </td>
     <td>
        <img src="assets/asset-selector-examples.gif" width="70px" height="70px" alt="资产选择器属性图形"><br/>
        <a href="asset-selector-customization.md">资源选择器属性</a>
        <p>
        <em>了解自定义Asset Selector的各种组件（如筛选器、资产选择、过期资产等）的基础知识。</em>
        </p>
    </td>
</tr>
<tr>
    <td>
        <img src="assets/asset-selector-properties.gif" width="70px" height="70px" alt="资产选择器示例图形"><br/>
        <a href="asset-selector-customization.md">资源选择器示例</a>
        <p>
        <em>了解属性的实际用法。</em>
        </p>
    </td>
    <td>
        <img src="assets/customize-asset-selector.gif" width="70px" height="70px" alt="自定义资产选择器图形"><br/>
        <a href="asset-selector-customization.md">资源选择器自定义项</a>
        <p>
        <em>根据您的可用性配置和自定义资产选择器的各种组件。</em>
        </p>
    </td>
    <td>
        <img src="assets/asset-selector-upload.gif" width="70px" height="70px" alt="资产选择器上传图"><br/>
        <a href="asset-selector-upload.md">资产选择器上传</a>
        <p>
        <em>了解如何从本地或第三方文件系统将文件或文件夹上传到Asset Selector。</em>
        </p>
    </td>
     <td>
        <img src="assets/asset-selector-collections.gif" width="70px" height="70px" alt="“资产选择器”收藏集图形"><br/>
        <a href="asset-selector-collections.md">资产选择器收藏集</a>
        <p>
        <em>了解如何在Asset Selector中使用Experience Manager存储库。</em>
        </p>
    </td>
    <td>
    </td>
</tr>
</table>

>[!MORELIKETHIS]
>
>* [资产选择器自定义项](/help/assets/asset-selector-customization.md)
>* [将资产选择器与各种应用程序集成](/help/assets/integrate-asset-selector.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
>* [将资源选择器与Dynamic Media与OpenAPI功能集成](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
