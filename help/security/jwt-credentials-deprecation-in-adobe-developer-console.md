---
title: 在 Adobe Developer Console 中弃用 JWT 凭据
description: 了解在 Adobe Developer Console 中弃用 JWT 凭据对 AEM 产生的影响。
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
feature: Security
role: Admin
source-git-commit: 957dedd81d14e921aa8a64de80ef21fd11f713ab
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 93%

---

# 在 Adobe Developer Console 中弃用 JWT 凭据 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 客户应参考 [AEM 6.5 的类似文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console)了解更多信息。

Adobe 客户使用 [Adobe Developer Console](https://developer.adobe.com/console) 生成通过其可访问各种 API 的凭据。客户可选择从 OAuth 服务器到服务器到单页应用程序的多种凭据类型。已弃用其中一种凭据类型，服务帐户 (JWT) 凭据，改为使用 OAuth 服务器到服务器凭据。无法在2024年6月3日或之后创建新的服务帐户(JWT)凭据，并且现有的JWT凭据在2025年6月30日或之后将无法工作。 可[了解该弃用](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文提供关于 AEM as a Cloud Service 应如何处理该弃用的某些其他背景信息。

重点在于，AEM 现支持 AEM as a Cloud Service 的新 OAuth 服务器到服务器凭据。您可能已经收到一封关于迁移 JWT 凭据的说明邮件，现在可以进行迁移了。

在以下部分中列出的场景中，既然 AEM 支持 OAuth 服务器到服务器凭据，客户就必须（或在某些情况下不得）将其服务帐户 (JWT) 凭据替换为这些凭据。[了解如何](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)迁移凭据。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)（注意名称中的 **AEM** 区分它与 **Adobe** Developer Console）提供一个实用程序以生成用于服务器到服务器 API 的 [JWT 令牌](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。未弃用并可继续使用这些凭据。

## 将 AEM 与其他 Adobe 解决方案集成 {#integrating-aem-with-other-adobe-solutions}

**操作**：由于 AEM 现支持 OAuth 凭据，请迁移您的配置。

**相关 AEM 版本**：AEM as a Cloud Service

AEM 客户使用 AEM 配置与许多其他 Adobe 解决方案的集成。例如，Adobe Target、Adobe Analytics 等。

请参阅[为 AEM as a Cloud Service 设置 IMS 集成](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md)，详细了解如何执行以下操作：

* 使用 OAuth 凭据创建配置
* 将使用 JWT 凭据创建的配置迁移到使用 OAuth 凭据

## Cloud Manager API {#cloud-manager-apis}

**操作**：将您的 JWT 凭据迁移到 OAuth 凭据，Cloud Manager 现在支持该凭据。

**相关 AEM 版本**：AEM as a Cloud Service

客户创建 Adobe Developer Console 项目，以使其可调用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。在弃用的JWT凭据于2025年6月过期之前，Adobe Developer项目中的凭据应迁移到OAuth服务器到服务器凭据类型。

## 自动生成的项目 {#autogen-projects}

**操作**：请勿迁移，因为 Adobe 将会代表您进行迁移。

**相关 AEM 版本**：AEM as a Cloud Service。

当 Cloud Manager 预配 AEM as a Cloud Service 环境时，它自动生成一个具有 JWT 凭据的 Adobe Developer Console 项目。此项目被标为只读，如以下屏幕快照中所示。客户不能也不应该尝试将这些项目迁移到 OAuth 服务器到服务器凭据。相反，Adobe 将在凭据不再可用之前自行迁移这些项目。

![自动生成的项目](/help/security/assets/jwt-deprecation-autogen-projects.png)

## 自动生成的项目常见问题解答 {#autogen-projects-faqs}

本节提供有关 AEM as a Cloud Service 中自动生成项目 JWT 凭据弃用的最常见问题解答。

**如何知道哪些项目是自动生成的？**

导航至“Adobe Developer Console | 项目”部分。AEM as a Cloud Service 自动生成的项目将有一个带有“自动生成”标识符的锁定图标。自动生成的项目遵循 AEM-p#####-e###### 格式，由技术帐户用户创建。

![自动生成的项目](/help/security/assets/jwt-alert.png)

**如果我们自动生成的项目遇到问题该怎么办？**

联系 [Adobe 客户关怀](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html) 

**应该继续迁移我们自动生成的项目吗？**

无需进行任何操作，因为 Adobe 将代表您迁移 AEM 版本 17258（2024 年 8 月发行）及更高版本环境中的自动生成项目。

**迁移自动生成项目的时间线是什么？**

Adobe 将于 2025 年第一季度启动分阶段迁移方法，从开发环境开始迁移。

**如果我们的 AEM 版本早于 AEM 版本 17258（2024 年 8 月发行），AEM as a Cloud Service 实例将受到怎样的影响？**

如果自动生成的项目集成未在 2025 年 6 月之前迁移到 OAuth，则将停止工作。

要确保顺利过渡，客户应立即联系 [Adobe 客户关怀](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)，开始更新至[最新的 AEM 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/release-notes/maintenance/latest)。这将为回归测试提供充足的时间，并允许 Adobe 有效地管理项目的迁移。

**是否可以在不升级 AEM as a Cloud Service AEM 版本的情况下升级到受支持的 OAuth 版本？**

不行。要确保顺利过渡，客户应立即联系 [Adobe 客户关怀](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)，开始更新至[最新的 AEM 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/release-notes/maintenance/latest)。这将为回归测试提供充足的时间，并允许 Adobe 有效地管理项目的迁移。
