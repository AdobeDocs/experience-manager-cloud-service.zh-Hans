---
title: 的资源选择器 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: 使用资源选择器可在应用程序中搜索、查找和检索资源的元数据和演绎版。
contentOwner: Adobe
role: Admin,User
source-git-commit: af36101d8fecd7fab2300f93d40bba4c92f8eafe
workflow-type: tm+mt
source-wordcount: '2378'
ht-degree: 3%

---


# 微型前端资产选择器 {#Overview}

微型前端资产选择器提供了一个用户界面，可轻松与 [!DNL Experience Manager Assets as a Cloud Service] 存储库，以便您可以浏览或搜索存储库中可用的数字资产，并在应用程序创作体验中使用它们。

使用资产选择器软件包，可以在您的应用程序体验中使用Micro-Frontend用户界面。 将自动导入对包的任何更新，并在应用程序中自动加载最新部署的资产选择器。

![概述](assets/overview.png)

资产选择器提供了许多好处，例如：

* 使用Vanilla JavaScript库轻松与任何Adobe或非Adobe应用程序集成。
* 易于维护，因为资产选择器包的更新会自动部署到可用于您的应用程序的资产选择器。 您的应用程序中不需要更新即可加载最新修改。
* 易于自定义，因为有一些属性可用于控制资产选择器显示在应用程序中。

* 全文搜索、现成和自定义筛选条件，可快速导航到要在创作体验中使用的资源。

* 能够在IMS组织内切换存储库以进行资产选择。

* 能够按名称、维度和大小对资源排序，并在列表、网格、图库或瀑布视图中查看这些资源。

本文的范围是演示如何将资产选择器与 [!DNL Adobe] Unified Shell下的应用程序，或者已经为身份验证生成了imsToken时。 本文将这些工作流称为非SUSI流。

执行以下任务，将资产选择器与您的集成和使用 [!DNL Experience Manager Assets as a Cloud Service] 存储库：

* [使用Vanilla JS集成资产选择器](#integration-with-vanilla-js)
* [定义资源选择器显示属性](#asset-selector-properties)
* [使用资源选择器](#using-asset-selector)

## 使用Vanilla JS集成资产选择器 {#integration-with-vanilla-js}

您可以集成任何 [!DNL Adobe] 或非Adobe应用程序 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 并从应用程序中选择资源。

通过导入资产选择器软件包，并使用Vanilla JavaScript库连接到Assetsas a Cloud Service，可完成集成。 您需要编辑 `index.html` 或应用程序中的任何相应文件 — 
* 定义身份验证详细信息
* 访问Assetsas a Cloud Service存储库
* 配置资源选择器显示属性

<!--
Asset Selector supports authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS) properties such as `imsScope` or `imsClientID`. Authentication using these IMS properties is referred to as SUSI (Sign Up Sign In) flow in this article.

You can perform authentication without defining some of the IMS properties, such as `imsScope` or `imsClientID`, if:

*   You are integrating an [!DNL Adobe] application on [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
*   You already have an IMS token generated for authentication.

Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining `imsScope` or `imsClientID` IMS properties is referred to as a non-SUSI flow in this article.
-->

在以下情况下，您可以在不定义某些IMS属性的情况下执行身份验证：

* 您正在集成 [!DNL Adobe] 应用程序 [Unifiedshell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
* 您已经为身份验证生成了IMS令牌。

## 前提条件 {#prerequisites}

<!--
If your application requires user based authentication, out-of-the-box Asset Selector also supports a flow for authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS.)

You can use properties such as `imsScope` or `imsClientID` to retrieve `imsToken` automatically. You can use SUSI (Sign Up Sign In) flow and IMS properties. Also, you can obtain your own imsToken and pass it to Asset Selector by integrating within [!DNL Adobe] application on Unified Shell or if you already have an imsToken obtained via other methods (for example, using technical account). Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining IMS properties (For example, `imsScope` and `imsClientID`) is referred to as a non-SUSI flow.
-->

在中定义先决条件 `index.html` 文件或应用程序实施中的类似文件，以定义用于访问 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 存储库。 先决条件包括：
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

资产选择器可通过两个ESM CDN使用(例如， [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/))和 [UMD](https://github.com/umdjs/umd) 版本。

在浏览器中使用 **UMD版本** （推荐）：

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

在浏览器中，使用 `import maps` 支持使用 **ESM CDN版本**：

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

在Deno/Webpack模块联合中，使用 **ESM CDN版本**：

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### 选定的资源类型 {#selected-asset-type}

选定的资源类型是一个对象数组，其中包含使用时的资源信息 `handleSelection`， `handleAssetSelection`、和 `onDrop` 函数。

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

下表介绍了“选定的资产”对象的一些重要属性。

| 属性 | 类型 | 解释 |
|---|---|---|
| *repo：repositoryId* | 字符串 | 存储资产的存储库的唯一标识符。 |
| *repo：id* | 字符串 | 资源的唯一标识符。 |
| *repo：assetClass* | 字符串 | 资产的分类（例如，图像或视频、文档）。 |
| *repo：name* | 字符串 | 资源的名称，包括文件扩展名。 |
| *repo：size* | 数字 | 资源的大小，以字节为单位。 |
| *repo：path* | 字符串 | 资源在存储库中的位置。 |
| *repo：ancestors* | `Array<string>` | 存储库中资产的上级项目数组。 |
| *repo：state* | 字符串 | 存储库中资产的当前状态（例如，活动、已删除等）。 |
| *repo：createdBy* | 字符串 | 创建资产的用户或系统。 |
| *repo：createDate* | 字符串 | 创建资产的日期和时间。 |
| *repo：modifiedBy* | 字符串 | 上次修改资产的用户或系统。 |
| *repo：modifyDate* | 字符串 | 上次修改资产的日期和时间。 |
| *dc:format* | 字符串 | 资源的格式，例如文件类型(例如，JPEG、PNG等)。 |
| *tiff：imageWidth* | 数字 | 资源的宽度。 |
| *tiff：imageLength* | 数字 | 资源的高度。 |
| *计算元数据* | `Record<string, any>` | 一个对象，表示各种资产元数据（存储库、应用程序或嵌入元数据）的存储桶。 |
| *链接(_L)* | `Record<string, any>` | 相关资产的超媒体链接。 包括元数据和演绎版等资源的链接。 |
| *_链接。http://ns.adobe.com/adobecloud/rel/rendition* | `Array<Object>` | 包含有关资源演绎版信息的对象数组。 |
| *_链接。http://ns.adobe.com/adobecloud/rel/rendition[].href* | 字符串 | 呈现版本的URI。 |
| *_链接。http://ns.adobe.com/adobecloud/rel/rendition[].type* | 字符串 | 节目的MIME类型。 |
| *_链接。http://ns.adobe.com/adobecloud/rel/rendition[].&#39;repo：size`* | 数字 | 演绎版的大小（字节）。 |
| *_链接。http://ns.adobe.com/adobecloud/rel/rendition[].width* | 数字 | 演绎版的宽度。 |
| *_链接。http://ns.adobe.com/adobecloud/rel/rendition[].height* | 数字 | 节目高度。 |

有关资产的完整列表和详细示例，请访问 [资源选择器代码示例](https://github.com/adobe/aem-assets-selectors-mfe-examples).

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

### 非SUSI流的示例 {#non-susi-vanilla}

此示例演示了如何在运行时为非SUSI流使用资产选择器 [!DNL Adobe] Unified Shell下的应用程序，或者当您已经拥有 `imsToken` 为身份验证生成。

使用在您的代码中包含资产选择器软件包 `script` 标记，如中所示 _6到15行_ 下面示例中的。 加载脚本后， `PureJSSelectors` 全局变量可供使用。 定义资源选择器 [属性](#asset-selector-properties) 如所示 _第16行至第23行_. 此 `imsOrg` 和 `imsToken` 在非SUSI流中进行身份验证时，属性都是必需的。 此 `handleSelection` 属性用于处理选定的资产。 要呈现资产选择器，请调用 `renderAssetSelector` 中提到的函数 _17号线_. 资源选择器显示在 `<div>` 容器元素，如所示 _第21行和第22行_.

按照以下步骤操作，您可以在中使用具有非SUSI流的资产选择器 [!DNL Adobe] 应用程序。

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

有关详细的示例，请访问 [资源选择器代码示例](https://github.com/adobe/aem-assets-selectors-mfe-examples).

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

您可以使用资源选择器属性自定义资源选择器的呈现方式。 下表列出了可用于自定义和使用Asset Selector的属性。

| 属性 | 类型 | 必填 | 默认 | 描述 |
|---|---|---|---|---|
| *边栏* | 布尔型 | 否 | false | 如果已标记 `true`，资产选择器将在左边栏视图中渲染。 如果已标记 `false`，资产选择器将在模式视图中呈现。 |
| *imsOrg* | 字符串 | 是 |  | Adobe在配置时分配的Identity Management System (IMS) ID [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 您的组织。 此 `imsOrg` 需要密钥来验证您访问的组织是否处于Adobe IMS下。 |
| *imsToken* | 字符串 | 否 |  | 用于身份验证的IMS持有者令牌。 `imsToken` 如果您使用的是非SUSI流，则为必填项。 |
| *apiKey* | 字符串 | 否 |  | 用于访问AEM Discovery服务的API密钥。 `apiKey` 如果您使用的是非SUSI流，则为必需。 |
| *根路径* | 字符串 | 否 | /content/dam/ | 资源选择器显示资源的文件夹路径。 `rootPath` 也可以以封装的形式使用。 例如，给定以下路径， `/content/dam/marketing/subfolder/`，资产选择器不允许您遍历任何父文件夹，但仅显示子文件夹。 |
| *路径* | 字符串 | 否 |  | 呈现资产选择器时用于导航到资产的特定目录的路径。 |
| *filterschema* | 数组 | 否 |  | 用于配置过滤器属性的模型。 当您想要限制资源选择器中的某些过滤器选项时，这将很有用。 |
| *filterFormProps* | 对象 | 否 |  | 指定优化搜索所需的过滤器属性。 例如，MIME类型JPG、PNG、GIF。 |
| *selectedassets* | 数组 `<Object>` | 否 |  | 在呈现资源选择器时指定选定的资源。 需要包含资产的id属性的对象数组。 例如， `[{id: 'urn:234}, {id: 'urn:555'}]` 资源必须位于当前目录中。 如果需要使用其他目录，请为 `path` 产权。 |
| *acvConfig* | 对象 | 否 |  | 包含要覆盖默认值的自定义配置的对象的资产收藏集视图属性。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |  | 如果OOTB翻译无法满足应用程序的需求，则可以公开一个界面，通过该界面可以通过传递您自己的自定义本地化值 `i18nSymbols` prop. 通过此界面传递值将覆盖提供的默认转换，并转而使用您自己的转换。  要执行覆盖，您必须传递一个有效的 [消息描述符](https://formatjs.io/docs/react-intl/api/#message-descriptor) 对象，指向的键 `i18nSymbols` 要覆盖的内容。 |
| *intl* | 对象 | 否 |  | 资产选择器提供默认的OOTB翻译。 您可以通过以下方式提供有效的区域设置字符串来选择翻译语言 `intl.locale` prop. 例如： `intl={{ locale: "es-es" }}` </br></br> 支持的区域设置字符串遵循 [ISO 639 — 代码](https://www.iso.org/iso-639-language-codes.html) 用于表示语言标准的名称。 </br></br> 支持的区域设置列表：英语 — &#39;en-us&#39;（默认）西班牙语 — &#39;es-es&#39;德语 — &#39;de-de&#39;法语 — &#39;fr-fr&#39;意大利语 — &#39;it-it&#39;日语 — &#39;ja-jp&#39;韩语 — &#39;ko-kr&#39;葡萄牙语 — &#39;pt-br&#39;中文（繁体） — &#39;zh-cn&#39;中文（台湾） — &#39;zh-tw&#39; |
| *repositoryId* | 字符串 | 否 | ” | 资源选择器从中加载内容的存储库。 |
| *其他AemSolutions* | `Array<string>` | 否 | [ ] | 它允许您添加其他AEM存储库的列表。 如果此资产中未提供任何信息，则只会考虑Media Library或AEM Assets存储库。 |
| *hideTreeNav* | 布尔型 | 否 |  | 指定是显示还是隐藏资源树导航侧栏。 它仅用于模态视图，因此此属性在边栏视图中没有任何影响。 |
| *onDrop* | 函数 | 否 |  | 属性允许使用资源的拖放功能。 |
| *dropOptions* | `{allowList?: Object}` | 否 |  | 使用“允许列表”配置放置选项。 |
| *颜色方案* | 字符串 | 否 |  | 配置主题(`light` 或 `dark`)作为资产选择器。 |
| *handleSelection* | 函数 | 否 |  | 在选择了资产且 `Select` 已单击模式上的按钮。 此函数仅在模态视图中调用。 对于边栏视图，请使用 `handleAssetSelection` 或 `onDrop` 函数。 示例: <pre>handleSelection=(assets：资源[])=> {...}</pre> 参见 [选定的资源类型](#selected-asset-type) 了解详细信息。 |
| *handleAssetSelection* | 函数 | 否 |  | 在选中或取消选中资产时，使用项目数组调用。 当您想要在用户选择资产时侦听资产时，这将很有用。 示例: <pre>handleSelection=(assets：资源[])=> {...}</pre> 参见 [选定的资源类型](#selected-asset-type) 了解详细信息。 |
| *onClose* | 函数 | 否 |  | 调用时间 `Close` 已按下模态视图中的按钮。 此调用仅在 `modal` 在中查看和忽略 `rail` 视图。 |
| *onFilterSubmit* | 函数 | 否 |  | 在用户更改不同的筛选条件时，通过筛选项目调用。 |
| *selectionType* | 字符串 | 否 | 单人 | 的配置 `single` 或 `multiple` 一次选择资源。 |

## 使用资源选择器属性的示例 {#usage-examples}

您可以定义资源选择器 [属性](#asset-selector-properties) 在 `index.html` 文件，以自定义应用程序中的资产选择器显示。

### 示例1：边栏视图中的资产选择器

![边栏视图示例](assets/rail-view-example-vanilla.png)

如果AssetSelector的值 `rail` 设置为 `false` 或者属性中未提及，默认情况下资产选择器会显示在模式视图中。

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### 示例2：元数据弹出框

使用各种属性定义要使用信息图标查看的资源的元数据。 信息弹出窗口提供有关资源或文件夹的信息集合，包括资源的标题、维度、修改日期、位置和描述。 在以下示例中，使用各种属性来显示资源的元数据，例如， `repo:path` 属性指定资源的位置。 <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-pover-example](assets/metadata-popover.png)


### 示例3：边栏视图中的自定义过滤器属性

除了面向搜索外，Assets Selector还允许您自定义各种属性以从以下来源优化搜索 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 应用程序。 您需要添加以下代码以在应用程序中添加自定义搜索过滤器。 在以下示例中， `Type Filter` 可在图像、文档或视频之间筛选资源类型，或筛选您为搜索添加的筛选器类型的搜索。

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

## 使用对象架构处理资源的选择 {#handling-selection}

此 `handleSelection` 属性用于处理Assets选择器中的单个或多个资产选择。 以下示例说明使用的语法 `handleSelection`.

![句柄选择](assets/handling-selection.png)

## 使用资源选择器 {#using-asset-selector}

设置资产选择器并验证您同意将资产选择器用于 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 应用程序时，您可以选择资源或执行各种其他操作来搜索存储库中的资源。

![using-asset-selector](assets/using-asset-selector.png)

* **A**： [隐藏/显示面板](#hide-show-panel)
* **B**： [存储库切换器](#repository-switcher)
* **C**： [资产](#repository)
* **D**： [筛选器](#filters)
* **E**： [搜索栏](#search-bar)
* **F**： [排序](#sorting)
* **G**： [按升序或降序排序](#sorting)
* **H**： [视图](#types-of-view)

### 隐藏/显示面板 {#hide-show-panel}

要在左侧导航中隐藏文件夹，请单击 **[!UICONTROL 隐藏文件夹]** 图标。 要撤消更改，请单击 **[!UICONTROL 隐藏文件夹]** 图标。

### 存储库切换器 {#repository-switcher}

资产选择器还允许您切换存储库以进行资产选择。 您可以从左侧面板中提供的下拉列表中选择所选存储库。 下拉列表中可用的存储库选项基于 `repositoryId` 在中定义的属性 `index.html` 文件。 它基于登录用户访问的选定IMS组织的环境。 消费者可以传递首选 `repositoryID` 在这种情况下，资产选择器停止渲染存储库切换器，并仅渲染给定存储库中的资产。
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### 资产存储库

它是可用于执行操作的资源文件夹的集合。

### 现成过滤器 {#filters}

资产选择器还提供现成的过滤器选项来优化搜索结果。 以下筛选器可用：

* `File type`：包括文件夹、文件、图像、文档或视频
* `MIME type`：包括JPG、GIF、PPTX、PNG、MP4、DOCX、TIFF、PDF、XLSX
* `Image Size`：包括图像的最小值/最大宽度、最小值/最大高度

![边栏视图示例](assets/filters-asset-selector.png)

### 自定义搜索

除了全文搜索之外，资产选择器还允许您使用自定义搜索来搜索文件内的资产。 您可以在模态视图和边栏视图模式下使用自定义搜索过滤器。

![custom-search](assets/custom-search.png)

您还可以创建默认搜索过滤器，以保存您经常搜索的字段并在以后使用。 要为资源创建自定义搜索，您可以使用 `filterSchema` 属性。

### 搜索栏 {#search-bar}

利用资源选择器，可对所选存储库中的资源执行全文搜索。 例如，如果键入关键字 `wave` 在搜索栏中，所有包含 `wave` 将显示在任意元数据属性中提到的关键字。

### 排序 {#sorting}

您可以在资源选择器中按名称、维度或资源大小对资源进行排序。 您还可以按升序或降序对资源排序。

### 视图类型 {#types-of-view}

资产选择器允许您以四种不同的视图查看资产：

* **![列表视图](assets/do-not-localize/list-view.png) [!UICONTROL 列表视图]**：列表视图在一列中显示了可滚动的文件和文件夹。
* **![网格视图](assets/do-not-localize/grid-view.png) [!UICONTROL 网格视图]**：网格视图在行和列的网格中显示可滚动的文件和文件夹。
* **![图库视图](assets/do-not-localize/gallery-view.png) [!UICONTROL 图库视图]**：图库视图以中心锁定水平列表显示文件或文件夹。
* **![瀑布视图](assets/do-not-localize/waterfall-view.png) [!UICONTROL 瀑布视图]**：瀑布视图以网桥的形式显示文件或文件夹。

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