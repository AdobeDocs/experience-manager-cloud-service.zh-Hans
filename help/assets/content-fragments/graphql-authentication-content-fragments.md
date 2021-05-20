---
title: 对内容片段的远程AEM GraphQL查询进行身份验证
description: 了解远程AEM GraphQL查询所需的身份验证，以保护无头内容交付的安全。
feature: 内容片段，GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: dab4c9393c26f5c3473e96fa96bf7ec51e81c6c5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 对内容片段{#authentication-for-remote-aem-graphql-queries-on-content-fragments}上的远程AEM GraphQL查询进行身份验证

[Adobe Experience Manager as aCloud Service(AEM)用于内容片段交付的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)的主要用例是接受来自第三方应用程序或服务的远程查询。 这些远程查询可能需要经过验证的API访问，以保护无头内容交付的安全。

>[!NOTE]
>
>要进行测试和开发，您还可以使用[GraphiQL接口](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)接口直接访问AEM GraphQL API。

为了进行身份验证，第三方服务需要[检索访问令牌](#retrieving-access-token)，该令牌随后可以在GraphQL请求](#use-access-token-in-graphql-request)中使用。[

## 检索访问令牌{#retrieving-access-token}

有关完整的详细信息，请参阅[为服务器端API生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 。

## 在GraphQL请求{#use-access-token-in-graphql-request}中使用访问令牌

要使第三方服务与AEM实例连接，它需要具有&#x200B;*访问令牌*。 然后，服务必须将此令牌添加到POST请求的`Authorization`标头中。

例如，GraphQL授权标头：

```xml
Authorization: Bearer <access_token>
```

## 权限要求{#permission-requirements}

使用访问令牌发出的所有请求实际上将由生成令牌&#x200B;*的用户帐户发出*。

这意味着您需要检查帐户是否具有运行GraphQL查询所需的权限。

您可以在本地实例上使用GraphiQL来检查此项。
