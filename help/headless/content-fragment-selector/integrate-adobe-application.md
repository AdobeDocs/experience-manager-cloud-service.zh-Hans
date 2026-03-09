---
title: 将内容片段选择器与Adobe应用程序集成
description: 将内容片段选择器与各种Adobe应用程序集成。
role: Admin, User, Developer
source-git-commit: a16d9e9fa6483a89283c595372abcc437d1d962e
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# 将内容片段选择器与Adobe应用程序集成 {#integrate-content-fragment-selector-with-adobe-application}

内容片段选择器允许您与各种Adobe应用程序集成，以使它们能够无缝地协同工作。

## 先决条件 {#prerequisites}

如果要将内容片段选择器与Adobe应用程序集成，请使用以下先决条件：

* [先决条件](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsOrg
* imsToken
* apikey

## 将内容片段选择器与Adobe应用程序集成 {#integrate-content-fragment-selector-with-an-adobe-application}

以下示例演示了以下情况：在Unified Shell下运行Adobe应用程序时，或者您已经为身份验证生成了`imsToken`时，对内容片段选择器的使用。

使用`script`标记在代码中包含内容片段选择器包，如下例所示。

* 加载脚本后，`PureJSContentFragmentSelectors`全局变量即可使用。
* 定义内容片段选择器[属性](/help/headless/content-fragment-selector/properties.md)：

   * 在Adobe应用程序中身份验证需要`imsOrg`和`imsToken`属性
   * `handleSelection`属性用于处理选定的片段。

* 要呈现内容片段选择器，请调用`renderFragmentSelector`函数。
* 内容片段选择器显示在`<div>`容器元素中。

按照这些步骤，您可以在Adobe应用程序中使用内容片段选择器。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Fragment Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-fragmentss-selectors/static-fragments/resources/fragments-selectors.js"></script>
    <script>
        // get the container element in which we want to render the FragmentSelector component
        const container = document.getElementById('fragment-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const fragmentSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (fragmentss: SelectedFragmentType[]) => {},
        };
        // Call the `renderFragmentSelector` available in PureJSContentFragmentSelectors globals to render FragmenttSelector
        PureJSContentFragmentSelectors.renderFragmentSelector(container, fragmentSelectorProps);
    </script>
</head>

<body>
    <div id="fragment-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

### ImsAuthProps {#imsauthprops}

`ImsAuthProps`属性定义内容片段选择器用于获取`imsToken`的身份验证信息和流程。 通过设置这些属性，您可以控制身份验证流程的行为方式，并为各种身份验证事件注册侦听器。

有关属性详细信息，请参阅[ImsAuthProps属性](/help/headless/content-fragment-selector/properties.md#imsauthprops-properties)

### ImsAuthService {#imsauthservice}

`ImsAuthService`类用于处理片段选择器的身份验证流。 它负责从Adobe IMS身份验证服务获取`imsToken`。 `imsToken`用于验证用户并授权对AEM as a Cloud Service存储库的访问。 `ImsAuthService`使用`ImsAuthProps`属性来控制身份验证流程并注册各种身份验证事件的侦听器。 您可以使用`registerFragmentsSelectorsAuthService`函数向片段选择器注册`ImsAuthService`实例。 `ImsAuthService`类中有以下函数可用。 但是，如果您使用`registerFragmentsSelectorsAuthService`函数，则无需直接调用这些函数。

有关属性详细信息，请参阅[ImsAuthService属性](/help/headless/content-fragment-selector/properties.md#imsauthservice-properties)

### 使用提供的IMS令牌进行验证 {#validation-with-provided-ims-token}

```javascript
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected fragment: ", selection);
    };
    function renderFragmentSelectorInline() {
    console.log("initializing Fragment Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('fragment-selector-container');
    PureJSContentFragmentSelectors.renderFragmentSelector(container, props);
    }
    $(document).ready(function() {
    renderFragmentSelectorInline();
    });
</script>
```

### 将回调注册到IMS服务 {#register-callbacks-to-ims-service}

```java
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
