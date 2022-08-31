---
title: AEM as a Cloud Service 团队和产品配置文件
description: 了解AEMas a Cloud Service团队和产品配置文件，以及如何授予和限制对许可Adobe解决方案的访问权限。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: d54c25791cbb06232ff6e24bb7b8005b366a2144
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 3%

---

# AEM as a Cloud Service 团队和产品配置文件 {#product-profiles}

了解AEMas a Cloud Service团队和产品配置文件，以及如何授予和限制对许可Adobe解决方案的访问权限。

## 产品配置文件 {#profiles}

在授予用户访问特定Adobe解决方案的权限时，您不一定希望授予他们完全访问权限。 产品配置文件使每个解决方案都具有其自身的一组用户权限。 这些资源可通过 [Admin Console。](/help/journey-onboarding/admin-console.md)

## AEMas a Cloud Service产品配置文件 {#aem-product-profiles}

AEMas a Cloud Service是一种完全云原生的产品，可将AEM作为服务进行交付。 它以云原生方式提供AEM，并具有诸如始终开启、始终为最新、始终为安全且始终为大规模的新属性。 同时，它保留了AEM作为客户可自定义的平台提供的主要价值主张，并允许企业级团队在其开发和交付过程中进行集成。 请参阅 [Adobe Experience Manager as a Cloud Service简介](/help/overview/introduction.md) 了解有关AEMas a Cloud Service的更多信息。

在入门过程中，您的AEMas a Cloud Service团队成员将通过Admin Console添加并分配到以下一个或多个产品配置文件。

* **AEM管理员**:AEM管理员通常分配给开发人员，特别是需要有权访问（例如）开发环境的开发人员。 AEM管理员的产品配置文件将用于在关联的AEM实例中授予管理员权限。

* **AEM用户**:AEM用户是您组织中通常使用AEMas a Cloud Service创建内容的用户。 这些用户需要访问AEM才能执行其任务。 AEM用户产品配置文件通常分配给创建和审阅内容的AEM内容作者。 此内容可以包含多种类型，如页面、资产、出版物等。 下面显示的AEM用户产品配置文件已分配给这些成员。

![产品配置文件](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>分配给AEMas a Cloud Service产品配置文件的每个用户都具有Cloud Manager的访问权限（只读）。

>[!TIP]
>
>有关载入过程的详细信息，请参阅 [入门历程。](/help/journey-onboarding/overview.md)

## Cloud Manager产品配置文件 {#cloud-manager-product-profiles}

Cloud Manager已预配置了产品配置文件，可将其视为基于角色的权限。 系统管理员负责通过将Cloud Manager团队分配给这些产品配置文件来设置他们。

>[!TIP]
>
>请参阅该文档 [Cloud Manager中基于角色的权限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) 以了解更多详细信息。

每个产品配置文件都具有与其关联的特定权限。

* **业务所有者**  — 在此角色中，您有权添加新程序或编辑程序、添加或更新环境、将代码部署到AEM环境或执行代码质量检查。
* **部署管理器**  — 在此角色中，您有权添加或更新环境、运行任何管道、将代码部署到AEM环境或执行代码质量检查。
* **开发人员**  — 在此角色中，您有权生成个人访问令牌以访问git。
* **项目经理**  — 在此角色中，您有权计划管道、覆盖3层质量门并提供生产批准。

可以将用户分配到多个产品配置文件。 例如，分配两者 **业务所有者** 和 **部署管理** r角色会为用户提供这些权限的总和。

您的Cloud Manager团队将至少包括：

* 一个 **业务所有者**，通常也是系统管理员，并且必须是登录和访问Cloud Manager的第一个人员
* 一个 **部署管理器**
* 一个 **开发人员**

>[!NOTE]
>
>要授予对AEMas a Cloud Service的访问权限，用户必须属于以下两个产品配置文件之一： `AEM Users` 或 `AEM Administrators`. 管理Cloud Manager的权限不够。
