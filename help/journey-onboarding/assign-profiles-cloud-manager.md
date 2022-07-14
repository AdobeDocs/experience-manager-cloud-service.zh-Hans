---
title: 将团队成员分配给Cloud Manager产品配置文件
description: 可查看本页以了解如何将团队成员分配给Cloud Manager产品配置文件
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 2%

---


# 将团队成员分配给 Cloud Manager 产品配置文件 {#assign-team-members}

在 [入门历程，](overview.md) 您将了解如何将团队成员分配给Cloud Manager产品配置文件。

## 目标 {#objective}

在此历程的上一步中， [访问Admin Console、](admin-console.md) 您现在已学会以系统管理员的身份登录到Admin Console并验证您的权限。 现在，您已准备好允许团队成员访问Cloud Manager。 要执行此操作，请分配产品配置文件。

在授予用户访问Adobe解决方案的权限时，您不一定希望授予他们完全访问权限。 产品配置文件使每个解决方案都具有其自身的一组用户权限。 您可以使用Admin Console分配产品配置文件。

您的第一步是授予用户访问Cloud Manager的权限。 Cloud manager通过企业开发设置及其专门构建的CI/CD管道为您提供支持，这些设备可确保进行全面测试，并提供最高的代码质量，以提供卓越的体验。

阅读本文档后，您应：

* 了解产品配置文件。
* 了解Cloud Manager是什么。
* 了解三个重要的Cloud Manager产品配置文件： **业务所有者**, **部署管理器**&#x200B;和 **开发人员**.
* 能够将团队成员分配给Cloud Manager产品配置文件。

## 前提条件 {#prerequisites}

要将团队成员分配给产品配置文件，您需要拥有有关团队成员的详细信息，这些成员将需要访问AEMas a Cloud Service，包括：

* 名称
* 电子邮件地址
* 角色和职责

>[!TIP]
>
>为了入门，Adobe建议您最初添加将参与即时任务的用户，如管理员、开发人员和内容作者。
>
>您无需添加所有用户即可继续载入过程。 载入完成后，您可以添加其他用户。

## 产品配置文件 {#product-profiles}

在授予用户访问Adobe解决方案的权限时，您不一定希望授予他们完全访问权限。 产品配置文件使每个解决方案都能够拥有自己的一组用户权限，这些权限是使用Admin Console设置的。

例如，在此历程的后面，您将使用Admin Console通过为AEM管理员和AEM作者分配产品配置文件来授予用户访问AEM解决方案的权限。

但是，下一步是授予产品配置文件，以便您的团队成员首先能够访问Cloud Manager。

## Cloud Manager {#cloud-manager}

作为系统管理员，您知道，成功的AEMas a Cloud Service项目不仅取决于使用AEM创建令人惊叹的内容，还取决于开发和部署您自己的自定义代码和应用程序以交付AEM内容。

Cloud Manager是AEMas a Cloud Service的一个组成部分，用于管理用于代码部署的CI/CD管道、管理代码存储库和管理环境。

在您的团队执行任何其他操作之前，必须通过向其授予必要的产品配置文件，将其载入Cloud Manager。 后续步骤将向您展示在何处使用Admin Console查找Cloud Manager产品配置文件，以及如何将其分配给团队成员。

## 查看Cloud Manager产品配置文件 {#review-product-profiles}

使用Admin Console，您可以看到Cloud Manager配置文件列表。

1. 登录Adobe Admin Console(位于 [adminconsole.adobe.com](https://adminconsole.adobe.com/) 和 **概述** 页面，选择 **Adobe Experience Manager as a Cloud Service** 从 **产品和服务** 卡。

   ![AEM as a product](/help/journey-onboarding/assets/assign-team1.png)

1. 导航到 **Cloud Manager** 实例。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 您将看到预配置的Cloud Manager产品配置文件列表。

   ![产品配置文件](/help/journey-onboarding/assets/assign-team3.png)

在初始载入过程中要分配的最重要用户档案包括：

* **业务所有者**  — 这些用户管理不同的程序。
* **部署管理器**  — 这些用户将代码从您的存储库部署到运行AEM环境。
* **开发人员**  — 这些用户开发自定义AEM应用程序并将代码提交到您的存储库。

了解这些角色是什么以及它们的作用，查看团队成员列表以确定谁需要哪个用户档案。 请记住，用户在您的团队中可以有并且通常具有多个角色，因此也需要多个用户档案。

## 分配业务所有者产品配置文件 {#assign-business-owner}

现在，您可以添加用户，并将其分配给 **业务所有者** 产品配置文件。

1. 确定需要管理Cloud Manager程序的用户。 这些将是您的 **企业所有者**.

1. 登录到Admin Console: `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 和 **概述** 页面，选择 **Adobe Experience Manager as a Cloud Service** 产品来源 **产品和服务** 卡。

   ![产品和服务](/help/journey-onboarding/assets/assign-team1.png)

1. 选择 **用户** 选项卡，然后选择 **添加用户**.

   ![添加用户](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **将用户添加到您的团队** 对话框中，输入要添加的用户的电子邮件ID。

   * 如果尚未设置团队成员的Federated ID，请选择 **Adobe ID** 对于 **ID类型**.

   ![添加用户详细信息](/help/journey-onboarding/assets/assign-team5.png)

1. 单击 **选择产品或用户组** 开始产品选择和选择的标题 **Adobe Experience Manager as a Cloud Service** 分配 **业务所有者** 将产品配置文件发送给用户。

   * 将每个用户至少分配一个产品配置文件，以便用户可以访问Cloud Manager。
   * 请记住，将您自己作为系统管理员分配给 **业务所有者** 角色。

   ![分配用户](/help/journey-onboarding/assets/assign-team6.png)

1. 单击 **保存** 并向您添加的用户发送欢迎电子邮件。 受邀用户可以通过单击欢迎电子邮件中的链接，然后使用其Adobe ID登录来访问Cloud Manager。

1. 为团队中的用户重复这些步骤。

您的 **业务所有者**&#x200B;已分配，现在可以访问Cloud Manager。 不要忘记将您自己作为系统管理员分配给 **业务所有者** 配置文件。

## 分配部署管理器产品配置文件 {#assign-deployment-manager}

1. 识别需要部署代码的用户。

1. 登录到Admin Console: `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 和 **概述** 页面选择 **Adobe Experience Manager as a Cloud Service** 产品 **产品和服务** 卡。

   ![产品和服务](/help/journey-onboarding/assets/assign-team1.png)

1. 选择 **用户** 选项卡，然后选择 **添加用户**.

   ![添加用户](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **将用户添加到您的团队** 对话框中，输入要添加的用户的电子邮件ID。

   * 如果尚未设置团队成员的Federated ID，请选择 **Adobe ID** 对于 **ID类型**.

   ![输入ID](/help/journey-onboarding/assets/assign-team5.png)

1. 单击 **选择产品或用户组** 开始产品选择和选择的标题 **Adobe Experience Manager as a Cloud Service** 分配 **部署管理器** 将产品配置文件发送给用户。

   ![分配配置文件](/help/journey-onboarding/assets/assign-team6.png)

您的 **部署管理器**&#x200B;已分配，现在可以访问Cloud Manager。 根据您将来的职责，您可能还需要（也可能不需要）将您自己作为系统管理员分配给 **部署管理器** 配置文件。

## 分配开发人员产品配置文件 {#assign-developer}

1. 识别需要开发AEM应用程序和管理代码的用户。

1. 登录到Admin Console: `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` 和 **概述** 页面选择 **Adobe Experience Manager as a Cloud Service** 产品 **产品和服务** 卡。

   ![产品和服务](/help/journey-onboarding/assets/assign-team1.png)

1. 选择 **用户** 选项卡，然后选择 **添加用户**.

   ![添加用户](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **将用户添加到您的团队** 对话框中，输入要添加的用户的电子邮件ID。

   * 如果尚未设置团队成员的Federated ID，请选择 **Adobe ID** 对于 **ID类型**.

   ![添加用户ID](/help/journey-onboarding/assets/assign-team5.png)

1. 单击 **选择产品或用户组** 开始产品选择和选择的标题 **Adobe Experience Manager as a Cloud Service** 分配 **开发人员** 将产品配置文件发送给用户。

   ![分配配置文件](/help/journey-onboarding/assets/assign-team6.png).

您的 **开发人员**&#x200B;已分配，现在可以访问Cloud Manager。 根据您将来的职责，您可能还需要（也可能不需要）将您自己作为系统管理员分配给 **开发人员** 配置文件。

## 下一步 {#whats-next}

恭喜！您新组建的Cloud Manager团队(包括您自己已分配给 **业务所有者** 配置文件)。 在 **业务所有者**，则现在只需一步之遥即可登录到Cloud Manager并启用云资源的创建。

在入门历程的这一部分中，您了解了如何将团队成员分配给Admin Console中的用户档案。 您现在应：

* 了解产品配置文件。
* 了解Cloud Manager是什么。
* 了解三个重要的Cloud Manager产品配置文件： **业务所有者**, **部署管理器**&#x200B;和 **开发人员**.
* 能够将团队成员分配给Cloud Manager产品配置文件。

现在，您可以通过下一步审阅文档来继续入门历程 [访问Cloud Manager、](cloud-manager.md) 您将在此处了解如何访问Cloud Manager和创建项目资源。

## 其他资源 {#additional-resources}

建议继续按照之前所述进行载入历程。 如果您希望从此历程深入探讨特定主题，则可以使用这些其他资源。

* [Cloud Manager简介](/help/onboarding/cloud-manager-introduction.md)  — 了解Cloud Manager、Cloud Manager程序和环境。
* [Cloud Manager产品配置文件](/help/onboarding/aem-cs-team-product-profiles.md)  — 了解AEMas a Cloud Service团队和产品配置文件。
* [Adobe Admin Console上的身份类型](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html) -Adobe的身份管理系统可帮助管理员创建和管理用户对应用程序和服务的访问权限。 Adobe提供这些身份类型或帐户来验证和授权用户。

