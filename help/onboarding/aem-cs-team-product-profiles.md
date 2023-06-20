---
title: AEM as a Cloud Service 团队和产品配置文件
description: 了解 AEM as a Cloud Service 团队和产品配置文件可怎样准许和限制访问您已许可的 Adobe 解决方案。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 94%

---

# AEM as a Cloud Service 团队和产品配置文件 {#product-profiles}

了解 AEM as a Cloud Service 团队和产品配置文件可怎样准许和限制访问您已许可的 Adobe 解决方案。

## 产品配置文件 {#profiles}

授予用户访问特定 Adobe 解决方案的权限时，您不一定要授予他们完全访问权限。 产品配置文件使每个解决方案都有自己的用户权限集。 可以通过 [Admin Console](/help/journey-onboarding/admin-console.md) 访问这些内容。

## AEM as a Cloud Service 产品配置文件 {#aem-product-profiles}

AEM as a Cloud Service 是一种全云本地服务，将 AEM 作为服务提供。 它以云端原生的方式提供 AEM，具有新的属性，如始终打开、始终最新、始终安全和始终保持规模。 同时，它保留了 AEM 作为可定制平台向客户提供的主要价值主张，并允许企业级团队整合到其开发和交付过程中。 请参阅 [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)，了解有关 AEM as a Cloud Service 的更多信息。

在新用户引导期间，您的AEMas a Cloud Service团队成员将通过Admin Console添加并分配到以下一个或多个产品配置文件。

* **AEM 管理员**：AEM 管理员通常分配给开发人员，尤其是需要访问开发环境的开发人员。例如，开发环境。 AEM管理员的产品配置文件用于在关联的AEM实例中授予管理员权限。

* **AEM 用户**：AEM 用户是您组织中通常使用 AEM as a Cloud Service 来创建内容的用户。 这些用户需要访问 AEM 才能执行任务。 AEM 用户产品配置文件通常分配给创建和审查内容的 AEM 内容作者。 此内容可以是多种类型，例如页面、资产、出版物等。 下面显示的 AEM 用户产品配置文件已分配给这些成员。

![产品配置文件](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>每个分配给 AEM as a Cloud Service 产品配置文件的用户都只能通过 **Cloud Manager 用户**&#x200B;角色只读地访问 Cloud Manager。
>
>仅有 **Cloud Manager 用户**&#x200B;角色的用户可登录到 Cloud Manager 并使用&#x200B;**项目**&#x200B;菜单选项导航到 AEM 作者环境（如果存在这些环境）。**Cloud Manager 用户**&#x200B;角色不足以访问项目详细信息。如果需要此类访问，则必须由系统管理员为用户授予其他角色。

>[!WARNING]
>
>不得更改 **AEM 管理员**&#x200B;产品配置文件名称。更改 **AEM 管理员**&#x200B;产品配置文件的名称将让所有分配给该配置文件的用户失去管理员权限。

>[!TIP]
>
>* 要详细了解 AEM 产品配置文件，请参阅文档[分配 AEM 产品配置文件](/help/journey-onboarding/assign-profiles-aem.md)。
>* 有关入门过程的详细信息，请参阅[入门历程](/help/journey-onboarding/overview.md)。

## Cloud Manager 产品配置文件 {#cloud-manager-product-profiles}

Cloud Manager 具有预配置的产品配置文件，可以将其视为基于角色的权限。 您的系统管理员负责通过将 Cloud Manager 团队分配给这些产品配置文件来进行设置。

>[!TIP]
>
>有关更多详细信息，请参阅文档 [Cloud Manager 中基于角色的权限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)。

每个产品配置文件都具有与其关联的特定权限。

* **业务负责人** – 在此角色中，您有权添加新程序或编辑程序、添加或更新环境、将代码部署到 AEM 环境或执行代码质量检查。
* **部署管理员** – 在此角色中，您有权添加或更新环境，运行任何管道，并将代码部署到 AEM 环境，或执行代码质量检查。
* **开发人员** – 在此角色中，您有权生成个人访问令牌以访问 git。
* **程序管理员** – 在此角色中，您有权计划管道、覆盖三层质量关卡并提供生产批准。

一个用户可以分配给多个产品配置文件。 例如，将&#x200B;**业务负责人**&#x200B;和&#x200B;**部署管理员**&#x200B;角色分配给用户，可以为他们提供所有这些权限。

您的 Cloud Manager 团队至少包括：

* 一位&#x200B;**业务负责人**，通常也是系统管理员，必须是第一个登录和访问 Cloud Manager 的人
* 一位&#x200B;**部署管理员**
* 一位&#x200B;**开发人员**

>[!NOTE]
>
>要被授予 AEM as a Cloud Service 访问权限，用户必须属于以下两种产品配置文件之一：`AEM Users` 或 `AEM Administrators`。 管理 Cloud Manager 的权限不够。

>[!TIP]
>
>* 要详细了解 Cloud Manager 产品配置文件，请参阅文档[将团队成员分配到 Cloud Manager 产品配置文件](/help/journey-onboarding/assign-profiles-cloud-manager.md)。
>* 有关入门过程的详细信息，请参阅[入门历程](/help/journey-onboarding/overview.md)。
