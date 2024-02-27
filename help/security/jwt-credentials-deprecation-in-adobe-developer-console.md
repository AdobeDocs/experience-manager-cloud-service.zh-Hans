---
title: Adobe Developer控制台中的JWT凭据弃用
description: 了解Adobe Developer控制台中弃用JWT凭据对AEM的影响
source-git-commit: e02e38a5267188111f0392a0a5c7b73e6a4f22b5
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Adobe Developer控制台中的JWT凭据弃用 {#jwt-credentials-deprecation-in-adobe-developer-console}

客户使用的Adobe [Adobe Developer控制台](https://developer.adobe.com/console) 生成凭据以启用对各种API的访问。 客户可从各种凭据类型（从OAuth服务器到服务器到单页应用程序）中进行选择。 这些凭据类型之一，服务帐户(JWT)凭据已弃用，推荐使用OAuth服务器到服务器凭据。 无法在2024年5月1日或之后创建新的服务帐户(JWT)凭据，并且现有JWT凭据在2025年1月1日或之后将无法工作。 您可以 [阅读有关弃用的信息](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

本文提供了有关AEMas a Cloud Service和AEM 6.5客户应如何处理弃用的其他上下文。

目前的主要结论是，AEM功能尚不支持新的OAuth服务器到服务器凭据。 支持即将推出 — 到2024年4月中旬，通过AEMas a Cloud Service的AEM版本，以及针对AEM 6.5安装的特殊兼容包，如果您运行的是最新的Service Pack 20或更低版本（Service Pack 21及更高版本将自动包含该版本）。 您可能已收到一封电子邮件，其中包含迁移JWT凭据的说明，但请放心，您可以也应该推迟凭据迁移，直到AEM支持新的OAuth服务器到服务器凭据类型。

以下部分列出了客户必须（或在某些情况下不得）使用OAuth服务器到服务器凭据替换其服务帐户(JWT)凭据的情况，一旦AEM在4月中旬支持这些凭据。 [了解如何操作](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) 以便将来替换凭据。

>[!NOTE]
>
>此 [**AEM** 开发人员控制台](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (请注意 **AEM** 在名称中，以将其与 **Adobe** 开发人员控制台)提供用于生成 [JWT令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 用于服务器到服务器API。 这些凭据未弃用，可以继续使用。


## 将AEM与其他Adobe解决方案集成 {#integrating-aem-with-other-adobe-solutions}

**操作**：请等待到2024年4月中旬之后再进行迁移，当时AEM支持该功能。

**相关AEM版本**：AEMas a Cloud Service，并AdobeManaged Services（Service Pack 20及更低版本）。


AEM客户使用AEM创作UI来配置与所有其他Adobe解决方案的集成。 例如，Adobe Target、Adobe Analytics、Adobe发布、AFCS等。

![将AEM与其他解决方案集成](/help/security/assets/jwt-deprecation.png)

例如，以下是 [说明](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=en) 用于配置与Adobe Target的集成。 中的API密钥 [在AEM中完成IMS配置](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) 一旦AEM在4月中旬支持这些凭据，应将部分迁移到OAuth服务器到服务器凭据类型。 这些说明将于4月中旬更新，以帮助您应用新的OAuth服务器到服务器凭据。

## Cloud Manager API {#cloud-manager-apis}

**操作**：请等待到2024年4月中旬之后再进行迁移，当时AEM支持该功能。

**相关AEM版本**：AEMas a Cloud Service，并AdobeManaged Services（Service Pack 20及更低版本）。

客户创建Adobe Developer Console项目以便调用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). 在AEM和Cloud Manager支持后，Adobe Developer项目中的凭据应迁移到OAuth服务器到服务器凭据类型。

## 自动生成的项目 {#autogen-projects}

**操作**：不迁移，因为Adobe将代表您迁移。

**相关AEM版本**：仅AEMas a Cloud Service。

当Cloud Manager设置AEMas a Cloud Service环境时，它使用JWT凭据自动生成Adobe Developer控制台项目。 此项目被标记为只读，如下面的屏幕快照所示。 客户不能也不应尝试将这些项目迁移到OAuth服务器到服务器凭据；相反，在凭据不再可用之前，Adobe将自行迁移这些项目。

![自动生成的项目](/help/security/assets/jwt-deprecation-autogen-projects.png)

