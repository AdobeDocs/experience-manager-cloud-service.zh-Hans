---
title: 使用 AEM Headless 的跨源资源共享 (CORS) 配置
description: Adobe Experience Manager 的跨源资源共享 (CORS) 允许 Headless Web 应用程序对 AEM 发出客户端调用。启用对 GraphQL 端点的访问需要 CORS 配置。
feature: GraphQL API
exl-id: 426be9f9-f44a-4744-ac08-e64bb97308a0
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 100%

---

# 跨源资源共享 (CORS) 配置

>[!NOTE]
>
>有关 AEM 中 CORS 资源共享策略的详细概述，请参阅[了解跨源资源共享 (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=zh-Hans#understand-cross-origin-resource-sharing-(cors))。

要访问 GraphQL 端点，必须配置 CORS 策略并添加到[通过 Cloud Manager 部署到 AEM](/help/implementing/cloud-manager/deploy-code.md) 的 AEM 项目。此操作可通过为所需端点添加相应的 OSGi CORS 配置文件来完成。可以创建多个 CORS 配置并部署到不同环境。在 [WKND 参考网站](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)中可找到示例。

CORS 配置必须指定可信网站源 `alloworigin` 或 `alloworiginregexp`，必须向其授予访问权限。

配置文件的命名必须类似于：`com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json`，其中 `appname` 体现了您应用程序的名称。

例如，要授予对 GraphQL 端点 `/content/cq:graphql/wknd/endpoint` 的访问权限，以及对 `https://my.domain` 的持久查询端点的访问权限，您可以使用：

```json
{
  "supportscredentials":false,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/cq:graphql/wknd/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

如果您已为端点配置虚名路径，还可以在 `allowedpaths` 中使用它。
