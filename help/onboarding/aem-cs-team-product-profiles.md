---
title: AEM as a Cloud Service 团队和产品配置文件
description: 了解 AEM as a Cloud Service 团队和产品简介，以及如何授予和限制对您许可的 Adobe 解决方案的访问权限。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: d4786b5d527092027e8e825d0a2475a8be6a710a
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 94%

---

# AEM as a Cloud Service 团队和产品配置文件 {#product-profiles}

了解 AEM as a Cloud Service 团队和产品简介，以及如何授予和限制对您许可的 Adobe 解决方案的访问权限。

## 产品配置文件 {#profiles}

授予用户访问特定 Adobe 解决方案的权限时，您不一定要授予他们完全访问权限。 产品配置文件使每个解决方案都有自己的用户权限集。 可以通过 [Admin Console](/help/journey-onboarding/admin-console.md) 访问这些内容。

## AEM as a Cloud Service 产品配置文件 {#aem-product-profiles}

AEM as a Cloud Service 是一种全云本地服务，将 AEM 作为服务提供。 它以云端原生的方式提供 AEM，具有新的属性，如始终打开、始终最新、始终安全和始终保持规模。 同时，它保留了 AEM 作为可定制平台向客户提供的主要价值主张，并允许企业级团队整合到其开发和交付过程中。 请参阅 [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)，了解有关 AEM as a Cloud Service 的更多信息。

您的 AEM as a Cloud Service 团队成员将在载入期间通过 Admin Console 添加并分配到以下一个或多个产品配置文件。

* **AEM 管理员**：AEM 管理员通常分配给开发人员，尤其是需要访问开发环境的开发人员。例如，开发环境。 AEM 管理员的产品配置文件将用于授予关联 AEM 实例中的管理员权限。

* **AEM 用户**：AEM 用户是您组织中通常使用 AEM as a Cloud Service 来创建内容的用户。 这些用户需要访问 AEM 才能执行任务。 AEM 用户产品配置文件通常分配给创建和审查内容的 AEM 内容作者。 此内容可以是多种类型，例如页面、资产、出版物等。 下面显示的 AEM 用户产品配置文件已分配给这些成员。

![产品配置文件](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>分配给 AEM as a Cloud Service 产品配置文件的每个用户有权（只读）访问 Cloud Manager。 

>[!TIP]
>
>* 要了解有关AEM产品配置文件的更多信息，请参阅此文档 [分配AEM产品配置文件。](/help/journey-onboarding/assign-profiles-aem.md)
>* 有关载入流程的更多信息，请参阅[入门培训历程](/help/journey-onboarding/overview.md)。


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
>* 要了解有关Cloud Manager产品配置文件的更多信息，请参阅此文档 [将团队成员分配给Cloud Manager产品配置文件。](/help/journey-onboarding/assign-profiles-cloud-manager.md)
>* 有关载入流程的更多信息，请参阅[入门培训历程](/help/journey-onboarding/overview.md)。

