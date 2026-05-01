---
title: 内容审查程序属性
description: 使用属性可以自定义在将内容审查程序与应用程序集成时内容审查程序的呈现方式。
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="适用于AEM Assets)。"
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: c92611e4b815e49887e175943b81177e60623067
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 24%

---

# 内容审查程序安装和属性 {#content-advisor-installation-properties}

Content Advisor还可用于与非Adobe（第三方）应用程序集成，从而将智能资产发现扩展到Adobe应用程序之外。 第三方集成支持相同的丰富功能集，包括AI支持的搜索、上下文感知推荐、基于活动简短的发现、访问Dynamic Media演绎版、内容片段发现、过滤器和资产元数据。

## 先决条件{#prereqs}

您必须确保采用以下通信方式：

* 主机应用程序在 HTTPS 上运行。
* 您无法在 `localhost` 上运行此应用程序。 如果要在本地计算机上集成内容审查程序，则需要创建一个自定义域，例如`[https://<your_campany>.localhost.com:<port_number>]`，并在`redirectUrl list`中添加此自定义域。
* 您可以使用相应的 `imsClientId` 配置 clientID 并将其添加到 AEM Cloud Service 环境变量中。
<!--
* You can configure and add `ADOBE_PROVIDED_CLIENT_ID` into the AEM Cloud Service environment variable with the respective `imsClientId`.
![Asset Selector IMS Client id environment](assets/asset-selector-ims-client-id-env.png)
-->
* 需要在环境配置中定义 IMS 范围列表。
* 该应用程序的 URL 位于 IMS 客户端的重定向 URL 允许列表中。
* 使用 Web 浏览器上的弹出窗口配置和呈现 IMS 登录流。 因此，应在目标浏览器上启用或允许弹出窗口。

如果需要Content Advisor的IMS身份验证工作流，请使用上述先决条件。 或者，如果您已经通过 IMS 工作流程进行身份验证，那么您可以添加 IMS 信息。

>[!IMPORTANT]
>
> 此存储库旨在作为补充文档，描述用于集成Content Advisor的可用API和使用示例。 在尝试安装或使用内容审查程序之前，请确保贵组织已获得内容审查程序的访问权限，作为Experience Manager Assets as a Cloud Service配置文件的一部分。 如果您尚未进行配置，则无法集成或使用这些组件。 要请求配置，您的程序管理员应该从 Admin Console 提交一个标记为 P2 的支持工单，并包含以下信息：
>
>* 托管集成应用程序的域名。
>* 配置之后，将为您的组织提供`imsClientId`、`imsScope`以及对应于所请求环境的`redirectUrl`，这些环境对于配置内容审查程序至关重要。 没有这些有效属性，您无法运行安装步骤。

## 安装 {#content-advisor-installation}

内容顾问可通过ESM CDN（例如，[esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)）和[UMD](https://github.com/umdjs/umd)版本使用。

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

## 内容审查程序属性 {#content-advisor-propertiess}

您可以使用内容审查程序属性来自定义内容审查程序的呈现方式。 下表列出了可用于定制和使用“内容指导”的属性。

| 属性 | 类型 | 必需 | 默认 | 描述 |
|---|---|---|---|---|
| *边栏* | 布尔值 | 否 | 假 | 如果标记为`true`，内容顾问将在左边栏视图中呈现。 如果将其标记为`false`，则内容顾问将在模式视图中呈现。 |
| *imsOrg* | 字符串 | 是 | | 为组织设置 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 时分配的 Adobe Identity Management System (IMS) ID。 需要使用`imsOrg`密钥来验证您访问的组织是否位于Adobe IMS下。 |
| *imsToken* | 字符串 | 否 | | 用于身份验证的 IMS 持有者令牌。 如果您使用[!DNL Adobe]应用程序进行集成，则需要`imsToken`。 |
| *apiKey* | 字符串 | 否 | | 用于访问 AEM 发现服务的 API 密钥。 如果您使用[!DNL Adobe]应用程序集成，则需要`apiKey`。 |
| *externalBrief* | 字符串 | 否 | | 允许您上传营销活动简介文档以发现相关资源，而无需手动输入搜索关键词。 内容审查程序会分析营销活动简介中的信息以了解营销活动的意图，并推荐AEM Assets中可用的相关资源。 |
| *filterSchema* | 数组 | 否 | | 用于配置过滤器属性的模型。 当您想要限制内容审查程序中的某些过滤器选项时，这将很有用。 |
| *filterFormProps* | 对象 | 否 | | 指定您需要用于细化搜索的过滤器属性。 为了！ 例如，MIME类型JPG、PNG、GIF。 |
| *selectedAssets* | 数组 `<Object>` | 否 |                 | 在呈现内容审查程序时指定选定的Assets。 包含资源的 id 属性的必需对象数组。 例如，`[{id: 'urn:234}, {id: 'urn:555'}]` 资源必须在当前目录中可用。 如果您需要使用其他目录，请也为 `path` 属性提供一个值。 |
| *acvConfig* | 对象 | 否 | | 资产收藏集视图属性，该属性包含用于覆盖默认值的自定义配置的对象。 此外，此属性与`rail`属性一起使用，以启用资产查看器的边栏视图。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | 否 |                 | 如果OOTB翻译无法满足应用程序的需求，则可以公开一个界面，通过该界面可通过`i18nSymbols` prop传递您自己的自定义本地化值。 通过此接口传递值将覆盖提供的默认翻译，而改用您自己的翻译。 要执行覆盖，您必须将一个有效的[消息描述符](https://formatjs.io/docs/react-intl/api/#message-descriptor)对象传递到要覆盖的 `i18nSymbols` 键。 |
| *intl* | 对象 | 否 | | 内容审查程序提供默认的OOTB翻译。 您可以通过用 `intl.locale` 属性提供有效的区域设置字符串来选择翻译语言。 例如： `intl={{ locale: "es-es" }}` </br></br>支持的语言环境字符串遵循[ISO 639 — 代码](https://www.iso.org/iso-639-language-codes.html)以表示语言标准的名称。</br></br> 支持的区域设置列表：英语 — &#39;en-us&#39;（默认）西班牙语 — &#39;es-es&#39;德语 — &#39;de-de&#39;法语 — &#39;fr-fr&#39;意大利语 — &#39;it-it&#39;日语 — &#39;ja-jp&#39;韩语 — &#39;ko-kr&#39;葡萄牙语 — &#39;pt-br&#39;中文（繁体） — &#39;zh-cn&#39;中文（台湾） — &#39;zh-tw&#39; |
| *repositoryId* | 字符串 | 否 | &#39;&#39; | 内容审查程序从中加载内容的存储库。 |
| *additionalAemSolutions* | `Array<string>` | 否 | [ ] | 它允许您添加其他AEM存储库的列表。 如果此属性中未提供任何信息，则仅考虑媒体库或 AEM Assets 存储库。 |
| *hideTreeNav* | 布尔值 | 否 |  | 指定是显示还是隐藏资源树导航侧边栏。 它仅在模态视图中使用，因此，该属性在边栏视图中不起作用。 |
| *onDrop* | 函数 | 否 | | 拖放功能用于将资产拖放至指定的拖放区域。 它支持交互式用户界面，可在其中无缝地移动和处理资产。 |
| *dropOptions* | `{allowList?: Object}` | 否 | | 使用“allowList”配置删除选项。 |
| *主题* | 字符串 | 否 | 默认 | 将主题应用到`default`到`express`之间的内容顾问应用程序。 它还支持`@react-spectrum/theme-express`。 |
| *handleSelection* | 函数 | 否 | | 在资源已选定并单击模态上的 `Select` 按钮时调用资源项数组。 仅在模态视图中调用此函数。 对于边栏视图，请使用 `handleAssetSelection` 或 `onDrop` 函数。 示例： <pre>handleSelection=（资源：资源[]）=> {...}</pre> 有关详细信息，请参阅[选择的资源](/help/assets/content-advisor-customization.md#selection-of-assets)。 |
| *handleAssetSelection* | 函数 | 否 | | 在选择或取消选择资源时调用项目数组。 如果您需要在用户选择资源时进行侦听，这会很有用。 示例： <pre>handleAssetSelection=(assets： Asset[])=> {...}</pre> 有关详细信息，请参阅[选择的资源](/help/assets/content-advisor-customization.md#selection-of-assets)。 |
| *onClose* | 函数 | 否 | | 在按下模态视图中的 `Close` 按钮时调用。 这仅在 `modal` 视图中被调用，在 `rail` 视图中将被忽略。 |
| *onFilterSubmit* | 函数 | 否 | | 当用户更改其他过滤器条件时调用过滤器项。 |
| *selectionType* | 字符串 | 否 | 单身 | 一次性为 `single` 或 `multiple` 资源选择配置。 |
| *dragOptions.允许列表* | 布尔型 | 否 | | 属性用于允许或拒绝拖动不可选资产。 查看[dragOptions属性](/help/assets/content-advisor-customization.md#drag-options-property) |
| *aemTierType* | 字符串 | 否 |  | 它允许您选择是显示交付层、创作层中的资产，还是同时显示两者。<br><br> 语法： `aemTierType: "author"  "delivery"` <br><br>例如，如果同时使用了`["author","delivery"]`，则存储库切换器将显示创作和投放选项。 |
| *handleNavigateToAsset* | 函数 | 否 | | 它是一个回调函数，用于处理资源的选择。 |
| *noWrap* | 布尔值 | 否 | | *noWrap*&#x200B;属性阻止内容顾问包装在对话框中。 如果未提及此属性，则默认情况下会呈现&#x200B;*对话框视图*。 |
| *dialogSize* | S， M， L，全屏，全屏接管 | 字符串 | 可选 | 通过使用给定选项指定布局大小可控制布局。 |
| *colorScheme* | 字符串（浅色、深色） | 否 | | 此属性用于设置内容审查程序应用程序的主题。 您可以选择浅色或深色主题。 |
| *filterRepoList* | 函数 | 否 | | 接收存储库列表并返回筛选列表的函数。 |
| *expiryOptions* | 函数 | | | 您可以在以下两个属性之间使用：**getExpiryStatus**，它提供已过期资源的状态。 函数根据您提供的资源的到期日期返回`EXPIRED`、`EXPIRING_SOON`或`NOT_EXPIRED`。 请参阅[自定义过期的资源](/help/assets/content-advisor-customization.md#customize-expired-assets)。 此外，您可以使用&#x200B;**allowSelectionAndDrag**，其中函数的值可以是`true`或`false`。 如果该值设置为`false`，则无法在画布上选择或拖动过期的资产。 |
| *showToast* | | 否 | | 它允许内容审查器为已过期的资源显示自定义的toast消息。 |
| *上载配置* | 对象 | | | 它是一个对象，其中包含用于上载的自定义配置。 请参阅[上传配置](#content-advisor-customization.md#upload-config)以了解可用性。 |
| *uploadConfig* > *metadataSchema* | 数组 | 否 | | 此属性嵌套在`uploadConfig`属性下。 添加您为从用户那里收集元数据而提供的字段数组。 使用此属性，您还可以使用自动分配给资源但用户不可见的隐藏元数据。 |
| *uploadConfig* > *onMetadataFormChange* | 回调函数 | 否 | | 此属性嵌套在`uploadConfig`属性下。 它包含`property`和`value`。 `Property`等于从&#x200B;*metadataSchema*&#x200B;传递的字段&#x200B;*mapToProperty*，该字段的值正在更新。 而，`value`等于提供的新值作为输入。 |
| *uploadConfig* > *targetUploadPath* | 字符串 |  | `"/content/dam"` | 此属性嵌套在`uploadConfig`属性下。 默认为资源存储库根目录的文件目标上传路径。 |
| *uploadConfig* > *隐藏上载按钮* | 布尔值 | | 假 | 它确保内部上传按钮是否隐藏。 此属性嵌套在`uploadConfig`属性下。 |
| *uploadConfig* > *onUploadStart* | 函数 | 否 |  | 它是一个回调函数，用于在Dropbox、OneDrive或本地之间传递上传源。 语法为`(uploadInfo: UploadInfo) => void`。 此属性嵌套在`uploadConfig`属性下。 |
| *uploadConfig* > *导入设置* | 函数 | | | 它支持从第三方来源导入资产。 `sourceTypes`使用要启用的导入源数组。 支持的源为Onedrive和Dropbox。 语法为`{ sourceTypes?: ImportSourceType[]; apiKey?: string; }`。 此外，此属性嵌套在`uploadConfig`属性下。 |
| *uploadConfig* > *onUploadComplete* | 函数 | 否 | | 它是一个回调函数，用于在成功、失败或复制之间传递文件上传状态。 语法为`(uploadStats: UploadStats) => void`。 此外，此属性嵌套在`uploadConfig`属性下。 |
| *uploadConfig* > *onFilesChange* | 函数 | 否 | | 此属性嵌套在`uploadConfig`属性下。 它是一个回调函数，用于在文件更改时显示上载行为。 它会传递挂起的待上传文件的新数组以及上传的源类型。 如果发生错误，Source类型可以为null。 语法为`(newFiles: File[], uploadType: UploadType) => void` |
| *uploadConfig* > *uploadingPlaceholder* | 字符串 | | | 它是一个占位符图像，在启动资源上传时替换元数据表单。 语法为`{ href: string; alt: string; }`，此外，此属性嵌套在`uploadConfig`属性下。 |
| *功能集* | 数组 | 字符串 | | `featureSet:[ ]`属性用于启用或禁用内容审查程序应用程序中的特定功能。 要启用组件或功能，您可以在数组中传递字符串值，或者将数组留空以禁用添加的功能，而只具有基本功能。 例如，要在内容审查器中启用上载功能，请使用语法`featureSet:["upload"]`。 同样，您可以使用`featureSet:["content-fragments"]`在内容顾问中启用内容片段。 要同时使用多个功能，语法为featureSet：[&quot;upload&quot;、&quot;content-fragments&quot;]。 |

<!--
| *selectedRendition* | Object | | | This property allows users to define and control which renditions of an asset are displayed when the panel is accessed. This customization enhances user experience by filtering out unnecessary renditions and showcasing only the most relevant renditions. For example, `CopyUrlHref` allows you to use Dynamic Media renditions in your Asset Selector application (delivery URL). |
| *featureSet* | Array | String | | The `featureSet:[ ]` property is used to enable or disable a particular functionaly in the Asset Selector application. To enable the component or a feature, you can pass a string value in the array or leave the array empty to disable that component. For example, you want to enable upload functionality in the Asset Selector, use the syntax `featureSet:[0:"upload"]`. Similarly, you can use `featureSet:[0:"collections"]` to enable collections in the Asset Selector. Addidionally, use `featureSet:[0:"detail-panel"]` to enable [details panel](overview-asset-selector.md#asset-details-and-metadata) of an asset. Also, `featureSet:[0:"dm-renditions"]` to show Dynamic Media renditions of an asset.|
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->

### ImsAuthProps {#ims-auth-props}

`ImsAuthProps`属性定义内容顾问用于获取`imsToken`的身份验证信息和流程。 通过设置这些属性，您可以控制身份验证流程的行为方式，并为各种身份验证事件注册侦听器。

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

### ImsAuthService {#ims-auth-service}

`ImsAuthService`类用于处理内容顾问的身份验证流程。 它负责从Adobe IMS身份验证服务获取`imsToken`。 `imsToken`用于对用户进行身份验证并授权作为[!DNL Cloud Service] Assets存储库访问[!DNL Adobe Experience Manager]。 ImsAuthService使用`ImsAuthProps`属性来控制身份验证流并注册各种身份验证事件的侦听器。 您可以使用方便的[`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice)函数向内容顾问注册&#x200B;_ImsAuthService_&#x200B;实例。 `ImsAuthService`类中有以下函数可用。 但是，如果您使用&#x200B;_registerAssetsSelectorsAuthService_&#x200B;函数，则无需直接调用这些函数。

| 函数名称 | 描述 |
|---|---|
| `isSignedInUser` | 确定用户当前是否已登录到服务并相应地返回布尔值。 |
| `getImsToken` | 检索当前登录用户的身份验证`imsToken`，该身份验证可用于验证其他服务（如生成资产_rendition）的请求。 |
| `signIn` | 启动用户的登录流程。 此函数使用`ImsAuthProps`在弹出窗口或全页重新加载中显示身份验证 |
| `signOut` | 将用户签出服务，使其身份验证令牌失效，并要求他们再次登录以访问受保护的资源。 调用此函数将重新加载当前页面。 |
| `refreshToken` | 刷新当前登录用户的身份验证令牌，防止该令牌过期，并确保对受保护资源的访问不会中断。 返回可用于后续请求的新身份验证令牌。 |

### contentFragmentSelectorProps {#content-fragment-selector-properties}

`contentFragmentSelectorProps`允许您配置如何在内容审查器中访问和显示内容片段。 通过启用`featureSet`中的内容片段功能并提供所需的配置，您可以将内容片段选择与资产无缝集成。 这使用户能够在同一统一界面中浏览、搜索和选择内容片段，从而确保跨资产和结构化内容的一致内容选择体验。

```
const assetSelectorProps = {
     featureSet: [
       'upload',            /* Include upload or other featureSet values to ensure no missing functionality */
       'content-fragments', /* Content Fragments pill will be shown */
     ],
     contentFragmentSelectorProps: {
       /* Configures the Content Fragments Pill experience */
       /* ...props @aem-sites/content-fragment-selector MFE supports */
    }
}

<AssetSelector {...assetSelectorProps} />
```

在`contentFragmentSelectorProps`中，您可以提及[内容片段选择器属性](/help/headless/content-fragment-selector/properties.md)中可用的任何属性。

有关如何将Content Advisor与Angular、React和JavaScript应用程序集成的信息，请参阅[Content Advisor集成示例](https://github.com/adobe/aem-assets-selectors-mfe-examples/tree/consolidate-docs-to-experience-league/examples)。


