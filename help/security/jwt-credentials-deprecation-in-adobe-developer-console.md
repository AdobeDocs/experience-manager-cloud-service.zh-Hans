---
title: 在 Adobe Developer Console 中弃用 JWT 凭据
description: 了解在 Adobe Developer Console 中弃用 JWT 凭据对 AEM 产生的影响
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: 484ad9721b1b9da95cf3966f139c0f11ff6ea473
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 71%

---

# 在 Adobe Developer Console 中弃用 JWT 凭据 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 客户应参考[本文](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html)了解更多信息。

Adobe 客户使用 [Adobe Developer Console](https://developer.adobe.com/console) 生成通过其可访问各种 API 的凭据。客户可选择从 OAuth 服务器到服务器到单页应用程序的多种凭据类型。已弃用其中一种凭据类型，服务帐户 (JWT) 凭据，改为使用 OAuth 服务器到服务器凭据。2024年6月3日或之后无法创建新服务帐户(JWT)凭据，并且现有JWT凭据在2025年1月27日或之后将无法工作。 可[了解该弃用](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文提供关于 AEM as a Cloud Service 应如何处理该弃用的某些其他背景信息。

目前主要重点是 AEM 功能尚不支持新的 OAuth 服务器到服务器凭据。将很快提供支持 — 最迟在2024年4月下旬，将通过AEMas a Cloud Service的AEM版本提供支持。 您可能已经收到一封电子邮件，其中包含迁移 JWT 凭据的说明，但请放心，您可以且应该推迟凭据迁移，直到 AEM 支持新的 OAuth 服务器到服务器凭据类型。

以下部分列出了客户必须（或在某些情况下不得）使用OAuth服务器到服务器凭据替换其服务帐户(JWT)凭据的情况，一旦AEM在4月下旬支持这些凭据。 [了解如何](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)在未来替换凭据。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)（注意名称中的 **AEM** 区分它与 **Adobe** Developer Console）提供一个实用程序以生成用于服务器到服务器 API 的 [JWT 令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。未弃用并可继续使用这些凭据。


## 将 AEM 与其他 Adobe 解决方案集成 {#integrating-aem-with-other-adobe-solutions}

**操作**：请等待迁移，直到2024年4月下旬AEM支持之后（届时将更新本文）

**相关 AEM 版本**：AEM as a Cloud Service

AEM 客户使用 AEM 创作 UI 配置与所有其他 Adobe 解决方案的集成。例如，Adobe Target、Adobe Analytics、Adobe Launch、AFCS 等解决方案。

![将 AEM 与其他解决方案集成](/help/security/assets/jwt-deprecation.png)

例如，此处就是配置与 Adobe Target 的集成的[说明](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=zh-Hans)。中的API密钥 [在AEM中完成IMS配置](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) 四月下旬AEM支持这些凭据后，应将部分迁移到OAuth服务器到服务器凭据类型。 这些说明将于4月底进行修订，以帮助您应用新的OAuth服务器到服务器凭据。

## Cloud Manager API {#cloud-manager-apis}

**操作**：请等待迁移，直到2024年4月下旬AEM支持之后（届时将更新本文）。

**相关 AEM 版本**：AEM as a Cloud Service

客户创建 Adobe Developer Console 项目，以使其可调用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。一旦 AEM 和 Cloud Manager 支持 OAuth 服务器到服务器凭据类型，即应将 Adobe Developer 项目中的凭据迁移到该类型。

## 自动生成的项目 {#autogen-projects}

**行动**：请勿迁移，因为 Adobe 将代表您进行迁移。

**相关 AEM 版本**：AEM as a Cloud Service。

当 Cloud Manager 预配 AEM as a Cloud Service 环境时，它自动生成一个具有 JWT 凭据的 Adobe Developer Console 项目。此项目被标为只读，如以下屏幕快照中所示。客户无法也不应尝试将这些项目迁移到 OAuth 服务器到服务器凭据；而是 Adobe 将在凭据不再可用之前自行迁移这些项目。

![自动生成的项目](/help/security/assets/jwt-deprecation-autogen-projects.png)
