---
title: 对内容片段的远程 AEM GraphQL 查询的身份验证
description: 了解远程AEM GraphQL查询所需的身份验证，以保护无头内容交付的安全。
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 4e37db128aa31d6e8e950be0d077eae921a27468
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 7%

---

# 对内容片段的远程 AEM GraphQL 查询的身份验证 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

用于 [Adobe Experience Manager as a Cloud Service(AEM)用于内容片段交付的GraphQL API](/help/headless/graphql-api/content-fragments.md) 接受来自第三方应用程序或服务的远程查询。 这些远程查询可能需要经过验证的API访问，以保护无头内容交付的安全。

>[!NOTE]
>
>要进行测试和开发，您还可以使用 [GraphiQL接口](/help/headless/graphql-api/graphiql-ide.md) 界面。

为了进行身份验证，第三方服务需要 [检索访问令牌](#retrieving-access-token)，则 [在GraphQL请求中使用](#use-access-token-in-graphql-request).

## 检索访问令牌 {#retrieving-access-token}

请参阅 [为服务器端API生成访问令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 以了解完整详细信息。

## 在GraphQL请求中使用访问令牌 {#use-access-token-in-graphql-request}

要使第三方服务与AEM实例连接，它需要具有 *访问令牌*. 然后，服务必须将此令牌添加到 `Authorization` 标头。

例如，GraphQL授权标头：

```xml
Authorization: Bearer <access_token>
```

## 权限要求 {#permission-requirements}

实际上，将使用访问令牌发出的所有请求都将发出 *由生成令牌的用户帐户*.

这意味着您需要检查帐户是否具有运行GraphQL查询所需的权限。

您可以在本地实例上使用GraphiQL来检查此项。 有关 [权限可在此处找到](/help/headless/security/permissions.md).
