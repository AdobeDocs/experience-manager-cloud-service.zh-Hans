---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 使用函数可自定义应用程序中的资产选择器。
role: Admin, User
exl-id: 0fd0a9f7-8c7a-4c21-9578-7c49409df609
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 24%

---

# 资产选择器自定义 {#asset-selector-customization}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

通过资产选择器，可根据首选项、要求或功能需求自定义各种组件。 您可以自定义以下组件[微前端资产选择器](#overview-asset-selector.md)：

* [自定义筛选器面板](#customize-filter-panel)
* [自定义模式视图中的信息](#customize-info-in-modal-view)
* [启用或禁用拖放模式](#enable-disable-drag-and-drop)
* [Assets选择](#selection-of-assets)
* [自定义过期的资源](#customize-expired-assets)
* [上下文调用过滤器](#contextual-invocation-filter)

您需要在&#x200B;**index.html**&#x200B;文件或应用程序实施中的类似文件中定义先决条件，以定义访问[!DNL Experience Manager Assets]存储库的身份验证详细信息。 完成后，您可以根据需要添加代码片段。

## 自定义筛选器面板 {#customize-filter-panel}

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

## 自定义模式视图中的信息 {#customize-info-in-modal-view}

单击![信息图标](assets/info-icon.svg)图标时，您可以自定义资源的详细信息视图。 执行以下代码：

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path')
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

## 启用或禁用拖放模式 {#enable-disable-drag-and-drop}

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

## Assets选择 {#selection-of-assets}

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
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition>`* | `Array<Object>` | 对象数组，包含有关资源演绎版的信息。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].href>`* | 字符串 | 演绎版的 URI。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].type>`* | 字符串 | 演绎版的 MIME 类型。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].repo:size>`* | 数字 | 演绎版的大小，以字节为单位。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].width>`* | 数字 | 演绎版的宽度。 |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].height>`* | 数字 | 演绎版的高度。 |

### 使用对象架构处理资源选择 {#handling-selection}

`handleSelection` 属性用于处理资源选择器中的单个或多个资源选择。以下示例说明了 `handleSelection` 的使用语法。

![handle-selection](assets/handling-selection.png)

### 禁用选择Assets {#disable-selection}

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

<!--For a complete list of properties and detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

## 自定义过期的资源 {#customize-expired-assets}

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

### 选择已过期的资产 {#selection-of-expired-asset}

您可以自定义已过期资源的使用情况，使其成为可选或不可选。 您可以自定义是否允许在资产选择器画布上拖放过期的资产。 要实现此目的，请使用以下参数使资产在画布上不可选择：

```
expiryOptions:{
    allowSelectionAndDrop: false;
}
```
<!--
Additionally, To do this, navigate to **[!UICONTROL Disable default expiry behavior]** under the [!UICONTROL Controls] tab and set the boolean value to `true` or `false` as per the requirement. If `true` is selected, you can see the select box over the expired asset, otherwise it remains unselected. You can hover to the info icon of an asset to know the details of an expired asset. 

![Disable default expiry behavior](assets/disable-default-expiry-behavior.png)-->

### 设置已过期资源的持续时间 {#set-duration-of-expired-asset}

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

### 自定义已过期资产的快显消息 {#customize-toast-message}

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

```
(args) => {
    const [selectedAssets, setSelectedAssets] = useState([]);
    const [showToast, setShowToast] = React.useState(false);
    const handleAssetSelection = (assets) => {
        let directorySelectedFlag = false;
        const temp = assets.filter((asset) => {
            if (asset['repo:assetClass'] === 'directory') {
                directorySelectedFlag = true;
                setShowToast(true);
            }
            return !(asset['repo:assetClass'] === 'directory');
        });
        if (!directorySelectedFlag) {
            setShowToast(false);
        }
        setSelectedAssets(temp);
    };
    return (
        <ASDialogWrapper
            {...args}
            showToast={showToast ? args.showToast : null}
            selectedAssets={selectedAssets}
            handleAssetSelection={handleAssetSelection}
        />
    );
}
```

## 上下文调用过滤器{#contextual-invocation-filter}

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

## 在资产选择器中上传 {#upload-in-asset-selector}

您可以从本地文件系统将文件或文件夹上传到Asset Selector。 要使用本地文件系统上传文件，您通常需要使用Asset Selector微型前端应用程序提供的上传功能。 在资产选择器中调用上传所需的各种代码片段包括：

* [基本上传表单代码段](#basic-upload)
* [上载元数据](#upload-with-metadata)
* [自定义上载](#customized-upload)
* [使用第三方源上传](#upload-using-third-party-source)

### 基本上传表单 {#basic-upload}

```
import { AllInOneUpload } from '@assets/upload';
import { TextField, ContextualHelp } from '@adobe/react-spectrum';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

export const UploadExample = () => {
    return (
        <>
            <TextField
                marginStart="size-200"
                width="size-6000"
                isDisabled={true}
                label="Target Upload Path"
                value={targetUploadPath}
                contextualHelp={
                    <ContextualHelp>
                        <Content>Use Storybook Controls panel to change the default upload location</Content>
                    </ContextualHelp>
                }
            />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
            />
        <>
    )
}
```

### 上载元数据 {#upload-with-metadata}

```
import { AllInOneUpload } from '@assets/upload';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

/**
 * see https://git.corp.adobe.com/CQ/assets-upload/blob/main/packages/@assets/upload/stories/data/SampleMetadataSchemas.ts
 * for full schema shape used in rendered example below
 */
const metadataSchema = [
    {
        mapToProperty: 'gmo:lineofBusiness',
        label: 'Line of Business',
        placeholder: 'Select one',
        required: true,
        element: 'dropdown',
        dropdownOptions: [
            {
                id: 'corporate',
                name: 'Corporate',
            },
            {
                id: 'digital-media-dme',
                name: 'Digital Media (DMe)',
            },
            {
                id: 'digital-experience-dx',
                name: 'Digital Experience (DX)',
            },
            {
                id: 'business-solutions',
                name: 'Business Solutions',
            },
        ],
    },
    // ... see link above for full schema
    {
        mapToProperty: 'dam:assetStatus',
        value: 'approved',
        // hidden metadata element, this metadata will be applied to the asset without rendering UI for user input
        element: 'hidden',
    },
];

const handleMetadataFormChange = (event: MetadataChangeEvent) => {
    const { property, value } = event;

    console.log({ property, value });
}

const UploadExampleWithMetadataForm = () => {
    return (
        <AllInOneUpload
            repositoryId={repoId}
            apiToken={apiToken}
            targetUploadPath={targetUploadPath}
            metadataSchema={sampleMetadataSchema}
            onMetadataFormChange={handleMetadataFormChange}
        />
    )
}
```

### 自定义上载 {#customized-upload}

```
const MultipleAllInOneUploadExample = () => {
    const mfeRef = React.useRef<{ iframeRef: { current: HTMLIFrameElement } }>(null);

    return (
        <>
            <Button
                onPress={() => UploadCoordinator.initiateUpload(mfeRef.current?.iframeRef?.current)}
            >
                External Initiate Upload
            </Button>
            <AllInOneUpload
                {...otherProps}
                ref={mfeRef}
            />
        <>
    );
}
```

### 使用第三方源上传 {#upload-using-third-party-source}

```
import { useState, useRef } from 'react';
import { AllInOneUpload, UploadCoordinator } from '@assets/upload';
import { Button, Flex, Divider } from '@adobe/react-spectrum';
import { sampleMetadataSchema } from './SampleMetadataSchemas';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

const defaultFiles = [
    new File(['file-content'], 'Controlled File 1'),
    new File(['file-content-with-more'], 'Controlled File 2')
];

const ControlledUploadExample = () => {
    const [controlledFiles, setControlledFiles] = useState<File[]>(defaultFiles)
    const inputRef = React.useRef<HTMLInputElement>(null);

    const handleFileInputChange = useCallback((e: ChangeEvent<HTMLInputElement>) => {
        if (e.target.files) {
            setMyFiles([...e.target.files]);
        }
    }, []);

    return (
        <Flex height="100%" alignItems="center" direction="column">
            <Flex direction="row" alignItems="center" justifyContent="center">
                <Button
                    variant="accent"
                    onPress={() => UploadCoordinator.initiateUpload()}
                    isDisabled={files.length < 1}
                >
                    External Initiate Upload
                </Button>
                <Button
                    variant="secondary"
                    onPress={() => {
                        inputRef.current?.click();
                    }}
                >
                    External Browse files
                </Button>
            </Flex>
            <Divider size="M" marginTop="size-200" />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
                files={controlledFiles}
                onFilesChange={setControlledFiles}
                hideUploadButton={true}
                metadataSchema={sampleMetadataSchema}
            />
            <input
                ref={inputRef}
                type="file"
                style={{ display: 'none' }}
                onChange={handleFileInputChange}
                multiple={true}
            />
        </Flex>
    )
}
```

>[!MORELIKETHIS]
>
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
>* [将资产选择器与各种应用程序集成](/help/assets/integrate-asset-selector.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
>* [将资源选择器与Dynamic Media与OpenAPI功能集成](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
