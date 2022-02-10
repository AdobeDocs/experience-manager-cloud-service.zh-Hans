---
title: 通过 Cloud Manager 设置云资源
description: 了解如何使用Cloud Manager来设置和管理您自己的云资源。
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 1%

---

# 通过 Cloud Manager 设置云资源 {#setup-cloud-resources}

了解如何使用Cloud Manager来设置和管理您自己的云资源。

## 目标 {#objective}

本文档可帮助您了解云资源的创建方式以及创建这些资源的人员。 阅读此部分后，您应该了解：

* 分配给 **业务所有者** 角色必须是您组织中第一个登录并访问Cloud Manager的用户。
* 如何创建云程序和环境。

## Communications API {#introduction}

通过Cloud Manager，由分配给的团队成员通过 **业务所有者** 产品配置文件。 此人员通常是了解业务需求并完成初始Cloud Manager设置的人员。

请阅读以下章节，了解如何创建 [云服务程序](#create-cloud-service-program) 和 [环境。](#create-cloud-environments)

### 前提条件 {#prerequisites}

* 分配给 **业务所有者** 角色必须先登录到Cloud Manager，然后才能使用 **业务所有者** 角色尝试访问Cloud Manager以执行的操作和本文档中描述的步骤。

   * 返回到 [将团队成员分配给Cloud Manager产品配置文件](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) 此历程的文档，以了解更多信息。

* 你必须明白 [导航并登录到Cloud Manager。](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* 您应该熟悉 [Cloud Manager产品配置文件。](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* 您应该了解Cloud Manager的概念 [项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/understand-program-types.md) 和 [环境。](/help/implementing/cloud-manager/manage-environments.md)

## 以系统管理员和业务所有者身份访问Cloud Manager {#access-sysadmin-bo}

在分配给 **业务所有者** 角色可以访问cloud manager并开始创建云资源，则必须为系统管理员分配 **业务所有者** 角色和登录到Cloud Manager。

1. 确保您作为系统管理员，拥有 **业务所有者** 角色。

   * 返回到此历程中的上一步， [将团队成员分配给Cloud Manager产品配置文件，](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) 以了解有关分配 **业务所有者** 角色授予系统管理员（如果尚未这样做）。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并显示正常登陆页面。

通过以系统管理员的身份登录， **业务所有者** 角色，您可以初始化Cloud Manager，以供其他用户使用 **业务所有者** 角色。 您将不会收到此消息或任何消息的确认消息。 只需登录即可。

在您以系统管理员的身份通过 **业务所有者** 角色的其他用户 **业务所有者** 角色将无法在Cloud Manager中创建项目，即使他们被分配了正确的角色。

## 导航到Cloud Manager {#navigate-cloud-manager}

具有 **业务所有者** 角色将收到一封欢迎电子邮件，其中包含要开始使用的链接。 使用此欢迎电子邮件，按照以下步骤导航到Cloud Manager。

1. 在欢迎电子邮件中，单击 **入门**，如下图所示。
   ![电子邮件示例](/help/journey-onboarding/assets/get-started-email.png)

1. 您将导航到Cloud Manager的 **项目和产品** 页面。

   >[!TIP]
   >
   >您还可以从 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). 请将此页面加入书签以供将来参考。

1. 系统会将您定向到Cloud Manager的登陆页面。 请参阅 [查看Cloud Manager的程序](#viewing-programs) 部分以了解更多详细信息。

您还可以导航到Cloud Manager的 **计划和产品** 页面来访问Adobe Experience Cloud主页

1. 直接导航到 [Adobe Experience Cloud](https://experience.adobe.com) 和使用Adobe ID登录。

1. 在Adobe Experience Cloud主页中，选择 **Experience Manager**.

   ![Experience Cloud主页](/help/journey-onboarding/assets/setup-resources2.png)

1. 这会将您转到AEM主页。 从此处，单击 **Launch** 在 **Cloud Manager** 拼贴。

   ![AEM主页](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登录后，系统会将您定向到Cloud Manager的登陆页面。 请参阅 [查看Cloud Manager的程序](#viewing-programs) 部分以了解更多详细信息。

如何通过Cloud Manager访问您的程序和产品取决于您自己，对您使用Cloud Manager的方式或管理程序的方式没有影响。

>[!NOTE]
>
>根据 [!UICONTROL Cloud Manager] 和应用程序的状态，则在使用 [!UICONTROL Cloud Manager] UI。

### 查看程序 {#viewing-programs}

成功访问Cloud Manager后，您将看到什么情况取决于程序的状态，如以下各节中所述。

#### 当不存在程序时 {#no-programs}

如果您的组织中不存在项目，则登陆页面会引导您创建第一个项目。

![无程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### 程序已存在时 {#programs-exist}

如果项目在您的组织中已存在，则登陆页面会显示您的现有项目，并提供一个用于添加其他项目的按钮。

![程序存在](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### 当程序存在且您是系统管理员时 {#programs-exist-sysadmin}

如果您的组织中已存在项目，并且您是系统管理员，则会显示您的登陆页面 **管理访问权限** 按钮与 **添加程序** 选项。

![系统管理员视图](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## 验证用户角色 {#verify-user-roles}

成功登录Cloud Manager后，您可以验证是否已为您分配 **业务所有者** 产品配置文件。

1. 从窗口的右上方选择您的用户档案。

   ![用户配置文件](/help/journey-onboarding/assets/setup-resources5.png)

1. 选择 **用户角色** 以显示分配给用户的角色。

   ![用户角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 确认用户已 **业务所有者** 角色。

   ![用户角色列表](/help/journey-onboarding/assets/setup-resources7.png)

您以业务所有者的身份成功登录到Cloud Manager! 如果未为您分配 **业务所有者** 角色，请与系统管理员联系。

## 创建Cloud Service程序 {#create-cloud-service-program}

现在，您已确保拥有适当的访问权限，接下来可以创建您的第一个程序。

1. 导航到Cloud Manager登录页面( [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 然后登录。

1. 在Cloud Manager登录页面上，单击 **添加程序** 启动“添加程序”向导。

   ![登录页面](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >有关如何使用“添加程序”向导的分步说明，请参阅此文档 [创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-program.md) 或者看这个 [视频](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) 了解如何创建AEM as a Cloud计划，并在创建计划之前了解重要注意事项。


1. 成功创建云程序后，您可以从Cloud Manager登录页面导航到程序，以查看 **概述** 页面。

   ![项目概述](/help/journey-onboarding/assets/setup-resources8.png)

1. 分配给开发人员产品配置文件的成员可以登录到Cloud Manager并管理Cloud Manager git存储库。

   * 如果您尚未这样做，则现在是将成员分配给 **开发人员** 角色。 返回到 [将团队成员分配给Cloud Manager产品配置文件](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) 此历程的文档，以了解更多信息。

现在，您的程序已成功创建，并且您的Cloud Manager git存储库可供开发人员访问！

## 创建云环境 {#create-cloud-environments}

成功创建云程序后，请创建云环境。

1. 导航到Cloud Manager登录页面( [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 选择 **添加** 中。

   ![“添加环境”按钮](/help/journey-onboarding/assets/setup-resources9.png)

1. 将启动“添加环境”向导，并指导您添加环境。 先添加开发环境，以熟悉向导。

   >[!TIP]
   >
   >请参阅文档 [添加环境](/help/implementing/cloud-manager/manage-environments.md#adding-environments) 了解更多或观看 [本快速视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) 以了解Cloud Manager环境以及如何将其添加到项目中。

1. 分配给的成员 **开发人员** 产品配置文件可以登录到Cloud Manager并管理Cloud Manager git存储库。

现在，您的程序已成功创建，并且您的Cloud Manager git可供开发人员访问！

## 下一步 {#whats-next}

现在，您的云资源已创建完毕，并且可供您的团队访问，系统管理员必须将您的团队成员分配给Adobe Admin Console中的AEMas a Cloud Service产品配置文件，才能访问这些资源。

您应该通过下一步审阅文档来继续入门历程 [将团队成员分配给AEMas a Cloud Service产品配置文件](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md) 您将在其中了解如何向团队成员授予他们访问新环境所需的权限。

## 其他资源 {#additional-resources}

请查看其他资源以了解：

* [程序类型和添加程序](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [环境类型和添加环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [管理Cloud Manager Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [配置对AEMas a Cloud Service的Admin Console访问](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
