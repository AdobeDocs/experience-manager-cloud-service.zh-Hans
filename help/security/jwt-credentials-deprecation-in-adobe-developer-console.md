---
title: 在 Adobe Developer Console 中弃用 JWT 凭据
description: 了解在 Adobe Developer Console 中弃用 JWT 凭据对 AEM 产生的影响
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: 62be3c6e98df9002cdfbeef50dd5475c4daa1576
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 87%

---

# 在 Adobe Developer Console 中弃用 JWT 凭据 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5客户应参考 [本文](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) 以了解更多信息。

Adobe 客户使用 [Adobe Developer Console](https://developer.adobe.com/console) 生成通过其可访问各种 API 的凭据。客户可选择从 OAuth 服务器到服务器到单页应用程序的多种凭据类型。已弃用其中一种凭据类型，服务帐户 (JWT) 凭据，改为使用 OAuth 服务器到服务器凭据。从 2024 年 5 月 1 日起无法创建新的服务帐户 (JWT) 凭据，而现有的 JWT 凭据将从 2025 年 1 月 1 日起失效。可[了解该弃用](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文提供了有关AEMas a Cloud Service应如何处理弃用的其他上下文。

目前主要的重点是 AEM 功能尚不支持新的 OAuth 服务器到服务器凭据。将很快提供支持 — 在2024年4月中旬之前通过AEMas a Cloud Service的AEM版本提供支持。 您可能已经收到一封电子邮件，其中包含迁移 JWT 凭据的说明，但请放心，您可以且应该推迟凭据迁移，直到 AEM 支持新的 OAuth 服务器到服务器凭据类型。

在以下部分中列出的场景中，一旦 AEM 在 4 月中旬支持 OAuth 服务器到服务器凭据，客户就必须（或在某些情况下不得）将其服务帐户 (JWT) 凭据替换为这些凭据。[了解如何](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)在未来替换凭据。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)（注意名称中的 **AEM** 区分它与 **Adobe** Developer Console）提供一个实用程序以生成用于服务器到服务器 API 的 [JWT 令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。未弃用并可继续使用这些凭据。


## 将 AEM 与其他 Adobe 解决方案集成 {#integrating-aem-with-other-adobe-solutions}

**行动**：等到 2024 年 4 月中旬后再迁移，届时 AEM 将支持它。

**相关AEM版本**：AEMas a Cloud Service

AEM 客户使用 AEM 创作 UI 配置与所有其他 Adobe 解决方案的集成。例如，Adobe Target、Adobe Analytics、Adobe Launch、AFCS 等解决方案。

![将 AEM 与其他解决方案集成](/help/security/assets/jwt-deprecation.png)

例如，此处就是配置与 Adobe Target 的集成的[说明](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=zh-Hans)。一旦 AEM 在 4 月中旬支持 OAuth 服务器到服务器凭据，即应将[在 AEM 中完成 IMS 配置](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem)部分中的 API 密钥迁移到 OAuth 服务器到服务器凭据类型。4 月中旬将更新和修订这些说明以帮助您应用新的 OAuth 服务器到服务器凭据。

## Cloud Manager API {#cloud-manager-apis}

**行动**：等到 2024 年 4 月中旬后再迁移，届时 AEM 将支持它。

**相关AEM版本**：AEMas a Cloud Service

客户创建 Adobe Developer Console 项目，以使其可调用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。一旦 AEM 和 Cloud Manager 支持 OAuth 服务器到服务器凭据类型，即应将 Adobe Developer 项目中的凭据迁移到该类型。

## 自动生成的项目 {#autogen-projects}

**行动**：请勿迁移，因为 Adobe 将代表您进行迁移。

**相关AEM版本**：AEMas a Cloud Service。

当 Cloud Manager 预配 AEM as a Cloud Service 环境时，它自动生成一个具有 JWT 凭据的 Adobe Developer Console 项目。此项目被标为只读，如以下屏幕快照中所示。客户无法也不应尝试将这些项目迁移到 OAuth 服务器到服务器凭据；而是 Adobe 将在凭据不再可用之前自行迁移这些项目。

![自动生成的项目](/help/security/assets/jwt-deprecation-autogen-projects.png)
