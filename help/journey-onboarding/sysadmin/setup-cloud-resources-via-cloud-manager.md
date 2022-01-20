---
title: 通过 Cloud Manager 设置云资源
description: 请阅读本页内容，了解如何通过Cloud Manager设置云资源
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 7fe39bbc8d5e965af7f339b2a524420c76360552
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 1%

---

# 通过 Cloud Manager 设置云资源 {#setup-cloud-resources}

分配给业务所有者角色的系统管理员应该有权访问并登录到Cloud Manager。 之后，分配给业务所有者产品配置文件的团队成员必须登录到Cloud Manager并创建您的云计划和环境，以便您的专家团队能够开始工作。

## 目标 {#objective}

本文档可帮助您了解云资源的创建方式以及谁可以执行此操作。

阅读此部分后，您应该了解：

* 分配给业务所有者角色的系统管理员必须是第一个访问和登录Cloud Manager的管理员。
* 如何创建云程序和环境。

## 简介 {#introduction}

由分配给Cloud Manager业务所有者产品配置文件的团队成员通过Cloud Manager来添加云资源。 此人员通常是了解业务需求并完成初始Cloud Manager设置的人员。

请阅读以下章节，了解如何创建 [云服务程序](#create-cloud-service-program) 和 [环境。](#create-cloud-environments)

### 先决条件 {#prerequisites}

* 分配给业务所有者角色的系统管理员应该有权访问并登录到Cloud Manager。

* 了解如何 [导航并登录到Cloud Manager。](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* 熟悉 [Cloud Manager产品配置文件。](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* 了解Cloud Manager的概念 [项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/understand-program-types.md) 和 [环境。](/help/implementing/cloud-manager/manage-environments.md)

## 导航到Cloud Manager {#navigate-cloud-manager}

业务所有者用户将收到一封欢迎电子邮件，其中包含要开始使用的链接，或者，如果找不到，则访问 [Cloud Manager](https://my.cloudmanager.adobe.com/) 直接通过使用您的Adobe ID登录。

按照以下步骤导航到Cloud Manager:

1. 在欢迎电子邮件中，单击 **入门**，如下图所示。
   ![](/help/journey-onboarding/assets/get-started-email.png)

1. 您将导航到Cloud Manager的 **项目和产品** 页面。

   >[!IMPORTANT]
   >
   >或者，您也可以从 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). 请将此页面加入书签以供将来参考，并帮助您直接导航到Cloud Manager的登陆页面。

1. 系统会将您定向到Cloud Manager的登陆页面。 请参阅 [查看Cloud Manager的程序](#viewing-programs) 部分以了解更多详细信息。

此外，您还可以导航到Cloud Manager的 **计划和产品** 页面来自Adobe Experience Cloud主页。 应遵循以下步骤：

1. 直接导航到 [Adobe Experience Cloud](https://experience.adobe.com) 和使用Adobe ID登录。

1. 在Adobe Experience Cloud主页中，选择 **Experience Manager**.

   ![](/help/journey-onboarding/assets/setup-resources2.png)

1. 这会将您转到AEM主页。 从此处，启动 **Cloud Manager** .

   ![](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登录后，系统会将您定向到Cloud Manager的登陆页面。 请参阅 [查看Cloud Manager的程序](#viewing-programs) 部分以了解更多详细信息。

   >[!NOTE]
   >
   >根据 [!UICONTROL Cloud Manager] 和应用程序的状态，则在使用 [!UICONTROL Cloud Manager] UI。

### 在Cloud Manager的登录页面中查看项目 {#viewing-programs}

成功登录后，系统会将您定向到Cloud Manager的登陆页面。 您将看到以下三个选项之一：

#### Cloud Manager中不存在程序时 {#no-programs}

如果您的组织中不存在项目，则登陆页面会引导您创建第一个项目，如下图所示。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### 当Cloud Manager中已存在程序时 {#programs-exist}

如果组织中已存在项目，则登录页面会指示您添加其他项目，并显示所有现有项目，如下图所示。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### 当程序存在且用户是系统管理员时 {#programs-exist-sysadmin}

如果您的组织中已存在项目，并且您是系统管理员，则会显示您的登陆页面 **管理访问权限** 按钮与 **添加程序** 选项，如下图所示。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## 验证用户角色 {#verify-user-roles}

成功登录Cloud Manager后，请按照以下步骤验证是否已为您分配了“业务所有者产品配置文件”：

1. 从右上方选择您的用户档案，如下所示。

   ![](/help/journey-onboarding/assets/setup-resources5.png)

1. 选择 **用户角色** 并确保您被分配给业务所有者。

   ![](/help/journey-onboarding/assets/setup-resources6.png)

1. 这将确认您作为业务所有者的用户角色。

   ![](/help/journey-onboarding/assets/setup-resources7.png)

   干得好！ 您以业务所有者的身份成功登录到Cloud Manager!

## 创建Cloud Service程序 {#create-cloud-service-program}

请按照以下步骤从Cloud Manager创建云服务程序：

1. 导航到Cloud Manager登录页面，如下所示。

   >[!NOTE]
   >
   >您必须是分配给Cloud Manager业务所有者产品配置文件的团队成员，才能成功完成此步骤。

   从此处，单击 **添加程序** 启动“添加程序”向导。

   ![](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >观看 [视频](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) 了解如何创建AEM as a Cloud计划，并在创建计划之前了解重要注意事项。

   >[!TIP]
   >
   >有关如何使用“添加程序”向导的分步说明，请转至 [此处](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-program.md).

1. 成功创建云程序后，您可以导航到程序以查看 **概述** 页面，如下所示。

   ![](/help/journey-onboarding/assets/setup-resources8.png)

   >[!NOTE]
   >
   >如果您尚未执行此操作，现在可以将开发人员成员添加到您的Cloud Manager团队。 请参阅将用户添加到开发人员产品配置文件，并按照列出的步骤操作。

1. 分配给开发人员产品配置文件的成员可以登录Cloud Manager和 [管理Cloud Manager Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

   干得好！ 现在，您的程序已成功创建，您的Cloud Manager Git可供开发人员访问！


## 创建云环境 {#create-cloud-environments}

成功创建云程序后，请创建云环境。

请按照以下步骤从Cloud Manager创建云环境：

1. 导航到Cloud Manager的 **概述** 页面并选择 **添加** 中。

   ![](/help/journey-onboarding/assets/setup-resources9.png)

   >[!IMPORTANT]
   >
   >必须登录具有“业务所有者”或“部署管理器”角色的Cloud Manager用户，才能成功完成此步骤。

   此外，请快速观看 [视频](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) 教程，了解如何将Cloud Manager环境以及如何将其添加到项目中。

1. 这将启动“添加环境”向导，该向导将指导您添加环境。 先添加开发环境，以熟悉向导。 请参阅 [添加环境](/help/implementing/cloud-manager/manage-environments.md#adding-environments) 以了解更多。

   >[!NOTE]
   >
   >如果您尚未执行此操作，现在可以将开发人员成员添加到您的Cloud Manager团队。 请参阅将用户添加到开发人员产品配置文件，并按照列出的步骤操作。

1. 分配给开发人员产品配置文件的成员可以登录Cloud Manager和 [管理Cloud Manager Git。](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

   干得好！ 现在，您的程序已成功创建，并且您的Cloud Manager Git可供开发人员访问！

   恭喜！ 现在，您的云程序环境已创建完毕，并且开发人员已添加到团队中！

## 下一步 {#whats-next}

您的团队成员必须获得对实例的权限，因为管理Cloud Manager的权限是不够的。 现在，您的云资源已创建完毕，并且可供您的团队访问，系统管理员必须将您的团队成员分配给Adobe Admin Console中的AEMas a Cloud Service产品配置文件。

>[!NOTE]
>
>要授予AEMas a Cloud Service用户的访问权限，必须属于两个产品配置文件之一 `AEM Users` 或 `AEM Administrators`. 请参阅 [在Admin Console中管理产品和用户访问权限](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) 以了解更多。

您应该通过下一步审阅文档来继续入门历程 [将团队成员分配给AEMas a Cloud Service产品配置文件。](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md)


## 其他资源 {#additional-resources}

请查看其他资源以了解：

* [程序类型和添加程序](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [环境类型和添加环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [管理Cloud Manager Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [配置对AEMas a Cloud Service的Admin Console访问](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
