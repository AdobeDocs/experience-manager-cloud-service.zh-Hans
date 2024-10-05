---
title: Dynatrace
description: 了解如何将Dynatrace与AEM as a Cloud Service结合使用
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

通过Adobe，能够使用Dynatrace在企业部署过程中监控AEM as a Cloud Service，确定任何潜在问题的原因，并根据需要采取措施进行补救。

使用Dynatrace，您可以获得所有AEM应用程序的无缝可观察性。 Dynatrace通过自动检测您的AEM应用程序并将其从网站到容器到Cloud Service的依赖项可视化，提供了对最终用户体验的全面可视性。 与所有层的端到端跟踪和实时监控相结合，将您的AEM内容引导型体验提升到新的水平，不存在空白或盲点。 如果出现任何异常，Dynatrace会使用Davis AI引擎实时诊断它们，并在客户受到影响之前将根本原因归结为代码损坏，从而最大限度地缩短平均修复时间。

要进一步了解Dynatrace，请参阅[AdobeAEM Cloud Service集成](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/)。

![AEM作者和发布者性能指标](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## 将Dynatrace与AEM as a Cloud Service集成 {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatrace客户可通过客户支持票证请求连接，从而监控其AEM环境。

连接请求所需的详情描述如下：

| **字段** | **描述** |
|---|---|
| [!DNL Dynatrace Environment URL] | Dynatrace环境URL。<br><br>对于Dynatrace SaaS客户，格式为`https://<your-environment-id>.live.dynatrace.com`。<br><br>对于Dynatrace托管客户，格式为`https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | 您的Dynatrace环境ID。 请参阅[如何获取Dynatrace连接详细信息？](#how-do-i-get-my-dynatrace-connection-details)以了解如何获取此项。 |
| [!DNL Dynatrace Environment Token] | 您的Dynatrace环境令牌。 请参阅[如何获取Dynatrace连接详细信息？](#how-do-i-get-my-dynatrace-connection-details)以了解如何获取此项。<br><br>这应视为机密，因此请使用适当的安全做法。 例如，密码可在客户支持票证可以引用的&#x200B;**zerobin.net**&#x200B;等网站中保护该密码以及密码。 |
| [!DNL Dynatrace API access token] | Dynatrace环境的API访问令牌。 请参阅[创建Dynatrace API访问令牌](#create-dynatrace-access-token)以了解如何创建该令牌。<br><br>这应视为机密，因此请使用适当的安全做法。 例如，密码可在客户支持票证可以引用的&#x200B;**zerobin.net**&#x200B;等网站中保护该密码以及密码。<br><br>注意：只有Dynatrace Managed才需要此项。 |
| [!DNL Dynatrace ActiveGate Port] | AEM集成应连接到的Dynatrace ActiveGate端口。<br><br>注意：只有Dynatrace Managed才需要此项。 |
| [!DNL Dynatrace ActiveGate Network Zone] | 您的[Dynatrace ActiveGate网络区域](https://docs.dynatrace.com/docs/manage/network-zones)可在数据中心和网络区域之间高效地路由AEM监控数据。<br><br>注意：Dynatrace ActiveGate网络区域是可选的。 |
| [!DNL AEM Environment ID(s)] | Dynatrace要监视的AEM环境ID。 |

>[!NOTE]
>
>集成Dynatrace后，数据将不再流向其他APM工具，例如New Relic（如果之前启用了它）。

## 常见问题解答 {#faq}

### Dynatrace AEM Monitoring需要哪个许可证？ {#which-license-do-i-need-for-AEM-monitoring}

Dynatrace AEM监控需要Dynatrace许可证。 Dynatrace AEM许可基于[对Kubernetes容器的全栈监视](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring)。 自动检测受监视的AEM容器（创作和发布者服务）的内存大小。

每个AEM环境的Adobe部署规范包括：

* 生产：平均4个容器，每个容器16 GB内存
* 非生产：平均4个容器，每个容器8 GB内存

要了解有关Dynatrace授权的更多信息，请参阅[Dynatrace平台订阅](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription)。

### 如何获取Dynatrace连接详细信息？ {#how-do-i-get-my-dynatrace-connection-details}

1. 对您的Dynatrace环境执行以下API请求：

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   将`<environmentUrl>`替换为您的Dynatrace环境URL，将`<accessToken>`替换为您创建的API访问令牌。

1. 从响应有效负载中复制`<environmentId>`和`<environmentToken>`并将其存储在安全位置。

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### 创建Dynatrace API访问令牌 {#create-dynatrace-access-token}

1. 登录到Dynatrace环境。
1. 转到&#x200B;**[!DNL Access tokens]**&#x200B;并选择&#x200B;**[!DNL Generate new token]**。
1. 定义[!DNL token name]。
1. 将令牌范围设置为&#x200B;**[!DNL PaaS integration - Installer download]**。
1. 选择&#x200B;**[!DNL Generate token]**。
1. 复制生成的访问令牌并将其存储在安全位置。





