---
title: 访问 Cloud Manager
description: 了解如何访问 Cloud Manager，以便您可以设置项目资源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: ht
source-wordcount: '1040'
ht-degree: 100%

---

# 访问 Cloud Manager {#cloud-resources}

在[入门历程](overview.md)这部分中，您学习如何访问 Cloud Manager，以使您可设置您的项目资源。

## 目标 {#objective}

在本次入门历程的前一篇文章[将团队成员分配给 Cloud Manager 产品配置文件](assign-profiles-cloud-manager.md)中，您已授予 AEMaaCS 团队适当的角色。 现在学习如何访问 Cloud Manager，以使您可设置您的团队使用的项目资源。

由于您完成了本次历程的前一步，您的团队可以访问 Cloud Manager。 Cloud Manager 用于创建和管理项目资源，如程序和环境。

阅读本文档后，您应该了解以下内容：

* 分配给&#x200B;**业务负责人**&#x200B;角色的系统管理员必须是您的组织中登录和访问 Cloud Manager 的第一人。
* 如何登录 Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要组成部分，是您团队的单一入口点。 它通过其专门构建的 CI/CD 管道为具有企业开发设置的客户提供支持，这些管道可确保全面测试和最佳代码质量，从而提供卓越的体验。 Cloud Manager 提供以自助方式启动所需的一切，包括创建云资源和环境的能力。

通常，分配给&#x200B;**业务负责人**&#x200B;产品配置文件的团队成员负责添加您的云资源，如程序和环境。 此人了解业务需求，并了解由谁完成初始 Cloud Manager 设置。

为了完成此次入门历程，您作为系统管理员，已将自己分配给&#x200B;**业务负责人**&#x200B;产品配置文件，并可设置云资源。根据实际项目要求的不同，业务负责人可能与系统管理员相同，也可能不同。

## 作为系统管理员和业务负责人访问 Cloud Manager {#access-sysadmin-bo}

必须为系统管理员分配&#x200B;**业务负责人**&#x200B;角色，然后您分配给&#x200B;**业务负责人**&#x200B;角色的团队成员才能访问 Cloud Manager 并开始创建云资源。他们还必须像您在此入门历程上一步中的那样登录到 Cloud Manager。

1. 确保为作为系统管理员的您分配了&#x200B;**业务负责人**&#x200B;角色。

   * 返回本次历程中的上一步，[将团队成员分配给 Cloud Manager 产品配置文件](assign-profiles-cloud-manager.md)以获得有关将&#x200B;**业务负责人**&#x200B;角色分配给系统管理员的详细信息。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并显示正常登陆页面。

通过使用&#x200B;**业务负责人**&#x200B;角色以系统管理员身份成功登录，您可以通过&#x200B;**业务负责人**&#x200B;角色初始化 Cloud Manager，以供其他用户使用。 您不会收到确认或任何消息。只需登录即可。

直到您作为具有&#x200B;**业务负责人**&#x200B;角色的系统管理员身份登录到 Cloud Manager，其他具有&#x200B;**业务负责人**&#x200B;角色的用户才能在 Cloud Manager 中创建项目。即使为这些用户分配的角色正确无误，这条规则也适用。

## 导航到 Cloud Manager {#navigate-cloud-manager}

具有&#x200B;**业务负责人**&#x200B;角色的用户收到一封欢迎电子邮件，其中包含开始使用的链接。按照以下步骤使用此欢迎电子邮件导航到 Cloud Manager。

1. 在欢迎电子邮件中，单击&#x200B;**开始使用**，如下图所示。
   ![电子邮件示例](/help/journey-onboarding/assets/get-started-email.png)

1. 导航到 Cloud Manager 的&#x200B;**项目和产品**&#x200B;页面。

   >[!TIP]
   >
   >还可直接从 `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)` 导航到 Cloud Manager 的登录页面。请将此页加入书签以供将来参考。

1. 您被引入 Cloud Manager 的登陆页面。

或者，您也可以按照以下步骤从 Adobe Experience Cloud 主页导航到 Cloud Manager 的&#x200B;**程序和产品**&#x200B;页面

1. 直接导航到 [Adobe Experience Cloud](https://experience.adobe.com) 并使用 Adobe ID 登录。

1. 从 Adobe Experience Cloud 主页中，选择 **Experience Manager** 以打开 AEM 主页。

   ![Experience Cloud 主页](/help/journey-onboarding/assets/setup-resources2.png)

1. 在 **Cloud Manager** 磁贴上，选择&#x200B;**启动**。

   ![AEM 主页](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登录后，您被引入 Cloud Manager 的登陆页面。有关更多详细信息，请参阅[查看 Cloud Manager 的项目](#viewing-programs)。

如何通过 Cloud Manager 访问您的项目和产品由您决定，并且不影响您如何使用 Cloud Manager 或如何管理您的项目。

>[!NOTE]
>
>根据在 Cloud Manager 中分配的角色和应用项目的状态，您在使用 Cloud Manager 用户界面时看到不同的屏幕。

## 查看项目 {#viewing-programs}

一旦您成功访问 Cloud Manager，您所看到的内容将取决于您的项目状态，详见以下部分。

### 当没有程序存在时 {#no-programs}

如果您的组织中不存在任何程序，则登陆页面会指示您创建第一个程序。

![无程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### 当程序已经存在时 {#programs-exist}

如果您的组织中存在项目，则登陆页将显示现有项目，并提供添加其他项目的按钮。

![程序存在](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### 当程序存在且您是系统管理员时 {#programs-exist-sysadmin}

如果您所在的组织中存在项目，并且您是系统管理员，则登陆页面将显示&#x200B;**管理访问权限**&#x200B;按钮以及&#x200B;**添加项目**&#x200B;选项。

![系统管理员视图](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## 正在验证您的用户角色 {#verify-user-roles}

成功登录 Cloud Manager 后，您可以验证您是否已被分配&#x200B;**业务负责人**&#x200B;产品配置文件。

1. 从窗口的右上角选择您的个人资料。

1. 选择&#x200B;**用户角色**，以显示分配给用户的角色。

   ![用户角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 该对话框应确认您的用户具有&#x200B;**业务负责人**&#x200B;角色。

   ![用户角色列表](/help/journey-onboarding/assets/setup-resources7.png)

您已作为业务负责人成功登录 Cloud Manager！ 如果您未被分配&#x200B;**业务负责人**&#x200B;角色，请联系您的系统管理员。

## 后续内容 {#whats-next}

现在您可以作为系统管理员访问 Cloud Manager，您已经准备好创建第一个项目了。

继续您的入门历程，然后查看文档[创建项目](create-program.md)，在那里您将学习如何创建项目。

## 其他资源 {#additional-resources}

如果您想了解入门历程以外的内容，以下是额外的可选资源。

* [Cloud Manager 简介](/help/onboarding/cloud-manager-introduction.md) –
了解 Cloud Manager、Cloud Manager 项目和环境。
* [AEM as a Cloud Service 团队和生产简介](/help/onboarding/aem-cs-team-product-profiles.md) – 了解 AEM as a Cloud Service 团队和产品简介，以及如何授予和限制对您许可的 Adobe 解决方案的访问权限。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
