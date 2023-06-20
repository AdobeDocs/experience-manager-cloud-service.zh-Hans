---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 使用资源选择器在您的应用程序中搜索、查找和检索资源的元数据和演绎版。
contentOwner: Adobe
role: Admin,User
exl-id: b968f63d-99df-4ec6-a9c9-ddb77610e258
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2376'
ht-degree: 99%

---

# 微前端资源选择器 {#Overview}

微前端资源选择器提供了一个用户界面，它可以轻松地与 [!DNL Experience Manager Assets as a Cloud Service] 存储库集成，以便您能够浏览或搜索存储库中可用的数字资源，并在您的应用程序创作体验中使用它们。

微前端用户界面可用于采用了资源选择器包的应用程序体验。对该包的任何更新都会自动导入，并且最新部署的资源选择器会自动加载到您的应用程序中。

![概述](assets/overview.png)

资源选择器提供了许多好处，例如：

* 使用 Vanilla JavaScript 库轻松与任何 Adobe 或非 Adobe 应用程序集成。
* 易于维护，因为对资源选择器包的更新将自动部署到可用于应用程序的资源选择器。您的应用程序中无需更新即可加载最新的修改。
* 易于定制，因为提供了用于控制应用程序中的资源选择器显示的属性。

* 全文搜索、开箱即用和自定义过滤器，可快速导航到资源以便在创作体验中使用。

* 能够在 IMS 组织内切换存储库以选择资源。

* 能够按名称、维度和大小对资源进行排序，并在列表、网格、库或瀑布视图中查看它们。

本文内容旨在说明如何将资源选择器与 Unified Shell 下的 [!DNL Adobe] 应用程序结合使用，或如何在已生成用于身份验证的 imsToken 时使用资源选择器。在本文中，我们将这些工作流称作非 SUSI 流。

执行以下任务以将资源选择器与您的 [!DNL Experience Manager Assets as a Cloud Service] 存储库集成和结合使用：

* [使用 Vanilla JS 集成资源选择器](#integration-with-vanilla-js)
* [定义资源选择器显示属性](#asset-selector-properties)
* [使用资源选择器](#using-asset-selector)

## 使用 Vanilla JS 集成资源选择器 {#integration-with-vanilla-js}

您可以将任何 [!DNL Adobe] 或非 Adobe 应用程序与 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 存储库集成，并从该应用程序中选择资源。

通过导入资源选择器包并使用 Vanilla JavaScript 库连接到 Assets as a Cloud Service 来实现集成。您需要编辑 `index.html` 或您应用程序中的任何相应文件以 -
* 定义身份验证详细信息
* 访问 Assets as a Cloud Service 存储库
* 配置资源选择器显示属性

<!--
Asset Selector supports authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS) properties such as `imsScope` or `imsClientID`. Authentication using these IMS properties is referred to as SUSI (Sign Up Sign In) flow in this article.

You can perform authentication without defining some of the IMS properties, such as `imsScope` or `imsClientID`, if:

*   You are integrating an [!DNL Adobe] application on [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
*   You already have an IMS token generated for authentication.

Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining `imsScope` or `imsClientID` IMS properties is referred to as a non-SUSI flow in this article.
-->

在以下情况下，您无需定义某些 IMS 属性即可执行身份验证：

* 您正在 [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=zh-Hans) 上集成 [!DNL Adobe] 应用程序。
* 您已生成用于身份验证的 IMS 令牌。

## 前提条件 {#prerequisites}

<!--
If your application requires user based authentication, out-of-the-box Asset Selector also supports a flow for authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS.)

You can use properties such as `imsScope` or `imsClientID` to retrieve `imsToken` automatically. You can use SUSI (Sign Up Sign In) flow and IMS properties. Also, you can obtain your own imsToken and pass it to Asset Selector by integrating within [!DNL Adobe] application on Unified Shell or if you already have an imsToken obtained via other methods (for example, using technical account). Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining IMS properties (For example, `imsScope` and `imsClientID`) is referred to as a non-SUSI flow.
-->

在 `index.html` 文件或应用程序实施中的类似文件中定义先决条件，以定义用于访问 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 存储库的身份验证详细信息。先决条件包括：
* imsOrg
* imsToken
* apikey
<!--
The prerequisites vary if you are authenticating using a SUSI flow or a non-SUSI flow.

**Non-SUSI flow**

*   imsOrg
*   imsToken
*   apikey

For more information on these properties, refer to [Asset Selector Properties](#asset-selector-properties).

**SUSI flow**

*   imsClientId
*   imsScope
*   redirectUrl
*   imsOrg
*   apikey

For more information on these properties, refer to [Example for the SUSI flow](#susi-vanilla) and [Asset Selector Properties](#asset-selector-properties).
-->

## 安装 {#installation}

可通过 ESM CDN（例如 [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)）和 [UMD](https://github.com/umdjs/umd) 版本获得资源选择器。

在使用 **UMD 版本**&#x200B;的浏览器中（推荐）：

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

在使用 **ESM CDN 版本**&#x200B;并支持 `import maps` 的浏览器中：

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

在使用 **ESM CDN 版本**&#x200B;的 Deno/Webpack 模块联合中：

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### 选定资源类型 {#selected-asset-type}

选定资源类型是一个对象数组，其中包含使用 `handleSelection`、`handleAssetSelection` 和 `onDrop` 函数时的资源信息。

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

| 属性 | 类型 | 解释 |
|---|---|---|
| *repo:repositoryId* | 字符串 | 存储资源的存储库的唯一标识符。 |
| *repo:id* | 字符串 | 资源的唯一标识符。 |
| *repo:assetClass* | 字符串 | 资源的分类（例如，图像、视频或文档）。 |
| *repo:name* | 字符串 | 资源的名称，包括文件扩展名。 |
| *repo:size* | 数字 | 资源的大小，以字节为单位。 |
| *repo:path* | 字符串 | 资源在存储库中的位置。 |
| *repo:ancestors* | `Array<string>` | 存储库中资源的祖先项数组。 |
| *repo:state* | 字符串 | 存储库中资源的当前状态（例如，活动、已删除等）。 |
| *repo:createdBy* | 字符串 | 创建资源的用户或系统。 |
| *repo:createDate* | 字符串 | 资源的创建日期和时间。 |
| *repo:modifiedBy* | 字符串 | 上次修改资源的用户或系统。 |
| *repo:modifyDate* | 字符串 | 资源的上次修改日期和时间。 |
| *dc:format* | 字符串 | 资源的格式，例如文件类型（例如 JPEG、PNG 等）。 |
| *tiff:imageWidth* | 数字 | 资源的宽度。 |
| *tiff:imageLength* | 数字 | 资源的高度。 |
| *computedMetadata* | `Record<string, any>` | 一个对象，表示所有类型的所有资源元数据（存储库、应用程序或嵌入式元数据）的存储桶。 |
| *_links* | `Record<string, any>` | 关联资源的超媒体链接。包括元数据和演绎版等资源的链接。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition* | `Array<Object>` | 对象数组，包含有关资源演绎版的信息。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].href* | 字符串 | 演绎版的 URI。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].type* | 字符串 | 演绎版的 MIME 类型。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].&#39;repo:size&#39;* | 数字 | 演绎版的大小，以字节为单位。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].width* | 数字 | 演绎版的宽度。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].height* | 数字 | 演绎版的高度。 |

有关属性和详细示例的完整列表，请访问[资源选择器代码示例](https://github.com/adobe/aem-assets-selectors-mfe-examples)。

<!--
### ImsAuthProps {#ims-auth-props}

The `ImsAuthProps` properties define the authentication information and flow that the Asset Selector uses to obtain an `imsToken`. By setting these properties, you can control how the authentication flow should behave and register listeners for various authentication events.

| Property Name | Description|
|---|---|
| `imsClientId`| A string value representing the IMS client ID used for authentication purposes. This value is provided by Adobe and is specific to your Adobe AEM CS organization.|
| `imsScope`| Describes the scopes used in authentication. The scopes determine the level of access that the application has to your organization resources. Multiple scopes can be separated by commas.|
| `redirectUrl` | Represents the URL where the user is redirected after authentication. This value is typically set to the current URL of the application. If a `redirectUrl` is not supplied, `ImsAuthService` will use the redirectUrl used to register the `imsClientId`|
| `modalMode`| A boolean indicating whether the authentication flow should be displayed in a modal (pop-up) or not. If set to `true`, the authentication flow is displayed in a pop-up. If set to `false`, the authentication flow is displayed in a full page reload. _Note:_ for better UX, you can dynamically control this value if the user has browser pop-up disabled. |
| `onImsServiceInitialized`| A callback function that is called when the Adobe IMS authentication service is initialized. This function takes one parameter, `service`, which is an object representing the Adobe IMS service. See [`ImsAuthService`](#imsauthservice-ims-auth-service) for more details.|
| `onAccessTokenReceived`| A callback function that is called when an `imsToken` is received from the Adobe IMS authentication service. This function takes one parameter, `imsToken`, which is a string representing the access token. |
| `onAccessTokenExpired`| A callback function that is called when an access token has expired. This function is typically used to trigger a new authentication flow to obtain a new access token. |
| `onErrorReceived`| A callback function that is called when an error occurs during authentication. This function takes two parameters: the error type and error message. The error type is a string representing the type of error and the error message is a string representing the error message. |

### ImsAuthService {#ims-auth-service}

`ImsAuthService` class handles the authentication flow for the Asset Selector. It is responsible for obtaining an `imsToken` from the Adobe IMS authentication service. The `imsToken` is used to authenticate the user and authorize access to the Adobe Experience Manager (AEM) CS Assets repository. ImsAuthService uses the `ImsAuthProps` properties to control the authentication flow and register listeners for various authentication events. You can use the convenient [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) function to register the _ImsAuthService_ instance with the Asset Selector. The following functions are available on the `ImsAuthService` class. However, if you're using the _registerAssetsSelectorsAuthService_ function, you do not need to call these functions directly.

| Function Name | Description |
|---|---|
| `isSignedInUser` | Determines whether the user is currently signed in to the service and returns a boolean value accordingly.|
| `getImsToken`    | Retrieves the authentication `imsToken` for the currently signed-in user, which can be used to authenticate requests to other services such as generating asset _rendition.|
| `signIn`| Initiates the sign-in process for the user. This function uses the `ImsAuthProps` to show authentication in either a pop-up or a full page reload |
| `signOut`| Signs the user out of the service, invalidating their authentication token and requiring them to sign in again to access protected resources. Invoking this function will reload the current page.|
| `refreshToken`| Refreshes the authentication token for the currently signed-in user, preventing it from expiring and ensuring uninterrupted access to protected resources. Returns a new authentication token that can be used for subsequent requests. |
-->

### 非 SUSI 流的示例 {#non-susi-vanilla}

此示例说明如何在 Unified Shell 下运行 [!DNL Adobe] 应用程序时或在您已生成用于身份验证的 `imsToken` 时，将资源选择器与非 SUSI 流结合使用。

在您的代码中使用 `script` 标记引入资源选择器包，如以下示例中的&#x200B;_第 6 行至第 15 行_&#x200B;中所示。加载该脚本后，`PureJSSelectors` 全局变量将可供使用。定义资源选择器[属性](#asset-selector-properties)，如&#x200B;_第 16 行至第 23 行_&#x200B;中所示。`imsOrg` 和 `imsToken` 属性是非 SUSI 流中的身份验证所必需的。`handleSelection` 属性用于处理选定资源。要呈现资源选择器，请调用 `renderAssetSelector` 函数，如&#x200B;_第 17 行_&#x200B;中所述。资源选择器将显示在 `<div>` 容器元素中，如&#x200B;_第 21 行和第 22 行_&#x200B;中所示。

通过执行这些步骤，您可以在 [!DNL Adobe] 应用程序中将资源选择器用于非 SUSI 流。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
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

有关详细示例，请访问[资源选择器代码示例](https://github.com/adobe/aem-assets-selectors-mfe-examples)。

<!--
### Example for the SUSI flow {#susi-vanilla}

Use this example `index.html` file for authentication if you are integrating your application using SUSI flow.

Access the Asset Selector package using the `Script` Tag, as shown in *line 9* to *line 11* of the example `index.html` file.

*Line 14* to *line 38* of the example describes the IMS flow properties, such as `imsClientId`, `imsScope`, and `redirectURL`. The function requires that you define at least one of the `imsClientId` and `imsScope` properties. If you do not define a value for `redirectURL`, the registered redirect URL for the client ID is used.

As you do not have an `imsToken` generated, use the `registerAssetsSelectorsAuthService` and `renderAssetSelectorWithAuthFlow` functions, as shown in line 40 to line 50 of the example `index.html` file. Use the `registerAssetsSelectorsAuthService` function before `renderAssetSelectorWithAuthFlow` to register the `imsToken` with the Asset Selector. [!DNL Adobe] recommends to call `registerAssetsSelectorsAuthService` when you instantiate the component.

Define the authentication and other Assets as a Cloud Service access-related properties in the `const props` section, as shown in *line 54* to *line 60* of the example `index.html` file.

The `PureJSSelectors` global variable, mentioned in *line 65*, is used to render the Asset Selector in the web browser.

Asset Selector is rendered on the `<div>` container element, as mentioned in *line 74* to *line 81*. The example uses a dialog to display the Asset Selector.

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
-->

## 使用资源选择器属性 {#asset-selector-properties}

您可以使用资源选择器属性来自定义资源选择器的呈现方式。下表列出了可用于自定义和使用资源选择器的属性。

| 属性 | 类型 | 必需 | 默认 | 描述 |
|---|---|---|---|---|
| *边栏* | 布尔型 | 否 | false | 如果已标记 `true`，资产选择器将在左边栏视图中渲染。 如果已标记 `false`，资产选择器将以模式视图呈现。 |
| *imsOrg* | 字符串 | 是 | | 为组织设置 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 时分配的 Adobe Identity Management System (IMS) ID。需要 `imsOrg` 密钥来验证您所访问的组织是否在 Adobe IMS 下。 |
| *imsToken* | 字符串 | 否 | | 用于身份验证的 IMS 持有者令牌。如果您使用的是非 SUSI 流，则需要 `imsToken`。 |
| *apiKey* | 字符串 | 否 | | 用于访问 AEM 发现服务的 API 密钥。如果您使用的是非 SUSI 流，则需要 `apiKey`。 |
| *rootPath* | 字符串 | 否 | /content/dam/ | 资源选择器从中显示您的资源的文件夹路径。也可采用封装形式使用 `rootPath`。例如，给定以下路径 `/content/dam/marketing/subfolder/`，资源选择器不允许您遍历任何父文件夹，而只显示子文件夹。 |
| *path* | 字符串 | 否 | | 在呈现资源选择器时用于导航到特定资源目录的路径。 |
| *filterSchema* | 数组 | 否 | | 用于配置过滤器属性的模型。这在需要限制资源选择器中的某些过滤器选项时很有用。 |
| *filterFormProps* | 对象 | 否 | | 指定您需要用于细化搜索的过滤器属性。例如，MIME 类型 JPG、PNG、GIF。 |
| *selectedAssets* | 数组 `<Object>` | 否 |                 | 呈现资源选择器时指定选定资源。包含资源的 id 属性的必需对象数组。例如，`[{id: 'urn:234}, {id: 'urn:555'}]` 资源必须在当前目录中可用。如果您需要使用其他目录，请也为 `path` 属性提供一个值。 |
| *acvConfig* | 对象 | 否 | | 包含对象的资源收藏集视图属性，该对象包含用于覆盖默认值的自定义配置。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |                 | 如果 OOTB 翻译不足以满足您的应用程序需求，您可以公开一个接口，利用该接口可通过 `i18nSymbols` 属性传递自定义本地化值。通过此接口传递值将覆盖提供的默认翻译，而改用您自己的翻译。要执行覆盖，您必须将一个有效的[消息描述符](https://formatjs.io/docs/react-intl/api/#message-descriptor)对象传递到要覆盖的 `i18nSymbols` 键。 |
| *intl* | 对象 | 否 | | 资源选择器提供默认的 OOTB 翻译。您可以通过用 `intl.locale` 属性提供有效的区域设置字符串来选择翻译语言。例如：`intl={{ locale: "es-es" }}` </br></br> 支持的区域设置字符串遵循语言标准名称表示的 [ISO 639 - 代码](https://www.iso.org/iso-639-language-codes.html)。</br></br> 支持的区域设置列表：英语 -“en-us”（默认）西班牙语 -“es-es”德语 -“de-de”法语 -“fr-fr”意大利语 -“it-it”日语 -“ja-jp”朝鲜语 -“ko-kr”葡萄牙语 -“pt-br”中文（繁体）-“zh-cn”中文（台湾地区）-“zh-tw” |
| *repositoryId* | 字符串 | 否 | &#39;&#39; | 资源选择器从中加载内容的存储库。 |
| *additionalAemSolutions* | `Array<string>` | 否 | [ ] | 它允许您添加其他 AEM 存储库的列表。如果此属性中未提供任何信息，则仅考虑媒体库或 AEM Assets 存储库。 |
| *hideTreeNav* | 布尔型 | 否 |  | 指定是显示还是隐藏资源树导航侧边栏。它仅在模态视图中使用，因此，该属性在边栏视图中不起作用。 |
| *onDrop* | 函数 | 否 | | 该属性允许资源的删除功能。 |
| *dropOptions* | `{allowList?: Object}` | 否 | | 使用“allowList”配置删除选项。 |
| *colorScheme* | 字符串 | 否 | | 为资源选择器配置主题（`light` 或 `dark`）。 |
| *handleSelection* | 函数 | 否 | | 在资源已选定并单击模态上的 `Select` 按钮时调用资源项数组。仅在模态视图中调用此函数。对于边栏视图，请使用 `handleAssetSelection` 或 `onDrop` 函数。示例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 有关详细信息，请参阅[所选资源类型](#selected-asset-type)。 |
| *handleAssetSelection* | 函数 | 否 | | 在选择或取消选择资源时调用项目数组。如果您需要在用户选择资源时进行侦听，这会很有用。示例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 有关详细信息，请参阅[所选资源类型](#selected-asset-type)。 |
| *onClose* | 函数 | 否 | | 在按下模态视图中的 `Close` 按钮时调用。这仅在 `modal` 视图中被调用，在 `rail` 视图中将被忽略。 |
| *onFilterSubmit* | 函数 | 否 | | 当用户更改其他过滤器条件时调用过滤器项。 |
| *selectionType* | 字符串 | 否 | 单个 | 一次性为 `single` 或 `multiple` 资源选择配置。 |

## 有关使用资源选择器属性的示例 {#usage-examples}

您可以在 `index.html` 文件中定义资源选择器[属性](#asset-selector-properties)，以自定义应用程序中的资源选择器显示。

### 示例 1：边栏视图中的资源选择器

![rail-view-example](assets/rail-view-example-vanilla.png)

如果 AssetSelector `rail` 的值设为 `false` 或未在属性中提及，则资源选择器默认显示在模态视图中。

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### 示例 2：元数据弹出窗口

使用各种属性来定义要使用信息图标查看的资源的元数据。信息弹出窗口提供有关资源或文件夹的信息集合，包括资源的标题、尺寸、修改日期、位置和描述。在下面的示例中，各种属性用于显示资源的元数据，例如，`repo:path` 属性指定资源的位置。<!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)


### 示例 3：边栏视图中的自定义过滤器属性

除了 Facet 搜索之外，资源选择器还允许您自定义各种属性来细化 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 应用程序中的搜索。您需要添加以下代码来在应用程序中添加自定义搜索过滤器。在下面的示例中，`Type Filter` 搜索过滤图像、文档或视频中的资源类型或已为搜索添加的过滤器类型。

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

<!-- Property details to be added here. Referred the ticket https://jira.corp.adobe.com/browse/ASSETS-19023-->

<!--
## Asset Selector Object Schema {#object-schema}

Schema describes the object properties associated with an asset selected using Asset Selector. It uses the combination of data types and their values to validate the object describing the selected Asset using an Asset Selector.

**Schema Syntax**
````
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
````

**Query Parameters**

| Parameter | Type | Description |
|---|---|---|
| repo:id | string | ID of an Asset |
| repo:name | string | The name of an Asset |
| repo:path | string | The path of an Asset |
| repo:size | number | Size of an Asset (in bytes) |
| repo:createdBy | string | ID of a user who created an Asset |
| repo: createdDate | string | The timestamp when an asset was created |
| repo:modifiedBy | string | ID of a user who modified the asset recently |
| repo:modifyDate | string | The timestamp when the asset was last modified |
| dc:format | string | MIME type of an Asset |
| tiff:imageWidth | number | The width of an image type of Asset |
| tiff:imageLength | number | The height of an image type of Asset |
| repo:state | string | The `Approved`, `Rejected`, or `Expired`state of an Asset |
| computedMetadata | string | It is an object that represents a bucket for all the Asset's metadata of all kinds (repository, application or embedded metadata) |
| _links | string | It represents the collection of links used in the Asset Selector. The links are represented in the form of an array. The parameters of an array include: `href`, `type`, `repo:size`, `width`, `height`, etc.  |

For the detailed example of Object Schema, click 
-->

## 使用对象架构处理资源选择 {#handling-selection}

`handleSelection` 属性用于处理资源选择器中的单个或多个资源选择。以下示例说明了 `handleSelection` 的使用语法。

![handle-selection](assets/handling-selection.png)

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

资源选择器还允许您切换存储库来选择资源。您可以从左侧面板中可用的下拉列表中选择所选存储库。下拉列表中可用的存储库选项基于 `index.html` 文件中定义的 `repositoryId` 属性。它基于由已登录用户访问的所选 IMS 组织中的环境。消费者可以传递首选 `repositoryID`，在这种情况下，资源选择器将停止呈现存储库切换器，并且仅呈现给定存储库中的资源。
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

除了全文搜索之外，资源选择器还允许您使用自定义搜索来搜索文件中的资源。您可以在“模态”视图和“边栏”视图模式下使用自定义搜索过滤器。

![custom-search](assets/custom-search.png)

您也可以创建默认搜索过滤器以保存经常搜索的字段并在以后使用。要为资源创建自定义搜索，可以使用 `filterSchema` 属性。

### 搜索栏 {#search-bar}

资源选择器允许您在所选存储库中对资源进行全文搜索。例如，如果您在搜索栏中键入关键字 `wave`，则将显示任意元数据属性中提及的所有带 `wave` 关键字的资源。

### 排序 {#sorting}

您可以在资源选择器中按资源的名称、尺寸或大小对资源进行排序。您还可以按升序或降序对资源进行排序。

### 视图类型 {#types-of-view}

资源选择器允许您在四种不同的视图中查看资源：

* **![列表视图](assets/do-not-localize/list-view.png)[!UICONTROL 列表视图]**：列表视图在单个列中显示可滚动的文件和文件夹。
* **![网格视图](assets/do-not-localize/grid-view.png)[!UICONTROL 网格视图]**：网格视图在行和列的网格中显示可滚动的文件和文件夹。
* **![库视图](assets/do-not-localize/gallery-view.png)[!UICONTROL 库视图]**：库视图在居中锁定的水平列表中显示文件或文件夹。
* **![瀑布视图](assets/do-not-localize/waterfall-view.png)[!UICONTROL 瀑布视图]**：瀑布视图以桥的形式显示文件或文件夹。

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
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It allows you to control the display of various text or symbols as per your choice.
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
*   **Open in media library** Allows you to open the asset in media library.
*   **Upload** Allows you to upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector allows you to know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->
