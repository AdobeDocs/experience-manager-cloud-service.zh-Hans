---
title: 访问 Cloud Manager
description: 了解如何访问Cloud Manager，以便设置项目资源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: fbf1e0b7cefb1dc981d7ee106283280fb2225007
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 1%

---

# 访问 Cloud Manager {#cloud-resources}

在 [入门历程，](overview.md) 您将了解如何访问Cloud Manager，以便设置项目资源。

## 目标 {#objective}

在本入门历程的上一篇文章中， [将团队成员分配给Cloud Manager产品配置文件，](assign-profiles-cloud-manager.md) 您授予AEMaaCS团队适当的角色。 现在，了解如何访问Cloud Manager，以便您能够设置团队将使用的项目资源。

由于您已完成此历程中的上一步，因此您的团队可以访问Cloud Manager。 Cloud Manager用于创建和管理项目资源，如项目和环境。

阅读本文档后，您应该了解：

* 系统管理员分配给 **业务所有者** 角色必须是您组织中第一个登录并访问Cloud Manager的用户。
* 如何登录Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager是AEMas a Cloud Service的一个基本组件，是您团队的单个入口点。 它通过专门构建的CI/CD管道为具有企业开发设置的客户提供支持，这些管道可确保进行彻底的测试和最高的代码质量，以提供卓越的体验。 Cloud Manager以自助方式提供入门所需的一切功能，包括创建云资源和环境的功能。

通常是分配给 **业务所有者** 产品配置文件负责添加云资源，如程序和环境。 此人员了解业务需求以及完成Cloud Manager初始设置的人员。

在此载入历程中，您（系统管理员）已经将自己分配给 **业务所有者** 产品配置文件和将设置云资源。 根据实际项目要求，业务所有者可能与系统管理员相同，也可能与系统管理员不同。

>[!NOTE]
>
>默认情况下，有权访问AEM环境的用户也将具有Cloud > Manager用户角色。 此角色本身及其本身不足以授予用户访问项目详细信息视图的权限。 此类仅具有Cloud Manager用户角色的用户能够通过项目菜单选项导航到AEM环境创作URL（如果存在环境）。 如果此类用户希望获得程序级访问权限，则必须联系其管理员。

## 以系统管理员和业务所有者身份访问Cloud Manager {#access-sysadmin-bo}

在分配给 **业务所有者** 角色可以访问cloud manager并开始创建云资源，必须为系统管理员分配 **业务所有者** 角色，并像在此入门历程的上一步中一样登录到Cloud Manager。

1. 确保您以系统管理员的身份，将 **业务所有者** 角色。

   * 返回到此历程中的上一步， [将团队成员分配给Cloud Manager产品配置文件，](assign-profiles-cloud-manager.md) 以了解有关分配 **业务所有者** 角色授予系统管理员（如果尚未这样做）。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并显示正常登陆页面。

通过以系统管理员的身份成功登录 **业务所有者** 角色，您可以初始化Cloud Manager，以供其他用户使用 **业务所有者** 角色。 您将不会收到此消息或任何消息的确认消息。 只需登录即可。

在您以系统管理员的身份登录到Cloud Manager之前，请使用 **业务所有者** 角色的其他用户 **业务所有者** 角色将无法在Cloud Manager中创建项目，即使他们被分配了正确的角色。

## 导航到Cloud Manager {#navigate-cloud-manager}

具有 **业务所有者** 角色将收到一封欢迎电子邮件，其中包含要开始使用的链接。 使用此欢迎电子邮件，按照以下步骤导航到Cloud Manager。

1. 在欢迎电子邮件中，单击 **入门**，如下图所示。
   ![电子邮件示例](/help/journey-onboarding/assets/get-started-email.png)

1. 您将导航到Cloud Manager的 **项目和产品** 页面。

   >[!TIP]
   >
   >您还可以从 `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. 请将此页面加入书签以供将来参考。

1. 系统会将您定向到Cloud Manager的登陆页面。

或者，您也可以导航到Cloud Manager的 **计划和产品** 页面来访问Adobe Experience Cloud主页

1. 直接导航到 [Adobe Experience Cloud](https://experience.adobe.com) 和使用Adobe ID登录。

1. 在Adobe Experience Cloud主页中，选择 **Experience Manager**.

   ![Experience Cloud主页](/help/journey-onboarding/assets/setup-resources2.png)

1. 这会将您转到AEM主页。 从此处，单击 **Launch** 在 **Cloud Manager** 拼贴。

   ![AEM主页](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登录后，系统会将您定向到Cloud Manager的登陆页面。 请参阅 [查看Cloud Manager的程序](#viewing-programs) 部分以了解更多详细信息。

如何通过Cloud Manager访问您的程序和产品取决于您自己，对您使用Cloud Manager的方式或管理程序的方式没有影响。

>[!NOTE]
>
>根据在Cloud Manager中分配的角色和应用程序的状态，您在使用Cloud Manager UI时将看到不同的屏幕。

## 查看程序 {#viewing-programs}

成功访问Cloud Manager后，您将看到什么情况取决于程序的状态，如以下各节中所述。

### 当不存在程序时 {#no-programs}

如果您的组织中不存在项目，则登陆页面会引导您创建第一个项目。

![无程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### 程序已存在时 {#programs-exist}

如果项目在您的组织中已存在，则登陆页面会显示您的现有项目，并提供一个用于添加其他项目的按钮。

![程序存在](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### 当程序存在且您是系统管理员时 {#programs-exist-sysadmin}

如果您的组织中已存在项目，并且您是系统管理员，则会显示您的登陆页面 **管理访问权限** 按钮与 **添加程序** 选项。

![系统管理员视图](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## 验证用户角色 {#verify-user-roles}

成功登录Cloud Manager后，您可以验证是否已为您分配 **业务所有者** 产品配置文件。

1. 从窗口的右上方选择您的用户档案。

   ![用户配置文件](/help/journey-onboarding/assets/setup-resources5.png)

1. 选择 **用户角色** 以显示分配给用户的角色。

   ![用户角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 对话框应确认您的用户在 **业务所有者** 角色。

   ![用户角色列表](/help/journey-onboarding/assets/setup-resources7.png)

您以业务所有者的身份成功登录到Cloud Manager! 如果未为您分配 **业务所有者** 角色，请与系统管理员联系。

## 下一步 {#whats-next}

现在，您可以以系统管理员身份访问Cloud Manager，接下来就可以创建您的第一个项目。

您应该通过下一步审阅文档来继续入门历程 [创建项目](create-program.md) 你将在那里学习如何这样做。

## 其他资源 {#additional-resources}

请查看其他资源以了解：

* [Cloud Manager简介](/help/onboarding/cloud-manager-introduction.md)  — 了解Cloud Manager、Cloud Manager程序和环境。
