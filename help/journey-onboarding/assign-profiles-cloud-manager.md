---
title: 将团队成员分配给 Cloud Manager 产品配置文件
description: 关注此页面，了解如何将团队成员分配给 Cloud Manager 产品配置文件
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 93%

---


# 将团队成员分配给 Cloud Manager 产品配置文件 {#assign-team-members}

在这部分中 [入门培训历程，](overview.md) 您将了解如何将团队成员分配给Cloud Manager产品配置文件。

## 目标 {#objective}

在本次历程的前一步[访问 Admin Console](admin-console.md) 中，您已学会登录 Admin Console 并验证您作为系统管理员的权限。 您现在可以允许团队成员访问 Cloud Manager 了。 您可以通过分配产品配置文件来实现这一点。

授予用户访问 Adobe 解决方案的权限时，您不一定要授予他们完全访问权限。 产品配置文件使每个解决方案都有自己的用户权限集。 您可以使用 Admin Console 分配产品配置文件。

第一步是授予用户访问 Cloud Manager 的权限。 Cloud Manager 通过企业开发设置及其专门构建的 CI/CD 管道为您提供支持，这些管道可确保全面测试和最佳代码质量，从而提供卓越的体验。 

阅读本文档后，您应：

* 了解什么是产品配置文件。
* 了解什么是 Cloud Manager。
* 了解三个重要的 Cloud Manager 产品配置文件：**业务负责人**、**部署管理员**&#x200B;和&#x200B;**开发人员**。
* 能够将团队成员分配给 Cloud Manager 产品配置文件。

## 前提条件 {#prerequisites}

要将团队成员分配给产品配置文件，您需要了解必须访问AEMas a Cloud Service的团队成员的详细信息，包括：

* 名称
* 电子邮件地址
* 角色和职责

>[!TIP]
>
>为了载入 AEM，Adobe 建议您首先添加将参与即时任务的用户，例如管理员、开发人员和内容作者。 
>
>您可以在不添加所有用户的情况下继续载入流程。 完成载入之后，您可以添加其他用户。

## 产品配置文件 {#product-profiles}

授予用户访问 Adobe 解决方案的权限时，您不一定要授予他们完全访问权限。 产品配置文件使每个解决方案都有自己的用户权限集，设置这些权限的目的是使用 Admin Console。

例如，在本历程的稍后部分，您将使用 Admin Console，通过为 AEM 管理员和 AEM 作者分配产品配置文件，授予用户访问 AEM 解决方案的权限。

然而，下一步是授予产品配置文件，以便您的团队成员首先可以访问 Cloud Manager。

## Cloud Manager {#cloud-manager}

作为系统管理员，您知道 AEM as a Cloud Service 项目的成功不仅取决于使用 AEM 创建令人惊叹的内容，还取决于开发和部署您自己的自定义代码和应用程序来投放 AEM 内容。

Cloud Manager 是 AEM as a Cloud Service 的一个组成部分，用于管理用于代码部署的 CI/CD 管道、管理代码存储库和管理环境。

在您的团队开始使用之前，必须通过授予必要的产品配置文件将他们载入到 Cloud Manager。 接下来的步骤将向您展示使用 Admin Console 在何处查找 Cloud Manager 产品配置文件，以及如何将其分配给您的团队成员。

## 查看 Cloud Manager 产品配置文件 {#review-product-profiles}

使用 Admin Console ，您可以看到 Cloud Manager 配置文件的列表。

1. 从 [adminconsole.adobe.com](https://adminconsole.adobe.com/) 和&#x200B;**概述**&#x200B;页面登录 Adobe Admin Console，然后从&#x200B;**产品和服务**&#x200B;信息卡中选择 **Adobe Experience Manager as a Cloud Service**。

   ![AEM 作为产品](/help/journey-onboarding/assets/assign-team1.png)

1. 从所有实例列表中导航到 **Cloud Manager** 实例。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 您可以看到预配置的Cloud Manager产品配置文件的列表。

   ![产品配置文件](/help/journey-onboarding/assets/assign-team3.png)

作为初始载入流程的一部分，最重要的配置文件包括：

* **业务负责人** – 这些用户管理不同的程序。
* **部署管理员** – 这些用户从您的存储库部署代码，可运行 AEM 环境。
* **开发人员** – 这些用户开发您的自定义 AEM 应用程序并将代码提交到存储库。

了解这些角色是什么以及他们做什么，就查看您的团队成员列表确定谁需要哪个配置文件。 请记住，用户在您的团队中可以并且经常拥有多个角色，因此也需要多个配置文件。

## 分配业务负责人产品配置文件 {#assign-business-owner}

现在，您可以添加用户并将其分配到&#x200B;**业务负责人**&#x200B;产品配置文件。

1. 确定需要管理 Cloud Manager 程序的用户。 这些是您的&#x200B;**业务负责人**。

1. 从 `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 和&#x200B;**概述**&#x200B;页面登录 Admin Console，然后从&#x200B;**产品和服务**&#x200B;信息卡中选择 **Adobe Experience Manager as a Cloud Service**。

   ![产品和服务](/help/journey-onboarding/assets/assign-team1.png)

1. 从顶部导航中选择&#x200B;**用户**&#x200B;选项卡，然后选择&#x200B;**添加用户**。

   ![添加用户](/help/journey-onboarding/assets/assign-team4.png)

1. 在&#x200B;**将用户添加到团队**&#x200B;对话框中，输入要添加的用户的电子邮件 ID。

   * 如果尚未为团队成员设置 Federated ID，请选择 **Adobe ID** 作为 **ID 类型**。

   ![添加用户详细信息](/help/journey-onboarding/assets/assign-team5.png)

1. 单击&#x200B;**选择产品或用户组**&#x200B;标题下的加号按钮开始产品选择，选择 **Adobe Experience Manager as a Cloud Service**，并将&#x200B;**业务负责人**&#x200B;产品配置文件分配给用户。

   * 为每个用户分配至少一个产品配置文件，以便用户可以访问 Cloud Manager。
   * 请记住，将您自己指定为&#x200B;**业务负责人**&#x200B;角色。

   ![分配用户](/help/journey-onboarding/assets/assign-team6.png)

1. 单击&#x200B;**保存**，这将向您添加的用户发送欢迎电子邮件。 受邀的用户可以通过单击欢迎电子邮件中的链接并使用其 Adobe ID 登录来访问 Cloud Manager。

1. 对团队中的用户重复这些步骤。

您的&#x200B;**业务负责人**&#x200B;已分配，现在可以访问 Cloud Manager。 别忘了将您自己作为系统管理员分配给&#x200B;**业务负责人**&#x200B;配置文件。

## 分配部署管理员产品配置文件 {#assign-deployment-manager}

1. 确定需要部署代码的用户。

1. 从 `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 和&#x200B;**概述**&#x200B;页面登录 Admin Console，然后从&#x200B;**产品和服务**&#x200B;信息卡中选择 **Adobe Experience Manager as a Cloud Service**。

   ![产品和服务](/help/journey-onboarding/assets/assign-team1.png)

1. 从顶部导航中选择&#x200B;**用户**&#x200B;选项卡，然后选择&#x200B;**添加用户**。

   ![添加用户](/help/journey-onboarding/assets/assign-team4.png)

1. 在&#x200B;**将用户添加到团队**&#x200B;对话框中，输入要添加的用户的电子邮件 ID。

   * 如果尚未为团队成员设置 Federated ID，请选择 **Adobe ID** 作为 **ID 类型**。

   ![输入 ID](/help/journey-onboarding/assets/assign-team5.png)

1. 单击&#x200B;**选择产品或用户组**&#x200B;标题下的加号按钮开始产品选择，选择 **Adobe Experience Manager as a Cloud Service**，并将&#x200B;**部署管理员**&#x200B;产品配置文件分配给用户。

   ![分配配置文件](/help/journey-onboarding/assets/assign-team6.png)

您的&#x200B;**部署管理员**&#x200B;已分配，现在可以访问 Cloud Manager。 根据您未来的职责，您可能需要也可能不需要将自己指定为&#x200B;**部署管理员**&#x200B;配置文件的系统管理员。

## 分配开发人员产品配置文件 {#assign-developer}

1. 确定需要开发 AEM 应用程序和管理代码的用户。

1. 从 `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 和&#x200B;**概述**&#x200B;页面登录 Admin Console，然后从&#x200B;**产品和服务**&#x200B;信息卡中选择 **Adobe Experience Manager as a Cloud Service**。

   ![产品和服务](/help/journey-onboarding/assets/assign-team1.png)

1. 从顶部导航中选择&#x200B;**用户**&#x200B;选项卡，然后选择&#x200B;**添加用户**。

   ![添加用户](/help/journey-onboarding/assets/assign-team4.png)

1. 在&#x200B;**将用户添加到团队**&#x200B;对话框中，输入要添加的用户的电子邮件 ID。

   * 如果尚未为团队成员设置 Federated ID，请选择 **Adobe ID** 作为 **ID 类型**。

   ![添加用户 ID](/help/journey-onboarding/assets/assign-team5.png)

1. 单击&#x200B;**选择产品或用户组**&#x200B;标题下的加号按钮开始产品选择，选择 **Adobe Experience Manager as a Cloud Service**，并将&#x200B;**开发人员**&#x200B;产品配置文件分配给用户。

   ![分配配置文件](/help/journey-onboarding/assets/assign-team6.png)。

您的&#x200B;**开发人员**&#x200B;已分配，现在可以访问 Cloud Manager。 根据您未来的职责，您可能需要也可能不需要将自己指定为&#x200B;**开发人员**&#x200B;配置文件的系统管理员。

## 后续内容 {#whats-next}

恭喜！您新组建的 Cloud Manager 团队（包括分配给&#x200B;**业务负责人**&#x200B;配置文件的您自己）已经设置。 作为&#x200B;**业务负责人**&#x200B;的角色，您现在离登录 Cloud Manager 并启用云资源创建只有一步之遥。

在入门培训历程的这一可选部分中，您了解了如何在 Admin Console 中将团队成员分配给配置文件。您现在应：

* 了解什么是产品配置文件。
* 了解什么是 Cloud Manager。
* 了解三个重要的 Cloud Manager 产品配置文件：**业务负责人**、**部署管理员**&#x200B;和&#x200B;**开发人员**。
* 能够将团队成员分配给 Cloud Manager 产品配置文件。

您现在可以通过下一次查看文档来继续您的入门培训历程 [访问Cloud Manager](cloud-manager.md) 在这里，您可以了解如何访问Cloud Manager和创建项目资源。

## 其他资源 {#additional-resources}

建议继续进行前面描述的入门培训历程。 如果您想深入了解此历程中的特定主题，以下是一些其他资源。

* [Cloud Manager 简介](/help/onboarding/cloud-manager-introduction.md) – 了解 Cloud Manager、Cloud Manager 程序和环境。
* [Cloud Manager 产品配置文件](/help/onboarding/aem-cs-team-product-profiles.md) – 了解 AEM as a Cloud Service 团队和产品配置文件。
* [Adobe Admin Console 上的身份类型](https://helpx.adobe.com/cn/enterprise/admin-guide.html/enterprise/using/identity.ug.html) – Adobe Identity Management 系统可帮助管理员创建和管理用户对应用程序和服务的访问。 Adobe 提供这些身份类型或帐户来验证和授权用户。

