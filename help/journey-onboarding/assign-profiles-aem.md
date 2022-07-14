---
title: 分配AEM产品配置文件
description: 配置云资源后，您将需要使用AEM产品配置文件授予您的团队访问AEM本身的权限。
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---

# 分配AEM产品配置文件 {#assign-profiles-aem}

在 [入门历程，](overview.md) 您将了解如何使用AEM产品配置文件授予您的团队访问AEM的权限。

## 目标 {#objective}

阅读此入门历程中的上一文档后， [创建环境、](create-environments.md) 配置了云资源后，您将需要使用AEM产品配置文件授予团队访问AEM本身的权限。 作为系统管理员，您可以通过分配AEM产品配置文件来执行此操作。

阅读本文档后，您应该了解：

* 什么是AEM产品配置文件。
* 如何将团队成员添加到AEM用户产品配置文件。
* 如何将团队成员添加到AEM Administrators产品配置文件。

## AEM产品配置文件 {#aem-product-profiles}

要使用AEM，必须将您的团队成员至少分配给一个AEM产品配置文件。 访问Cloud Manager的权限不够。 用户必须属于以下两个产品配置文件之一：

* `AEM Users`  — 此组包括执行日常内容创作任务的普通用户。
* `AEM Administrators`  — 此组包含负责高级功能或AEM的用户。

分配给AEM产品配置文件的每个用户也将获得Cloud Manager的只读访问权限。 可以通过其他产品配置文件授予Cloud Manager的写入权限。

## 前提条件 {#prerequisites}

在开始阅读此部分之前，您应提供以下有关将使用AEM的团队的信息。

* 名称
* 电子邮件地址
* 角色和职责

>[!TIP]
>
>为了入门，我们建议您最初添加将参与即时任务的用户，例如管理员、开发人员和内容作者。 您无需添加所有用户即可继续载入其余内容。 完成载入后，您可以稍后扩展到更多用户。

## 查看AEM产品配置文件 {#view-profiles}

请按照以下步骤从Admin Console中查看AEM产品配置文件。

1. 登录Admin Console: [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. 从 **概述** 页面，选择 **Adobe Experience Manager as a Cloud Service** 从 **产品和服务** 卡。

   ![产品和服务卡](/help/journey-onboarding/assets/assign-team1.png)

1. 导航并选择实例。

   ![选择实例](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. 您将看到可根据用户角色为其分配的AEMas a Cloud Service产品配置文件列表。

   ![产品配置文件](/help/journey-onboarding/assets/cloud-profiles-2.png)

## 将团队成员添加到产品配置文件 {#add-team-members}

现在，您已熟悉可用的用户档案，接下来可以根据需要将其分配给团队成员。

这些任务要求您是 **业务所有者** Cloud Manager产品配置文件。

1. 从Cloud Manager导航到您的项目，然后选择 **管理访问权限** 按钮。

   ![管理访问](/help/journey-onboarding/assets/add-team1.png)

1. 新选项卡会将您导航到您有权从中访问环境创作实例的Admin Console。 选择 **AEM管理员** 或 **AEM用户** 根据需要为此人授予的权限。

   ![分配访问权限](/help/journey-onboarding/assets/add-team2.png)

1. 选择 `AEM Administrator` 或 `AEM User` 单击 **添加用户** 如下所示，并提交必要的详细信息以完成添加团队成员。

   ![添加团队成员](/help/journey-onboarding/assets/add-team3.png)

1. 如果您拥有需要可用访问权限的团队成员的信息，请为所有环境（包括开发、暂存和生产）重复执行这些步骤。

您添加的用户现在将有权访问AEMas a Cloud Service创作服务！

## 历程结束？ {#the-end}

恭喜！现在，分配给AEMas a Cloud Service产品配置文件的用户便可以访问AEM创作环境并开始使用AEMas a Cloud Service创建内容。 同样，开发人员现在可以访问Cloud Manager以使用git存储自定义应用程序代码并对其进行部署。 从这个意义上讲，您的入门历程已完成，您的用户现在可以使用AEMaCS。

但是，如果您希望更好地了解作者和开发人员如何使用系统，则可以继续完成此入门历程的两个可选部分：

* [开发人员和部署管理器任务](developers.md)  — 您将在此处了解开发人员如何访问git以存储其自定义代码，并使用Cloud Manager管道进行部署。
* [AEM用户任务](aem-users.md)  — 您将在此处了解如何访问AEM环境，以开始创建内容。

## 其他资源 {#additional-resources}

* [在Admin Console中管理产品和用户访问权限](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console)  — 了解如何使用Admin Console管理使用访问权限。
* [配置对AEM演练的访问权限](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)  — 请查看此简略演练，了解如何在Admin Console中配置Adobe IMS用户、用户组和产品配置文件。

