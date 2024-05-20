---
title: 在 Adobe Developer Console 中弃用 JWT 凭据
description: 了解在 Adobe Developer Console 中弃用 JWT 凭据对 AEM 产生的影响。
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: b6e26ecaa73aaee37b6b824426dc0cd65d459502
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 62%

---

# 在 Adobe Developer Console 中弃用 JWT 凭据 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 客户应参考[本文](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console)了解更多信息。

Adobe 客户使用 [Adobe Developer Console](https://developer.adobe.com/console) 生成通过其可访问各种 API 的凭据。客户可选择从 OAuth 服务器到服务器到单页应用程序的多种凭据类型。已弃用其中一种凭据类型，服务帐户 (JWT) 凭据，改为使用 OAuth 服务器到服务器凭据。从 2024 年 6 月 3 日起无法创建新的服务帐户 (JWT) 凭据，而现有的 JWT 凭据将从 2025 年 1 月 1 日起失效。可[了解该弃用](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文提供关于 AEM as a Cloud Service 应如何处理该弃用的某些其他背景信息。

主要结论是，AEM现在支持AEMas a Cloud Service的新OAuth服务器到服务器凭据。 您可能已收到一封电子邮件，其中包含迁移JWT凭据的说明，现在可以完成此迁移。

以下部分列出了一些情况，在这些情况中，客户必须（或者在某些情况下，不能）使用OAuth服务器到服务器凭据替换其服务帐户(JWT)凭据，现在AEM支持这些凭据。 [了解如何操作](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) 以迁移凭据。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)（注意名称中的 **AEM** 区分它与 **Adobe** Developer Console）提供一个实用程序以生成用于服务器到服务器 API 的 [JWT 令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。未弃用并可继续使用这些凭据。

## 将 AEM 与其他 Adobe 解决方案集成 {#integrating-aem-with-other-adobe-solutions}

**操作**：迁移您的配置，因为AEM现在支持OAuth凭据。

**相关 AEM 版本**：AEM as a Cloud Service

AEM客户使用AEM来配置与许多其他Adobe解决方案的集成。 例如，Adobe Target、Adobe Analytics等。

请参阅 [为AEMas a Cloud Service设置IMS集成](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) ，以了解如何：

* 使用OAuth凭据创建配置
* 迁移使用JWT凭据创建的配置以使用OAuth凭据

## Cloud Manager API {#cloud-manager-apis}

**操作**：确认何时可以将这些凭据从JWT迁移到OAuth凭据。

**相关 AEM 版本**：AEM as a Cloud Service

客户创建 Adobe Developer Console 项目，以使其可调用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。在弃用的 JWT 凭证于 2025 年 1 月到期之前，Adobe Developer 项目中的凭据应迁移到 OAuth 服务器到服务器凭据类型。

## 自动生成的项目 {#autogen-projects}

**操作**：请勿迁移，因为 Adobe 将会代表您进行迁移。

**相关 AEM 版本**：AEM as a Cloud Service。

当 Cloud Manager 预配 AEM as a Cloud Service 环境时，它自动生成一个具有 JWT 凭据的 Adobe Developer Console 项目。此项目被标为只读，如以下屏幕快照中所示。客户不能也不应尝试将这些项目迁移到OAuth服务器到服务器凭据。 相反，Adobe将在凭据不再可用之前自行迁移这些项目。

![自动生成的项目](/help/security/assets/jwt-deprecation-autogen-projects.png)
