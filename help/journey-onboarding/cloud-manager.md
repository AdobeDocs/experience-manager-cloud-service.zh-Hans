---
title: 访问 Cloud Manager
description: 了解如何访问 Cloud Manager，以便您可以设置项目资源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 5c9dbaa25f0142afdae8b09dc18d1e1aaaf4c1fb
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 52%

---

# 访问 Cloud Manager {#cloud-resources}

在 [入门历程，](overview.md) 您将了解如何访问Cloud Manager，以便设置项目资源。

## 目标 {#objective}

在本次入门培训历程的前一篇文章[将团队成员分配给 Cloud Manager 产品配置文件](assign-profiles-cloud-manager.md)中，您已授予 AEMaaCS 团队适当的角色。 现在，了解如何访问Cloud Manager，以便您能够设置团队使用的项目资源。

由于您完成了本次历程的前一步，您的团队可以访问 Cloud Manager。 Cloud Manager 用于创建和管理项目资源，如程序和环境。

阅读本文档后，您应了解以下内容：

* 系统管理员分配给 **业务所有者** 角色必须是您组织中第一个登录并访问Cloud Manager的人。
* 如何登录 Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要组成部分，是您团队的单一入口点。 它通过其专门构建的 CI/CD 管道为具有企业开发设置的客户提供支持，这些管道可确保全面测试和最佳代码质量，从而提供卓越的体验。 Cloud Manager 提供以自助方式启动所需的一切，包括创建云资源和环境的能力。

通常，分配给&#x200B;**业务负责人**&#x200B;产品配置文件的团队成员负责添加您的云资源，如程序和环境。 此人了解业务需求，并了解由谁完成初始 Cloud Manager 设置。

在此载入历程中，您（系统管理员）已经将自己分配给 **业务所有者** 产品配置文件和可以设置云资源。 根据实际项目要求，业务所有者可能与系统管理员相同，也可能与系统管理员不同。

## 作为系统管理员和业务负责人访问 Cloud Manager {#access-sysadmin-bo}

在分配给 **业务所有者** 角色可以访问cloud manager并开始创建云资源，必须为系统管理员分配 **业务所有者** 角色。 他们还必须像您在此入门历程的上一步中所做的那样登录Cloud Manager。

1. 确保您作为系统管理员已分配&#x200B;**业务负责人**&#x200B;角色。

   * 返回到此历程中的上一步， [将团队成员分配给Cloud Manager产品配置文件，](assign-profiles-cloud-manager.md) 以了解有关分配 **业务所有者** 角色。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并显示正常登陆页面。

通过使用&#x200B;**业务负责人**&#x200B;角色以系统管理员身份成功登录，您可以通过&#x200B;**业务负责人**&#x200B;角色初始化 Cloud Manager，以供其他用户使用。 您未收到确认消息或任何消息。 仅仅登录就足够了。

在您以系统管理员的身份登录到Cloud Manager之前，请使用 **业务所有者** 角色的其他用户 **业务所有者** 角色无法在Cloud Manager中创建程序。 即使为他们分配了正确的角色，此规则也是正确的。

## 导航到 Cloud Manager {#navigate-cloud-manager}

具有 **业务所有者** 角色会收到一封欢迎电子邮件，其中包含要开始使用的链接。 按照以下步骤使用此欢迎电子邮件导航到 Cloud Manager。

1. 在欢迎电子邮件中，单击 **入门**，如下图所示。
   ![电子邮件示例](/help/journey-onboarding/assets/get-started-email.png)

1. 导航到Cloud Manager的 **项目和产品** 页面。

   >[!TIP]
   >
   >您还可以直接从 `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)` 导航到 Cloud Manager 的登录页面。 将此页面加入书签以供将来参考。

1. 系统会将您定向到Cloud Manager的登陆页面。

或者，您也可以按照以下步骤从 Adobe Experience Cloud 主页导航到 Cloud Manager 的&#x200B;**程序和产品**&#x200B;页面

1. 直接导航到 [Adobe Experience Cloud](https://experience.adobe.com) 并使用 Adobe ID 登录。

1. 从Adobe Experience Cloud主页中，选择 **Experience Manager** 打开AEM主页。

   ![Experience Cloud 主页](/help/journey-onboarding/assets/setup-resources2.png)

1. 在 **Cloud Manager** 拼贴，选择 **Launch**.

   ![AEM 主页](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登录后，系统会将您定向到Cloud Manager登录页面。 请参阅 [查看Cloud Manager的程序](#viewing-programs) 以了解更多详细信息。

如何通过 Cloud Manager 访问您的程序和产品取决于您，并且不影响您如何使用 Cloud Manager 或如何管理您的程序。

>[!NOTE]
>
>根据在Cloud Manager中分配的角色和应用程序的状态，您在使用Cloud Manager用户界面时会看到不同的屏幕。

## 查看程序 {#viewing-programs}

成功访问Cloud Manager后，您看到的内容取决于程序的状态，如以下各节中所述。

### 当没有程序存在时 {#no-programs}

如果您的组织中不存在任何程序，则登陆页面会指示您创建第一个程序。

![无程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### 当程序已经存在时 {#programs-exist}

如果项目存在于您的组织中，则登录页面会显示您的现有项目，并提供一个用于添加其他项目的按钮。

![程序存在](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### 当程序存在且您是系统管理员时 {#programs-exist-sysadmin}

如果您的组织中存在项目，并且您是系统管理员，则会显示您的登陆页面 **管理访问权限** 按钮与 **添加程序** 选项。

![系统管理员视图](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## 正在验证您的用户角色 {#verify-user-roles}

成功登录 Cloud Manager 后，您可以验证您是否已被分配&#x200B;**业务负责人**&#x200B;产品配置文件。

1. 从窗口的右上角选择您的个人资料。

   ![用户配置文件](/help/journey-onboarding/assets/setup-resources5.png)

1. 要显示分配给用户的角色，请选择 **用户角色**.

   ![用户角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 该对话框应确认您的用户具有&#x200B;**业务负责人**&#x200B;角色。

   ![用户角色列表](/help/journey-onboarding/assets/setup-resources7.png)

您已作为业务负责人成功登录 Cloud Manager！ 如果您未被分配&#x200B;**业务负责人**&#x200B;角色，请联系您的系统管理员。

## 后续内容 {#whats-next}

现在您可以作为系统管理员访问 Cloud Manager，您已经准备好创建第一个程序了。

通过下一步审阅文档，继续入门历程 [创建项目](create-program.md) 从中学习如何执行此操作。

## 其他资源 {#additional-resources}

如果您希望不仅仅访问载入历程的内容，还可以选择使用以下其他资源。

* [Cloud Manager 简介](/help/onboarding/cloud-manager-introduction.md) –
了解 Cloud Manager、Cloud Manager 程序和环境。
* [AEM as a Cloud Service 团队和生产简介](/help/onboarding/aem-cs-team-product-profiles.md) – 了解 AEM as a Cloud Service 团队和产品简介，以及如何授予和限制对您许可的 Adobe 解决方案的访问权限。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
