---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 将资源选择器与各种Adobe、非Adobe和第三方应用程序集成。
role: Admin, User
exl-id: 55848de0-aff2-42a0-b959-c771235d9425
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 6%

---

# 与非Adobe应用程序集成 {#integrate-asset-selector-non-adobe-app}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Asset Selector允许您使用各种非Adobe应用程序或第三方应用程序进行集成，以使它们能够无缝地协同工作。

## 先决条件 {#prereqs-non-adobe-app}

如果要将Asset Selector与非Adobe应用程序集成，请使用以下先决条件：

* [通信方法](/help/assets/overview-asset-selector.md#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

当您将[!DNL Experience Manager Assets]存储库与非Adobe应用程序集成时，Asset Selector支持使用Identity Management System (IMS)属性（如`imsScope`或`imsClientID`）对其进行身份验证。

## 为非Adobe应用程序配置资源选择器 {#configure-non-adobe-app}

要为非Adobe应用程序配置资产选择器，必须首先记录用于预配的支持票证，然后执行集成步骤。

### 记录支持票证 {#log-a-support-ticket}

通过 Admin Console 记录支持工单的步骤：

1. 在票证标题中添加带有AEM Assets **的**&#x200B;资源选择器。

1. 请在描述中提供以下详细信息：

   * [!DNL Experience Manager Assets]作为[!DNL Cloud Service] URL（项目ID和环境ID）。
   * 托管非AdobeWeb应用程序的域名。

## 集成步骤 {#non-adobe-app-integration-steps}

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
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>
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

## 无法访问投放存储库 {#unable-to-access-delivery-repository}

>[!TIP]
>
>如果您已使用注册登录工作流集成资产选择器，但仍无法访问投放存储库，请确保清理了浏览器Cookie。 否则，您最终会在控制台中收到`invalid_credentials All session cookies are empty`错误。

>[!MORELIKETHIS]
>
>* [将资产选择器与各种应用程序集成](/help/assets/integrate-asset-selector.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
>* [将资源选择器与Dynamic Media与OpenAPI功能集成](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [资产选择器自定义项](/help/assets/asset-selector-customization.md)
