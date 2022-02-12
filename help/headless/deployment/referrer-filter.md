---
title: 使用AEM Headless的反向链接过滤器配置
description: Adobe Experience Manager的反向链接过滤器允许从第三方主机访问。 需要反向链接过滤器的OSGi配置，以便能够访问无头应用程序的GraphQL端点。
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# 反向链接过滤器 {#referrer-filter}

Adobe Experience Manager的反向链接过滤器允许从第三方主机访问。 需要反向链接过滤器的OSGi配置，以便能够访问无头应用程序的GraphQL端点。

这通过为反向链接过滤器添加适当的OSGi配置来完成，该配置：

* 指定可信网站主机名；e `allow.hosts` 或 `allow.hosts.regexp`,
* 授予对此主机名的访问权限。

文件的名称必须为 `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

例如，使用反向链接授予请求的访问权限 `my.domain` 您可以：

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>客户仍有责任：
>
>* 仅授予对受信任域的访问权限
>* 确保不泄露任何敏感信息
>* 不使用通配符 [*] 语法；这将禁用对GraphQL端点的经过身份验证的访问，并向全世界展示该端点。


>[!CAUTION]
>
>所有GraphQL [模式](#schema-generation) (从已 **已启用**)可通过GraphQL端点读取。
>
>这意味着您需要确保没有可用的敏感数据，因为这些数据可能会以这种方式泄露；例如，这包括模型定义中可以显示为字段名称的信息。
