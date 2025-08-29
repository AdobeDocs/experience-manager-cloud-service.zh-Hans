---
title: 在Forms的规则编辑器中集成API
description: 了解规则编辑器中的调用服务的最新增强功能，包括如何在不使用表单数据模型的情况下，基于核心组件集成自适应Forms的API。
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: 在规则编辑器中集成API，调用服务增强功能
source-git-commit: 5d25204516cb46334c4d594c16852b033f3e6c90
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---


# 在规则编辑器中集成API

<span>规则编辑器中的Integrating API位于早期采用程序程序下。 您可以从官方电子邮件ID写入`aem-forms-ea@adobe.com`以加入早期采用者计划并请求访问功能。</span>

自适应Forms中的可视规则编辑器支持直接API集成，而无需创建表单数据模型。 您可以通过输入API URL（以JSON格式）或通过cURL命令导入配置来连接到API端点。 集成后，**调用服务**&#x200B;操作可用于调用API。

表单字段可以直接映射到API配置中定义的输入参数。 同样，可以使用相应API响应的&#x200B;**事件有效负载**&#x200B;选项将输出参数映射到表单字段。

此外，可视规则编辑器允许您在调用服务时定义&#x200B;**success**&#x200B;和&#x200B;**failure处理程序**。 成功处理程序指定在成功API调用后要执行的操作，而失败处理程序定义表单在错误发生时应如何响应。

>[!NOTE]
>
> 规则编辑器中的API集成也适用于Edge Delivery Services Forms。

## 比较： API集成方法

| 方面 | API与表单数据模型(FDM)集成 | 直接API集成（通过&#x200B;*创建API集成*） |
|--------------------------------|---------------------------------------------------------------------|-----------------------------------------------------------|
| **用途** | 跨多个表单的集中化、可重复使用的API集成 | 特定于表单的快速集成API |
| **安装位置** | 在表单数据模型编辑器(AEM控制台)中创建和编辑 | 直接在自适应表单规则编辑器中创建和编辑 |
| **复杂性** | 设置工作量更大（需要映射和配置） | 简单而轻量 |
| **最适合** | 具有多种表单的企业或大规模用例 | 小型表单、原型或一次性API调用 |

## API集成配置

以下屏幕截图显示API集成配置窗口：

![API集成配置](/help/forms/assets/api-integration-configuration.png)

### 关键配置选项

**API集成配置**

* **从cURL导入**：通过粘贴现成的cURL命令配置API集成，而不是手动输入详细信息，如API URL、HTTP方法、标头和参数。
* **显示名称**： API服务的自定义名称。
* **API URL**： API服务的端点。
* **选择HTTP方法**：用于调用API的HTTP请求方法。
* **内容类型**：定义请求和响应格式。
* **需要加密**： （可选）确保在传输期间对敏感数据进行加密。
* **在客户端执行**：启用后，将从客户端（浏览器）而不是服务器执行API调用。

**身份验证类型**

* **选项**：无、基本、API密钥、OAuth 2.0。

**输入参数**

* **上载输入的JSON**：上载示例JSON文件以自动填充输入映射。
   * **名称**： API所需的输入参数名称。
   * **类型**：输入的数据类型（字符串、数字、布尔等）。
   * **In**：参数（查询、标头或正文）的位置。
   * **默认值**：如果未由用户提供，则为预填充值。
   * **添加**：用于添加其他输入参数的选项。

**输出参数**

* **上载输出的JSON**：上载示例API响应以自动生成映射。
   * **名称**： API响应中的输出参数名称。
   * **类型**：输出参数的预期数据类型（字符串、数字等）。
   * **In**：定义需要映射值的位置。
   * **添加/删除**：添加新映射或删除现有映射。

## 用例：在签证申请表中填写国家/地区字段

**方案**：政府机构提供包含以下字段的在线签证申请表：

1. 全名（文本）
2. 出生日期（日期）
3. 国籍国家/地区（下拉列表）
4. 护照号码（文本）
5. 护照签发国家/地区（下拉列表）
6. 目标国家/地区（下拉列表）
7. 预定到达日期（日期）

表单使用&#x200B;**getcountryname API**&#x200B;动态获取国家/地区信息(大陆、资本、ISO Alpha代码等)，而不是维护静态的国家/地区列表：

`https://secure.geonames.org/countryInfoJSON?username=aemforms`

这可确保在填写表单时始终看到最新的准确国家/地区列表。

### 在规则编辑器中使用API集成进行实施

您可以通过单击规则编辑器中的&#x200B;**创建API集成**&#x200B;按钮，在不创建表单数据模型的情况下集成API。

![创建API集成](/help/forms/assets/create-api-integration.png)

在规则编辑器中的&#x200B;**API集成配置**&#x200B;下配置了名为&#x200B;**getcountryname**&#x200B;的API服务：

![API Rest终结点配置](/help/forms/assets/api-restendpoint.png)

* **API终结点URL** → `https://secure.geonames.org/countryInfoJSON?username=aemforms`
* GET→的&#x200B;**HTTP方法**
* **内容类型**→JSON
* **输入**→`username`作为查询参数(`aemforms`)传递。
* **输出** →响应字段（如`continent`、`capital`、`countrynames`、`isoAlpha3`和`languages`）映射到表单字段。

在&#x200B;**Visa申请表**&#x200B;中，三个下拉字段&#x200B;**公民国家/地区**、**Passport颁发国家/地区**&#x200B;和&#x200B;**目的地国家/地区**&#x200B;将绑定到&#x200B;**调用服务**&#x200B;操作。

加载表单时，**调用服务**&#x200B;从API获取国家/地区列表。 然后，将映射响应以自动填充下拉选项。

例如，当用户打开&#x200B;**公民国家/地区**&#x200B;时，将从API响应动态显示国家/地区列表。

![invoke-service-api-integration](/help/forms/assets/invoke-service-api-integration.png)

![API集成输出](/help/forms/assets/api-integration-output.png)

同样，**Passport Issuance国家/地区**&#x200B;和&#x200B;**目标国家/地区**&#x200B;使用相同的API调用，确保所有三个字段中的数据一致且最新。

## 实施API失败的重试机制

当API请求失败时，在向用户报告错误之前重试请求通常很有用。 通过在&#x200B;**function.js**&#x200B;文件中写入自定义代码，您可以实施轮询和重试机制。

以下示例演示了如何处理最多包含两次重试和两次重试之间的指数回退的API失败：

```javascript
/**
 * Handles request retries with up to 2 retry attempts
 * @param {function} requestFn - The request function to execute
 * @return {Promise} A promise that resolves with the response or rejects after all retries
 */
function retryHandler(requestFn) {
    const MAX_RETRIES = 2;
    
    /**
     * Attempts the request with retry metadata
     * @param {number} retryCount - Current retry attempt count
     * @return {Promise} The request promise
     */
    function attemptRequest(retryCount = 0) {
        // Include retry metadata if this is a retry
        const requestOptions = retryCount > 0 ? {
            headers: {
                'X-Retry': 'true',
                'X-Retry-Count': retryCount.toString(),
                'X-Retry-Time': new Date().toISOString()
            },
            body: {
                retry: true,
                retryCount: retryCount,
                timestamp: Date.now()
            }
        } : undefined;

        return requestFn(requestOptions)
            .then(function(response) {
                if (response && response.status >= 400) {
                    console.warn('Request failed with status ' + response.status);
                    throw new Error('Request failed with status ' + response.status);
                }
                return response;
            })
            .catch(function(error) {
                console.warn('Request attempt ' + (retryCount + 1) + ' failed:', error.message);
                
                // Retry if max attempts not reached
                if (retryCount < MAX_RETRIES) {
                    console.log('Retrying request, attempt ' + (retryCount + 2) + ' of ' + (MAX_RETRIES + 1));
                    
                    // Exponential backoff delay: 1s, 2s, 4s...
                    const delay = Math.pow(2, retryCount) * 1000;
                    
                    return new Promise(function(resolve) {
                        setTimeout(resolve, delay);
                    }).then(function() {
                        return attemptRequest(retryCount + 1);
                    });
                } else {
                    // All retries exhausted
                    console.error('All retry attempts failed. Final error:', error.message);
                    throw new Error('Request failed after ' + (MAX_RETRIES + 1) + ' attempts: ' + error.message);
                }
            });
    }
    
    // Start the first attempt
    return attemptRequest(0);
}
```

在上述代码中，**retryHandler**&#x200B;函数通过自动重试管理API请求，以防失败。 它使用一个请求函数(requestFn)，最多尝试请求两次，为每次重试添加元数据。

>[!NOTE]
>
> 有关如何添加自定义函数的详细步骤，请参阅[基于核心组件的自适应Forms的自定义函数简介](/help/forms/create-and-use-custom-functions.md)一文。

## 常见问题解答

* **我是否需要创建表单数据模型以集成Adaptive Forms中的API？**\
  不行。通过可视化规则编辑器，您可以使用&#x200B;**创建API集成**&#x200B;选项直接集成API，而无需创建表单数据模型。 此方法最适合轻量级或特定于表单的用例。

* **我能否保护从规则编辑器发出的API调用？**\
  是。API集成配置提供身份验证选项，如&#x200B;**基本、API密钥和OAuth 2.0**。 您还可以启用&#x200B;**需要加密**&#x200B;以确保安全传输敏感数据。