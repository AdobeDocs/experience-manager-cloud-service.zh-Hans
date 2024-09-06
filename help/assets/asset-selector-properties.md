---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 使用资源选择器在您的应用程序中搜索、查找和检索资源的元数据和演绎版。
role: Admin, User
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: f9f5b2a25933e059cceacf2ba69e23d528858d4b
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 42%

---

# 资源选择器属性 {#asset-selector-properties}

您可以使用资源选择器属性来自定义资源选择器的呈现方式。下表列出了可用于自定义和使用资源选择器的属性。

| 属性 | 类型 | 必需 | 默认 | 描述 |
|---|---|---|---|---|
| *边栏* | 布尔值 | 否 | 假 | 如果标记为`true`，则资产选择器将在左边栏视图中呈现。 如果资产选择器标记为`false`，则会在模式视图中呈现该资产选择器。 |
| *imsOrg* | 字符串 | 是 | | 为组织设置 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 时分配的 Adobe Identity Management System (IMS) ID。需要使用`imsOrg`密钥来验证您访问的组织是否位于Adobe IMS下。 |
| *imsToken* | 字符串 | 否 | | 用于身份验证的 IMS 持有者令牌。如果您使用[!DNL Adobe]应用程序进行集成，则需要`imsToken`。 |
| *apiKey* | 字符串 | 否 | | 用于访问 AEM 发现服务的 API 密钥。如果您使用[!DNL Adobe]应用程序集成，则需要`apiKey`。 |
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
| *主题* | 字符串 | 否 | 默认 | 将主题应用于`default`到`express`之间的资产选择器应用程序。 它还支持`@react-spectrum/theme-express`。 |
| *handleSelection* | 函数 | 否 | | 在资源已选定并单击模态上的 `Select` 按钮时调用资源项数组。仅在模态视图中调用此函数。对于边栏视图，请使用 `handleAssetSelection` 或 `onDrop` 函数。示例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 有关详细信息，请参阅[选择的资源](/help/assets/asset-selector-customization.md#selection-of-assets)。 |
| *handleAssetSelection* | 函数 | 否 | | 在选择或取消选择资源时调用项目数组。如果您需要在用户选择资源时进行侦听，这会很有用。示例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 有关详细信息，请参阅[选择的资源](/help/assets/asset-selector-customization.md#selection-of-assets)。 |
| *onClose* | 函数 | 否 | | 在按下模态视图中的 `Close` 按钮时调用。这仅在 `modal` 视图中被调用，在 `rail` 视图中将被忽略。 |
| *onFilterSubmit* | 函数 | 否 | | 当用户更改其他过滤器条件时调用过滤器项。 |
| *selectionType* | 字符串 | 否 | 单身 | 一次性为 `single` 或 `multiple` 资源选择配置。 |
| *dragOptions.允许列表* | 布尔型 | 否 | | 属性用于允许或拒绝拖动不可选资产。 |
| *aemTierType* | 字符串 | 否 |  | 它允许您选择是显示交付层、创作层中的资产，还是同时显示两者。 <br><br>语法： `aemTierType:[0]: "author" 1: "delivery"` <br><br>例如，如果同时使用了`["author","delivery"]`，则存储库切换器将显示创作和投放选项。 |
| *handleNavigateToAsset* | 函数 | 否 | | 它是一个回调函数，用于处理资源的选择。 |
| *noWrap* | 布尔值 | 否 | | *noWrap*&#x200B;属性有助于在侧边栏面板中呈现资产选择器。 如果未提及此属性，则默认情况下会呈现&#x200B;*对话框视图*。 |
| *dialogSize* | 小型、中型、大型、全屏或全屏接管 | 字符串 | 可选 | 通过使用给定选项指定布局大小可控制布局。 |
| *colorScheme* | 浅色或深色 | 否 | | 此属性用于设置Asset Selector应用程序的主题。 您可以选择浅色或深色主题。 |
| *filterRepoList* | 函数 | 否 |  | 您可以使用`filterRepoList`回调函数来调用Experience Manager存储库并返回已过滤的存储库列表。 |
| *expiryOptions* | 函数 | | | 您可以在以下两个属性之间使用：**getExpiryStatus**，它提供已过期资源的状态。 函数根据您提供的资源的到期日期返回`EXPIRED`、`EXPIRING_SOON`或`NOT_EXPIRED`。 请参阅[自定义过期的资源](/help/assets/asset-selector-customization.md#customize-expired-assets)。 此外，您可以使用&#x200B;**allowSelectionAndDrag**，其中函数的值可以是`true`或`false`。 如果该值设置为`false`，则无法在画布上选择或拖动过期的资产。 |
| *showToast* | | 否 | | 它允许资产选择器为已过期的资产显示自定义的toast消息。 |
| *metadataSchema* | 数组 | 否 | | 添加您为从用户那里收集元数据而提供的字段数组。 使用此属性，您还可以使用自动分配给资源但用户不可见的隐藏元数据。 |
| *onMetadataFormChange* | 回调函数 | 否 | | 它包含`property`和`value`。 `Property`等于从&#x200B;*metadataSchema*&#x200B;传递的字段&#x200B;*mapToProperty*，该字段的值正在更新。 而，`value`等于提供的新值作为输入。 |
| *targetUploadPath* | 字符串 |  | `"/content/dam"` | 默认为资源存储库根目录的文件目标上传路径。 |
| *hideUploadButton* | 布尔值 | | 假 | 它确保内部上传按钮是否隐藏。 |
| *onUploadStart* | 函数 | 否 |  | 它是一个回调函数，用于在Dropbox、OneDrive或本地之间传递上传源。 语法为`(uploadInfo: UploadInfo) => void` |
| *importSettings* | 函数 | | | 它支持从第三方来源导入资产。 `sourceTypes`使用要启用的导入源数组。 支持的源为Onedrive和Dropbox。 语法为`{ sourceTypes?: ImportSourceType[]; apiKey?: string; }` |
| *onUploadComplete* | 函数 | 否 | | 它是一个回调函数，用于在成功、失败或复制之间传递文件上传状态。 语法为`(uploadStats: UploadStats) => void` |
| *onFilesChange* | 函数 | 否 | | 它是一个回调函数，用于在文件更改时显示上载行为。 它会传递挂起的待上传文件的新数组以及上传的源类型。 如果发生错误，Source类型可以为null。 语法为`(newFiles: File[], uploadType: UploadType) => void` |
| *uploadingPlaceholder* | 字符串 | | | 它是一个占位符图像，在启动资源上传时替换元数据表单。 语法为`{ href: string; alt: string; } ` |
| *上载配置* | 对象 | | | 它是一个对象，其中包含用于上载的自定义配置。 |
| *功能集* | 数组 | 字符串 | | `featureSet:[ ]`属性用于启用或禁用Asset Selector应用程序中的特定功能。 要启用该组件或功能，您可以在数组中传递字符串值，或将数组留空以禁用该组件。 例如，要在资产选择器中启用上载功能，请使用语法`featureSet:[0:"upload"]`。 |

<!--
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->
