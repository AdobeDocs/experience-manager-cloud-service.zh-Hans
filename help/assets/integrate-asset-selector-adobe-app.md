---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 将资源选择器与各种Adobe、非Adobe和第三方应用程序集成。
role: Admin, User
exl-id: a0c030e2-2213-406b-ad92-4761f1e2ee9f
source-git-commit: 575980320c1dbd32f799bf9c2fddf3d6773c838a
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 8%

---

# 将资源选择器与Adobe应用程序集成 {#integrate-asset-selector-with-adobe-app}

Asset Selector允许您使用各种Adobe应用程序进行集成，以使它们能够无缝地协同工作。

## 先决条件{#prereqs-adobe-app}

如果要将资产选择器与[!DNL Adobe]应用程序集成，请使用以下先决条件：

* [通信方法](/help/assets/overview-asset-selector.md#prereqs)
* imsOrg
* imsToken
* apikey

## 将资产选择器与[!DNL Adobe]应用程序集成 {#adobe-app-integration-vanilla}

以下示例演示了在Unified Shell下运行[!DNL Adobe]应用程序或已经为身份验证生成`imsToken`时，资产选择器的用法。

使用`script`标记将资产选择器包包含在您的代码中，如以下示例的&#x200B;_行6-15_&#x200B;所示。 加载该脚本后，`PureJSSelectors` 全局变量将可供使用。定义资产选择器[属性](/help/assets/asset-selector-properties.md)，如&#x200B;_行16-23_&#x200B;中所示。 在Adobe应用程序中身份验证需要`imsOrg`和`imsToken`属性。 `handleSelection` 属性用于处理选定资源。要呈现资源选择器，请调用 `renderAssetSelector` 函数，如&#x200B;_第 17 行_&#x200B;中所述。资源选择器将显示在 `<div>` 容器元素中，如&#x200B;_第 21 行和第 22 行_&#x200B;中所示。

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

### ImsAuthProps {#ims-auth-props}

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

### ImsAuthService {#ims-auth-service}

`ImsAuthService`类用于处理资产选择器的身份验证流程。 它负责从Adobe IMS身份验证服务获取`imsToken`。 `imsToken`用于对用户进行身份验证并授权作为[!DNL Cloud Service] Assets存储库访问[!DNL Adobe Experience Manager]。 ImsAuthService使用`ImsAuthProps`属性来控制身份验证流并注册各种身份验证事件的侦听器。 您可以使用方便的[`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice)函数向资产选择器注册&#x200B;_ImsAuthService_&#x200B;实例。 `ImsAuthService`类中有以下函数可用。 但是，如果您使用&#x200B;_registerAssetsSelectorsAuthService_&#x200B;函数，则无需直接调用这些函数。

| 函数名称 | 描述 |
|---|---|
| `isSignedInUser` | 确定用户当前是否已登录到服务并相应地返回布尔值。 |
| `getImsToken` | 检索当前登录用户的身份验证`imsToken`，该身份验证可用于验证其他服务（如生成资产_rendition）的请求。 |
| `signIn` | 启动用户的登录流程。 此函数使用`ImsAuthProps`在弹出窗口或全页重新加载中显示身份验证 |
| `signOut` | 将用户签出服务，使其身份验证令牌失效，并要求他们再次登录以访问受保护的资源。 调用此函数将重新加载当前页面。 |
| `refreshToken` | 刷新当前登录用户的身份验证令牌，防止该令牌过期，并确保对受保护资源的访问不会中断。 返回可用于后续请求的新身份验证令牌。 |

### 使用提供的IMS令牌进行验证 {#validation-ims-token}

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

### 将回调注册到IMS服务 {#register-callback-ims-service}

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

>[!MORELIKETHIS]
>
>* [将资产选择器与各种应用程序集成](/help/assets/integrate-asset-selector.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
>* [将资源选择器与Dynamic Media与OpenAPI功能集成](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [资产选择器自定义项](/help/assets/asset-selector-customization.md)
