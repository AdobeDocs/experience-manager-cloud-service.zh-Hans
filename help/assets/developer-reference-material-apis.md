---
title: 开发人员参考 [!DNL Assets]
description: '"[!DNL Assets] 通过API和开发人员参考内容，您可以管理资产，包括二进制文件、元数据、演绎版、注释和 [!DNL Content Fragments]“'
contentOwner: AG
feature: Assets HTTP API
role: Developer, Architect, Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 7%

---

# [!DNL Adobe Experience Manager Assets] 开发人员用例、API和参考资料 {#assets-cloud-service-apis}

本文包含面向开发人员的建议、参考资料和资源。 [!DNL Assets] as a [!DNL Cloud Service]. 其中包括新的资产上传模块、API引用，以及有关后处理工作流中提供的支持的信息。

## [!DNL Experience Manager Assets] API和操作 {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service] 提供了多个API以便以编程方式与数字资产交互。 每个API都支持特定的用例，如下表所述。 此 [!DNL Assets] 用户界面， [!DNL Experience Manager] 桌面应用程序和 [!DNL Adobe Asset Link] 支持全部或部分操作。

>[!CAUTION]
>
>某些API继续存在但不受主动支持(用×表示)。 请尽量不要使用这些API。

| 支持级别 | 描述 |
| ------------- | --------------------------- |
| ✓ | 支持 |
| × | 不支持。 请勿使用。 |
| - | 不可用 |

| 用例 | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager/Sling/JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) Java API | [asset compute服务](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlet | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **原始二进制文件** |  |  |  |  |  |  |
| 创建原始文件 | ✓ | × | - | × | × | - |
| 读取原始 | - | × | ✓ | ✓ | ✓ | - |
| 更新原始内容 | ✓ | × | ✓ | × | × | - |
| 删除原始内容 | - | ✓ | - | ✓ | ✓ | - |
| 复制原件 | - | ✓ | - | ✓ | ✓ | - |
| 移动原始 | - | ✓ | - | ✓ | ✓ | - |
| **元数据** |  |  |  |  |  |  |
| 创建元数据 | - | ✓ | ✓ | ✓ | ✓ | - |
| 读取元数据 | - | ✓ | - | ✓ | ✓ | - |
| 更新元数据 | - | ✓ | ✓ | ✓ | ✓ | - |
| 删除元数据 | - | ✓ | ✓ | ✓ | ✓ | - |
| 复制元数据 | - | ✓ | - | ✓ | ✓ | - |
| 移动元数据 | - | ✓ | - | ✓ | ✓ | - |
| **内容片段(CF)** |  |  |  |  |  |  |
| 创建Cf | - | ✓ | - | ✓ | - | - |
| 读取CF | - | ✓ | - | ✓ | - | ✓ |
| 更新CF | - | ✓ | - | ✓ | - | - |
| 删除Cf | - | ✓ | - | ✓ | - | - |
| 复制CF | - | ✓ | - | ✓ | - | - |
| 移动Cf | - | ✓ | - | ✓ | - | - |
| **版本** |  |  |  |  |  |  |
| 创建版本 | ✓ | ✓ | - | - | - | - |
| 读取版本 | - | ✓ | - | - | - | - |
| 删除版本 | - | ✓ | - | - | - | - |
| **文件夹** |  |  |  |  |  |  |
| 创建文件夹 | ✓ | ✓ | - | ✓ | - | - |
| 读取文件夹 | - | ✓ | - | ✓ | - | - |
| 删除文件夹 | ✓ | ✓ | - | ✓ | - | - |
| 复制文件夹 | ✓ | ✓ | - | ✓ | - | - |
| 移动文件夹 | ✓ | ✓ | - | ✓ | - | - |

## 资产上传 {#asset-upload}

在 [!DNL Experience Manager] as a [!DNL Cloud Service]，您可以使用HTTP API直接将资源上传到云存储。 上传二进制文件的步骤如下。 在外部应用程序而不是内部执行这些步骤 [!DNL Experience Manager] JVM。

1. [提交HTTP请求](#initiate-upload). 它会通知 [!DNL Experience Manage]或部署了您上传新二进制文件的意图。
1. [PUT二进制文件的内容](#upload-binary) 初始化请求提供的一个或多个URI。
1. [提交HTTP请求](#complete-upload) 通知服务器已成功上载二进制文件的内容。

![直接二进制上传协议概述](assets/add-assets-technical.png)

>[!IMPORTANT]
>
>在外部应用程序(而不是在 [!DNL Experience Manager] JVM。

该方法提供了可扩展且更高效的资产上传处理方式。 与 [!DNL Experience Manager] 6.5为：

* 二进制文件不通过 [!DNL Experience Manager]，现在只需将上传过程与为部署配置的二进制云存储进行协调即可。
* 二进制云存储可与内容交付网络(CDN)或边缘网络配合使用。 CDN为客户端选择更近的上传端点。 当数据在邻近端点之间传输较短距离时，上传性能和用户体验会得到改善，对于地理上分散的团队尤其如此。

>[!NOTE]
>
>请参阅客户端代码以在开源中实施此方法 [aem-upload库](https://github.com/adobe/aem-upload).
>
>[!IMPORTANT]
>
>在某些情况下，由于Cloud Service中的存储最终具有一致的性质，因此更改可能不会在请求Experience Manager之间完全传播。 这会导致404响应启动或完成上载调用，因为没有传播所需的文件夹创建。 客户端应会收到404响应，并通过使用回退策略实施重试来处理这些响应。

### 启动上载 {#initiate-upload}

将HTTPPOST请求提交到所需的文件夹。 在此文件夹中创建或更新资产。 包含选择器 `.initiateUpload.json` 指示请求是启动二进制文件上传。 例如，应创建资产的文件夹的路径为 `/assets/folder`. POST请求是 `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

请求正文的内容类型应为 `application/x-www-form-urlencoded` 表单数据，包含以下字段：

* `(string) fileName`：必填。 资产在中显示的名称 [!DNL Experience Manager].
* `(number) fileSize`：必填。 要上传的资源的文件大小（以字节为单位）。

只要每个二进制文件包含必需字段，就可以使用单个请求启动多个二进制文件的上传。 如果成功，请求将做出响应 `201` 状态代码和包含JSON数据的正文，格式如下：

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` （字符串）：在二进制文件完成上载时调用此URI。 URI可以是绝对URI或相对URI，客户端应该能够处理任一URI。 即，值可以是 `"https://[aem_server]:[port]/content/dam.completeUpload.json"` 或 `"/content/dam.completeUpload.json"` 请参阅 [完成上传](#complete-upload).
* `folderPath` （字符串）：上传二进制文件的文件夹的完整路径。
* `(files)` （数组）：其长度和顺序与启动请求中提供的二进制信息列表的长度和顺序匹配的元素列表。
* `fileName` （字符串）：相应二进制文件的名称，在启动请求中提供。 此值应包含在完整的请求中。
* `mimeType` （字符串）：在启动请求中提供的相应二进制文件的mime类型。 此值应包含在完整的请求中。
* `uploadToken` （字符串）：相应二进制文件的上载令牌。 此值应包含在完整的请求中。
* `uploadURIs` （数组）：字符串的列表，其值是二进制文件的内容应上载到的完整URI(请参阅 [上载二进制文件](#upload-binary))。
* `minPartSize` （数字）：可以提供给任一个服务器的数据的最小长度，以字节为单位。 `uploadURIs`，表示存在多个URI。
* `maxPartSize` （数字）：可以提供给 `uploadURIs`，表示存在多个URI。

### 上载二进制文件 {#upload-binary}

启动上载的输出包括一个或多个上载URI值。 如果提供了多个URI，则客户端可以按顺序将二进制文件拆分成多个部分，并向所提供的上传URI发出每个部分的PUT请求。 如果选择将二进制文件拆分为多个部分，请遵循以下准则：

* 每个部件（最后一个除外）的大小必须大于或等于 `minPartSize`.
* 每个部分的大小必须小于或等于 `maxPartSize`.
* 如果二进制文件的大小超过 `maxPartSize`，将二进制文件拆分为多个部分以上传。
* 您无需使用所有URI。

如果二进制文件的大小小于或等于 `maxPartSize`，您可以改为将整个二进制文件上传到单个上传URI。 如果提供了多个上传URI，请使用第一个上传URI并忽略其余上传URI。 您无需使用所有URI。

CDN边缘节点有助于加速请求的二进制文件上传。

完成此任务的最简单方法是使用 `maxPartSize` 作为部件大小。 如果您使用此值作为部分大小，API合同可确保有足够的上传URI来上传您的二进制文件。 要执行此操作，请将二进制文件拆分为大小部分 `maxPartSize`，按顺序为每个部件使用一个URI。 最终部分可以具有小于或等于任意大小 `maxPartSize`. 例如，假设二进制文件的大小总计为20,000字节， `minPartSize` 为5,000字节， `maxPartSize` 为8,000字节，上传URI数为5。 执行以下步骤：

* 使用第一个上传URI上载二进制文件的前8,000个字节。
* 使用第二个上传URI上传二进制文件的第二个8,000字节。
* 使用第三个上传URI上传二进制文件的最后4,000个字节。 由于这是最后一部分，因此它不需要大于 `minPartSize`.
* 您无需使用最后两个上传URI。 你可以忽略他们。

常见的错误是根据API提供的上传URI数计算部分大小。 API合同并不保证此方法有效，并且实际上可能会导致部件大小超出两者之间的范围 `minPartSize` 和 `maxPartSize`. 这可能会导致二进制上传失败。

同样，最简单、最安全的方法就是简单地使用大小等于 `maxPartSize`.

如果上传成功，服务器将使用响应每个请求 `201` 状态代码。

>[!NOTE]
>
>有关上载算法的更多信息，请参见 [官方功能文档](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) 和 [API文档](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) 在Apache Jackrabbit Oak项目中。

### 完成上传 {#complete-upload}

上传二进制文件的所有部分后，向启动数据提供的完整URI提交HTTPPOST请求。 请求正文的内容类型应为 `application/x-www-form-urlencoded` 表单数据，包含以下字段。

| 字段 | 类型 | 必需或非必需 | 描述 |
|---|---|---|---|
| `fileName` | 字符串 | 必填 | 资源的名称，由启动数据提供。 |
| `mimeType` | 字符串 | 必填 | 由启动数据提供的二进制文件的HTTP内容类型。 |
| `uploadToken` | 字符串 | 必填 | 由启动数据提供的二进制文件的上载令牌。 |
| `createVersion` | 布尔值 | 可选 | 如果 `True` 并且存在具有指定名称的资产，则 [!DNL Experience Manager] 创建资源的新版本。 |
| `versionLabel` | 字符串 | 可选 | 如果创建新版本，则标签与资源的新版本关联。 |
| `versionComment` | 字符串 | 可选 | 如果创建了新版本，则注释将与该版本相关联。 |
| `replace` | 布尔值 | 可选 | 如果 `True` 并且存在具有指定名称的资产， [!DNL Experience Manager] 删除资产，然后重新创建资产。 |
| `uploadDuration` | 数字 | 可选 | 文件上传完整文件所花费的总时间，以毫秒为单位。 如果指定，上传持续时间将包含在系统的日志文件中，用于传输速率分析。 |
| `fileSize` | 数字 | 可选 | 文件的大小（以字节为单位）。 如果指定，文件大小将包含在系统的日志文件中，以便进行传输速率分析。 |

>[!NOTE]
>
>如果资产存在但两者都不存在 `createVersion` 也不 `replace` 已指定，则 [!DNL Experience Manager] 使用新二进制文件更新资产的当前版本。

与启动过程一样，完整的请求数据可能包含多个文件的信息。

在调用文件的完整URL之前，不会完成上传二进制文件的过程。 上传过程完成后会处理资产。 即使资产的二进制文件已完全上传但未完成上传过程，处理也不会开始。 如果上传成功，服务器将做出响应 `200` 状态代码。

### 将资产上传到AEMas a Cloud Service的示例Shell脚本 {#upload-assets-shell-script}

以下示例shell-script说明了在AEMas a Cloud Service中用于直接二进制访问的多步上传过程 `aem-upload.sh`：

```bash
#!/bin/bash

# Check if pv is installed
if ! command -v pv &> /dev/null; then
    echo "Error: 'pv' command not found. Please install it before running the script."
    exit 1
fi

# Check if jq is installed
if ! command -v jq &> /dev/null; then
    echo "Error: 'jq' command not found. Please install it before running the script."
    exit 1
fi

# Set DEBUG to true to enable debug statements
DEBUG=true

# Function for printing debug statements
function debug() {
    if [ "${DEBUG}" = true ]; then
        echo "[DEBUG] $1"
    fi
}

# Function to check if a file exists
function file_exists() {
    [ -e "$1" ]
}

# Function to check if a path is a directory
function is_directory() {
    [ -d "$1" ]
}

# Check if the required number of parameters are provided
if [ "$#" -ne 4 ]; then
    echo "Usage: $0 <aem-url> <asset-folder> <file-to-upload> <bearer-token>"
    exit 1
fi

AEM_URL="$1"
ASSET_FOLDER="$2"
FILE_TO_UPLOAD="$3"
BEARER_TOKEN="$4"

# Extracting file name or folder name from the file path
NAME=$(basename "${FILE_TO_UPLOAD}")

# Step 1: Check if "file-to-upload" is a folder
if is_directory "${FILE_TO_UPLOAD}"; then
    echo "Uploading files from the folder recursively..."
    
    # Recursively upload files in the folder
    find "${FILE_TO_UPLOAD}" -type f | while read -r FILE_PATH; do
        FILE_NAME=$(basename "${FILE_PATH}")
        debug "Uploading file: ${FILE_PATH}"
        
        # You can choose to initiate upload for each file here
        # For simplicity, let's assume you use the same ASSET_FOLDER for all files
        ./aem-upload.sh "${AEM_URL}" "${ASSET_FOLDER}" "${FILE_PATH}" "${BEARER_TOKEN}"
    done
else
    # "file-to-upload" is a single file
    FILE_NAME="${NAME}"

    # Step 2: Calculate File Size
    FILE_SIZE=$(stat -c %s "${FILE_TO_UPLOAD}")

    # Step 3: Initiate Upload
    INITIATE_UPLOAD_ENDPOINT="${AEM_URL}/content/dam/${ASSET_FOLDER}.initiateUpload.json"

    debug "Initiating upload..."
    debug "Initiate Upload Endpoint: ${INITIATE_UPLOAD_ENDPOINT}"
    debug "File Name: ${FILE_NAME}"
    debug "File Size: ${FILE_SIZE}"

    INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
        -d "fileName=${FILE_NAME}" \
        -d "fileSize=${FILE_SIZE}" \
        ${INITIATE_UPLOAD_ENDPOINT})

    # Continue with the rest of the script...
fi


# Check if the response body contains the specified HTML content for a 404 error
if echo "${INITIATE_UPLOAD_RESPONSE}" | grep -q "<title>404 Specified folder not found</title>"; then
    echo "Folder not found. Creating the folder..."

    # Attempt to create the folder
    CREATE_FOLDER_ENDPOINT="${AEM_URL}/api/assets/${ASSET_FOLDER}"

    debug "Creating folder..."
    debug "Create Folder Endpoint: ${CREATE_FOLDER_ENDPOINT}"

    CREATE_FOLDER_RESPONSE=$(curl -X POST \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -d '{"class":"'${ASSET_FOLDER}'","properties":{"title":"'${ASSET_FOLDER}'"}}' \
        ${CREATE_FOLDER_ENDPOINT})

    # Check the response code and inform the user accordingly
    STATUS_CODE_CREATE_FOLDER=$(echo "${CREATE_FOLDER_RESPONSE}" | jq -r '.properties."status.code"')
    case ${STATUS_CODE_CREATE_FOLDER} in
        201)
            echo "Folder created successfully. Initiating upload again..."

            # Retry Initiate Upload after creating the folder
            INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
                -H "Authorization: Bearer ${BEARER_TOKEN}" \
                -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
                -d "fileName=${FILE_NAME}" \
                -d "fileSize=${FILE_SIZE}" \
                ${INITIATE_UPLOAD_ENDPOINT})
            ;;
        409)
            echo "Error: Folder already exists."
            ;;
        412)
            echo "Error: Precondition failed. Root collection cannot be found or accessed."
            exit 1
            ;;
        500)
            echo "Error: Internal Server Error. Something went wrong."
            exit 1
            ;;
        *)
            echo "Error: Unexpected response code ${STATUS_CODE_CREATE_FOLDER}"
            exit 1
            ;;
    esac
fi

# Extracting values from the response
FOLDER_PATH=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.folderPath')
UPLOAD_URIS=($(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadURIs[]'))
UPLOAD_TOKEN=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadToken')
MIME_TYPE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].mimeType')
MIN_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].minPartSize')
MAX_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].maxPartSize')
COMPLETE_URI=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.completeURI')

# Extracting "Affinity-cookie" from the response headers
AFFINITY_COOKIE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | grep -i 'Affinity-cookie' | awk '{print $2}')

debug "Folder Path: ${FOLDER_PATH}"
debug "Upload Token: ${UPLOAD_TOKEN}"
debug "MIME Type: ${MIME_TYPE}"
debug "Min Part Size: ${MIN_PART_SIZE}"
debug "Max Part Size: ${MAX_PART_SIZE}"
debug "Complete URI: ${COMPLETE_URI}"
debug "Affinity Cookie: ${AFFINITY_COOKIE}"
if $DEBUG; then
    i=1
    for UPLOAD_URI in "${UPLOAD_URIS[@]}"; do
        debug "Upload URI $i: "$UPLOAD_URI
        i=$((i+1))
    done
fi


# Calculate the number of parts needed
NUM_PARTS=$(( (FILE_SIZE + MAX_PART_SIZE - 1) / MAX_PART_SIZE ))
debug "Number of Parts: $NUM_PARTS"

# Calculate the part size for the last chunk
LAST_PART_SIZE=$(( FILE_SIZE % MAX_PART_SIZE ))
if [ "${LAST_PART_SIZE}" -eq 0 ]; then
    LAST_PART_SIZE=${MAX_PART_SIZE}
fi

# Step 4: Upload binary to the blob store in parts
PART_NUMBER=1
for i in $(seq 1 $NUM_PARTS); do
    PART_SIZE=${MAX_PART_SIZE}
    if [ ${PART_NUMBER} -eq ${NUM_PARTS} ]; then
        PART_SIZE=${LAST_PART_SIZE}
        debug "Last part size: ${PART_SIZE}"
    fi

    PART_FILE="/tmp/${FILE_NAME}_part${PART_NUMBER}"

    # Creating part file 
    SKIP=$((PART_NUMBER - 1))
    SKIP=$((MAX_PART_SIZE * SKIP))
    dd if="${FILE_TO_UPLOAD}" of="${PART_FILE}"  bs="${PART_SIZE}" skip="${SKIP}" count="${PART_SIZE}" iflag=skip_bytes,count_bytes  > /dev/null 2>&1
    debug "Creating part file: ${PART_FILE} with size ${PART_SIZE}, skipping first ${SKIP} bytes."

    
    UPLOAD_URI=${UPLOAD_URIS[$PART_NUMBER-1]}

    debug "Uploading part ${PART_NUMBER}..."
    debug "Part Size: $PART_SIZE"
    debug "Part File: ${PART_FILE}"
    debug "Part File Size: $(stat -c %s "${PART_FILE}")"
    debug "Upload URI: ${UPLOAD_URI}"

    # Upload the part in the background
    if command -v pv &> /dev/null; then
        pv "${PART_FILE}" | curl --progress-bar -X PUT --data-binary "@-" "${UPLOAD_URI}" &
    else
        curl -# -X PUT --data-binary "@${PART_FILE}" "${UPLOAD_URI}" &
    fi

    PART_NUMBER=$((PART_NUMBER + 1))
done

# Wait for all background processes to finish
wait

# Step 5: Complete the upload in AEM
COMPLETE_UPLOAD_ENDPOINT="${AEM_URL}${COMPLETE_URI}"

debug "Completing the upload..."
debug "Complete Upload Endpoint: ${COMPLETE_UPLOAD_ENDPOINT}"

RESPONSE=$(curl -X POST \
    -H "Authorization: Bearer ${BEARER_TOKEN}" \
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
    -H "Affinity-cookie: ${AFFINITY_COOKIE}" \
    --data-urlencode "uploadToken=${UPLOAD_TOKEN}" \
    --data-urlencode "fileName=${FILE_NAME}" \
    --data-urlencode "mimeType=${MIME_TYPE}" \
    "${COMPLETE_UPLOAD_ENDPOINT}")
    
debug $RESPONSE

echo "File upload completed successfully."
```

### 开源上传库 {#open-source-upload-library}

要了解有关上传算法的更多信息或构建您自己的上传脚本和工具，Adobe提供了开源库和工具：

* [开源aem-upload库](https://github.com/adobe/aem-upload).
* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
>
>aem-upload库和命令行工具都使用 [node-httptransfer库](https://github.com/adobe/node-httptransfer/)

### 已弃用的资产上传API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

仅支持新的上传方法 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. API来自 [!DNL Adobe Experience Manager] 6.5已弃用。 以下API弃用了与上传或更新资产或演绎版（任何二进制上传）相关的方法：

* [EXPERIENCE MANAGER ASSETS HTTP API](mac-api-assets.md)
* `AssetManager` Java API，如 `AssetManager.createAsset(..)`， `AssetManager.createAssetForBinary(..)`， `AssetManager.getAssetForBinary(..)`， `AssetManager.removeAssetForBinary(..)`， `AssetManager.createOrUpdateAsset(..)`， `AssetManager.createOrReplaceAsset(..)`

>[!MORELIKETHIS]
>
>* [开源aem-upload库](https://github.com/adobe/aem-upload).
>* [开源命令行工具](https://github.com/adobe/aio-cli-plugin-aem).
>* [用于直接上传的Apache Jackrabbit Oak文档](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).

## 资产处理和后处理工作流 {#post-processing-workflows}

在 [!DNL Experience Manager]，资产处理基于 **[!UICONTROL 处理配置文件]** 使用的配置 [资源微服务](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). 处理不需要开发人员扩展。

对于后处理工作流配置，请使用带有自定义步骤的扩展的标准工作流。

## 后处理工作流中支持工作流步骤 {#post-processing-workflows-steps}

如果您从以前的版本升级 [!DNL Experience Manager]，则可以使用资产微服务来处理资产。 云原生资源微服务配置和使用更加简单。 中使用的几个工作流步骤 [!UICONTROL DAM更新资产] 不支持以前版本中的工作流。 有关支持的类的详细信息，请参见 [Java API引用或Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

以下技术工作流模型已被资产微服务取代，或者该支持不可用：

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).