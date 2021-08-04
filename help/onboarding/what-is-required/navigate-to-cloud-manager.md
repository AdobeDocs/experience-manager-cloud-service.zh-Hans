---
title: 导航到Cloud Manager
description: 可查看本页以了解如何导航到Cloud Manager登录页面
exl-id: 9cf25d1d-a351-4ea0-b2e9-1df6ca4915b7
source-git-commit: 149776bdd7acce3e00710e50600d9bd1d7cc6b9b
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 6%

---

# 导航到Cloud Manager {#cloud-manager}

Cloud Manager是AEM as a Cloud的重要部分。 它允许组织在云中自行管理Experience Manager。 它包含一个持续集成和持续交付 (CI/CD) 框架，使 IT 团队和实施合作伙伴能够在不影响性能或安全性的情况下快速交付自定义或更新。使用用户界面，您可以配置并启动CI/CD管线。

在系统管理员授予您访问Cloud Manager的权限后，您将收到一封电子邮件，将带您转到[Adobe Experience Cloud](https://experience.adobe.com)主页。

>[!NOTE]
>您必须作为用户添加，并且系统管理员必须至少将您分配给一个Cloud Manager角色(Admin Console中的产品配置文件)。

1. 在欢迎电子邮件中，单击&#x200B;**开始**，如下图所示。
   ![](/help/onboarding/what-is-required/assets/get-started-email.png)


   >[!IMPORTANT]
   >或者，您也可以从[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)直接导航到Cloud Manager的登录页面。 请为此页面添加书签以供将来使用，以帮助您直接导航到Cloud Manager的登陆页面。

此外，您还可以从Adobe Experience Cloud主页导航到Cloud Manager的&#x200B;**程序和产品**&#x200B;页面。 应遵循以下步骤：

1. 直接导航到[Adobe Experience Cloud](https://experience.adobe.com)，然后使用Adobe ID登录。

1. 选择&#x200B;**Experience Manager**。
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page1.png)

1. 从Cloud Manager卡片中单击&#x200B;**Launch**。 成功登录到[!UICONTROL Cloud Manager]后，即可使用用户界面(UI)。
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page2.png)

1. 成功登录后，系统会将您定向到Cloud Manager的登陆页面。


## Cloud Manager登录页面 {#cloud-manager-landing}

成功登录后，系统会将您定向到Cloud Manager的登陆页面。

>[!NOTE]
>根据在[!UICONTROL Cloud Manager]中分配的角色和应用程序的状态，在使用[!UICONTROL Cloud Manager] UI时，您将看到不同的屏幕。

您将看到以下三个选项之一：

* **Cloud Manager中不存在程序时**

   如果您的组织中不存在项目，则登陆页面会引导您创建第一个项目，如下图所示。
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

* **当Cloud Manager中已存在程序时**

   如果组织中已存在项目，则登录页面会指示您添加其他项目，并显示所有现有项目，如下图所示。

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

* **当程序存在且用户是系统管理员时**

   如果组织中已存在项目，并且您是系统管理员，则登录页面会显示&#x200B;**管理访问**&#x200B;按钮以及&#x200B;**添加项目**&#x200B;选项，如下图所示。

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

在此处，具有权限的用户（如Cloud Manager中的业务所有者角色）能够选择&#x200B;**添加程序**&#x200B;以启动[添加程序向导](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en#getting-access)。

要了解如何在Cloud Manager中添加程序，请参阅创建：

* [生产计划](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/creating-production-program.html?lang=en)
* [沙盒项目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/creating-sandbox-program.html?lang=en)