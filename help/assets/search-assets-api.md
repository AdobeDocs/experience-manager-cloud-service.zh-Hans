---
title: 搜索Assets API
description: 了解如何使用Search Assets API。
role: User
source-git-commit: 3e2fe458460fe8ec4c1dd12152c1134bfb9ca62b
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 搜索Assets API {#search-assets-api}

可以使用投放URL搜索Experience Manager资源存储库中可用的所有[批准的资源](approve-assets.md)，然后将其传递到集成的下游应用程序。

从Experience Manager存储库中搜索正确的已批准资源是使用投放URL交付资源的第一步。 对搜索请求的响应包括对应于满足搜索条件的资产的JSON文档数组。 每个JSON文档都使用`id`字段进行标识，该字段用于构成资产投放请求。

![直接二进制上传协议概述](assets/search-assets-api-overview.png)

您可以在Search Assets API请求中定义属性以启用以下功能：

* **全文搜索**：使用`match`查询定义要搜索的文本。  您还可以使用`match`查询中的运算符来筛选结果。

* **应用筛选器**：使用`term`查询通过定义`key`和一个或多个值进一步筛选结果。 `key`标识其值必须匹配的字段，`value`表示要匹配的对象。 同样，您可以使用`range`查询通过“大于(gt)”、“大于或等于(gte)”、“小于(lt)”和“小于或等于(lte)”属性来定义字段的范围。

* **排序结果**：使用`OrderBy`属性根据一个或多个字段对搜索结果排序。 您可以按升序或降序对结果进行排序。

* **分页**：使用`limit`和`cursor`属性在搜索API请求中定义分页属性。 `limit`属性定义API响应中要检索的最大项数。 `cursor`属性有助于检索`limit`属性中定义的下一组资源的起点。 例如，如果您在API请求中将`50`定义为限制，则可以使用`cursor`属性启动并使用下一个API请求检索接下来的50个项目。

## 搜索资产API端点 {#search-assets-api-endpoint}

Search Assets API请求中的端点必须采用以下格式：
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

投放域的结构与Experience Manager创作环境的域类似。 唯一的区别是将术语`author`替换为`delivery`。

`pXXXX`引用项目ID

`eYYYY`引用环境ID

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

要调用搜索API，需要在`Authorization`详细信息中定义IMS令牌。 IMS令牌从技术帐户中获取。 请参阅[获取AEM as a Cloud Service凭据](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials)以创建新的技术帐户。 请参阅[生成访问令牌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)以生成IMS令牌并在搜索资产API请求标头中正确使用它。

要查看请求示例、响应示例和响应代码，请参阅[搜索Assets API](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search)。
