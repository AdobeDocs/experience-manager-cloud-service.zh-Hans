---
title: AEMas a Cloud Service团队和产品配置文件
description: 可查看本页以了解AEMas a Cloud Service团队和产品配置文件。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: fd23701414a2ae4142ea2a11cef92bc0cb202421
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# AEMas a Cloud Service团队和产品配置文件 {#product-profiles}

## 产品配置文件 {#profiles}

在授予用户访问特定Adobe解决方案的权限时，您不一定希望授予他们完全访问权限。 产品配置文件使每个解决方案都具有自己的一组用户权限。 这些资源可通过 [Adobe Admin Console](/help/onboarding/learn-concepts/admin-console.md).

有关更多信息 [AEMas a Cloud Service产品配置文件](#aem-product-profiles) 和 [Cloud Manager产品配置文件](#cloud-manager-product-profiles) 了解在您的团队设置时，这些组件如何协同工作。

## AEMas a Cloud Service产品配置文件 {#aem-product-profiles}

AEMas a Cloud Service是完全云原生的产品，可将AEM作为服务进行交付。 它以云原生方式提供AEM，并具有诸如始终开启、始终为最新、始终为安全且始终为大规模的新属性。 同时，它保留了AEM作为客户可自定义的平台提供的主要价值主张，并允许企业级团队在其开发和交付过程中进行集成。 请参阅 [Adobe Experience Manager as a Cloud Service简介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en) 了解有关AEMas a Cloud Service的更多信息。

在入门过程中，您的AEMas a Cloud Service团队成员将通过Admin Console添加并分配到以下一个或多个产品配置文件。

* **AEM管理员**:AEM管理员通常会分配给开发人员，特别是需要有权访问（例如）开发环境的开发人员。 AEM管理员产品配置文件将用于在关联的AEM实例中授予管理员权限。

* **AEM用户**:AEM用户是指您组织中在与Adobe的协议中使用AEMas a Cloud Service的用户。 这些成员需要访问AEM才能执行其任务。 AEM用户产品配置文件通常分配给创建和审阅内容的AEM内容作者(这可以是几种类型；（例如，页面、资产、出版物等）。 下面显示的AEM用户产品配置文件已分配给这些成员。

   ![](/help/onboarding/learn-concepts/assets/admin-console-profiles.png)

   >[!NOTE]
   >分配给AEMas a Cloud Service产品配置文件的每个用户都具有Cloud Manager的访问权限（只读）。

## Cloud Manager产品配置文件 {#cloud-manager-product-profiles}

Cloud Manager已预配置了产品配置文件，或者更简单的，基于角色的权限。 系统管理员将负责通过将Cloud Manager团队分配给这些产品配置文件来设置他们，并且必须熟悉这些产品配置文件以及要为其分配的团队成员。
>[!NOTE]
>请参阅 [Cloud Manager中基于角色的权限](/help/onboarding/learn-concepts/cloud-manager-introduction.md##role-based-permissions) 以了解更多详细信息。

每个产品配置文件都具有与其关联的特定权限。 例如，如果您的角色是：

* **业务所有者**，则您有权添加新程序或编辑程序、添加或更新环境、添加/编辑/删除管道并运行任何管道，以及将代码部署到AEM环境或代码质量。

* **部署管理器**，则您有权添加或更新环境、运行任何管道，以及将代码部署到AEM环境或代码质量。

* **开发人员**，则您有权生成访问Git的个人访问令牌。

* **项目经理**，则您有权计划管道、覆盖3层质量门并提供生产批准。

可以将用户分配到多个产品配置文件。 例如，将业务所有者和部署管理员角色分配给用户，可为其提供这些权限的组合或总和。

您的Cloud Manager团队将至少包括：

* 一位业务所有者（通常也是系统管理员）必须是登录和访问Cloud Manager的第一个人员
* 一个部署管理器
* 一名开发人员

   >[!NOTE]
   >要授予对AEMas a Cloud Service的访问权限，用户必须属于以下两个产品配置文件之一： `AEM Users` 或 `AEM Administrators`. 您必须被授予实例的权限，但管理关联的Cloud Manager的权限是不够的。
