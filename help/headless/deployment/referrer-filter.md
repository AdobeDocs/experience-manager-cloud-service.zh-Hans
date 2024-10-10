---
title: AEM Headless 的反向链接筛选条件
description: Adobe Experience Manager 的反向链接筛选条件实现了从第三方主机的访问。对于 Headless 应用程序，需要反向链接筛选条件的 OSGi 配置来启用对 GraphQL 端点的访问。
feature: Headless, GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
solution: Experience Manager
role: Admin, Developer
source-git-commit: 3096436f8057833419249d51cb6c15e6c28e9e13
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 55%

---

# 反向链接筛选条件 {#referrer-filter}

Adobe Experience Manager 的反向链接筛选条件实现了从第三方主机的访问。

需要反向链接筛选条件的 OSGi 配置，来通过 HTTP POST 启用对 Headless 应用程序 GraphQL 端点的访问。使用通过 HTTP GET 访问 AEM 的 AEM Headless P持久查询时，不需要反向链接筛选条件配置。

>[!WARNING]
> AEM 的反向链接筛选条件不是 OSGi 配置工厂，这意味着一次只有一个配置在 AEM 服务上处于活动状态。如果可能，请避免添加自定义反向链接筛选条件配置，因为这会覆盖 AEM 的本机配置，并可能破坏产品功能。

此操作可通过为满足下列条件的反向链接筛选条件添加相应的 OSGi 配置来完成：

* 指定了可信的网站主机名；可以为 `allow.hosts` 或 `allow.hosts.regexp`。
* 授予了对此主机名的访问权限。

文件的名称必须为 `org.apache.sling.security.impl.ReferrerFilter.cfg.json`。

## 示例配置 {#example-configuration}

例如，要授予反向链接 `my.domain` 的请求的访问权限，您可以：

>[!CAUTION]
>
>这是一个可能覆盖标准配置的基本示例。 您需要确保始终将产品更新应用于任何自定义设置。

```xml
{
    "allow.empty": false,
    "allow.hosts": [
      "my.domain"
    ],
    "allow.hosts.regexp": [
      ""
    ],
    "filter.methods": [
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp": [
      ""
    ]
}
```

## 数据安全性 {#data-security}

>[!CAUTION]
>
>您仍有责任充分处理以下各点。

要确保数据安全，您必须确保：

* 仅向受信任的域授予访问&#x200B;**权限**

* **中未使用**&#x200B;中的通配符[`*`]语法；这既禁用了对GraphQL端点的经过身份验证的访问，也将其公开给整个世界

* 敏感信息&#x200B;**从不公开**；不直接也不间接：

   * 例如，所有[GraphQL架构](/help/headless/graphql-api/content-fragments.md#schema-generation)都是：

      * 派生自&#x200B;**已启用**&#x200B;的内容片段模型

     **和**

      * 可通过GraphQL端点读取

     这意味着在模型定义中以字段名称形式呈现的信息可以变得可用。

您必须确保不以任何方式提供敏感数据，因此必须仔细考虑此类详细信息。
