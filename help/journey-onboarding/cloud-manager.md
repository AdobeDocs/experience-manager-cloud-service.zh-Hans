---
title: 访问 Cloud Manager
description: 了解如何访问 Cloud Manager，以便您可以设置项目资源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 0db48ef4c15b6ca530b2626f7078c7172c872fff
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 63%

---

# 访问 Cloud Manager {#cloud-resources}

在[加入历程](overview.md)的这一部分中，您学习如何访问 Cloud Manager，以使您可设置您的项目资源。

## 目标 {#objective}

在本次加入历程的前一篇文章[将团队成员分配给 Cloud Manager 产品配置文件](assign-profiles-cloud-manager.md)中，您已授予 AEMaaCS 团队适当的角色。 现在，了解如何访问Cloud Manager，以便您可以设置团队打算使用的项目资源。

由于您完成了本次历程的前一步，您的团队可以访问 Cloud Manager。 Cloud Manager用于创建和管理项目资源，如程序和环境。

阅读本文档后，您应该了解以下内容：

* 分配给&#x200B;**业务负责人**&#x200B;角色的系统管理员必须是您的组织中登录和访问 Cloud Manager 的第一人。
* 如何登录 Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要组成部分，是您团队的单一入口点。 它通过其专门构建的 CI/CD 管道为具有企业开发设置的客户提供支持，这些管道可确保全面测试和最佳代码质量，从而提供卓越的体验。 Cloud Manager提供以自助方式开始所需的一切，包括创建云资源和环境的能力。

通常，分配给&#x200B;**业务负责人**&#x200B;产品配置文件的团队成员负责添加您的云资源，如程序和环境。 此人了解业务需求，并了解由谁完成初始 Cloud Manager 设置。

为了完成此次加入历程，您作为系统管理员，已将自己分配给&#x200B;**业务负责人**&#x200B;产品配置文件，并可设置云资源。根据实际项目要求的不同，业务负责人可能与系统管理员相同，也可能不同。

## 作为系统管理员和业务负责人访问 Cloud Manager {#access-sysadmin-bo}

在您分配给&#x200B;**业务负责人**&#x200B;角色的团队成员可以访问Cloud Manager并开始创建云资源之前，必须为系统管理员分配&#x200B;**业务负责人**&#x200B;角色。 他们还必须像您在此加入历程上一步中的那样登录到 Cloud Manager。

1. 确保为作为系统管理员的您分配了&#x200B;**业务负责人**&#x200B;角色。

   返回上一步[将团队成员分配给Cloud Manager产品配置文件](assign-profiles-cloud-manager.md)，了解有关将&#x200B;**业务负责人**&#x200B;角色分配给系统管理员的详细信息。

1. 在[experience.adobe.com](https://experience.adobe.com)登录Cloud Manager。
1. 在快速访问分组中，单击&#x200B;**Experience Manager**。
1. 单击左侧面板中的&#x200B;**Cloud Manager**。

   控制台![Cloud Manager](/help/journey-onboarding/assets/consol-cloud-manager.png)

通过使用&#x200B;**业务负责人**&#x200B;角色以系统管理员身份成功登录，您可以使用Cloud Manager供具有&#x200B;**业务负责人**&#x200B;角色的其他用户使用。 您不会收到确认或任何消息。只需登录即可。

在您使用&#x200B;**业务负责人**&#x200B;角色以系统管理员身份登录Cloud Manager之前，具有&#x200B;**业务负责人**&#x200B;角色的其他用户无法在Cloud Manager中创建程序。 即使为这些用户分配的角色正确无误，这条规则也适用。

## 导航到 Cloud Manager {#navigate-cloud-manager}

具有&#x200B;**业务负责人**&#x200B;角色的用户收到一封欢迎电子邮件，其中包含开始使用的链接。按照以下步骤使用此欢迎电子邮件导航到 Cloud Manager。

1. 在欢迎电子邮件中，单击&#x200B;**开始使用**，如下图所示。
   ![电子邮件示例](/help/journey-onboarding/assets/get-started-email.png)

1. 导航到 Cloud Manager 的&#x200B;**程序和产品**&#x200B;页面。

   >[!TIP]
   >
   >还可直接从 `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)` 导航到 Cloud Manager 的登录页面。请将此页加入书签以供将来参考。

1. 您被引入 Cloud Manager 的登陆页面。

<!-- OLD
Alternatively, you can navigate to Cloud Manager's **Programs and Products** page from the Adobe Experience Cloud home page using these steps.

1. Navigate directly to [Adobe Experience Cloud](https://experience.adobe.com) and login using your Adobe ID.

1. From the Adobe Experience Cloud home page, select **Experience Manager** to open the AEM home page.

   ![Experience Cloud homepage](/help/journey-onboarding/assets/setup-resources2.png)

1. On the **Cloud Manager** tile, select **Launch**.

   ![AEM home page](/help/journey-onboarding/assets/setup-resources3.png)

1. After successfully logging on, you are directed to the Cloud Manager landing page. See [Viewing Cloud Manager's Programs](#viewing-programs) for more details.

How you access your programs and products via Cloud Manager is up to you and has no effect on how you use Cloud Manager or how you manage your programs.

>[!NOTE]
>
>Depending on the roles assigned in Cloud Manager and the state of the application, you see different screens while using the Cloud Manager user interface. -->

## 查看项目群 {#viewing-programs}

一旦您成功访问 Cloud Manager，您所看到的内容将取决于您的程序状态，详见以下部分。

### 当不存在程序时 {#no-programs}

如果您的组织中不存在任何程序，则登陆页面会指示您创建第一个程序。

![无程序](/help/journey-onboarding/assets/cloud-manager-programs-do-not-exist.png)

### 当程序已存在时 {#programs-exist}

如果您的组织中存在程序，则登陆页将显示现有程序，并提供添加其他程序的按钮。

![程序存在](/help/journey-onboarding/assets/cloud-manager-programs-exist.png)

### 当程序存在并且您是系统管理员时 {#programs-exist-sysadmin}

如果您的组织中存在程序，并且您是系统管理员，则登陆页面将显示&#x200B;**管理访问权限**&#x200B;按钮以及&#x200B;**添加程序**&#x200B;选项。

![系统管理员视图](/help/journey-onboarding/assets/cloud-manager-programs-as-sysadmin.png)

## 验证您的用户角色 {#verify-user-roles}

成功登录Cloud Manager后，您可以验证您是否分配了&#x200B;**业务负责人**&#x200B;产品配置文件。

1. 在页面的右上角附近，单击&#x200B;**帐户**&#x200B;图标。

1. 单击&#x200B;**用户角色**。

   ![用户角色](/help/journey-onboarding/assets/cloud-manager-user-roles.png)

1. 在&#x200B;**用户角色**&#x200B;对话框中，确认您的用户具有&#x200B;**业务负责人**&#x200B;角色。

   ![用户角色列表](/help/journey-onboarding/assets/cloud-manager-user-roles-business-owner.png)

您已作为业务负责人成功登录Cloud Manager。 如果您未被分配&#x200B;**业务负责人**&#x200B;角色，请联系您的系统管理员。

## 后续内容 {#whats-next}

现在您可以作为系统管理员访问 Cloud Manager，您已经准备好创建第一个程序了。

继续您的加入历程，然后查看文档[创建程序](create-program.md)，在那里您将学习如何创建程序。

## 其他资源 {#additional-resources}

如果您想了解加入历程以外的内容，以下是额外的可选资源。

* [Cloud Manager 简介](/help/onboarding/cloud-manager-introduction.md) –
了解 Cloud Manager、Cloud Manager 程序和环境。
* [AEM as a Cloud Service 团队和产品配置文件](/help/onboarding/aem-cs-team-product-profiles.md) – 了解 AEM as a Cloud Service 团队和产品配置文件如何授予和限制访问您经许可的 Adobe 解决方案。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
