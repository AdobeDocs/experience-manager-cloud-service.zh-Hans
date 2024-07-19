---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 使用资源选择器在您的应用程序中搜索、查找和检索资源的元数据和演绎版。
contentOwner: KK
role: Admin,User
feature: Selectors
exl-id: b968f63d-99df-4ec6-a9c9-ddb77610e258
source-git-commit: d12aba19a8f166afcaa071478c1cb6d995010cd8
workflow-type: tm+mt
source-wordcount: '4725'
ht-degree: 36%

---


# 微前端资源选择器 {#Overview}

微前端资源选择器提供了一个用户界面，它可以轻松地与 [!DNL Experience Manager Assets] 存储库集成，以便您能够浏览或搜索存储库中可用的数字资源，并在您的应用程序创作体验中使用它们。

微前端用户界面可用于采用了资源选择器包的应用程序体验。对该包的任何更新都会自动导入，并且最新部署的资源选择器会自动加载到您的应用程序中。

![概述](assets/overview.png)

资源选择器提供了许多好处，例如：

* 使用Vanilla JavaScript库轻松与任何[Adobe](#asset-selector-ims)或[非Adobe](#asset-selector-non-ims)应用程序集成。
* 易于维护，因为对资源选择器包的更新将自动部署到可用于应用程序的资源选择器。您的应用程序中无需更新即可加载最新的修改。
* 易于定制，因为提供了用于控制应用程序中的资源选择器显示的属性。
* 全文搜索、开箱即用和自定义过滤器，可快速导航到资源以便在创作体验中使用。
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

必须确保以下通信方法：

* 应用程序正在HTTPS上运行。
* IMS客户端重定向URL允许列表中应用程序的URL。
* IMS登录流通过Web浏览器上的弹出窗口进行配置和渲染。 因此，应在目标浏览器上启用或允许弹出窗口。

如果您需要资产选择器的IMS身份验证工作流，请使用上述先决条件。 或者，如果您已通过IMS工作流身份验证，则可以改为添加IMS信息。

>[!IMPORTANT]
>
> 此存储库旨在作为补充文档，描述用于集成Asset Selector的可用API和使用示例。 在尝试安装或使用资产选择器之前，请确保贵组织已获得资产选择器的访问权限，且已作为Experience Manager Assetsas a Cloud Service配置文件的一部分进行配置。 如果您尚未配置，则无法集成或使用这些组件。 要请求配置，您的项目管理员应从Admin Console中提出标记为P2的支持票证并包含以下信息：
>
>* 托管集成应用程序的域名。
>* 配置之后，将为您的组织提供`imsClientId`、`imsScope`以及对应于您请求的环境的`redirectUrl`，这对于配置资产选择器至关重要。 如果没有这些有效属性，您将无法运行安装步骤。

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
* [将资源选择器与非Adobe应用程序集成](#adobe-non-app-integration)
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
| `imsClientId` | 表示用于身份验证的IMS客户端ID的字符串值。 此值由Adobe提供，特定于您的AdobeAEM CS组织。 |
| `imsScope` | 描述身份验证中使用的范围。 范围决定了应用程序对组织资源的访问级别。 多个范围可以用逗号分隔。 |
| `redirectUrl` | 表示验证后用户被重定向到的URL。 此值通常设置为应用程序的当前URL。 如果未提供`redirectUrl`，`ImsAuthService`将使用用于注册`imsClientId`的redirectUrl |
| `modalMode` | 布尔值，指示是否应在模态（弹出窗口）中显示身份验证流程。 如果设置为`true`，则身份验证流程将在弹出窗口中显示。 如果设置为`false`，则身份验证流程将以整页重新加载方式显示。 _注意：_&#x200B;为获得更好的UX，如果用户禁用了浏览器弹出窗口，则可以动态控制此值。 |
| `onImsServiceInitialized` | Adobe IMS身份验证服务初始化时调用的回调函数。 此函数接受一个参数`service`，该参数是表示Adobe IMS服务的对象。 有关更多详细信息，请参阅[`ImsAuthService`](#imsauthservice-ims-auth-service)。 |
| `onAccessTokenReceived` | 在从Adobe IMS身份验证服务收到`imsToken`时调用的回调函数。 此函数接受一个参数`imsToken`，该参数是一个表示访问令牌的字符串。 |
| `onAccessTokenExpired` | 访问令牌过期时调用的回调函数。 此函数通常用于触发新的身份验证流程以获取新的访问令牌。 |
| `onErrorReceived` | 身份验证期间发生错误时调用的回调函数。 此函数采用两个参数：错误类型和错误消息。 错误类型是表示错误类型的字符串，错误消息是表示错误消息的字符串。 |

+++

+++**ImsAuthService**
`ImsAuthService`类用于处理资产选择器的身份验证流程。 它负责从Adobe IMS身份验证服务获取`imsToken`。 `imsToken`用于对用户进行身份验证并授权作为[!DNL Cloud Service] Assets存储库访问[!DNL Adobe Experience Manager]。 ImsAuthService使用`ImsAuthProps`属性来控制身份验证流并注册各种身份验证事件的侦听器。 您可以使用方便的[`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice)函数向资产选择器注册&#x200B;_ImsAuthService_&#x200B;实例。 `ImsAuthService`类中有以下函数可用。 但是，如果您使用&#x200B;_registerAssetsSelectorsAuthService_&#x200B;函数，则无需直接调用这些函数。

| 函数名称 | 描述 |
|---|---|
| `isSignedInUser` | 确定用户当前是否已登录到服务并相应地返回布尔值。 |
| `getImsToken` | 检索当前登录用户的身份验证`imsToken`，该身份验证可用于验证其他服务（如生成资产_rendition）的请求。 |
| `signIn` | 启动用户的登录流程。 此函数使用`ImsAuthProps`在弹出窗口或全页重新加载中显示身份验证 |
| `signOut` | 将用户签出服务，使其身份验证令牌失效，并要求他们再次登录以访问受保护的资源。 调用此函数将重新加载当前页面。 |
| `refreshToken` | 刷新当前登录用户的身份验证令牌，防止该令牌过期，并确保对受保护资源的访问不会中断。 返回可用于后续请求的新身份验证令牌。 |

+++

+++**IMS令牌验证**

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

如果要将Asset Selector与非Adobe应用程序集成，请使用以下先决条件：

* [通信方法](#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

当您将[!DNL Experience Manager Assets]存储库与非Adobe应用程序集成时，Asset Selector支持使用Identity Management System (IMS)属性（如`imsScope`或`imsClientID`）对其进行身份验证。

### 将资源选择器与非Adobe应用程序集成 {#adobe-non-app-integration}

要将资产选择器与非Adobe应用程序集成，您需要执行各种验证，如记录支持工单、集成等。

+++**为非Adobe应用程序配置资源选择器**
要为非Adobe应用程序配置资产选择器，必须首先记录用于预配的支持票证，然后执行集成步骤。

**正在记录支持票证**
通过Admin Console记录支持票证的步骤：

1. 在票证标题中添加带有AEM Assets **的**&#x200B;资源选择器。

1. 请在描述中提供以下详细信息：

   * [!DNL Experience Manager Assets]作为[!DNL Cloud Service] URL（项目ID和环境ID）。
   * 托管非AdobeWeb应用程序的域名。
+++

+++**集成步骤**
在将Asset Selector与非Adobe应用程序集成时，使用此示例`index.html`文件进行身份验证。

使用`Script`标记访问资产选择器包，如示例`index.html`文件的&#x200B;*第9*&#x200B;行到&#x200B;*第11*&#x200B;行所示。

示例的&#x200B;*行14*&#x200B;到&#x200B;*行38*&#x200B;描述了IMS流属性，如`imsClientId`、`imsScope`和`redirectURL`。 函数要求您至少定义`imsClientId`和`imsScope`属性之一。 如果您没有为`redirectURL`定义值，则使用客户端ID的注册重定向URL。

由于您没有生成`imsToken`，请使用`registerAssetsSelectorsAuthService`和`renderAssetSelectorWithAuthFlow`函数，如示例`index.html`文件的第40行至第50行所示。 使用`renderAssetSelectorWithAuthFlow`之前的`registerAssetsSelectorsAuthService`函数通过资产选择器注册`imsToken`。 [!DNL Adobe]建议在实例化组件时调用`registerAssetsSelectorsAuthService`。

在`const props`部分中定义身份验证和其他Assetsas a Cloud Service访问相关的属性，如示例`index.html`文件的&#x200B;*行54*&#x200B;到&#x200B;*行60*&#x200B;所示。

*行65*&#x200B;中提到的`PureJSSelectors`全局变量用于呈现Web浏览器中的资产选择器。

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
* 要访问具有OpenAPI功能的Dynamic Media，您必须具有以下功能的许可证：
   * Assets存储库(例如，Experience Manager Assetsas a Cloud Service)。
   * AEM Dynamic Media。
* 只有[个批准的资产](#approved-assets.md)可用于确保品牌一致性。

### Dynamic Media与OpenAPI功能集成{#adobe-app-integration-polaris}

资产选择器与Dynamic Media OpenAPI进程的集成涉及各种步骤，包括创建自定义的Dynamic Media URL或准备选择Dynamic Media URL等。

+++**将Dynamic Media的资源选择器与OpenAPI功能集成**

`rootPath`和`path`属性不应包含在具有OpenAPI功能的Dynamic Media中。 相反，您可以配置`aemTierType`属性。 以下是配置的语法：

```
aemTierType:[1: "delivery"]
```

利用此配置，可查看所有批准的资产，但不包含文件夹或采用平面结构。 有关详细信息，请导航到[资产选择器属性](#asset-selector-properties)下的`aemTierType`属性

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
| API根 | `/adobe/dynamicmedia/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| 格式 | `.jpg` |

**批准的资源交付API规范**

URL格式：
`https://<delivery-api-host>/adobe/dynamicmedia/deliver/<asset-id>/<seo-name>.<format>?<image-modification-query-parameters>`

其中，

* 主机为`https://delivery-pxxxxx-exxxxxx.adobe.com`
* API根是`"/adobe/dynamicmedia/deliver"`
* `<asset-id>`是资产标识符
* `<seo-name>`是资源的名称
* `<format>`为输出格式
* `<image modification query parameters>`作为已批准资产的投放API规范的支持

**已批准的资产交付API**

动态投放URL具有以下语法：
`https://<delivery-api-host>/adobe/assets/deliver/<asset-id>/<seo-name>`，其中，

* 主机为`https://delivery-pxxxxx-exxxxxx.adobe.com`
* 原始节目投放的API根为`"/adobe/assets/deliver"`
* `<asset-id>`是资产标识符
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

* **缩略图：**缩略图可以是图像，资产可以是PDF、视频、图像等。 但是，您可以将资产缩略图的高度和宽度属性用作动态投放演绎版。
以下演绎版集可用于PDF类型资源：
在sidekick中选择PDF后，选择上下文会提供以下信息。 以下是遍历JSON对象的方式：

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  您可以在上面的屏幕快照中引用`selection[0].....selection[4]`以获取演绎版链接数组。 例如，其中一个缩略图呈现版本的关键属性包括：

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?accept-experimental=1&width=319&height=319&preferwebp=true", 
      "type": "image/webp" 
  } 
  ```

在上面的屏幕快照中，如果需要PDF，则需要将PDF原始演绎版的投放URL合并到目标体验中，而不是合并其缩略图。 例如，`https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf?accept-experimental=1`

* **视频：**您可以为使用嵌入式iFrame的视频类型资源使用视频播放器URL。 您可以在Target体验中使用以下数组演绎版：
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/asDragDrop.2.jpg?accept-experimental=1&width=319&height=319&preferwebp=true", 
      "type": "image/webp" 
  } 
  ```

  您可以在上面的屏幕快照中引用`selection[0].....selection[4]`以获取演绎版链接数组。 例如，其中一个缩略图呈现版本的关键属性包括：

  上述屏幕快照中的代码片段是视频资源的一个示例。 它包括呈现版本链接数组。 摘录中的`selection[5]`是图像缩略图的示例，可用作目标体验中视频缩略图的占位符。 演绎版数组中的`selection[5]`适用于视频播放器。 这提供了一个HTML，可以设置为iframe的`src`。 它支持自适应比特率流，该流是Web优化的视频交付。

  在上例中，视频播放器URL为`https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play?accept-experimental=1`

+++具有OpenAPI功能的Dynamic Media的&#x200B;**资源选择器用户界面**

在与Adobe的微前端资源选择器集成后，您可以在Experience Manager资源存储库中查看所有已批准资源的仅资源结构。

具有OpenAPI功能UI的![Dynamic Media](assets/polaris-ui.png)

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
通过OpenAPI功能的Dynamic Media资源选择器，可配置自定义属性以及基于这些属性的过滤器。 `filterSchema`属性用于配置此类属性。 自定义项可以作为`metadata.<metadata bucket>.<property name>.`公开，可以根据它配置筛选器，其中，

* `metadata`是资产的信息
* `embedded`是用于配置的静态参数，并且
* `<propertyname>`是您配置的筛选器名称

对于配置，对于要配置的筛选器，在`jcr:content/metadata/`级别定义的属性将公开为`metadata.<metadata bucket>.<property name>.`。

例如，在用于具有OpenAPI功能的Dynamic Media的资源选择器中，`asset jcr:content/metadata/client_name:market`上的某个属性被转换为`metadata.embedded.client_name:market`以进行筛选器配置。

要获取名称，必须完成一次性活动。 对资产进行搜索API调用，然后获取属性名称（本质上是存储桶）。

+++

>[!ENDTABS]

## 资源选择器属性 {#asset-selector-properties}

您可以使用资源选择器属性来自定义资源选择器的呈现方式。下表列出了可用于自定义和使用资源选择器的属性。

| 属性 | 类型 | 必需 | 默认 | 描述 |
|---|---|---|---|---|
| *边栏* | 布尔型 | 否 | false | 如果标记为`true`，则资产选择器将在左边栏视图中呈现。 如果资产选择器标记为`false`，则会在模式视图中呈现该资产选择器。 |
| *imsOrg* | 字符串 | 是 | | 为组织设置 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 时分配的 Adobe Identity Management System (IMS) ID。需要使用`imsOrg`密钥来验证您访问的组织是否位于Adobe IMS下。 |
| *imsToken* | 字符串 | 否 | | 用于身份验证的 IMS 持有者令牌。如果您使用[!DNL Adobe]应用程序进行集成，则需要`imsToken`。 |
| *apiKey* | 字符串 | 否 | | 用于访问 AEM 发现服务的 API 密钥。如果您使用[!DNL Adobe]应用程序集成，则需要`apiKey`。 |
| *filterSchema* | 数组 | 否 | | 用于配置过滤器属性的模型。这在需要限制资源选择器中的某些过滤器选项时很有用。 |
| *filterFormProps* | 对象 | 否 | | 指定您需要用于细化搜索的过滤器属性。例如，MIME 类型 JPG、PNG、GIF。 |
| *selectedAssets* | 数组 `<Object>` | 否 |                 | 呈现资源选择器时指定选定资源。包含资源的 id 属性的必需对象数组。例如，`[{id: 'urn:234}, {id: 'urn:555'}]` 资源必须在当前目录中可用。如果您需要使用其他目录，请也为 `path` 属性提供一个值。 |
| *acvConfig* | 对象 | 否 | | 资产收藏集视图属性，该属性包含用于覆盖默认值的自定义配置的对象。 此外，此属性与`rail`属性一起使用，以启用资产查看器的边栏视图。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |                 | 如果OOTB翻译无法满足应用程序的需求，则可以公开一个界面，通过该界面可通过`i18nSymbols` prop传递您自己的自定义本地化值。 通过此界面传递值将覆盖提供的默认转换，并转而使用您自己的转换。 要执行覆盖，您必须将一个有效的[消息描述符](https://formatjs.io/docs/react-intl/api/#message-descriptor)对象传递到要覆盖的 `i18nSymbols` 键。 |
| *intl* | 对象 | 否 | | 资产选择器提供默认的OOTB翻译。 您可以通过用 `intl.locale` 属性提供有效的区域设置字符串来选择翻译语言。例如：`intl={{ locale: "es-es" }}` </br></br> 支持的区域设置字符串遵循语言标准名称表示的 [ISO 639 - 代码](https://www.iso.org/iso-639-language-codes.html)。</br></br> 支持的区域设置列表：英语 -“en-us”（默认）西班牙语 -“es-es”德语 -“de-de”法语 -“fr-fr”意大利语 -“it-it”日语 -“ja-jp”朝鲜语 -“ko-kr”葡萄牙语 -“pt-br”中文（繁体）-“zh-cn”中文（台湾地区）-“zh-tw” |
| *repositoryId* | 字符串 | 否 | &#39;&#39; | 资源选择器从中加载内容的存储库。 |
| *additionalAemSolutions* | `Array<string>` | 否 | [ ] | 它允许您添加其他AEM存储库的列表。 如果此属性中未提供任何信息，则仅考虑媒体库或 AEM Assets 存储库。 |
| *hideTreeNav* | 布尔型 | 否 |  | 指定是显示还是隐藏资源树导航侧边栏。它仅在模态视图中使用，因此，该属性在边栏视图中不起作用。 |
| *onDrop* | 函数 | 否 | | 该属性允许资源的删除功能。 |
| *dropOptions* | `{allowList?: Object}` | 否 | | 使用“allowList”配置删除选项。 |
| *colorScheme* | 字符串 | 否 | | 为资源选择器配置主题（`light` 或 `dark`）。 |
| *handleSelection* | 函数 | 否 | | 在资源已选定并单击模态上的 `Select` 按钮时调用资源项数组。仅在模态视图中调用此函数。对于边栏视图，请使用 `handleAssetSelection` 或 `onDrop` 函数。示例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 有关详细信息，请参阅[所选资源类型](#selected-asset-type)。 |
| *handleAssetSelection* | 函数 | 否 | | 在选择或取消选择资源时调用项目数组。如果您需要在用户选择资源时进行侦听，这会很有用。示例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 有关详细信息，请参阅[所选资源类型](#selected-asset-type)。 |
| *onClose* | 函数 | 否 | | 在按下模态视图中的 `Close` 按钮时调用。这仅在 `modal` 视图中被调用，在 `rail` 视图中将被忽略。 |
| *onFilterSubmit* | 函数 | 否 | | 当用户更改其他过滤器条件时调用过滤器项。 |
| *selectionType* | 字符串 | 否 | 单个 | 一次性为 `single` 或 `multiple` 资源选择配置。 |
| *dragOptions.允许列表* | 布尔型 | 否 | | 属性用于允许或拒绝拖动不可选资产。 |
| *aemTierType* | 字符串 | 否 | | 它允许您选择是显示交付层、创作层中的资产，还是同时显示两者。 <br><br>语法： `aemTierType:[0: "author" 1: "delivery"` <br><br>例如，如果同时使用了`["author","delivery"]`，则存储库切换器将显示创作和投放选项。 <br>此外，在Dynamic Media中通过OpenAPI功能将`["delivery"]`用于与投放相关的资源。 |
| *handleNavigateToAsset* | 函数 | 否 | | 它是一个回调函数，用于处理资源的选择。 |
| *noWrap* | 布尔型 | 否 | | *noWrap*&#x200B;属性有助于在侧边栏面板中呈现资产选择器。 如果未提及此属性，则默认情况下会呈现&#x200B;*对话框视图*。 |
| *dialogSize* | 小型、中型、大型、全屏或全屏接管 | 字符串 | 可选 | 通过使用给定选项指定布局大小可控制布局。 |
| *colorScheme* | 浅色或深色 | 否 | | 此属性用于设置Asset Selector应用程序的主题。 您可以选择浅色或深色主题。 |
| *filterRepoList* | 函数 | 否 |  | 您可以使用`filterRepoList`回调函数来调用Experience Manager存储库并返回已过滤的存储库列表。 |

<!--| *rootPath* | string | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | string | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |-->

## 有关使用资源选择器属性的示例 {#usage-examples}

您可以在 `index.html` 文件中定义资源选择器[属性](#asset-selector-properties)，以自定义应用程序中的资源选择器显示。

### 示例 1：边栏视图中的资源选择器

![rail-view-example](assets/rail-view-example-vanilla.png)

如果AssetSelector `rail`的值设置为`false`或未在属性中提及，则默认情况下，Asset Selector会显示在模式视图中。 `acvConfig`属性用于启用资产查看器的边栏视图。 访问[启用或禁用拖放](#enable-disable-drag-and-drop)以了解`acvConfig`属性的用法。

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
    },
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

将以下属性添加到`assetSelectorProp`以启用拖放模式。 要禁用拖放，请使用`false`替换`true`参数。

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
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
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
| *repo:repositoryId* | 字符串 | 存储资源的存储库的唯一标识符。 |
| *repo:id* | 字符串 | 资源的唯一标识符。 |
| *repo:assetClass* | 字符串 | 资源的分类（例如，图像、视频或文档）。 |
| *repo:name* | 字符串 | 资源的名称，包括文件扩展名。 |
| *repo:size* | 数字 | 资源的大小，以字节为单位。 |
| *repo:path* | 字符串 | 资源在存储库中的位置。 |
| *repo:ancestors* | `Array<string>` | 存储库中资源的祖先项数组。 |
| *repo:state* | 字符串 | 存储库中资产的当前状态（例如，活动、删除等）。 |
| *repo:createdBy* | 字符串 | 创建资源的用户或系统。 |
| *repo:createDate* | 字符串 | 资源的创建日期和时间。 |
| *repo:modifiedBy* | 字符串 | 上次修改资源的用户或系统。 |
| *repo:modifyDate* | 字符串 | 资源的上次修改日期和时间。 |
| *dc:format* | 字符串 | 资源的格式，如文件类型(例如，JPEG、PNG等)。 |
| *tiff:imageWidth* | 数字 | 资源的宽度。 |
| *tiff:imageLength* | 数字 | 资源的高度。 |
| *computedMetadata* | `Record<string, any>` | 一个对象，表示所有类型的所有资源元数据（存储库、应用程序或嵌入式元数据）的存储桶。 |
| *_links* | `Record<string, any>` | 关联资源的超媒体链接。包括元数据和演绎版等资源的链接。 |
| *_links.<http://ns.adobe.com/adobecloud/rel/rendition>* | `Array<Object>` | 对象数组，包含有关资源演绎版的信息。 |
| *_links.<http://ns.adobe.com/adobecloud/rel/rendition[].href>* | 字符串 | 演绎版的 URI。 |
| *_links.<http://ns.adobe.com/adobecloud/rel/rendition[].type>* | 字符串 | 演绎版的 MIME 类型。 |
| *_links.<http://ns.adobe.com/adobecloud/rel/rendition[].'repo:size>&#39;* | 数字 | 演绎版的大小，以字节为单位。 |
| *_links.<http://ns.adobe.com/adobecloud/rel/rendition[].width>* | 数字 | 演绎版的宽度。 |
| *_links.<http://ns.adobe.com/adobecloud/rel/rendition[].height>* | 数字 | 演绎版的高度。 |

有关属性和详细示例的完整列表，请访问[资源选择器代码示例](https://github.com/adobe/aem-assets-selectors-mfe-examples)。

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

要在左侧导航中隐藏文件夹，请单击&#x200B;**[!UICONTROL 隐藏文件夹]**&#x200B;图标。要撤消更改，请再次单击&#x200B;**[!UICONTROL 隐藏文件夹]**&#x200B;图标。

### 存储库切换器 {#repository-switcher}

通过资产选择器，您还可以切换存储库以进行资产选择。 您可以从左侧面板中可用的下拉列表中选择所选存储库。下拉列表中可用的存储库选项基于 `index.html` 文件中定义的 `repositoryId` 属性。它基于登录用户访问的选定IMS组织的环境。 消费者可以传递首选 `repositoryID`，在这种情况下，资源选择器将停止呈现存储库切换器，并且仅呈现给定存储库中的资源。
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### 资源存储库

它是可用于执行操作的资源文件夹的集合。

### 开箱即用的过滤器 {#filters}

资源选择器还提供开箱即用的过滤器选项来细化您的搜索结果。可用过滤器如下：

* `File type`：包括文件夹、文件、图像、文档或视频
* `MIME type`：包括 JPG、GIF、PPTX、PNG、MP4、DOCX、TIFF、PDF、XLSX
* `Image Size`：包括图像的最小/最大宽度、最小/最大高度

  ![rail-view-example](assets/filters-asset-selector.png)

### 自定义搜索

除了全文搜索之外，资产选择器还允许您使用自定义搜索在文件中搜索资产。 您可以在“模态”视图和“边栏”视图模式下使用自定义搜索过滤器。

![custom-search](assets/custom-search1.png)

您也可以创建默认搜索过滤器以保存经常搜索的字段并在以后使用。要为资源创建自定义搜索，可以使用 `filterSchema` 属性。

### 搜索栏 {#search-bar}

通过资源选择器，您可以对所选存储库中的资源执行全文搜索。 例如，如果您在搜索栏中键入关键字 `wave`，则将显示任意元数据属性中提及的所有带 `wave` 关键字的资源。

### 排序 {#sorting}

您可以在资源选择器中按资源的名称、尺寸或大小对资源进行排序。您还可以按升序或降序对资源进行排序。

### 视图类型 {#types-of-view}

通过资源选择器，您可以在四种不同的视图中查看资源：

* **![列表视图](assets/do-not-localize/list-view.png)[!UICONTROL 列表视图]**：列表视图在单个列中显示可滚动的文件和文件夹。
* **![网格视图](assets/do-not-localize/grid-view.png)[!UICONTROL 网格视图]**：网格视图在行和列的网格中显示可滚动的文件和文件夹。
* **![库视图](assets/do-not-localize/gallery-view.png)[!UICONTROL 库视图]**：库视图在居中锁定的水平列表中显示文件或文件夹。
* **![瀑布视图](assets/do-not-localize/waterfall-view.png)[!UICONTROL 瀑布视图]**：瀑布视图以桥的形式显示文件或文件夹。

<!--
### Support for multiple instances

The micro front-end design supports the display of multiple instances of Asset Selector on a single screen.

![multiple-instance](assets/multiple-instance.png)
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
