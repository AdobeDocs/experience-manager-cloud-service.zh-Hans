---
title: AEM as a Team和Cloud Service配置文件
description: 请阅读本页，了解AEM as a Team和Product Profiles。
source-git-commit: 312b1ce7dc660d1bb4fe199be0e7403069d30161
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---


# AEM as a Team和产品配置文件{#product-profiles}

AEM as a Cloud Service是完全云原生的产品，可将AEM作为服务进行交付。 它以云原生方式提供AEM，并具有诸如始终开启、始终为最新、始终为安全且始终为大规模的新属性。 同时，它保留了AEM作为客户可自定义的平台提供的主要价值主张，并允许企业级团队在其开发和交付过程中进行集成。 请参阅[Adobe Experience Manager as aCloud Service简介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en) ，了解有关AEM as aCloud Service的更多信息。

在入门过程中，您的AEM as a Analytics团队成员将通过Admin Console添加并分配到以下一个或多个产品配置文件。


## AEM as a Cloud Service产品配置文件{#aem-product-profiles}

AEM作为Cloud Service团队提供了以下产品配置文件：

* **AEM管理员**:AEM管理员通常会分配给开发人员，特别是需要有权访问（例如）开发环境的开发人员。AEM管理员产品配置文件将用于在关联的AEM实例中授予管理员权限。

* **AEM用户**:AEM用户是指您组织中在与Adobe的协议中使用AEM作为Cloud Service的用户。这些成员需要访问AEM才能执行其任务。 AEM用户产品配置文件通常分配给创建和审阅内容的AEM内容作者(这可以是几种类型；（例如，页面、资产、出版物等）。 下面显示的AEM用户产品配置文件已分配给这些成员。

   >[!NOTE]
   >分配给AEM as a Cloud Service产品配置文件的每个用户都具有Cloud Manager的访问权限（只读）。

## Cloud Manager产品配置文件{#cloud-manager-product-profiles}

Cloud Manager已预配置了产品配置文件，或者更简单的，基于角色的权限。 系统管理员将负责通过将分配给这些产品配置文件来设置您的Cloud Manager团队，并且必须熟悉这些产品配置文件以及要为其分配的团队成员。
>[!NOTE]
>有关更多详细信息，请参阅Cloud Manager中的[基于角色的权限](/help/onboarding/what-is-required/user-roles-permissions.md)。

每个产品配置文件都具有与其关联的特定权限。 例如，如果您的角色是：

* **业务所有者**，您拥有以下权限：添加新程序或编辑程序、添加或更新环境、添加/编辑/删除管道并运行任何管道，以及将代码部署到AEM环境或代码质量。

* **部署管理器**&#x200B;中，您有权添加或更新环境、运行任何管道，以及将代码部署到AEM环境或代码质量。

* **开发人员**，您有权生成访问Git的个人访问令牌。

* **程序管理器**&#x200B;中，则表示您有权访问Git。

可以将用户分配到多个产品配置文件。 例如，将业务所有者和部署管理员角色分配给用户，可为其提供这些权限的组合或总和。

您的Cloud Manager团队将至少包括：

* 一位业务所有者（通常也是系统管理员）必须是登录和访问Cloud Manager的第一个人员
* 一个部署管理器
* 一名开发人员

   >[!NOTE]
   >要获得AEM as aCloud Service的访问权限，用户必须属于两个产品配置文件`AEM Users-xxx`或`AEM Administrators-xxx`中的一个。 您必须拥有实例的权限。 管理关联的Cloud Manager的权限是不够的。