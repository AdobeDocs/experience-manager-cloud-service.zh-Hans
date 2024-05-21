---
title: 为AEMas a Cloud Service设置IMS集成
description: 了解如何为AEMas a Cloud Service设置IMS集成
source-git-commit: 6945980cac24d4413a84343b035a8380b04e7444
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---


# 为AEMas a Cloud Service设置IMS集成 {#setting-up-ims-integrations-for-aemaacs}

>[!NOTE]
>
>不应手动迁移自动设置的JWT配置，因为它们将由Adobe自动处理。

Adobe Experience Manager (AEM) as a Cloud Service可与许多其他Adobe解决方案集成。 例如，Adobe Target、Adobe Analytics等。

这些集成使用通过S2S OAuth配置的IMS集成。

* 创建后：

   * [开发人员控制台中的凭据](#credentials-in-the-developer-console)

* 然后，您可以：

   * 创建（新） [OAuth配置](#creating-oauth-configuration)

   * [将现有JWT配置迁移到OAuth配置](#migrating-existing-JWT-configuration-to-oauth)

>[!CAUTION]
>
>以前，配置使用的是 [现在可在Adobe Developer控制台中弃用的JWT凭据](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md).
>
>此类配置无法再创建或更新，但可以迁移到OAuth配置。

## 开发人员控制台中的凭据 {#credentials-in-the-developer-console}

第一步，您需要在Adobe Developer控制台中配置OAuth凭据。

有关如何执行此操作的详细信息，请参阅开发人员控制台文档，具体取决于您的要求：

* 概述：

   * [服务器到服务器身份验证](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

* 创建新的OAuth凭据：

   * [OAuth服务器到服务器凭据实施指南](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)

* 将现有JWT凭据迁移到OAuth凭据：

   * [从服务帐户(JWT)凭据迁移到OAuth服务器到服务器凭据](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)

例如：

![开发人员控制台中的OAuth凭据](assets/ims-configuration-developer-console.png)

## 创建OAuth配置 {#creating-oauth-configuration}

要使用OAuth创建新的Adobe IMS集成，请执行以下操作：

1. 在AEM中，导航到 **工具**， **安全性**， **Adobe IMS集成**.

1. 选择&#x200B;**创建**。

1. 根据中的详细信息完成配置 [开发人员控制台](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). 例如：

   ![创建OAuth配置](assets/ims-create-oauth-configuration.png)

1. **保存** 您所做的更改。

## 将现有JWT配置迁移到OAuth配置 {#migrating-existing-JWT-configuration-to-oauth}

要基于JWT凭据迁移现有Adobe IMS集成，请执行以下操作：

>[!NOTE]
>
>此示例显示了Launch IMS配置。

1. 在AEM中，导航到 **工具**， **安全性**， **Adobe IMS集成**.

1. 选择需要迁移的JWT配置。 JWT配置标有警告 **JWT凭据（已弃用）**.

1. 选择 **属性**：

   ![选择JWT配置](assets/ims-migrate-jwt-select-configuration.png)

1. 该配置将以只读方式打开：

   ![配置属性 — 只读](assets/ims-migrate-jwt-properties-read-only.png)

1. 选择 **OAuth** 从 **身份验证类型** 下拉列表：

   ![选择身份验证类型](assets/ims-migrate-jwt-authentication-type.png)

1. 将更新可用的属性。 使用开发人员控制台中的详细信息完成它们：

   ![完成OAuth详细信息](assets/ims-migrate-jwt-complete-oauth-details.png)

1. 使用 **保存并关闭** 以保留您的更新。
当您返回到控制台时， **JWT凭据（已弃用）** 警告会消失。