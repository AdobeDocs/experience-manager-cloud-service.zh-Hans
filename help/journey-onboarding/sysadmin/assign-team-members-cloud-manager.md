---
title: 将团队成员分配给Cloud Manager产品配置文件
description: 可查看本页以了解如何将团队成员分配给Cloud Manager产品配置文件
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 1%

---

# 将团队成员分配给 Cloud Manager 产品配置文件 {#assign-team-members}

在此历程的上一步中， [入门流程](/help/journey-onboarding/sysadmin/get-started-onboarding-journey.md)，您现在已学会登录到Admin Console并以系统管理员的身份查看您的权限。 现在，您已准备好将团队成员分配给Cloud Manager产品配置文件。

## 目标 {#objective}

本文档概述了如何从Adobe Admin Console将团队成员分配给Cloud Manager产品配置文件。 分配后，这些成员可以创建访问云资源，如此历程的下一步中所述。

阅读此部分后，您应该能够：

* 了解添加团队成员的原因和方式。
* 了解三个重要的Cloud Manager产品配置文件： **业务所有者**, **部署管理器**&#x200B;和 **开发人员**.
* 将团队成员分配给Cloud Manager产品配置文件。

>[!TIP]
>
>为了入门，Adobe建议您最初添加将参与即时任务（如管理员、开发人员和内容作者）的用户。 您无需添加所有用户即可继续载入过程。 载入完成后，您可以添加其他用户。

## 前提条件 {#prerequisites}

在开始此部分之前，应满足以下先决条件。 您必须：

* 成为系统管理员并了解Cloud Manager产品配置文件。
   * 返回到 [入门历程概述](onboarding-journey-overview.md) 如果您不熟悉这些概念。
* 了解Adobe Admin Console基础知识。
   * 返回到 [入门历程概述](onboarding-journey-overview.md) 如果您不熟悉这些概念。
* 详细了解您的团队成员，他们需要访问AEMas a Cloud Service，包括
   * 名称
   * 电子邮件地址
   * 角色和职责

## 查看Cloud Manager产品配置文件 {#review-product-profiles}

在Adobe Admin Console中，您可以看到Cloud Manager配置文件列表。

1. 登录Adobe Admin Console(位于 [adminconsole.adobe.com](https://adminconsole.adobe.com/) 和 **概述** 页面，选择 **Adobe Experience Manager as a Cloud Service** 从 **产品和服务** 卡。

   ![AEM as a product](/help/journey-onboarding/assets/assign-team1.png)

1. 导航到 **Cloud Manager** 实例。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 您将看到预配置的Cloud Manager产品配置文件列表。

   ![产品配置文件](/help/journey-onboarding/assets/assign-team3.png)

## 将用户分配给业务所有者产品配置文件 {#assign-users-business-owner}

现在，您可以添加用户，并将其分配给 **业务所有者** 产品配置文件。

1. 确定将管理Cloud Manager程序的用户，并将其添加到业务所有者产品配置文件。

1. 登录到Admin Console: [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) 和 **概述** 页面，选择 **Adobe Experience Manager as a Cloud Service** 产品来源 **产品和服务** 卡。

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

您新组建的Cloud Manager团队(包括您自己已分配给 **业务所有者** 角色)。 在 **业务所有者**，则现在只需一步之遥即可登录到Cloud Manager并启用云资源的创建。

## 将用户分配给Deployment Manager产品配置文件 {#assign-users-deployment-manager}

1. 确定将管理Cloud Manager程序的用户，并将其添加到Deployment Manager产品配置文件中。

1. 登录到Admin Console: [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) 和 **概述** 页面选择 **Adobe Experience Manager as a Cloud Service** 产品 **产品和服务** 卡。

   ![产品和服务](/help/journey-onboarding/assets/assign-team1.png)

1. 选择 **用户** 选项卡，然后选择 **添加用户**.

   ![添加用户](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **将用户添加到您的团队** 对话框中，输入要添加的用户的电子邮件ID。

   * 如果尚未设置团队成员的Federated ID，请选择 **Adobe ID** 对于 **ID类型**.

   ![输入ID](/help/journey-onboarding/assets/assign-team5.png)

1. 单击 **选择产品或用户组** 开始产品选择和选择的标题 **Adobe Experience Manager as a Cloud Service** 分配 **部署管理器** 将产品配置文件发送给用户。

   ![分配配置文件](/help/journey-onboarding/assets/assign-team6.png).

## 将用户分配给开发人员产品配置文件 {#assign-users-developer}

1. 确定将管理Cloud Manager程序的用户。

1. 登录到Admin Console: [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) 和 **概述** 页面选择 **Adobe Experience Manager as a Cloud Service** 产品 **产品和服务** 卡。

   ![产品和服务](/help/journey-onboarding/assets/assign-team1.png)

1. 选择 **用户** 选项卡，然后选择 **添加用户**.

   ![添加用户](/help/journey-onboarding/assets/assign-team4.png)

1. 在 **将用户添加到您的团队** 对话框中，输入要添加的用户的电子邮件ID。

   * 如果尚未设置团队成员的Federated ID，请选择 **Adobe ID** 对于 **ID类型**.

   ![添加用户ID](/help/journey-onboarding/assets/assign-team5.png)

1. 单击 **选择产品或用户组** 开始产品选择和选择的标题 **Adobe Experience Manager as a Cloud Service** 分配 **开发人员** 将产品配置文件发送给用户。

   ![分配配置文件](/help/journey-onboarding/assets/assign-team6.png).

## 下一步 {#whats-next}

在入门历程的这一部分中，您学习了有关将团队成员分配给Admin Console中的角色的所有信息。 您现在应该：

* 了解添加团队成员的原因和方式。
* 了解三个重要的Cloud Manager产品配置文件： **业务所有者**, **部署管理器**&#x200B;和 **开发人员**.
* 能够将团队成员分配给Cloud Manager产品配置文件。

现在，您可以通过下一步审阅文档来继续入门历程 [通过Cloud Manager设置云资源](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md)，您可从中学习：

1. 要让其他业务所有者创建程序，您以系统管理员的身份分配给 **业务所有者** 角色，必须先访问并登录Cloud Manager。
1. 用户如何使用 **业务所有者** 角色可以登录并设置您的云资源，包括您的云项目和环境。
1. 用户如何使用 **开发人员** 和 **部署管理器** 角色可以访问Cloud Manager。

## 其他资源 {#additional-resources}

建议继续按照之前所述进行载入历程。 如果您希望从此历程深入探讨特定主题，则可以使用这些其他资源。

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Cloud Manager产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Admin Console身份概述](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
