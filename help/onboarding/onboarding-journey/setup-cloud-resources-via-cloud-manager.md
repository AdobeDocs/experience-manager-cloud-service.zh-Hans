---
title: 通过Cloud Manager设置云资源
description: 请阅读本页内容，了解如何通过Cloud Manager设置云资源
hide: true
hidefromtoc: true
index: false
source-git-commit: 5f599eb877565c65aad3d54af411bd8d40f4580d
workflow-type: tm+mt
source-wordcount: '1429'
ht-degree: 0%

---

# 通过Cloud Manager设置云资源 {#setup-cloud-resources}

分配给业务所有者角色的系统管理员应该有权访问并登录到Cloud Manager。 之后，分配给业务所有者产品配置文件的团队成员必须登录到Cloud Manager并创建您的云计划和环境，以便您的专家团队能够开始工作。

## 目标 {#objective}

本文档可帮助您了解云资源的创建方式以及谁可以执行此操作。

阅读此部分后，您应该了解：

* 分配给业务所有者角色的系统管理员必须是第一个访问和登录Cloud Manager的管理员。
* 如何创建云程序和环境。

## 简介 {#introduction}

由分配给Cloud Manager业务所有者产品配置文件的团队成员通过Cloud Manager来添加云资源。 此人员通常是了解业务需求并完成初始Cloud Manager设置的人员。

请按照以下各节了解如何创建[云服务程序](#create-cloud-service-program)和[环境](#create-cloud-environments)。

### 先决条件 {#prerequisites}

* 分配给业务所有者角色的系统管理员应该有权访问并登录到Cloud Manager。

* 了解如何[导航和登录到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en)。

* 熟悉[Cloud Manager产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)。

* 了解Cloud Manager [程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html?lang=en)和[环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en)的概念

## 导航到Cloud Manager {#navigate-cloud-manager}

业务所有者用户将收到一封欢迎电子邮件，其中包含要开始使用的链接，或者如果找不到该链接，则直接转到[Adobe Experience Cloud](https://experience.adobe.com)并使用Adobe ID登录。

按照以下步骤导航到Cloud Manager:

1. 在欢迎电子邮件中，单击&#x200B;**开始**，如下图所示。
   ![](/help/onboarding/onboarding-journey/assets/get-started-email.png)

1. 您将导航到Cloud Manager的&#x200B;**程序和产品**&#x200B;页面。

   >[!IMPORTANT]
   >或者，您也可以从[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)直接导航到Cloud Manager的登录页面。 请将此页面加入书签以供将来参考，并帮助您直接导航到Cloud Manager的登陆页面。

1. 系统会将您定向到Cloud Manager的登陆页面。 有关更多详细信息，请参阅[查看Cloud Manager的程序](#viewing-programs)部分。

此外，您还可以从Adobe Experience Cloud主页导航到Cloud Manager的&#x200B;**程序和产品**&#x200B;页面。 应遵循以下步骤：

1. 直接导航到[Adobe Experience Cloud](https://experience.adobe.com)，然后使用Adobe ID登录。

1. 在Adobe Experience Cloud主页中，选择&#x200B;**Experience Manager**。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources2.png)

1. 这会将您转到AEM主页。 从此处启动&#x200B;**Cloud Manager** 。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources3.png)

1. 成功登录后，系统会将您定向到Cloud Manager的登陆页面。 有关更多详细信息，请参阅[查看Cloud Manager的程序](#viewing-programs)部分。

   >[!NOTE]
   >根据在[!UICONTROL Cloud Manager]中分配的角色和应用程序的状态，在使用[!UICONTROL Cloud Manager] UI时，您将看到不同的屏幕。

### 在Cloud Manager的登录页面中查看项目 {#viewing-programs}

成功登录后，系统会将您定向到Cloud Manager的登陆页面。 您将看到以下三个选项之一：

#### Cloud Manager中不存在程序时 {#no-programs}

如果您的组织中不存在项目，则登陆页面会引导您创建第一个项目，如下图所示。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### 当Cloud Manager中已存在程序时 {#programs-exist}

如果组织中已存在项目，则登录页面会指示您添加其他项目，并显示所有现有项目，如下图所示。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### 当程序存在且用户是系统管理员时 {#programs-exist-sysadmin}

如果组织中已存在项目，并且您是系统管理员，则登录页面会显示&#x200B;**管理访问**&#x200B;按钮以及&#x200B;**添加项目**&#x200B;选项，如下图所示。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## 验证用户角色 {#verify-user-roles}

成功登录Cloud Manager后，请按照以下步骤验证是否已为您分配了“业务所有者产品配置文件”：

1. 从右上方选择您的用户档案，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources5.png)

1. 选择&#x200B;**用户角色**&#x200B;并确保将您分配给业务所有者。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources6.png)

1. 这将确认您作为业务所有者的用户角色。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources7.png)

   干得好！ 您以业务所有者的身份成功登录到Cloud Manager!

## 创建Cloud Service程序 {#create-cloud-service-program}

请按照以下步骤从Cloud Manager创建云服务程序：

1. 导航到Cloud Manager登录页面，如下所示。

   >[!NOTE]
   >您必须是分配给Cloud Manager业务所有者产品配置文件的团队成员，才能成功完成此步骤。

   从此处，单击&#x200B;**添加程序**&#x200B;以启动“添加程序”向导。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

   >[!NOTE]
   >请观看[视频](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)，了解如何创建AEM as a Cloud程序，并在创建程序之前了解重要注意事项。

   >[!IMPORTANT]
   >有关如何使用“添加程序”向导的分步说明，请转至[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en)。
   >
   >* 请记住，程序名称在创建后无法更改。 我们建议您确定您希望给程序提供什么名称。
   >* 如果您必须更改项目名称，则需要通过Adobe支持部门打开一个案例，或者联系您的Adobe代表。 他们将协助有效删除该程序。 您必须重新开始工作，您的团队可能会失去工作。


1. 成功创建云程序后，您可以导航到程序以查看程序的&#x200B;**概述**&#x200B;页面，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources8.png)

   >[!NOTE]
   >如果您尚未执行此操作，现在可以将开发人员成员添加到您的Cloud Manager团队。 请参阅将用户添加到开发人员产品配置文件，并按照列出的步骤操作。

1. 分配给开发人员产品配置文件的成员可以登录到Cloud Manager和[管理Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)。

   干得好！ 现在，您的程序已成功创建，您的Cloud Manager Git可供开发人员访问！


## 创建云环境 {#create-cloud-environments}

成功创建云程序后，请创建云环境。

请按照以下步骤从Cloud Manager创建云环境：

1. 导航到Cloud Manager的&#x200B;**概述**&#x200B;页面，然后从环境卡中选择&#x200B;**添加**。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources9.png)

   >[!IMPORTANT]
   >必须登录具有“业务所有者”或“部署管理器”角色的Cloud Manager用户，才能成功完成此步骤。

   此外，请观看[视频](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en)快速教程，了解Cloud Manager环境以及如何将它们添加到您的项目中。

1. 这将启动“添加环境”向导，该向导将指导您添加环境。 先添加开发环境，以熟悉向导。 请参阅[添加环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments)以了解更多信息。

   >[!NOTE]
   >如果您尚未执行此操作，现在可以将开发人员成员添加到您的Cloud Manager团队。 请参阅将用户添加到开发人员产品配置文件，并按照列出的步骤操作。

1. 分配给开发人员产品配置文件的成员可以登录到Cloud Manager和[管理Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)。

   干得好！ 现在，您的程序已成功创建，并且您的Cloud Manager Git可供开发人员访问！

   恭喜！ 现在，您的云程序环境已创建完毕，并且开发人员已添加到团队中！

## 下一步 {#whats-next}

您的团队成员必须获得对实例的权限，因为管理Cloud Manager的权限是不够的。 现在，您的云资源已创建完毕，并且可供您的团队访问，系统管理员必须将您的团队成员作为Adobe Admin Console中的Cloud Service产品配置文件分配给AEM。

>[!NOTE]
>要获得AEM as a Cloud Service用户的访问权限，用户必须属于两个产品配置文件`AEM Users`或`AEM Administrators`中的一个。 请参阅[管理Admin Console中的产品和用户访问权限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console)以了解更多信息。

您应该通过下一步审阅将团队成员作为Cloud Service产品配置文件分配给AEM文档，来继续入门历程。


## 其他资源 {#additional-resources}

请查看其他资源以了解：

* [程序类型和添加程序](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)
* [环境类型和添加环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en)
* [管理Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)
* [将对AEM的访问配置为从Admin ConsoleCloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#adobe-ims-users)
