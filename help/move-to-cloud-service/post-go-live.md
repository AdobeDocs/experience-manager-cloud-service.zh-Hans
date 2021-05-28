---
title: 上线后阶段
description: 上线后阶段
exl-id: f9b0b2fa-e29c-4faa-a5e7-e5edd04b25ca
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 73%

---

# 上线后 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="故障诊断AEM"
>abstract="查看持续开发的最佳实践并管理日志，以及诸如开发人员控制台和CRXDE Lite之类的工具，以帮助解决AEM问题"
>additional-url="https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="访问和管理日志"
>additional-url="https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service开发工具"


在上线后阶段，您应确保清理临时文件，审查持续开发的最佳实践并管理日志。

以下工具可用于对 AEM as a Cloud Service 环境进行故障诊断：

* **开发人员控制台**
* **CRX/DE Lite**
* **管理日志**


## 开发人员控制台 {#developer-console}

开发人员控制台中提供了调试 AEM as a Cloud Service 开发人员环境的功能，可用于开发、暂存和生产环境。

请参阅[实施 AEM as a Cloud Service](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools)，了解有关开发工具的更多信息。

## CRX/DE Lite {#crxde-lite}

作为用户，您可以在开发环境中访问 CRX/DE Lite，但不能在暂存或生产环境中访问。

>[!IMPORTANT]
>在运行时写入不可变存储库（例如 `/libs` 和 `/apps`）将会导致错误。此外，作为客户，您将无法访问用于暂存和生产环境的开发人员工具。

请参阅[使用 CRX/DE Lite 进行开发](/help/implementing/developing/tools/crxde.md)，了解如何使用 CRX/DE Lite 来开发 AEM 应用程序。

## 管理日志 {#managing-logs}

用户可以访问选定环境的可用日志文件列表。

请参阅[访问和管理日志](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html)，了解如何通过 UI 或通过 Cloud Manager 从 API 访问和管理日志。

### 其他支持 {#additional-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="帮助和支持"
>abstract="请联系我们的AEM支持团队，以获取说明或解决任何问题。"
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="支持Experience Cloud"

如果您对访问Cloud Service有任何疑问，请联系您的Adobe代表或[Experience Cloud支持](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html)以获取更多详细信息。
