---
title: 访问 Admin Console
description: 一旦您了解了入门所需的准备工作和AEM as a Cloud Service结构的基础知识，您就可以首次登录Admin Console了。
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 8ed13eb6f476bab07da07549a83ab9ac16bdea72
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 55%

---

# 访问 Admin Console {#accessing-admin-console}

在[加入历程](overview.md)的这一部分中，您将了解首次登录系统之前所需的准备工作。

## 目标 {#objective}

现在您已经阅读了文章 [AEM as a Cloud Service 术语](terminology.md)并了解了 AEMaaCS 结构的基本知识，您可以首次登录到 Admin Console 了！

作为系统管理员，您负责使用Admin Console管理组织内的用户。 阅读本节后，您应该能够执行以下操作，

* 了解 Adobe ID 是什么。
* 能够登录到Admin Console。
* 了解如何通过Admin Console查看您作为系统管理员的权限。
* 知道如何联系 Adobe 支持人员寻求帮助。

## 关于Admin Console {#admin-console}

Adobe Admin Console 是管理 Adobe 产品许可证和用户的中心位置。Admin Console 让您在单个位置而不是在各种单独的解决方案中创建和管理用户。

### Adobe ID {#adobe-id}

要登录到 Admin Console，您需要一个 Adobe ID。Adobe ID是一个绑定到特定电子邮件地址的帐户，登录和访问AEM as a Cloud Service或任何Adobe解决方案都需要该帐户。 通过使用Adobe ID，您可以将所有Adobe计划和产品与单个帐户关联。

当您作为系统管理员在 Admin Console 中设置团队时，请指定用作 Adobe ID 的电子邮件地址。

Adobe ID 有三种类型：

* **个人ID**：默认类型的Adobe ID，创建于adobe.com。 由Adobe管理，任何人都可以创建此类型的帐户。

* **Enterprise ID**：组织通常希望增加对用户帐户的控制。 只有系统管理员才能创建 Enterprise ID，组织拥有这些帐户，Adobe 仅作为主机。

* **Federated ID**：使用Federated ID，组织将完全拥有和控制帐户。 贵组织必须将Adobe Experience Cloud与SAML2单点登录(SSO)系统集成。 这样做可让用户根据其组织的SSO系统而不是Adobe托管的帐户进行身份验证。

作为系统管理员，您可以使用个人ID将自己和团队载入AEM as a Cloud Service。 请在准备好Enterprise ID或Federated ID之前执行此任务。 一旦设置了 Enterprise 或 Federated ID，就可以将成员转换为使用这些 ID。

### 直接登录Admin Console {#steps-admin-console}

在使用 Admin Console 管理团队中的用户之前，您需要确保自己能够正确访问它并拥有适当的权限。

1. 作为系统管理员，您在载入流程中会收到来自Adobe的多封电子邮件。 查找欢迎电子邮件，其中提供了有关您被授予访问权限的组织名称的信息。

1. 单击欢迎电子邮件中的&#x200B;**开始使用**&#x200B;链接以导航到Admin Console。 如果找不到电子邮件，请直接在浏览器中输入网址 [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) 打开 Admin Console。

   ![欢迎电子邮件](/help/journey-onboarding/assets/get-started-email.png)

1. 使用您的 Adobe ID 登录。成功登录后，您将看到 Adobe Admin Console 的&#x200B;**概述**&#x200B;页面。

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. 如果您有权访问多个组织，请确保您已登录到正确的组织。 若要更改您的组织，请单击右上角的组织名称，然后选择您需要访问的组织。

   ![更改组织](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. 在&#x200B;**用户**&#x200B;信息卡中选择&#x200B;**管理员**，验证您是否为系统管理员。

   ![查看管理员](/help/journey-onboarding/assets/get-started2.png)

1. 在从&#x200B;**用户**&#x200B;信息卡中单击&#x200B;**管理员**&#x200B;后，您可以通过输入 Adobe ID 电子邮件、用户名、名字或姓氏进行搜索。

   ![搜索用户](/help/journey-onboarding/assets/get-started3.png)

1. 如果一切运行正常，则搜索将返回您的记录。 如果&#x200B;**管理员角色**&#x200B;列中的值显示&#x200B;**系统**，则表示您自己（或显示的用户）是系统管理员。

   ![系统状态](/help/journey-onboarding/assets/get-started4.png)

恭喜，系统管理员！

## 通过Experience Hub访问Admin Console  {#access-admin-console-via-experience-hub}

[Experience Hub](/help/experience-hub.md)是AEM的统一、个性化主页。 它将AEM Tools和Admin Console融于一体。

Experience Hub主页上显示的![Admin Console选项](/help/journey-onboarding/assets/experiencehub-adminconsole1.png)

**要通过Experience Hub访问Admin Console，请执行以下操作：**

1. 单击[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home)打开Experience Hub主页。

1. 在&#x200B;**快速访问**&#x200B;分组中，单击&#x200B;[**Admin Console**](https://experience.adobe.com)。

## Adobe Identity Management System {#ims}

AEM as a Cloud Service 预先配置了 Adobe Identity Management System（也称为 IMS）进行身份验证。作为系统管理员，您无需执行任何操作即可启用此功能。

通过使用 IMS，AEM as a Cloud Service 整合了 AEM 与 Adobe experience Cloud 其余部分之间的登录体验。拥有许多Adobe产品的企业获得的好处最多。 在Admin Console中创建基于角色的组，并通过IMS(如AEM as a Cloud Service)授予产品访问权限。

在此加入历程的下一步中，您将详细了解产品配置文件和分配用户。

## 联系Adobe支持 {#support}

如果您有任何问题，可以通过 Admin Console 访问 Adobe 支持。**支持**&#x200B;选项卡允许您通过简单易用的界面访问各种 Adobe 支持功能。

![“支持”选项卡](/help/journey-onboarding/assets/support-menu.png)

该选项卡让您创建和管理案例，直接与 Adobe 客户支持代表聊天，以及计划与专家的会议。系统管理员和支持管理员必须登录才能访问支持案例和专家会话选项。

## 后续内容 {#whats-next}

现在您已阅读本文档，您应：

* 了解 Adobe ID 是什么。
* 能够登录到Admin Console。
* 了解如何使用Admin Console查看您作为系统管理员的权限。
* 知道如何联系 Adobe 支持人员寻求帮助。

您已准备好通过学习如何[将团队成员分配给Cloud Manager产品配置文件](assign-profiles-cloud-manager.md)来继续您的入门培训历程，以便您的同事也可以访问AEMaaCS。

## 其他资源 {#additional-resources}

如果您想了解加入历程以外的内容，以下是额外的可选资源。

* [Admin Console 概述](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) – Admin Console 全面概述
* [创建或更新您的 Adobe ID](https://helpx.adobe.com/cn/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) – 了解如何创建 Adobe ID 并进行更改，以及如何管理多个 Adobe ID。
* [SAML 2.0 身份验证处理程序](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/security/saml-2-0-authenticationhandler#) – AEM 附带 SAML 身份验证处理程序。此处理程序使用 HTTP POST 绑定支持 SAML 2.0 身份验证请求协议（Web-SSO 配置文件）。
* [管理员角色](https://helpx.adobe.com/cn/enterprise/using/admin-roles.html) – 通过使用 Adobe Admin Console，组织可以定义灵活的管理层次结构，从而更精细地管理对 Adobe 产品的访问和使用。
* [支持和专家讲座](https://helpx.adobe.com/cn/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.html) — 了解如何访问Admin Console上的支持选项、管理您的支持案例、安排专家讲座等等。
