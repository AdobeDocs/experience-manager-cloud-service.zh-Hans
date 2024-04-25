---
title: 在 Adobe Developer Console 中弃用 JWT 凭据
description: 了解Adobe Developer控制台中弃用JWT凭据对AEM的影响。
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: b52da0a604d2c320d046136f5e526e2b244fa6cb
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 72%

---

# 在 Adobe Developer Console 中弃用 JWT 凭据 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 客户应参考[本文](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console)了解更多信息。

Adobe 客户使用 [Adobe Developer Console](https://developer.adobe.com/console) 生成通过其可访问各种 API 的凭据。客户可选择从 OAuth 服务器到服务器到单页应用程序的多种凭据类型。已弃用其中一种凭据类型，服务帐户 (JWT) 凭据，改为使用 OAuth 服务器到服务器凭据。从 2024 年 6 月 3 日起无法创建新的服务帐户 (JWT) 凭据，而现有的 JWT 凭据将从 2025 年 1 月 1 日起失效。可[了解该弃用](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文提供关于 AEM as a Cloud Service 应如何处理该弃用的某些其他背景信息。

目前，主要结论是AEM功能尚不支持新的OAuth服务器到服务器凭据。 即将推出对AEMas a Cloud Service的AEM版本的支持，支持截止日期为2024年4月中旬。 您可能已经收到一封电子邮件，其中包含迁移 JWT 凭据的说明，但请放心，您可以且应该推迟凭据迁移，直到 AEM 支持新的 OAuth 服务器到服务器凭据类型。

以下部分列出了在4月中旬得到AEM支持后，客户必须（有时不可以）使用OAuth服务器到服务器凭据替换其服务帐户(JWT)凭据的场景。 [了解如何](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)在未来替换凭据。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)（注意名称中的 **AEM** 区分它与 **Adobe** Developer Console）提供一个实用程序以生成用于服务器到服务器 API 的 [JWT 令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。未弃用并可继续使用这些凭据。


## 将 AEM 与其他 Adobe 解决方案集成 {#integrating-aem-with-other-adobe-solutions}

**操作**：等到 2024 年 4 月下旬之后再进行迁移，届时 AEM 将支持该操作（届时本文将更新）

**相关 AEM 版本**：AEM as a Cloud Service

AEM 客户使用 AEM 创作 UI 配置与所有其他 Adobe 解决方案的集成。例如，Adobe Target、Adobe Analytics、Adobe Launch、AFCS 等解决方案。

![将 AEM 与其他解决方案集成](/help/security/assets/jwt-deprecation.png)

例如，此处就是配置与 Adobe Target 的集成的[说明](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=zh-Hans)。一旦 AEM 在 4 月中旬支持 OAuth 服务器到服务器凭据，即应将[在 AEM 中完成 IMS 配置](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem)部分中的 API 密钥迁移到 OAuth 服务器到服务器凭据类型。这些说明将于4月中旬更新，以帮助您应用新的OAuth服务器到服务器凭据。

## Cloud Manager API {#cloud-manager-apis}

**操作**：等到 2024 年 4 月下旬之后再进行迁移，届时 AEM 将支持该操作（届时本文将更新）。

**相关 AEM 版本**：AEM as a Cloud Service

客户创建 Adobe Developer Console 项目，以使其可调用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。一旦 AEM 和 Cloud Manager 支持 OAuth 服务器到服务器凭据类型，即应将 Adobe Developer 项目中的凭据迁移到该类型。

## 自动生成的项目 {#autogen-projects}

**操作**：不迁移，因为Adobe将代表您迁移。

**相关 AEM 版本**：AEM as a Cloud Service。

当Cloud Manager设置AEMas a Cloud Service环境时，它将使用JWT凭据自动生成一个Adobe Developer控制台项目。 此项目被标为只读，如以下屏幕快照中所示。客户不能也不应尝试将这些项目迁移到OAuth服务器到服务器凭据；相反，在凭据不再可用之前，Adobe将自行迁移这些项目。

![自动生成的项目](/help/security/assets/jwt-deprecation-autogen-projects.png)
