---
title: AEM Headless 的反向链接筛选条件
description: Adobe Experience Manager 的反向链接筛选条件实现了从第三方主机的访问。对于 Headless 应用程序，需要反向链接筛选条件的 OSGi 配置来启用对 GraphQL 端点的访问。
feature: GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 100%

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

例如，要授予反向链接 `my.domain` 的请求的访问权限，您可以：

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

>[!CAUTION]
>
>客户仍然有下列责任：
>
>* 仅向可信域授予访问权限
>* 确保未公开敏感信息
>* 不使用通配符 [*] 语法，这不仅会禁用对 GraphQL 端点的经过身份验证的访问，还会将其向全世界公开。

>[!CAUTION]
>
>所有 GraphQL [架构](#schema-generation)（派生自&#x200B;**已启用**&#x200B;的内容片段模型）可通过 GraphQL 端点读取。
>
>这意味着您需要确保其中没有提供敏感数据，因为这种方式可能会导致泄露；例如，这包括可能在模型定义中作为字段名称呈现的信息。
