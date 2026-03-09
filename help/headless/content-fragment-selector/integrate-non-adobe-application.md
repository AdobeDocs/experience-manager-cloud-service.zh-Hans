---
title: 将内容片段选择器与非Adobe或第三方应用程序集成
description: 将内容片段选择器与各种Adobe、非Adobe和第三方应用程序集成。
role: Admin, User, Developer
source-git-commit: 3af1a89489af96bf9c9908aea7fb20883956517b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# 与非Adobe应用程序集成 {#integration-with-non-adobe-application}

内容片段选择器允许您与各种非Adobe或第三方应用程序集成，以使它们能够无缝地协同工作。

## 先决条件 {#prerequisites}

如果您要将内容片段选择器与非Adobe应用程序集成，请使用以下先决条件：

* [先决条件](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

将其与非Adobe应用程序集成时，内容片段选择器支持使用Identity Management System (IMS)属性（如`imsScope`或`imsClientID`）对Adobe Experience Manager (AEM) as a Cloud Service存储库进行身份验证。

## 为非Adobe应用程序配置内容片段选择器 {#configure-content-fragment-selector-for-a-non-adobe-application}

要为非Adobe应用程序配置内容片段选择器，您必须先记录用于预配的支持票证，然后再继续集成步骤。

### 记录支持票证 {#logging-a-support-ticket}

通过 Admin Console 记录支持工单的步骤：

1. 在票证标题中添加带有AEM片段&#x200B;**的**&#x200B;内容片段选择器。

1. 请在描述中提供以下详细信息：

   * Experience Manager as a Cloud Service URL（项目ID和环境ID）。
   * 托管非Adobe Web应用程序的域名。

## 集成步骤 {#integration-steps}

将内容片段选择器与非Adobe应用程序集成时，请使用以下示例`index.html`文件进行身份验证：

* 使用`Script`标记访问内容片段选择器包。

* 定义IMS流属性，如`imsClientId`、`imsScope`和`redirectURL`。

   * 函数要求您至少定义`imsClientId`和`imsScope`属性之一。
   * 如果您没有为`redirectURL`定义值，则使用客户端ID的注册重定向URL。

* 由于示例未生成`imsToken`，因此请使用`registerFragmentsSelectorsAuthService`和`renderFragmentSelectorWithAuthFlow`函数。

   * 使用`registerFragmentsSelectorsAuthService`之前的`renderFragmentSelectorWithAuthFlow`函数在内容片段选择器中注册`imsToken`。
   * Adobe建议在实例化该组件时调用`registerFragmentsSelectorsAuthService`。

* 在`const props`部分中定义身份验证和其他片段as a Cloud Service访问相关的属性。
* `PureJSContentFragmentSelectors`全局变量用于在Web浏览器中呈现内容片段选择器。
* 内容片段选择器将在`<div>`容器元素中呈现。 此示例使用对话框来显示内容片段选择器。

**示例`ìndex.html`**

```html {line-numbers="true"}
<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <link rel="icon" type="image/svg+xml" href="/vite.svg" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>testing-cf-mfe-integration-with-3rd-party-app</title>
        <script
            id="content-fragments-selector"
            src="https://experience.adobe.com/solutions/CQ-sites-content-fragment-selector/static-assets/resources/content-fragment-selector.js"
        ></script>
        <script>
            const imsProps = {
                imsClientId: '<IMS_CLIENT_ID>',
                imsScope:
                    'additional_info.projectedProductContext, AdobeID, openid, read_organizations',
                redirectUrl: window.location.href,
                onImsServiceInitialized: (service) => {
                    // invoked when the ims service is initialized and is ready
                    console.log('onImsServiceInitialized', service);
                },
                onAccessTokenReceived: (token) => {
                    console.log('onAccessTokenReceived', token);
                },
                onAccessTokenExpired: () => {
                    console.log('onAccessTokenError');
                    // re-trigger sign-in flow
                },
                onErrorReceived: (type, msg) => {
                    console.log('onErrorReceived', type, msg);
                },
            };

            function load() {
                const registeredTokenService =
                    PureJSContentFragmentSelectors.registerContentFragmentSelectorAuthService(
                        imsProps
                    );
                imsInstance = registeredTokenService;
            }

            // initialize the IMS flow before attempting to render the content fragment selector
            load();

            // function that will render the content fragment selector
            function renderContentFragmentSelectorWithAuthFlow() {
                const contentFragmentSelectorDialog = document.getElementById(
                    'content-fragment-selector-dialog'
                );

                const contentFragmentSelectorProps = {
                    inventoryViewToggleEnabled: true,
                    isOpen: true,
                    noWrap: false,
                    orgId: 'YOUR_ORG_ID@AdobeOrg',
                    // repoId: "author-p12345-e67890.adobeaemcloud.com", // if wanted to restrict to a specific repo
                    runningInUnifiedShell: false,
                    onDismiss: () => contentFragmentSelectorDialog.close(),
                    onSubmit: ({ contentFragments }) => {
                        const selectedContentFragment = contentFragments[0];
                        alert(selectedContentFragment.path);
                    },
                };
                // container element on which you want to render the ContentFragmentSelector component
                const container = document.getElementById('content-fragment-selector');

                /// Use the PureJSContentFragmentSelectors in globals to render the ContentFragmentSelector component
                PureJSContentFragmentSelectors.renderContentFragmentSelectorWithAuthFlow(
                    container,
                    contentFragmentSelectorProps,
                    () => contentFragmentSelectorDialog.showModal()
                );
            }
        </script>
    </head>
    <body>
        <div>
            <button onclick="renderContentFragmentSelectorWithAuthFlow()">
                Content Fragment Selector - Select Content Fragments with Ims Flow
            </button>
        </div>
        <dialog id="content-fragment-selector-dialog">
            <div
                id="content-fragment-selector"
                style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px"
            ></div>
        </dialog>
    </body>
</html>
```

## 无法访问投放存储库 {#unable-to-access-delivery-repository}

如果您已使用注册登录工作流集成内容片段选择器，但仍无法访问投放存储库，请确保已清理浏览器Cookie。

否则，您最终可能会在控制台中看到`invalid_credentials All session cookies are empty`错误。
