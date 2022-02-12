---
title: 使用AEM无头的跨源资源共享(CORS)配置
description: Adobe Experience Manager的跨域资源共享(CORS)允许无头Web应用程序对AEM进行客户端调用。 需要CORS配置才能访问GraphQL端点。
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# 跨源资源共享(CORS)配置

>[!NOTE]
>
>有关AEM中CORS资源共享策略的详细概述，请参阅 [了解跨源资源共享(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

要访问GraphQL端点，必须配置CORS策略并将其添加到以下AEM项目： [通过Cloud Manager部署到AEM](/help/implementing/cloud-manager/deploy-code.md). 这是通过为所需端点添加相应的OSGi CORS配置文件来完成的。 可以创建多个CORS配置并将其部署到不同的环境。 示例可在 [WKND参考站点](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

CORS配置必须指定受信任的网站源 `alloworigin` 或 `alloworiginregexp` 必须授予其访问权限。

配置文件的名称必须如下： `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` where `appname` 反映您的应用程序的名称。

例如，授予对GraphQL端点的访问权限 `/content/cq:graphql/wknd/endpoint` 和保留的查询端点 `https://my.domain` 您可以使用：

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

如果您为端点配置了虚路径，则还可以在 `allowedpaths`.


