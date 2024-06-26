---
title: 搜索Assets API
description: 了解如何使用Search Assets API。
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 搜索Assets API {#search-assets-api}

全部 [批准的资产](approve-assets.md) 可以搜索Experience Manager资源存储库中的可用资源，然后使用投放URL将其交付给集成的下游应用程序。

从Experience Manager存储库中搜索正确的已批准资源是使用投放URL交付资源的第一步。 对搜索请求的响应包括对应于满足搜索条件的资产的JSON文档数组。 每个JSON文档均使用 `id` 字段，用于撰写资产投放请求。

![直接二进制上传协议概述](assets/search-assets-api-overview.png)

您可以在Search Assets API请求中定义属性以启用以下功能：

* **全文搜索**：使用 `match` 查询以定义要搜索的文本。  您还可以在中使用运算符 `match` 查询以筛选结果。

* **应用过滤器**：使用 `term` 查询：通过定义 `key` 以及一个或多个值。 `key` 标识其值必须匹配的字段，并且 `value` 表示要与之匹配的内容。 同样，您可以使用 `range` 使用“大于(gt)”、“大于或等于(gte)”、“小于(lt)”和“小于或等于(lte)”属性定义字段范围。

* **排序结果**：使用 `OrderBy` 根据一个或多个字段对搜索结果排序的属性。 您可以按升序或降序对结果进行排序。

* **分页**：使用 `limit` 和 `cursor` 属性，以定义Search API请求中的分页属性。 `limit` 属性定义在API响应中检索的最大项数。 `cursor` 属性有助于检索中定义的下一组资源的起点 `limit` 属性。 例如，如果您定义 `50` 作为API请求中的限制，您可以使用 `cursor` 属性以开始使用下一个API请求并检索接下来的50项。

## 搜索资产API端点 {#search-assets-api-endpoint}

Search Assets API请求中的端点必须采用以下格式：
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

投放域的结构与Experience Manager创作环境的域类似。 唯一的区别是替换术语 `author` 替换为 `delivery`.

`pXXXX` 是指项目ID

`eYYYY` 是指环境ID

## 搜索资产API请求方法 {#search-assets-api-request-method}

POST

## 搜索Assets API标头 {#search-assets-api-header}

在“搜索资产API”中定义标头时，您需要提供以下详细信息：

```java
headers: {
      'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    },
```

要调用搜索API，需要在中定义IMS令牌 `Authorization` 详细信息。 IMS令牌从技术帐户中获取。 请参阅 [获取AEM as a Cloud Service凭据](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) 以创建新的技术帐户。 请参阅 [生成访问令牌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) 以生成IMS令牌并在搜索资产API请求标头中正确使用它。

要查看请求示例、响应示例和响应代码，请参阅 [搜索Assets API](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search).

