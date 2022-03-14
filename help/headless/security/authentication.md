---
title: 对内容片段的远程 AEM GraphQL 查询的身份验证
description: 了解远程 AEM GraphQL 查询所需的身份验证，用于保护您的 Headless 内容投放。
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 4e37db128aa31d6e8e950be0d077eae921a27468
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 100%

---

# 对内容片段的远程 AEM GraphQL 查询的身份验证 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

[用于内容片段投放的 Adobe Experience Manager as a Cloud Service (AEM) GraphQL API](/help/headless/graphql-api/content-fragments.md) 的主要用例是接受来自第三方应用程序或服务的远程查询。这些远程查询可能需要经过身份验证的 API 访问，以保护 Headless 内容投放。

>[!NOTE]
>
>对于测试和开发，您还可以使用 [GraphiQL](/help/headless/graphql-api/graphiql-ide.md) 接口直接访问 AEM GraphQL API。

对于身份验证，第三方服务需要[检索访问令牌](#retrieving-access-token)，该令牌随后[可用于 GraphQL 请求中](#use-access-token-in-graphql-request)。

## 检索访问令牌 {#retrieving-access-token}

有关完整详细信息，请参阅[为服务器端 API 生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。

## 在 GraphQL 请求中使用访问令牌 {#use-access-token-in-graphql-request}

对于要连接到 AEM 实例的第三方服务，它需要具有&#x200B;*访问令牌*。然后，服务必须添加此令牌到 POST 请求的 `Authorization` 标头。

例如，GraphQL 授权标头：

```xml
Authorization: Bearer <access_token>
```

## 权限要求 {#permission-requirements}

使用访问令牌发出的所有请求将会&#x200B;*由生成令牌的用户帐户*&#x200B;实际发出。

这意味着，您需要确保帐户具有运行 GraphQL 查询所需的权限。

您可以通过在本地实例上使用 GraphiQL 来检查这一点。有关[权限的更多详细信息见此处](/help/headless/security/permissions.md)。
