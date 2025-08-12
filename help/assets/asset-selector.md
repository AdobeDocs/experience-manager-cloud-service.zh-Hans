---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 使用资源选择器在您的应用程序中搜索、查找和检索资源的元数据和演绎版。
contentOwner: KK
feature: Selectors
role: Admin,User
exl-id: 5f962162-ad6f-4888-8b39-bf5632f4f298
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '5357'
ht-degree: 38%

---

# 微前端资源选择器 {#Overview}

微前端资源选择器提供了一个用户界面，它可以轻松地与 [!DNL Experience Manager Assets] 存储库集成，以便您能够浏览或搜索存储库中可用的数字资源，并在您的应用程序创作体验中使用它们。

微前端用户界面可用于采用了资产选择器包的应用程序体验。对该包的任何更新都会自动导入，并且最新部署的资产选择器会自动加载到您的应用程序中。

![概述](assets/overview.png)

资产选择器提供了许多好处，例如：

* 使用Vanilla JavaScript库轻松与任何[Adobe](#asset-selector-ims)或[非Adobe](#asset-selector-non-ims)应用程序集成。
* 易于维护，因为对资产选择器包的更新将自动部署到可用于应用程序的资产选择器。您的应用程序中无需更新即可加载最新的修改。
* 易于定制，因为提供了用于控制应用程序中的资产选择器显示的属性。
* 全文搜索、开箱即用和自定义过滤器，可快速导航到资产以便在创作体验中使用。
* 能够在 IMS 组织内切换存储库以选择资源。
* 能够按名称、维度和大小对资源进行排序，并在列表、网格、库或瀑布视图中查看它们。

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

* 该应用程序在 HTTPS 上运行。
* 该应用程序的 URL 位于 IMS 客户端的重定向 URL 允许列表中。
* 使用 Web 浏览器上的弹出窗口配置和呈现 IMS 登录流。因此，应在目标浏览器上启用或允许弹出窗口。

如果您需要资产选择器的IMS身份验证工作流，请使用上述先决条件。 或者，如果您已经通过 IMS 工作流程进行身份验证，那么您可以添加 IMS 信息。

>[!IMPORTANT]
>
> 此存储库旨在作为补充文档，描述集成资产选择器的可用 API 和使用示例。在尝试安装或使用资产选择器之前，请确保您的组织已在 Experience Manager Assets as a Cloud Service 配置文件中被授予访问资产选择器的权限。如果您尚未进行配置，则无法集成或使用这些组件。要请求配置，您的项目管理员应从Admin Console中提出标记为P2的支持票证并包含以下信息：
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

## 使用 Vanilla JS 集成资源选择器 {#integration-using-vanilla-js}

您可以将任何[!DNL Adobe]或非Adobe应用程序与[!DNL Experience Manager Assets]存储库集成并从应用程序中选择资源。 请参阅[资产选择器与各种应用程序的集成](#asset-selector-integration-with-apps)。

通过导入资源选择器包并使用 Vanilla JavaScript 库连接到 Assets as a Cloud Service 来实现集成。编辑应用程序中的`index.html`或任何适当的文件，以：

* 定义身份验证详细信息
* 访问 Assets as a Cloud Service 存储库
* 配置资源选择器显示属性

在以下情况下，您无需定义某些 IMS 属性即可执行身份验证：

* 您正在 [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=zh-Hans) 上集成 [!DNL Adobe] 应用程序。
* 您已生成用于身份验证的 IMS 令牌。

## 将资产选择器与各种应用程序集成 {#asset-selector-integration-with-apps}

您可以将Asset Selector与各种应用程序集成，例如：

* [将资产选择器与 [!DNL Adobe] 应用程序集成](#adobe-app-integration-vanilla)
* [将资产选择器与一个非应用程序集成](#adobe-non-app-integration)
* [Dynamic Media与OpenAPI功能集成](#adobe-app-integration-polaris)

>[!BEGINTABS]

<!--Integration with an Adobe application content starts here-->

>[!TAB 与Adobe应用程序集成]

### 先决条件{#prereqs-adobe-app}

如果要将资产选择器与[!DNL Adobe]应用程序集成，请使用以下先决条件：

* [通信方法](#prereqs)
* imsOrg
* imsToken
* apikey

### 将资产选择器与[!DNL Adobe]应用程序集成 {#adobe-app-integration-vanilla}

以下示例演示了在Unified Shell下运行[!DNL Adobe]应用程序或已经为身份验证生成`imsToken`时，资产选择器的用法。

使用`script`标记将资产选择器包包含在您的代码中，如以下示例的&#x200B;_行6-15_&#x200B;所示。 加载该脚本后，`PureJSSelectors` 全局变量将可供使用。定义资产选择器[属性](#asset-selector-properties)，如&#x200B;_行16-23_&#x200B;中所示。 在Adobe应用程序中身份验证需要`imsOrg`和`imsToken`属性。 `handleSelection` 属性用于处理选定资源。要呈现资源选择器，请调用 `renderAssetSelector` 函数，如&#x200B;_第 17 行_&#x200B;中所述。资源选择器将显示在 `<div>` 容器元素中，如&#x200B;_第 21 行和第 22 行_&#x200B;中所示。

按照这些步骤，您可以将资产选择器与[!DNL Adobe]应用程序结合使用。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const assetSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderAssetSelector` available in PureJSSelectors globals to render AssetSelector
        PureJSSelectors.renderAssetSelector(container, assetSelectorProps);
    </script>
</head>

<body>
    <div id="asset-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

<!--For detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

+++**ImsAuthProps**
`ImsAuthProps`属性定义资产选择器用于获取`imsToken`的身份验证信息和流程。 通过设置这些属性，您可以控制身份验证流程的行为方式，并为各种身份验证事件注册侦听器。

| 属性名称 | 描述 |
|---|---|
| `imsClientId` | 表示用于身份验证的IMS客户端ID的字符串值。 此值由Adobe提供，特定于您的Adobe AEM CS组织。 |
| `imsScope` | 描述身份验证中使用的范围。 范围决定了应用程序对组织资源的访问级别。 多个范围可以用逗号分隔。 |
| `redirectUrl` | 表示验证后用户被重定向到的URL。 此值通常设置为应用程序的当前URL。 如果未提供`redirectUrl`，`ImsAuthService`将使用用于注册`imsClientId`的redirectUrl |
| `modalMode` | 布尔值，指示是否应在模态（弹出窗口）中显示身份验证流程。 如果设置为`true`，则身份验证流程将在弹出窗口中显示。 如果设置为`false`，则身份验证流程将以整页重新加载方式显示。 _Note :_为获得更好的UX，如果用户禁用了浏览器弹出窗口，则可以动态控制此值。 |
| `onImsServiceInitialized` | Adobe IMS身份验证服务初始化时调用的回调函数。 此函数接受一个参数`service`，该参数是表示Adobe IMS服务的对象。 有关更多详细信息，请参阅[`ImsAuthService`](#imsauthservice-ims-auth-service)。 |
| `onAccessTokenReceived` | 在从Adobe IMS身份验证服务收到`imsToken`时调用的回调函数。 此函数接受一个参数`imsToken`，该参数是一个表示访问令牌的字符串。 |
| `onAccessTokenExpired` | 访问令牌过期时调用的回调函数。 此函数通常用于触发新的身份验证流程以获取新的访问令牌。 |
| `onErrorReceived` | 身份验证期间发生错误时调用的回调函数。 此函数采用两个参数：错误类型和错误消息。 错误类型是表示错误类型的字符串，错误消息是表示错误消息的字符串。 |

+++

+++**ImsAuthService**
`ImsAuthService`类用于处理资产选择器的身份验证流程。 它负责从Adobe IMS身份验证服务获取`imsToken`。 `imsToken`用于对用户进行身份验证并授权作为[!DNL Adobe Experience Manager] Assets存储库访问[!DNL Cloud Service]。 ImsAuthService使用`ImsAuthProps`属性来控制身份验证流并注册各种身份验证事件的侦听器。 您可以使用方便的[`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice)函数向资产选择器注册&#x200B;_ImsAuthService_&#x200B;实例。 `ImsAuthService`类中有以下函数可用。 但是，如果您使用&#x200B;_registerAssetsSelectorsAuthService_&#x200B;函数，则无需直接调用这些函数。

| 函数名称 | 描述 |
|---|---|
| `isSignedInUser` | 确定用户当前是否已登录到服务并相应地返回布尔值。 |
| `getImsToken` | 检索当前登录用户的身份验证`imsToken`，该身份验证可用于验证其他服务（如生成资产_rendition）的请求。 |
| `signIn` | 启动用户的登录流程。 此函数使用`ImsAuthProps`在弹出窗口或全页重新加载中显示身份验证 |
| `signOut` | 将用户签出服务，使其身份验证令牌失效，并要求他们再次登录以访问受保护的资源。 调用此函数将重新加载当前页面。 |
| `refreshToken` | 刷新当前登录用户的身份验证令牌，防止该令牌过期，并确保对受保护资源的访问不会中断。 返回可用于后续请求的新身份验证令牌。 |

+++

+++使用提供的IMS令牌进行&#x200B;**验证**

```
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected asset: ", selection);
    };
    function renderAssetSelectorInline() {
    console.log("initializing Asset Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('asset-selector-container');
    PureJSSelectors.renderAssetSelector(container, props);
    }
    $(document).ready(function() {
    renderAssetSelectorInline();
    });
</script>
```

+++

+++**向IMS服务注册回调**

```
// object `imsProps` to be defined as below 
let imsProps = {
    imsClientId: <IMS Client Id>,
        imsScope: "openid",
        redirectUrl: window.location.href,
        modalMode: true,
        adobeImsOptions: {
            modalSettings: {
            allowOrigin: window.location.origin,
},
        useLocalStorage: true,
},
onImsServiceInitialized: (service) => {
            console.log("onImsServiceInitialized", service);
},
onAccessTokenReceived: (token) => {
            console.log("onAccessTokenReceived", token);
},
onAccessTokenExpired: () => {
            console.log("onAccessTokenError");
// re-trigger sign-in flow
},
onErrorReceived: (type, msg) => {
            console.log("onErrorReceived", type, msg);
},
}
```

+++

<!--Integration with non-Adobe application content starts here-->

>[!TAB 与非Adobe应用程序集成]

<!--### Integrate Asset Selector with a [!DNL non-Adobe] application {#adobe-non-app-integration}-->

### 先决条件 {#prereqs-non-adobe-app}

如果您要将资源选择器与非Adobe应用程序集成，请使用以下先决条件：

* [通信方法](#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

将资产选择器与非Adobe应用程序集成时，该资产选择器支持使用Identity Management System (IMS)属性（如[!DNL Experience Manager Assets]或`imsScope`）对`imsClientID`存储库进行身份验证。

+++**为非Adobe应用程序配置资源选择器**
要为非Adobe应用程序配置Asset Selector，您必须先记录用于预配的支持票证，然后执行集成步骤。

**正在记录支持票证**
通过Admin Console记录支持票证的步骤：

1. 在票证标题中添加带有AEM Assets **的**&#x200B;资源选择器。

1. 请在描述中提供以下详细信息：

   * [!DNL Experience Manager Assets]作为[!DNL Cloud Service] URL（项目ID和环境ID）。
   * 托管非Adobe Web应用程序的域名。
+++

+++**集成步骤**
在将Asset Selector与非Adobe应用程序集成时，使用此示例`index.html`文件进行身份验证。

使用`Script`标记访问资产选择器包，如示例&#x200B;*文件的*&#x200B;第9 *行到*&#x200B;第11`index.html`行所示。

示例的&#x200B;*行14*&#x200B;到&#x200B;*行38*&#x200B;描述了IMS流属性，如`imsClientId`、`imsScope`和`redirectURL`。 函数要求您至少定义`imsClientId`和`imsScope`属性之一。 如果您没有为`redirectURL`定义值，则使用客户端ID的注册重定向URL。

由于您没有生成`imsToken`，请使用`registerAssetsSelectorsAuthService`和`renderAssetSelectorWithAuthFlow`函数，如示例`index.html`文件的第40行至第50行所示。 使用`registerAssetsSelectorsAuthService`之前的`renderAssetSelectorWithAuthFlow`函数通过资产选择器注册`imsToken`。 [!DNL Adobe]建议在实例化组件时调用`registerAssetsSelectorsAuthService`。

在`const props`部分中定义身份验证和其他Assets as a Cloud Service访问相关的属性，如示例&#x200B;*文件的*&#x200B;行54 *到*&#x200B;行60`index.html`所示。

`PureJSSelectors`行65 *中提到的*&#x200B;全局变量用于呈现Web浏览器中的资产选择器。

资产选择器在`<div>`容器元素中呈现，如&#x200B;*行74*&#x200B;到&#x200B;*行81*&#x200B;中所述。 此示例使用对话框来显示资源选择器。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta charset="utf-8">
    <title>Asset Selectors</title>
    <link rel="stylesheet" href="index.css">
    <script id="asset-selector"
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/asset-selectors.js"></script>
    <script>

        const imsProps = {
            imsClientId: "<obtained from IMS team>",
            imsScope: "openid, <other scopes>",
            redirectUrl: window.location.href,
            modalMode: true, // false to open in a full page reload flow
            onImsServiceInitialized: (service) => {
                // invoked when the ims service is initialized and is ready
                console.log("onImsServiceInitialized", service);
            },
            onAccessTokenReceived: (token) => {
                console.log("onAccessTokenReceived", token);
            },
            onAccessTokenExpired: () => {
                console.log("onAccessTokenError");
                // re-trigger sign-in flow
            },
            onErrorReceived: (type, msg) => {
                console.log("onErrorReceived", type, msg);
            },
        }

        function load() {
            const registeredTokenService = PureJSSelectors.registerAssetsSelectorsAuthService(imsProps);
            imsInstance = registeredTokenService;
        };

        // initialize the IMS flow before attempting to render the asset selector
        load();
        

        //function that will render the asset selector
            const otherProps = {
            // any other props supported by asset selector
            }
            const assetSelectorProps = {
                "imsOrg": "imsorg",
                ...otherProps
            }
             // container element on which you want to render the AssetSelector/DestinationSelector component
            const container = document.getElementById('asset-selector');

            /// Use the PureJSSelectors in globals to render the AssetSelector/DestinationSelector component
            PureJSSelectors.renderAssetSelectorWithAuthFlow(container, assetSelectorProps, () => {
                const assetSelectorDialog = document.getElementById('asset-selector-dialog');
                assetSelectorDialog.showModal();
            });
        }
    </script>

</head>
<body class="asset-selectors">
    <div>
        <button onclick="renderAssetSelectorWithAuthFlowFlow()">Asset Selector - Select Assets with Ims Flow</button>
    </div>
        <dialog id="asset-selector-dialog">
            <div id="asset-selector" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
            </div>
        </dialog>
    </div>
</body>

</html>
```

+++

+++**无法访问投放存储库**

>[!TIP]
>
>如果您已使用注册登录工作流集成资产选择器，但仍无法访问投放存储库，请确保清理了浏览器Cookie。 否则，您最终会在控制台中收到`invalid_credentials All session cookies are empty`错误。

+++

<!--Integration with Polaris application content starts here-->

>[!TAB Dynamic Media与OpenAPI功能的集成]

### 先决条件 {#prereqs-polaris}

如果要将资产选择器与Dynamic Media以及OpenAPI功能集成，请使用以下先决条件：

* [通信方法](#prereqs)
* 要通过OpenAPI功能访问Dynamic Media，您必须拥有以下许可证：
   * Assets存储库(例如，Experience Manager Assets as a Cloud Service)。
   * AEM Dynamic Media。
* 只有[个批准的资产](#approved-assets.md)可用于确保品牌一致性。

### Dynamic Media与OpenAPI功能集成{#adobe-app-integration-polaris}

资产选择器与Dynamic Media OpenAPI进程的集成涉及多个步骤，包括创建自定义的Dynamic Media URL或准备选取Dynamic Media URL等。

+++**将Dynamic Media的资产选择器与OpenAPI功能集成**

`rootPath`和`path`属性不应包含在具有OpenAPI功能的Dynamic Media中。 相反，您可以配置`aemTierType`属性。 以下是配置的语法：

```
aemTierType:[1: "delivery"]
```

利用此配置，可查看所有批准的资产，但不包含文件夹或采用平面结构。 有关详细信息，请导航到`aemTierType`资产选择器属性[下的](#asset-selector-properties)属性

+++

+++**从批准的资源创建动态投放URL**
设置资源选择器后，将使用对象架构从所选资源创建动态投放URL。
例如，在选择资产时接收的来自对象数组中的某个对象的模式：

```
{
"dc:format": "image/jpeg",
"repo:assetId": "urn:aaid:aem:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"repo:name": "image-7.jpg",
"repo:repositoryId": "delivery-pxxxx-exxxxxx.adobe.com",
...
}
```

所有选定资源均由用作JSON对象的`handleSelection`函数承载。 例如，`JsonObj`。动态投放URL是通过组合以下运营商创建的：

| 对象 | JSON |
|---|---|
| 主机 | `assetJsonObj["repo:repositoryId"]` |
| API根 | `/adobe/assets` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| 格式 | `.jpg` |

**批准的资源交付API规范**

URL格式：
`https://<delivery-api-host>/adobe/assets/<asset-id>/as/<seo-name>.<format>?<image-modification-query-parameters>`

其中，

* 主机为`https://delivery-pxxxxx-exxxxxx.adobe.com`
* API根是`"/adobe/assets"`
* `<asset-id>`是资产标识符
* `as`是开放API规范中的常量部分，用于指示将资源称为
* `<seo-name>`是资源的名称
* `<format>`为输出格式
* `<image modification query parameters>`作为已批准资产的投放API规范的支持

**已批准资源原始演绎版投放API**

动态投放URL具有以下语法：
`https://<delivery-api-host>/adobe/assets/<asset-id>/original/as/<seo-name>`，其中，

* 主机为`https://delivery-pxxxxx-exxxxxx.adobe.com`
* 原始节目投放的API根为`"/adobe/assets"`
* `<asset-id>`是资产标识符
* `/original/as`是开放API规范的常量部分，指明了原始演绎版的含义
* `<seo-name>`是包含扩展名或不包含扩展名的资源的名称

+++

+++**已准备好挑选动态投放URL**
所有选定资源都由用作JSON对象的`handleSelection`函数承载。 例如，`JsonObj`。动态投放URL是通过组合以下运营商创建的：

| 对象 | JSON |
|---|---|
| 主机 | `assetJsonObj["repo:repositoryId"]` |
| API根 | `/adobe/assets/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"]` |

以下是遍历JSON对象的两种方式：

![动态投放URL](assets/dynamic-delivery-url.png)

* **缩略图：**&#x200B;缩略图可以是图像，资产可以是PDF、视频、图像等。 但是，您可以将资产缩略图的高度和宽度属性用作动态投放演绎版。
以下演绎版集可用于PDF类型资源：
在sidekick中选择PDF后，选择上下文会提供以下信息。 以下是遍历JSON对象的方式：

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  您可以在上面的屏幕快照中引用`selection[0].....selection[4]`以获取演绎版链接数组。 例如，其中一个缩略图呈现版本的关键属性包括：

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

在上面的屏幕截图中，如果需要PDF，则需要将PDF原始演绎版的投放URL合并到Target Experience中，而不是合并其缩略图。 例如，`https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf`

* **视频：**&#x200B;您可以为使用嵌入式iFrame的视频类型资源使用视频播放器URL。 您可以在Target体验中使用以下数组演绎版：
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/asDragDrop.2.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

  您可以在上面的屏幕快照中引用`selection[0].....selection[4]`以获取演绎版链接数组。 例如，其中一个缩略图呈现版本的关键属性包括：

  上述屏幕快照中的代码片段是视频资源的一个示例。 它包括呈现版本链接数组。 摘录中的`selection[5]`是图像缩略图的示例，可用作目标体验中视频缩略图的占位符。 演绎版数组中的`selection[5]`适用于视频播放器。 它提供一个HTML，可以设置为iframe的`src`。 它支持自适应比特率流，该流是Web优化的视频交付。

  在上例中，视频播放器URL为`https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play`

+++具有OpenAPI功能的Dynamic Media的&#x200B;**资产选择器用户界面**

与Adobe的微前端资产选择器集成后，您可以在Experience Manager资产存储库中查看所有已批准资产的纯资产结构。

![具有OpenAPI功能UI的Dynamic Media](assets/polaris-ui.png)

* **A**：[隐藏/显示面板](#hide-show-panel)
* **B**： [Assets](#repository)
* **C**： [排序](#sorting)
* **D**：[过滤器](#filters)
* **E**：[搜索栏](#search-bar)
* **F**： [按升序或降序排序](#sorting)
* **G**：取消选择
* **H**：选择单个或多个资源

+++

+++**配置自定义筛选条件**
通过OpenAPI功能的Dynamic Media资产选择器，可配置自定义属性以及基于这些属性的过滤器。 `filterSchema`属性用于配置此类属性。 自定义项可以作为`metadata.<metadata bucket>.<property name>.`公开，可以根据它配置筛选器，其中，

* `metadata`是资产的信息
* `embedded`是用于配置的静态参数，并且
* `<propertyname>`是您配置的筛选器名称

对于配置，对于要配置的筛选器，在`jcr:content/metadata/`级别定义的属性将公开为`metadata.<metadata bucket>.<property name>.`。

例如，在具有OpenAPI功能的Dynamic Media的资源选择器中，`asset jcr:content/metadata/client_name:market`上的属性被转换为`metadata.embedded.client_name:market`以进行筛选器配置。

要获取名称，必须完成一次性活动。 对资产进行搜索API调用，然后获取属性名称（本质上是存储桶）。

+++

>[!ENDTABS]

## 资产选择器属性 {#asset-selector-properties}

您可以使用资源选择器属性来自定义资源选择器的呈现方式。下表列出了可用于自定义和使用资源选择器的属性。

| 属性 | 类型 | 必需 | 默认 | 描述 |
|---|---|---|---|---|
| *边栏* | 布尔值 | 否 | 假 | 如果标记为`true`，则资产选择器将在左边栏视图中呈现。 如果资产选择器标记为`false`，则会在模式视图中呈现该资产选择器。 |
| *imsOrg* | 字符串 | 是 | | 为组织设置 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 时分配的 Adobe Identity Management System (IMS) ID。需要使用`imsOrg`密钥来验证您访问的组织是否位于Adobe IMS下。 |
| *imsToken* | 字符串 | 否 | | 用于身份验证的 IMS 持有者令牌。如果您使用`imsToken`应用程序进行集成，则需要[!DNL Adobe]。 |
| *apiKey* | 字符串 | 否 | | 用于访问 AEM 发现服务的 API 密钥。如果您使用`apiKey`应用程序集成，则需要[!DNL Adobe]。 |
| *filterSchema* | 数组 | 否 | | 用于配置过滤器属性的模型。这在需要限制资源选择器中的某些过滤器选项时很有用。 |
| *filterFormProps* | 对象 | 否 | | 指定您需要用于细化搜索的过滤器属性。为了！ 例如，MIME类型JPG、PNG、GIF。 |
| *selectedAssets* | 数组 `<Object>` | 否 |                 | 呈现资源选择器时指定选定资源。包含资源的 id 属性的必需对象数组。例如，`[{id: 'urn:234}, {id: 'urn:555'}]` 资源必须在当前目录中可用。如果您需要使用其他目录，请也为 `path` 属性提供一个值。 |
| *acvConfig* | 对象 | 否 | | 资产收藏集视图属性，该属性包含用于覆盖默认值的自定义配置的对象。 此外，此属性与`rail`属性一起使用，以启用资产查看器的边栏视图。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |                 | 如果OOTB翻译无法满足应用程序的需求，则可以公开一个界面，通过该界面可通过`i18nSymbols` prop传递您自己的自定义本地化值。 通过此界面传递值将覆盖提供的默认转换，并转而使用您自己的转换。 要执行覆盖，您必须将一个有效的[消息描述符](https://formatjs.io/docs/react-intl/api/#message-descriptor)对象传递到要覆盖的 `i18nSymbols` 键。 |
| *intl* | 对象 | 否 | | 资产选择器提供默认的OOTB翻译。 您可以通过用 `intl.locale` 属性提供有效的区域设置字符串来选择翻译语言。例如：`intl={{ locale: "es-es" }}` </br></br> 支持的区域设置字符串遵循语言标准名称表示的 [ISO 639 - 代码](https://www.iso.org/iso-639-language-codes.html)。</br></br> 支持的区域设置列表：英语 -“en-us”（默认）西班牙语 -“es-es”德语 -“de-de”法语 -“fr-fr”意大利语 -“it-it”日语 -“ja-jp”朝鲜语 -“ko-kr”葡萄牙语 -“pt-br”中文（繁体）-“zh-cn”中文（台湾地区）-“zh-tw” |
| *repositoryId* | 字符串 | 否 | &#39;&#39; | 资源选择器从中加载内容的存储库。 |
| *additionalAemSolutions* | `Array<string>` | 否 | [ ] | 它允许您添加其他AEM存储库的列表。 如果此属性中未提供任何信息，则仅考虑媒体库或 AEM Assets 存储库。 |
| *hideTreeNav* | 布尔值 | 否 |  | 指定是显示还是隐藏资源树导航侧边栏。它仅在模态视图中使用，因此，该属性在边栏视图中不起作用。 |
| *onDrop* | 函数 | 否 | | 该属性允许资源的删除功能。 |
| *dropOptions* | `{allowList?: Object}` | 否 | | 使用“allowList”配置删除选项。 |
| *colorScheme* | 字符串 | 否 | | 为资源选择器配置主题（`light` 或 `dark`）。 |
| *handleSelection* | 函数 | 否 | | 在资源已选定并单击模态上的 `Select` 按钮时调用资源项数组。仅在模态视图中调用此函数。对于边栏视图，请使用 `handleAssetSelection` 或 `onDrop` 函数。示例： <pre>handleSelection=（资源：资源[]）=> {...}</pre> 有关详细信息，请参阅[所选资源类型](#selected-asset-type)。 |
| *handleAssetSelection* | 函数 | 否 | | 在选择或取消选择资源时调用项目数组。如果您需要在用户选择资源时进行侦听，这会很有用。示例： <pre>handleSelection=（资源：资源[]）=> {...}</pre> 有关详细信息，请参阅[所选资源类型](#selected-asset-type)。 |
| *onClose* | 函数 | 否 | | 在按下模态视图中的 `Close` 按钮时调用。这仅在 `modal` 视图中被调用，在 `rail` 视图中将被忽略。 |
| *onFilterSubmit* | 函数 | 否 | | 当用户更改其他过滤器条件时调用过滤器项。 |
| *selectionType* | 字符串 | 否 | 单身 | 一次性为 `single` 或 `multiple` 资源选择配置。 |
| *dragOptions.允许列表* | 布尔型 | 否 | | 属性用于允许或拒绝拖动不可选资产。 |
| *aemTierType* | 字符串 | 否 |  | 它允许您选择是显示交付层、创作层中的资产，还是同时显示两者。 <br><br>语法： `aemTierType:[0]: "author" 1: "delivery"` <br><br>例如，如果同时使用了`["author","delivery"]`，则存储库切换器将显示创作和投放选项。 |
| *handleNavigateToAsset* | 函数 | 否 | | 它是一个回调函数，用于处理资源的选择。 |
| *noWrap* | 布尔值 | 否 | | *noWrap*&#x200B;属性有助于在侧边栏面板中呈现资产选择器。 如果未提及此属性，则默认情况下会呈现&#x200B;*对话框视图*。 |
| *dialogSize* | 小型、中型、大型、全屏或全屏接管 | 字符串 | 可选 | 通过使用给定选项指定布局大小可控制布局。 |
| *colorScheme* | 浅色或深色 | 否 | | 此属性用于设置Asset Selector应用程序的主题。 您可以选择浅色或深色主题。 |
| *filterRepoList* | 函数 | 否 |  | 您可以使用调用Experience Manager存储库并返回存储库筛选列表的`filterRepoList`回调函数。 |
| *expiryOptions* | 函数 | | | 您可以在以下两个属性之间使用：**getExpiryStatus**，它提供已过期资源的状态。 函数根据您提供的资源的到期日期返回`EXPIRED`、`EXPIRING_SOON`或`NOT_EXPIRED`。 请参阅[自定义过期的资源](#customize-expired-assets)。 此外，您可以使用&#x200B;**allowSelectionAndDrag**，其中函数的值可以是`true`或`false`。 如果该值设置为`false`，则无法在画布上选择或拖动过期的资产。 |
| *showToast* | | 否 | | 它允许资产选择器为已过期的资产显示自定义的toast消息。 |

<!--
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](#customize-expired-assets). |
-->

## 有关使用资源选择器属性的示例 {#usage-examples}

您可以在 `index.html` 文件中定义资源选择器[属性](#asset-selector-properties)，以自定义应用程序中的资源选择器显示。

### 示例 1：边栏视图中的资源选择器

![rail-view-example](assets/rail-view-example-vanilla.png)

如果AssetSelector `rail`的值设置为`false`或未在属性中提及，则默认情况下，Asset Selector会显示在模式视图中。 `acvConfig`属性允许进行一些深入配置，如拖放。 访问[启用或禁用拖放](#enable-disable-drag-and-drop)以了解`acvConfig`属性的用法。

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### 示例 2：元数据弹出窗口

使用各种属性来定义要使用信息图标查看的资源的元数据。信息弹出窗口提供有关资源或文件夹的信息集合，包括资源的标题、尺寸、修改日期、位置和描述。在下面的示例中，各种属性用于显示资源的元数据，例如，`repo:path` 属性指定资源的位置。<!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)

### 示例 3：边栏视图中的自定义过滤器属性

除了面向搜索之外，Assets Selector还允许您自定义各种属性，以细化从[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]应用程序进行的搜索。 添加以下代码以在应用程序中添加自定义搜索过滤器。 在下面的示例中，`Type Filter` 搜索过滤图像、文档或视频中的资源类型或已为搜索添加的过滤器类型。

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

## 功能设置代码段{#code-snippets}

在`index.html`文件或应用程序实施中的类似文件中定义先决条件，以定义访问[!DNL Experience Manager Assets]存储库的身份验证详细信息。 完成后，您可以根据需要添加代码片段。

### 自定义筛选器面板 {#customize-filter-panel}

您可以在`assetSelectorProps`对象中添加以下代码片段以自定义筛选器面板：

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    }},
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

### 自定义模式视图中的信息 {#customize-info-in-modal-view}

单击![信息图标](assets/info-icon.svg)图标时，您可以自定义资源的详细信息视图。 执行以下代码：

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path'
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

### 启用或禁用拖放模式 {#enable-disable-drag-and-drop}

将以下属性添加到`assetSelectorProp`以启用拖放模式。 要禁用拖放，请使用`true`替换`false`参数。

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

### Assets选择 {#selection-of-assets}

选定资源类型是一个对象数组，其中包含使用 `handleSelection`、`handleAssetSelection` 和 `onDrop` 函数时的资源信息。

执行以下步骤以配置单个或多个资源的选择：

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

**架构语法**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'https://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

下表描述了选定资源对象的一些重要属性。

| 属性 | 类型 | 描述 |
|---|---|---|
| *存储库:repositoryId* | 字符串 | 存储资源的存储库的唯一标识符。 |
| *存储库:id* | 字符串 | 资源的唯一标识符。 |
| *存储库:assetClass* | 字符串 | 资源的分类（例如，图像、视频或文档）。 |
| *存储库:name* | 字符串 | 资源的名称，包括文件扩展名。 |
| *存储库:size* | 数字 | 资源的大小，以字节为单位。 |
| *存储库:path* | 字符串 | 资源在存储库中的位置。 |
| *存储库:ancestors* | `Array<string>` | 存储库中资源的祖先项数组。 |
| *存储库:state* | 字符串 | 存储库中资产的当前状态（例如，活动、删除等）。 |
| *存储库:createdBy* | 字符串 | 创建资源的用户或系统。 |
| *存储库:createDate* | 字符串 | 资源的创建日期和时间。 |
| *存储库:modifiedBy* | 字符串 | 上次修改资源的用户或系统。 |
| *存储库:modifyDate* | 字符串 | 资源的上次修改日期和时间。 |
| *dc:format* | 字符串 | 资源的格式，如文件类型(例如，JPEG、PNG等)。 |
| *tiff:imageWidth* | 数字 | 资源的宽度。 |
| *tiff:imageLength* | 数字 | 资源的高度。 |
| *computedMetadata* | `Record<string, any>` | 一个对象，表示所有类型的所有资源元数据（存储库、应用程序或嵌入式元数据）的存储桶。 |
| *_links* | `Record<string, any>` | 关联资源的超媒体链接。包括元数据和演绎版等资源的链接。 |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition>* | `Array<Object>` | 对象数组，包含有关资源演绎版的信息。 |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition[].href>* | 字符串 | 演绎版的 URI。 |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition[].type>* | 字符串 | 演绎版的 MIME 类型。 |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition[].repo:size>&#39;* | 数字 | 演绎版的大小，以字节为单位。 |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition[].width>* | 数字 | 演绎版的宽度。 |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition[].height>* | 数字 | 演绎版的高度。 |

<!--For a complete list of properties and detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

### 自定义过期的资源 {#customize-expired-assets}

通过资源选择器，您可以控制已过期资源的使用情况。 您可以使用即将过期的&#x200B;**徽章**&#x200B;自定义已过期的资产，该徽章可帮助您提前了解将在当前日期起30天内过期的资产。 此外，还可根据需要自定义标记。 您还可以允许在画布上选择已过期的资源，反之亦然。 可以通过多种方式使用某些代码片段来自定义已过期的资源：

<!--{
    getExpiryStatus: function, // to control Expired/Expiring soon badges of the asset
    allowSelectionAndDrag: boolean, // set true to allow the selection of expired assets on canvas, set false, otherwise.
}-->

```
expiryOptions: {
    getExpiryStatus: getExpiryStatus;
}
```

#### 选择已过期的资产 {#selection-of-expired-asset}

您可以自定义已过期资源的使用情况，使其成为可选或不可选。 您可以自定义是否允许在资产选择器画布上拖放过期的资产。 要实现此目的，请使用以下参数使资产在画布上不可选择：

```
expiryOptions:{
    allowSelectionAndDrop: false;
}
```

<!--
Additionally, To do this, navigate to **[!UICONTROL Disable default expiry behavior]** under the [!UICONTROL Controls] tab and set the boolean value to `true` or `false` as per the requirement. If `true` is selected, you can see the select box over the expired asset, otherwise it remains unselected. You can hover to the info icon of an asset to know the details of an expired asset. 

![Disable default expiry behavior](assets/disable-default-expiry-behavior.png)-->

#### 设置已过期资源的持续时间 {#set-duration-of-expired-asset}

以下代码片段可帮助您为将在未来五天内过期的资产设置&#x200B;**即将过期**&#x200B;徽章：<!--The `expirationDate` property is used to set the expiration duration of an asset. Refer to the code snippet below:-->

```
/**
  const getExpiryStatus = async (asset) => {
  if (!asset.expirationDate) {
    return null;
  }
  const currentDate = new Date();
  const millisecondsInDay = 1000 * 60 * 60 * 24;
  const fiveDaysFromNow = new Date(value: currentDate.getTime() + 5 * millisecondsInDay);
  const expirationDate = new Date(asset.expirationDate);
  if (expirationDate.getTime() < currentDate.getTime()) {
    return 'EXPIRED';
  } else if (expirationDate.getTime() < fiveDaysFromNow.getTime()) {
    return 'EXPIRING_SOON';
  } else {
    return 'NOT_EXPIRED';
  }
};
```

<!--In the above code snippet, the `getExpiryStatus` function is used to show the **Expiring soon** badge that have expiration date stored in `customExpirationDate`. Additionally, it sets the expiration date of an asset to five days from the current date. The `millisecondsInDay` helps you set expiry of an asset by specifying the time range in milliseconds. You can replace milliseconds with hours directly or customize function as per the requirement. Whereas, the `getTime()` function returns the number of milliseconds for the mentioned date. See [properties](#asset-selector-properties) to know about `expirationDate` property.-->

请参阅以下示例，了解属性如何用于获取当前日期和时间：

```
const currentData = new Date();
currentData.getTime(),
```

返回`1718779013959`，其格式为日期格式2024-06-19T06:36:53.959Z。

#### 自定义已过期资产的快显消息 {#customize-toast-message}

`showToast`属性用于自定义要在已过期资源上显示的Toast消息。

语法：

```
{
    type: 'ERROR', 'NEUTRAL', 'INFO', 'SUCCESS',
    message: '<message to be shown>',
    timeout: optional,
}
```

默认超时为500毫秒。 但是，您可以根据需要对其进行修改。 此外，传递值`timeout: 0`会保持toast处于打开状态，直至您单击交叉按钮。

下面是一个示例，在需要禁止选择文件夹并显示相应消息时显示一则快显通知消息：

```
const showToast = {
    type: 'ERROR',
    message: 'Folder cannot be selected',
    timeout: 5000,
}
```

使用以下代码片段显示有关使用已过期资产的toast消息：

![快显通知](assets/toast-message.png)

### 上下文调用过滤器{#contextual-invocation-filter}

资产选择器允许您添加标记选取器过滤器。 它支持将所有相关标记组合到特定标记组的标记组。 此外，您还可以通过它选择与要查找的资源对应的其他标记。 此外，您还可以在上下文调用过滤器下设置您最常用的默认标记组，以便您能够随时访问它们。

>
>
> * 您需要添加上下文调用代码片段以在搜索中启用标记过滤器。
> * 必须使用与标记组类型`(property=xcm:keywords.id=)`对应的名称属性。

语法：

```
const filterSchema=useMemo(() => {
    return: [
        {
            element: 'taggroup',
            name: 'property=xcm:keywords.id='
        },
    ];
}, []);
```

要在过滤器面板中添加标记组，必须添加至少一个标记组作为默认值。 此外，使用以下代码片段添加从标记组中预先选定的默认标记。

```
export const WithAssetTags = (props) = {
const [selectedTags, setSelectedTags] = useState (
new Set(['orientation', 'color', 'facebook', 'experience-fragments:', 'dam', 'monochrome'])
const handleSelectTags = (selected) => {
setSelectedTags (new Set (selected)) ;
};
const filterSchema = useMemo ((); => {
    return {
        schema: [
            ｛
                fields: [
                    {
                    element: 'checkbox', 
                    name: 'property=xcm:keywords=', 
                    defaultValue: Array. from(selectedTags), 
                    options: assetTags, 
                    orientation: 'vertical',
                    },
                ],
    header: 'Asset Tags', 
    groupkey: 'AssetTagsGroup',
        ],
    },
｝；
}, [selectedTags]);
```

![标记组筛选器](assets/tag-group.gif)

## 使用对象架构处理资源选择 {#handling-selection}

`handleSelection` 属性用于处理资源选择器中的单个或多个资源选择。以下示例说明了 `handleSelection` 的使用语法。

![handle-selection](assets/handling-selection.png)

## 禁用选择Assets {#disable-selection}

禁用选择用于隐藏或禁用资源或文件夹不可选择。 它会隐藏信息卡或资源中的选择复选框，以防被选择。 要使用此功能，您可以声明要在数组中禁用的资源或文件夹的位置。 例如，如果要禁止选择显示在第一个位置的文件夹，可以添加以下代码：
`disableSelection: [0]:folder`

可以为数组提供要禁用的mime类型（如图像、文件夹、文件或其他mime类型，如image/jpeg）的列表。 您声明的mime类型已映射到资产的`data-card-type`和`data-card-mimetype`属性。

此外，带有禁用选择的Assets是可拖动的。 要禁用特定资源类型的拖放，您可以使用`dragOptions.allowList`属性。

禁用选择的语法如下：

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> 对于资产，选择复选框处于隐藏状态；而对于文件夹，文件夹处于不可选状态，但仍会显示提及文件夹的导航。

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

要在左侧导航中隐藏文件夹，请单击&#x200B;**[!UICONTROL 隐藏文件夹]**&#x200B;图标。要撤消更改，请再次单击&#x200B;**[!UICONTROL 隐藏文件夹]**&#x200B;图标。

### 存储库切换器 {#repository-switcher}

资产选择器还允许您切换存储库以进行资产选择。您可以从左侧面板中可用的下拉列表中选择所选存储库。下拉列表中可用的存储库选项基于 `repositoryId` 文件中定义的 `index.html` 属性。它基于登录用户访问的选定 IMS 组织的环境。消费者可以传递首选 `repositoryID`，在这种情况下，资产选择器将停止呈现存储库切换器，并且仅呈现给定存储库中的资产。

### 资产存储库

它是可用于执行操作的资产文件夹的集合。

### 开箱即用的过滤器 {#filters}

资产选择器还提供开箱即用的过滤器选项来细化您的搜索结果。可用过滤器如下：

* **[!UICONTROL 状态]：** 包括 `all`、`approved`、`rejected` 或 `no status` 中的当前资产状态。
* **[!UICONTROL 文件类型]：** 包括 `folder`、 `file`、 `images`、 `documents` 或 `video`。
* **[!UICONTROL 过期状态]：** 根据到期时间提及资产。您可以选中 `[!UICONTROL Expired]` 复选框来过滤过期的资产；或设置资产的 `[!UICONTROL Expiration Duration]`，以根据资产的到期持续时间显示资产。当资产已过期或即将过期时，将显示一个描述该资产的徽章。 此外，您可以控制是否允许使用（或拖放）过期资产。详细了解[自定义过期资产](#customize-expired-assets)。默认情况下，对于未来30天即将过期的资产，会显示&#x200B;**即将过期**&#x200B;徽章。 但是，您可以使用 `expirationDate` 属性配置有效期限。

  >[!TIP]
  >
  > 如果您想根据资产的未来到期日查看或筛选资产，请在 `[!UICONTROL Expiration Duration]` 字段中注明未来的日期范围。它显示了带有&#x200B;**即将到期**&#x200B;徽章的资产。

* **[!UICONTROL MIME 类型]：** 包括 `JPG`、`GIF`、`PPTX`、`PNG`、`MP4`、`DOCX`、`TIFF`、`PDF`、`XLSX`。
* **[!UICONTROL 图像大小]：** 包括图像的最小/最大宽度、最小/最大高度。

  ![rail-view-example](assets/filters-asset-selector.png)

### 自定义搜索

除了全文搜索外，资产选择器还允许您使用自定义搜索在文件中搜索资产。您可以在“模态”视图和“边栏”视图模式下使用自定义搜索过滤器。

![custom-search](assets/custom-search1.png)

您也可以创建默认搜索过滤器以保存经常搜索的字段并在以后使用。要为资源创建自定义搜索，可以使用 `filterSchema` 属性。

### 搜索栏 {#search-bar}

通过资源选择器，您可以对所选存储库中的资源执行全文搜索。 例如，如果您在搜索栏中键入关键字 `wave`，则将显示任意元数据属性中提及的所有带 `wave` 关键字的资产。

### 排序 {#sorting}

您可以在资产选择器中按资产的名称、尺寸或大小对资产进行排序。您还可以按升序或降序对资产进行排序。

### 视图类型 {#types-of-view}

资产选择器允许您在四种不同的视图中查看资产：

* **![列表视图](assets/do-not-localize/list-view.png) [!UICONTROL 列表视图]**&#x200B;列表视图在单个列中显示可滚动的文件和文件夹。
* **![网格视图](assets/do-not-localize/grid-view.png) [!UICONTROL 网格视图]** 网格视图以行和列的网格显示可滚动的文件和文件夹。
* **![库视图](assets/do-not-localize/gallery-view.png) [!UICONTROL 库视图]** 库视图以居中锁定的水平列表显示文件或文件夹。
* **![瀑布视图](assets/do-not-localize/waterfall-view.png) [!UICONTROL 瀑布视图]** 瀑布图以桥的形式显示文件或文件夹。

<!--
### Modes to view Asset Selector

Asset Selector supports two types of out of the box views:

**  Modal view or Inline view:** The modal view or inline view is the default view of Asset Selector that represents Assets folders in the front area. The modal view allows users to view assets in a full screen to ease the selection of multiple assets for import. Use `<AssetSelector rail={false}>` to enable modal view.

    ![modal-view](assets/modal-view.png)

**  Rail view:** The rail view represents Assets folders in a left panel. The drag and drop of assets can be performed in this view. Use `<AssetSelector rail={true}>` to enable rail view.

    ![rail-view](assets/rail-view.png)
-->
<!--

### Application Integration

Asset Selector is flexible and can be integrated within your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application. It is accessible and localized to add, search, and select assets in your application. With Asset Selector you can:
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It lets you control the display of various text or symbols as per your choice.
*   **Perfect fit** Asset selector easily fits in your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application and choose the way you want to view. The mode of view can be inline, rail, or modal view.
*   **Accessible** With Asset Selector, you can reach the desired asset in an easy manner.
*   **Localize** Assets can be availed for the various locales available as per Adobe's localization standards.
-->
<!--

### Support for multiple instances

The micro front-end design supports the display of multiple instances of Asset Selector on a single screen.

![multiple-instance](assets/multiple-instance.png)
-->

<!--

### Controlled selection with multi-select

You can make default multi-selection of assets by specifying the assets to the component using `selectedAssets` property. You should specify an array of asset IDs. For example, `[{id: 'urn:234}, {id: 'urn:555'}].`
-->
<!--

### Action buttons

When you customize your application with Asset Selector based on ReactJS, you are provided with the following action buttons to perform various actions:
*   **Open in media library** Lets you open the asset in media library.
*   **Upload** Lets you upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector lets you know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->



<!--Best Practice-->
<!--
+++**Control default selection of the filter**
You can make the selection of filter default by implementing the following code snippet:

```
"defaultValue": [
    "image/*",
    "application/*"
],

{
    "label": "Documents",
    "value": "application/*"
}
```

+++
-->
