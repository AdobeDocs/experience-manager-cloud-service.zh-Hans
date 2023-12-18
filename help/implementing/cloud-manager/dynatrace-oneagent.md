---
title: Dynatrace OneAgent
description: 了解如何将Dynatrace的OneAgent与AEMas a Cloud Service结合使用
source-git-commit: 2e70c8be73915bea860b98e02c08772bb4f5dcd2
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Dynatrace OneAgent {#dynatrace-oneagent}

通过Adobe，您可以使用Dynatrace的OneAgent在企业部署过程中监控AEMas a Cloud Service，确定任何潜在问题的原因，并根据需要采取措施进行补救。 <!-- When GA, add: Read this [Dynatrace article](https://www.dynatrace.com/hub/detail/adobe-experience-manager/) about AEM monitoring to learn more. -->

## 将OneAgent与AEMas a Cloud Service集成 {#integrating-oneagent-with-aem-as-a-cloud-service}

Dynatrace OneAgent客户可通过客户支持票证请求连接，从而监控其AEM使用情况。

连接请求所需的详情描述如下：

| **字段** | **描述** |
|---|---|
| Dynatrace环境URL | Dynatrace环境URL。<br><br>对于Dynatrace SaaS客户，格式为 `https://<environment>.live.dynatrace.com`.<br><br>对于Dynatrace Managed客户，格式为 `https://<your-managed-url>/e/<environmentId>` |
| 动态环境ID | 您的Dynatrace环境ID，可在环境URL中找到 |
| Dynatrace环境令牌 | 您的OneAgent环境令牌。 请参阅Dynatrace文档以了解如何创建此项。<br><br>这应被视为机密，因此请使用适当的安全做法。 例如，密码可以在网站上对其进行保护，例如 **zerobin.net**，客户支持工单可以引用该文件以及密码。 |
| Dynatrace API访问令牌 | Dynatrace环境的API访问令牌。 请参阅Dynatrace文档以了解如何创建此项。<br><br>这应被视为机密，因此请使用适当的安全做法。 例如，密码可以在网站上对其进行保护，例如 **zerobin.net**，客户支持工单可以引用该文件以及密码。<br><br>注意：只有Dynatrace Managed才需要此项。 |
| Dynatrace目标端口 | Dynatrace目标端口。<br><br>注意：只有Dynatrace Managed才需要此项。 |
| AEM环境Id | 供Dynatrace监控的AEM环境ID。 |


