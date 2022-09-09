---
title: 访问Admin Console
description: 了解入门准备工作和AEMaaCS结构的基础知识后，您便可以首次登录Admin Console。
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 2%

---

# 访问Admin Console {#accessing-admin-console}

在 [入门历程，](overview.md) 在首次登录系统之前，您将了解必要的准备情况。

## 目标 {#objective}

既然你读过文章 [AEMas a Cloud Service术语](terminology.md) 了解AEMaaCS结构的基础知识，您便可以首次登录Admin Console!

作为系统管理员，您负责管理组织内的用户。 您可以使用Admin Console执行此操作。 阅读此部分后，您应：

* 了解Adobe ID是什么。
* 能够登录到Admin Console。
* 了解如何以系统管理员的身份通过Admin Console查看您的权限。
* 了解如何联系Adobe支持以获取帮助。

## Admin Console {#admin-console}

Adobe Admin Console是管理和管理Adobe产品许可证和用户的中心位置。 利用Admin Console，可在单个位置创建和管理用户，而不是在各个解决方案中创建和管理用户。

## Adobe ID {#adobe-id}

要登录Admin Console，您需要Adobe ID。 而Adobe ID是一个帐户，该帐户绑定到特定的电子邮件地址，用于登录和访问AEMas a Cloud Service或任何Adobe解决方案。 通过使用Adobe ID，您可以将所有Adobe计划和产品与单个帐户关联。

当您作为系统管理员在Admin Console中设置您的团队时，您需要指定将用作Adobe ID的电子邮件地址。

AdobeID有三种类型：

* **个人ID**:这是默认类型的Adobe ID，创建于adobe.com。 此帐户由Adobe管理，任何人都可以创建此类型的帐户。

* **Enterprise ID**:组织通常希望加强对用户帐户的控制。 只有系统管理员才能创建企业ID，并且组织拥有这些帐户，并且Adobe仅作为主机。

* **Federated ID**:借助联合ID，组织可以完全拥有并控制帐户。 为此，贵组织需要将Adobe Experience Cloud与SAML2单点登录(SSO)系统相集成。 这允许用户针对其组织的SSO系统进行身份验证，而不是针对由Adobe托管的帐户进行身份验证。

作为系统管理员，您可以决定在设置企业ID或联合ID之前，使用个人ID将您自己和您的团队载入AEMas a Cloud Service。 设置Enterprise ID或Federated ID后，可以使用这些ID将成员转换为。

## 登录到Admin Console {#steps-admin-console}

在使用Admin Console管理团队中的用户之前，您需要确保您自己能够正确访问该组并拥有相应的权限。

1. 作为系统管理员，您将在载入过程中从Adobe收到多封电子邮件。 查找欢迎电子邮件，其中提供有关您已获得访问权限的组织名称的信息。

1. 单击 **入门** 链接以导航到Admin Console。 如果找不到电子邮件，请直接打开浏览器以在Admin Console [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

   ![欢迎电子邮件](/help/journey-onboarding/assets/get-started-email.png)

1. 使用您的 Adobe ID 登录。成功登录后，您将看到 **概述** 页面。

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. 如果您有权访问多个组织，请确保您已登录到正确的组织。 要更改您的组织，请单击右上角的组织名称，然后选择您需要访问的所需组织。

   ![更改组织](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. 选择 **管理员** 从 **用户** 用于验证您是否是系统管理员的卡。

   ![查看管理员](/help/journey-onboarding/assets/get-started2.png)

1. 单击 **管理员** 从 **用户** 信息卡，您可以通过输入Adobe ID电子邮件、用户名、名字或姓氏进行搜索。

   ![搜索用户](/help/journey-onboarding/assets/get-started3.png)

1. 如果一切正常，搜索将返回您的记录。 如果 **管理员角色** 列显示 **系统**，您（或显示的用户）是系统管理员。

   ![系统状态](/help/journey-onboarding/assets/get-started4.png)

恭喜，系统管理员！

## Adobe Identity Management System {#ims}

AEMas a Cloud Service预配置了AdobeIdentity Management系统（也称为IMS）以进行身份验证。 要启用此功能，您无需以系统管理员身份执行任何操作。

通过使用IMS，AEM  as a Cloud Service可整合AEM与Adobe Experience Cloud其余部分之间的登录体验。 具有多个Adobe产品的组织在Admin Console中创建基于角色的组，然后通过IMS为包括AEM as a Cloud Service在内的多个产品分配访问权限，这对他们特别有益。

您将在此入门历程的下一部分中了解有关产品配置文件和分配用户的更多信息。

## 联系Adobe支持 {#support}

如果您遇到任何问题，可以通过Admin Console访问Adobe支持。 的 **支持** 选项卡，您可以通过简单易用的界面访问各种Adobe支持功能。

![“支持”选项卡](/help/journey-onboarding/assets/support-menu.png)

利用选项卡，可创建和管理案例、直接与Adobe客户支持代表聊天，以及安排与专家的会议。 系统管理员和支持管理员必须登录才能访问支持案例和专家会话选项。

## 下一步 {#whats-next}

现在，您已阅读本文档，您应：

* 明白什么，Adobe ID。
* 能够登录到Admin Console。
* 了解如何以系统管理员的身份通过Admin Console查看您的权限。
* 了解如何联系Adobe支持以获取帮助。

您已准备好通过了解如何 [将团队成员分配给Cloud Manager产品配置文件](assign-profiles-cloud-manager.md) 以便您的同事也可以访问AEMaCS。

## 其他资源 {#additional-resources}

* [Admin Console概述](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)  — 全面概述Admin Console
* [创建或更新Adobe ID](https://helpx.adobe.com/ca/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID)  — 了解如何创建、更改和管理多个Adobe IDIDAdobe。
* [SAML 2.0身份验证处理程序](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html) - AEM随SAML身份验证处理程序一起提供。 此处理程序支持使用HTTPPOST绑定的SAML 2.0身份验证请求协议（Web-SSO配置文件）。
* [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.ug.html)  — 使用Adobe Admin Console，组织可以定义灵活的管理层次结构，以便对Adobe产品访问和使用情况进行细粒度管理。
* [支持和专家会议](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)  — 了解如何在Admin Console中访问支持选项、管理支持案例、安排专家会议，等等。
