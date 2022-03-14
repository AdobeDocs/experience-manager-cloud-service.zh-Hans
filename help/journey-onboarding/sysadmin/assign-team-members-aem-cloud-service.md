---
title: 将团队成员分配给 AEM as a Cloud Service 产品配置文件
description: 可查看本页以了解如何将团队成员分配给AEMas a Cloud Service产品配置文件
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 5%

---

# 将团队成员分配给 AEM as a Cloud Service 产品配置文件 {#assign-team-members-cloud-service}

## 目标 {#objective}

本文档可帮助您了解系统管理员为将团队成员分配给AEMas a Cloud Service产品配置文件所必须执行的步骤，以及为什么让AEM作者能够开始使用AEM的旅程至关重要。

阅读此部分后，您应该了解：

* 为何以及如何将您的团队成员分配给AEMas a Cloud Service的产品配置文件。
* 如何将团队成员添加到AEM用户产品配置文件。
* 如何将团队成员添加到AEM Administrators产品配置文件。


## 简介 {#introduction}

要授予AEMas a Cloud Service用户的访问权限，必须属于以下两个产品配置文件之一：  `AEM Users` 或 `AEM Administrators`. 您的团队成员必须获得对AEM实例的权限，因为管理Cloud Manager的权限是不够的。

>[!NOTE]
>系统管理员分配给AEM用户产品配置文件的每个用户都将拥有Cloud Manager的（只读）访问权限。

## 先决条件 {#prerequisites}

在开始阅读本节之前，您应当考虑以下先决条件：

* 了解 [AEMas a Cloud Service产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)
* 熟悉 [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)
* 已根据需要将Cloud Manager产品配置文件分配给团队成员，并且已设置云资源
* 有关您的团队成员的详细信息：系统管理员必须具有姓名和电子邮件地址，以及需要访问AEMas a Cloud Service的团队成员的角色和职责。

   >[!NOTE]
   >为了入门，我们建议您最初添加将参与即时任务的用户，例如管理员、开发人员和内容作者。 您无需添加所有用户即可继续载入其余内容。 完成载入后，您可以稍后扩展到更多用户。


   >[!IMPORTANT]
   >在开始审核将团队成员分配给AEMas a Cloud Service产品配置文件的步骤之前，请确保遵循以下两个步骤：
   >
   >1. 登录到 [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en). 有关更多详细信息，请参阅登录Admin Console。
   >
   >1. 审阅 [AEMas a Cloud Service产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).


请按照以下步骤查看Adobe Admin Console中的Cloud Manager配置文件列表：

1. 登录到 [Adobe Admin Console](https://adminconsole.adobe.com/). 从 **概述** 页面，选择 **Adobe Experience Manager as a Cloud Service** 从 **产品和服务** 卡。

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. 导航并选择实例（开发环境的创作实例），如下图所示。

   ![](/help/journey-onboarding/assets/cloud-profiles-1.png)


1. 您将看到AEMas a Cloud Service产品配置文件列表，用户需要根据其角色对其进行分配。

   >[!NOTE]
   >要了解有关这些内容的更多信息，请参阅 [AEMas a Cloud Service产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/journey-onboarding/assets/cloud-profiles-2.png)


## 将团队成员添加到AEM用户或AEM管理员产品配置文件 {#add-team-members}

要授予AEMas a Cloud Service实例用户的访问权限，必须属于两个产品配置文件之一 `AEM Users` 或 `AEM Administrators`.

>[!NOTE]
>您必须获得实例的权限，但管理Cloud Manager的权限是不够的。 了解更多。

以下步骤必须由同时具有“业务所有者”角色的系统管理员执行。

1. 从Cloud Manager导航到您的项目，然后选择 **管理访问权限** 按钮，如下所示。

   ![](/help/journey-onboarding/assets/add-team1.png)

1. 新选项卡会将您导航到您有权从中访问环境创作实例的Adobe Admin Console。 选择 **AEM管理员** 或 **AEM用户** 根据此个人需要授予的权限。 详细了解 [AEMas a Cloud Service产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/journey-onboarding/assets/add-team2.png)

1. 选择 `AEM Administrator` 或 `AEM User` 单击 **添加用户** 如下所示，并提交必要的详细信息以完成添加团队成员。

   ![](/help/journey-onboarding/assets/add-team3.png)

   您添加的用户现在将有权访问AEMas a Cloud Service创作服务！

   >[!NOTE]
   >如果您拥有需要访问的团队成员信息，则需要对所有环境（包括开发、暂存和生产）重复执行这些步骤。


## 下一步 {#whats-next}

现在，分配给AEMas a Cloud Service产品配置文件的用户已准备好了解如何访问创作，并熟悉AEMas a Cloud Service中的创作页面。 您应该遵循该路径，方法是接下来查看文档的学习路径 [AEM用户](/help/journey-onboarding/sysadmin/learning-path-aem-users.md) 或 [开发人员和部署管理器](/help/journey-onboarding/sysadmin/learning-path-developers-deploymentmanagers.md).

## 其他资源 {#additional-resources}

* [在 Admin Console 中管理产品和用户访问权限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console)
* [配置对AEM的访问权限](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [页面创作快速入门指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)
