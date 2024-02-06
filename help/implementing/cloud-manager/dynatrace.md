---
title: Dynatrace
description: 了解如何将Dynatrace与AEMas a Cloud Service配合使用
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
source-git-commit: fec3aa6debec49014406ab241c3ce0338ec5a1d2
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

通过Adobe，您可以使用Dynatrace在企业部署过程中监控AEMas a Cloud Service，确定任何潜在问题的原因，并根据需要采取措施进行补救。

使用Dynatrace，您可以获得所有AEM应用程序的无缝可观察性。 Dynatrace通过自动检测您的AEM应用程序并将其从网站到容器的依赖项可视化到云服务，提供了对最终用户体验的全面可视性。 与所有层的端到端跟踪和Real User Monitoring相结合，将您的AEM内容引导型体验提升到新的水平，没有差距或盲点。 如果出现任何异常，Dynatrace会使用Davis AI引擎实时诊断它们，并在客户受到影响之前查明代码中断的根本原因，从而最大限度地缩短平均修复时间。

要了解有关Dynatrace的更多信息，请参阅 [AdobeAEM Cloud Service集成](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![AEM作者和发布者性能指标](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## 将Dynatrace与AEMas a Cloud Service集成 {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatrace客户可通过客户支持票证请求连接，从而监控其AEM环境。

连接请求所需的详情描述如下：

| **字段** | **描述** |
|---|---|
| [!DNL Dynatrace Environment URL] | Dynatrace环境URL。<br><br>对于Dynatrace SaaS客户，格式为 `https://<your-environment-id>.live.dynatrace.com`.<br><br>对于Dynatrace Managed客户，格式为 `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | 您的动态环境ID。 请参阅 [获取Dynatrace环境信息](#get-dynatrace-env-info) 知道怎么拿到这个。 |
| [!DNL Dynatrace Environment Token] | 您的Dynatrace环境标记。 请参阅 [获取Dynatrace环境信息](#get-dynatrace-env-info) 知道怎么拿到这个。<br><br>这应被视为机密，因此请使用适当的安全做法。 例如，密码可以在网站上对其进行保护，例如 **zerobin.net**，客户支持工单可以引用该文件以及密码。 |
| [!DNL Dynatrace API access token] | Dynatrace环境的API访问令牌。  请参阅 [创建Dynatrace API访问令牌](#create-dynatrace-access-token) 以了解如何创建此项。<br><br>这应被视为机密，因此请使用适当的安全做法。 例如，密码可以在网站上对其进行保护，例如 **zerobin.net**，客户支持工单可以引用该文件以及密码。<br><br>注意：只有Dynatrace Managed才需要此项。 |
| [!DNL Dynatrace ActiveGate Port] | AEM集成应连接到的Dynatrace ActiveGate端口。<br><br>注意：只有Dynatrace Managed才需要此项。 |
| [!DNL Dynatrace ActiveGate Network Zone] | 您的 [Dynatrace ActiveGate网络区域](https://docs.dynatrace.com/docs/manage/network-zones) 在数据中心和网络区域之间高效地路由AEM监控数据。<br><br>注意：Dynatrace ActiveGate网络区域是可选的。 |
| [!DNL AEM Environment ID(s)] | 供Dynatrace监控的AEM环境ID。 |

>[!NOTE]
>
>一旦集成了Dynatrace，数据将不再流向其他APM工具，例如New Relic（如果之前启用了它）。


## 创建Dynatrace API访问令牌 {#create-dynatrace-access-token}

1. 登录Dynatrace环境。
1. 在 [!DNL Dynatrace] 菜单，转到 [!DNL Manage] > [!DNL Access tokens].
1. 选择 [!DNL Generate new token].
1. 定义 [!DNL token name].

1. 可选：设置 [!DNL expiration date]. 请确保在令牌过期之前生成新令牌。
1. 设置 [!DNL token scope] 到 [!DNL PaaS integration - Installer download]
1. 选择 [!DNL Generate token].
1. 复制生成的访问令牌并将其存储在安全位置。


## 获取Dynatrace环境信息 {#get-dynatrace-env-info}

1. 对Dynatrace环境执行以下API请求：

`curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"`

替换\&lt;environmenturl> 包含您的Dynatrace环境URL和\&lt;accesstoken> 使用您创建的API访问令牌。

1. 复制\&lt;environmentid> 和\&lt;environmenttoken> 并将它们存储在安全位置。

```
{
   "tenantUUID": "<environmentId>",
   "tenantToken": "<environmentToken>",
   "communicationEndpoints": [
   ... 
   ],
   "formattedCommunicationEndpoints": "<endpoints>" 
}
```


