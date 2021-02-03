---
title: 内容片段上的远程AEM GraphQL查询身份验证
description: 了解远程AEM GraphQL查询所需的身份验证。
translation-type: tm+mt
source-git-commit: 42ca0c70f7018a6e3c9be68ef13adefafc987864
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 内容片段{#authentication-for-remote-aem-graphql-queries-on-content-fragments}上的远程AEM GraphQL查询的身份验证

[作为Cloud Service(AEM) GraphQL API，用于内容片段投放](/help/assets/content-fragments/graphql-api-content-fragments.md)的主要用例是接受来自第三方应用程序或服务的远程查询。  这些远程查询可能需要经过身份验证的API访问。

>[!NOTE]
>
>对于测试和开发，您还可以使用[GraphiQL接口](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)接口直接访问AEM GraphQL API。

要进行身份验证，第三方服务需要使用[访问令牌](#access-token)，然后该标识符可以在GraphQL请求](#use-access-token-in-graphql-request)中使用。[

## 检索访问令牌{#retrieving-access-token}

有关完整的详细信息，请参阅[为服务器端API生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。

## 使用GraphQL请求{#use-access-token-in-graphql-request}中的访问令牌

要使第三方服务与AEM实例连接，它需要具有&#x200B;*访问令牌*。 服务随后必须将此令牌添加到POST请求的`Authorization`头。

例如，GraphQL授权标头：

```xml
Authorization: Bearer <access_token>
```

## 权限要求{#permission-requirements}

使用访问令牌发出的所有请求实际上将由生成令牌的用户帐户&#x200B;*发出。*

这意味着您需要检查帐户是否具有运行GraphQL查询所需的权限。

可以在本地实例上使用GraphiQL来检查此项。
