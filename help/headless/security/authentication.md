---
title: 对内容片段的远程 AEM GraphQL 查询的身份验证
description: 了解远程Adobe Experience Manager GraphQL查询所需的身份验证，以保护Headless内容投放。
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 31%

---

# 对内容片段的远程 AEM GraphQL 查询的身份验证 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

的主要用例 [用于内容片段投放的Adobe Experience Manager as a Cloud Service (AEM) GraphQL API](/help/headless/graphql-api/content-fragments.md) 是接受来自第三方应用程序或服务的远程查询。 这些远程查询可能需要经过身份验证的 API 访问，以保护 Headless 内容投放。

>[!NOTE]
>
>对于测试和开发，您还可以使用直接访问AEM GraphQL API [GraphiQL接口](/help/headless/graphql-api/graphiql-ide.md).

对于身份验证，第三方服务必须 [检索访问令牌](#retrieving-access-token) 然后可以是 [在GraphQL请求中使用](#use-access-token-in-graphql-request).

## 检索访问令牌 {#retrieving-access-token}

参见 [为服务器端API生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 以了解完整的详细信息。

## 在 GraphQL 请求中使用访问令牌 {#use-access-token-in-graphql-request}

对于要与AEM实例连接的第三方服务，它必须具有 *访问令牌*. 然后，服务必须添加此令牌到 POST 请求的 `Authorization` 标头。

例如，GraphQL 授权标头：

```xml
Authorization: Bearer <access_token>
```

## 权限要求 {#permission-requirements}

使用访问令牌发出的所有请求都会发出 *通过生成令牌的用户帐户*.

此用户帐户意味着您必须检查该帐户是否具有运行GraphQL查询所需的权限。

您可以通过在本地实例上使用GraphiQL来检查这些权限。 有关[权限的更多详细信息见此处](/help/headless/security/permissions.md)。
