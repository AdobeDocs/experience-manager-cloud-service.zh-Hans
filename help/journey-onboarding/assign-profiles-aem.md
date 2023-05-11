---
title: 分配 AEM 产品配置文件
description: 配置云资源后，您需要使用 AEM 产品配置文件授予您的团队访问 AEM 本身的权限。
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 77ae5d79ecb8a11a230cee461f247ffe0e9891a5
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 97%

---

# 分配 AEM 产品配置文件 {#assign-profiles-aem}

在[入门培训历程的这一可选部分中，](overview.md)您将了解如何使用 AEM 产品配置文件授予您的团队访问 AEM 的权限。

## 目标 {#objective}

一旦您阅读了本次入门培训历程中的上一篇文档[创建环境](create-environments.md)，并配置好云资源，您需要使用 AEM 产品配置文件授予您的团队访问 AEM 本身的权限。 作为系统管理员，您可以通过分配 AEM 产品配置文件来完成此操作。

阅读本文档后，您应该了解：

* 什么是 AEM 产品配置文件。
* 如何将团队成员添加到 AEM 用户产品配置文件。
* 如何将团队成员添加到 AEM 管理员产品配置文件。

## AEM 产品配置文件 {#aem-product-profiles}

要使用 AEM，必须为您的团队成员分配至少一个 AEM 产品配置文件。 访问 Cloud Manager 的权限不够。 用户必须属于以下两种产品配置文件之一：

* `AEM Users` – 此组包括执行日常内容创作任务的普通用户。
* `AEM Administrators` – 此组包括负责高级功能或 AEM 的用户。

分配给 AEM 产品配置文件的每个用户也将获得 Cloud Manager 的只读访问权限。 可以通过其他产品配置文件授予对 Cloud Manager 的写入权限。

>[!CAUTION]
>
>不要编辑或删除名为“AEM 管理员”或“AEM 用户”的产品配置文件。编辑这些配置文件名可能会中断对 AEM 云实例的登录。

## 前提条件 {#prerequisites}

在开始阅读本节之前，您应该了解有关将使用 AEM 的团队的以下信息。

* 名称
* 电子邮件地址
* 角色和职责

>[!TIP]
>
>为了加入 AEM，我们建议您首先添加将参与即时任务的用户，例如管理员、开发人员和内容作者。 您可以在不添加所有用户的情况下继续其余的载入。 完成载入后，您可以稍后扩展到更多的用户。

## 查看 AEM 产品配置文件 {#view-profiles}

按照以下步骤从 Admin Console 查看 AEM 产品配置文件。

1. 登录到 Admin Console，网址是 [`https://adminconsole.adobe.com`。](https://adminconsole.adobe.com)

1. 在&#x200B;**概述**&#x200B;页面，从&#x200B;**产品和服务**&#x200B;信息卡中选择 **Adobe Experience Manager as a Cloud Service**。

   ![产品和服务信息卡](/help/journey-onboarding/assets/assign-team1.png)

1. 导航并选择实例。

   ![选择实例](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. 您将看到 AEM as a Cloud Service 产品配置文件的列表，这些配置文件可以根据用户的角色分配给用户。

   ![产品配置文件](/help/journey-onboarding/assets/cloud-profiles-2.png)

## 将团队成员添加到产品配置文件 {#add-team-members}

现在您已经熟悉了可用的配置文件，可以根据需要将其分配给团队成员。

这些任务要求您是具有&#x200B;**业务负责人** Cloud Manager 产品配置文件的系统管理员。

1. 从 Cloud Manager 导航到您的程序，然后从感兴趣的环境上下文中选择&#x200B;**管理访问权限**。

   ![管理访问权限](/help/journey-onboarding/assets/add-team1.png)

1. 新的选项卡会将您导航到 Admin Console，您可以从中访问环境的作者实例。 根据需要授予的权限，选择 **AEM 管理员**&#x200B;或 **AEM 用户**。

   ![分配访问权限](/help/journey-onboarding/assets/add-team2.png)

1. 选择 `AEM Administrator` 或 `AEM User`，然后单击&#x200B;**添加用户**，如下所示，并提交必要的详细信息以完成添加团队成员。

   ![添加团队成员](/help/journey-onboarding/assets/add-team3.png)

1. 如果您有需要访问的团队成员的信息，请对所有环境重复这些步骤，包括开发、暂存和生产。

您添加的用户现在可以有权访问 AEM as a Cloud Service 作者服务！

## 历程结束？ {#the-end}

恭喜！您分配给 AEM as a Cloud Service 产品配置文件的用户现在可以访问 AEM 创作环境，并开始使用 AEM as a Cloud Service 创建内容。 同样，开发人员现在可以访问 Cloud Manager，使用 Git 存储自定义应用程序代码并进行部署。 从这个意义上说，您的入门培训历程已经完成，您的用户现在可以使用 AEMaaCS 了。

然而，如果您想更好地了解作者和开发人员如何使用该系统，您可以继续此入门培训历程的两个可选部分：

* [开发人员和部署管理员任务](developers.md) – 在这里，您将了解开发人员如何访问 Git 以存储其自定义代码并使用 Cloud Manager 管道进行部署。
* [AEM 用户任务](aem-users.md) – 在这里，您将了解如何进入 AEM 环境并开始创建内容。

## 其他资源 {#additional-resources}

如果您希望不仅仅访问载入历程的内容，还可以选择使用以下其他资源。

* [在 Admin Console 管理产品和用户访问权限](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) – 了解如何使用 Admin Console 管理用户访问权限。
* [配置 AEM 演练的访问权限](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=zh-Hans) – 查看此简化演练，了解如何在 Admin Console 中配置 Adobe IMS 用户、用户组和产品配置文件。

