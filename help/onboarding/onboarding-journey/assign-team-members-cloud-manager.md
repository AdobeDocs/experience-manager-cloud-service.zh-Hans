---
title: '将团队成员分配给Cloud Manager产品配置文件 '
description: 可查看本页以了解如何将团队成员分配给Cloud Manager产品配置文件
hide: true
hidefromtoc: true
index: false
source-git-commit: 9caf3447fedf13fa81bb616cc54b7cb6a08ff159
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 0%

---


# 将团队成员分配给Cloud Manager产品配置文件 {#assign-team-members}

了解如何登录[Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)并以[系统管理员](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en)的身份查看您的权限后，即可将团队成员分配给Cloud Manager产品配置文件。

## 目标 {#objective}

本文档概述了如何从Admin Console将团队成员分配给Cloud Manager产品配置文件。

阅读此部分后，您应该能够：

* 了解添加团队成员的原因和方式。
* 了解三个不同的Cloud Manager产品配置文件，如业务所有者、部署管理员和开发人员。
* 将团队成员分配给Cloud Manager产品配置文件，如“业务所有者”、“部署管理器”和“开发人员”。

## 前提条件 {#prerequisites}

在开始此部分之前，应考虑以下先决条件。 您必须：

* 成为系统管理员并了解[Cloud Manager产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)。
* 了解[Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)基础知识。
* 详细了解您的团队成员。 系统管理员必须具有姓名和电子邮件地址，以及需要作为Cloud Service访问AEM的团队成员的角色和职责。

   >[!NOTE]
   >为了入门，我们建议您最初添加将参与即时任务的用户，例如管理员、开发人员和内容作者。 您无需添加所有用户即可继续载入其余内容。 完成载入后，您可以稍后扩展到更多用户。

## 查看Cloud Manager产品配置文件 {#review-product-profiles}

从Admin Console中，您可以看到Cloud Manager配置文件列表。

>[!NOTE]
>在从Admin Console查看Cloud Manager产品配置文件之前，建议先查看可用的[Cloud Manager产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)。

请按照以下步骤查看Cloud Manager配置文件列表：

1. 登录到[Adobe Admin Console](https://adminconsole.adobe.com/)。 从&#x200B;**概述**&#x200B;页面中，从&#x200B;**产品和服务**&#x200B;卡中选择&#x200B;**Adobe Experience Manager作为Cloud Service**。

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

   >[!NOTE]
   >请参阅登录到Admin Console，了解如何使用Admin Console。


1. 从包含所有实例列表的表中导航到&#x200B;**Cloud Manager**&#x200B;实例。

   ![](/help/onboarding/onboarding-journey/assets/assign-team2.png)

1. 您将看到预配置的[Cloud Manager产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)的列表。

   ![](/help/onboarding/onboarding-journey/assets/assign-team3.png)


## 将用户分配给业务所有者产品配置文件 {#assign-users-business-owner}

现在，您可以添加用户并将其分配给Cloud Manager业务所有者产品配置文件。

>[!NOTE]
>要成功执行此操作，您必须从Adobe管理控制台将用户添加到产品(在本例中为AEM)和[Cloud Manager业务所有者产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)。

以下步骤将指导您完成此步骤：

1. 确定将管理Cloud Manager程序的用户，并将其添加到业务所有者产品配置文件。 系统管理员必须是第一个访问和登录Cloud Manager的人员。 您必须先将自己（系统管理员）添加到业务所有者产品配置文件中。

1. 在[Admin Console](https://adminconsole.adobe.com/enterprise/overview) **概述**&#x200B;页面中，选择&#x200B;**Adobe Experience Manager作为**&#x200B;产品和服务&#x200B;**卡中的Cloud Service**&#x200B;产品，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. 从顶部导航中选择&#x200B;**Users**&#x200B;选项卡，然后选择&#x200B;**Add User**。

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. 在&#x200B;**将用户添加到团队**&#x200B;对话框中，键入要添加的用户的电子邮件ID。 对于ID类型，如果尚未设置团队成员的Federated ID，请选择Adobe ID。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. 在“产品”选项中，选择&#x200B;**Adobe Experience Manager作为Cloud Service**，并将&#x200B;**业务所有者**&#x200B;产品配置文件分配给用户，如下所示。

   >[!NOTE]
   >请参阅[Cloud Manager产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)，以确保在Admin Console中为正确的用户分配正确的角色，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team6.png)

   >[!NOTE]
   >将用户至少分配一个产品配置文件，以便用户可以访问Cloud Manager。 请记住将您自己（系统管理员）分配给业务所有者。

1. 单击&#x200B;**保存**。系统会向您添加的用户发送一封欢迎电子邮件。 受邀用户可以通过单击欢迎电子邮件中的链接，然后使用其Adobe ID登录来访问Cloud Manager。

恭喜！ 现在，您新组建的Cloud Manager团队（包括您自己分配给“业务所有者”角色的团队）已经设置完成。 会员将收到一封欢迎电子邮件，邀请他们登录并访问Cloud Manager。 在“业务所有者”角色中，您现在只需一步即可登录到Cloud Manager并启用云资源的创建。

## 将用户分配给Deployment Manager产品配置文件 {#assign-users-deployment-manager}

1. 确定将管理Cloud Manager程序的用户，并将其添加到Deployment Manager产品配置文件中。 系统管理员必须是第一个访问和登录Cloud Manager的人员。 您必须先将自己（系统管理员）添加到业务所有者产品配置文件中。

1. 在[Admin Console](https://adminconsole.adobe.com/enterprise/overview) **概述**&#x200B;页面中，选择&#x200B;**Adobe Experience Manager作为**&#x200B;产品和服务&#x200B;**卡中的Cloud Service**&#x200B;产品，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. 从顶部导航中选择&#x200B;**Users**&#x200B;选项卡，然后选择&#x200B;**Add User**。

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. 在&#x200B;**将用户添加到团队**&#x200B;对话框中，键入要添加的用户的电子邮件ID。 对于ID类型，如果尚未设置团队成员的Federated ID，请选择Adobe ID。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. 在“产品”选项中，选择&#x200B;**Adobe Experience Manager作为Cloud Service**，并将&#x200B;**Deployment Manager**&#x200B;产品配置文件分配给用户，如下所示。

   >[!NOTE]
   >请参阅[Cloud Manager产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)，以确保在Admin Console中为正确的用户分配正确的角色，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team6.png)。

   >[!IMPORTANT]
   >在创建Cloud Manager资源后，可以将用户添加到部署管理器产品配置文件。

## 将用户分配给开发人员产品配置文件 {#assign-users-developer}

1. 识别将管理Cloud Manager项目的用户，并将其添加到开发人员产品配置文件。 系统管理员必须是第一个访问和登录Cloud Manager的人员。 您必须先将自己（系统管理员）添加到业务所有者产品配置文件中。

1. 在[Admin Console](https://adminconsole.adobe.com/enterprise/overview) **概述**&#x200B;页面中，选择&#x200B;**Adobe Experience Manager作为**&#x200B;产品和服务&#x200B;**卡中的Cloud Service**&#x200B;产品，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. 从顶部导航中选择&#x200B;**Users**&#x200B;选项卡，然后选择&#x200B;**Add User**。

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. 在&#x200B;**将用户添加到团队**&#x200B;对话框中，键入要添加的用户的电子邮件ID。 对于ID类型，如果尚未设置团队成员的Federated ID，请选择Adobe ID。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. 在“产品”选项中，选择&#x200B;**Adobe Experience Manager作为Cloud Service**，并将&#x200B;**Developer**&#x200B;产品配置文件分配给用户，如下所示。

   >[!NOTE]
   >请参阅[Cloud Manager产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)，以确保在Admin Console中为正确的用户分配正确的角色，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team6.png)。


   >[!IMPORTANT]
   >在创建Cloud Manager资源后，可以将用户添加到开发人员产品配置文件。

## 下一步 {#whats-next}

现在，您已了解了三个不同的Cloud Manager产品配置文件（如业务所有者、部署管理器和开发人员），并将团队成员分配给Cloud Manager产品配置文件（如业务所有者、部署管理器和开发人员），接下来，您应该通过Cloud Manager查看文档设置资源，以便了解：

1. 作为分配给&#x200B;*业务所有者*&#x200B;角色的系统管理员，您必须访问并登录Cloud Manager。

1. 接下来，具有&#x200B;*业务所有者*&#x200B;角色的Cloud Manager用户可以登录并设置您的云资源，包括您的云计划和环境。 这将确保您的专家团队能够尽快开始访问AEMCloud Service。

1. 在&#x200B;*业务所有者*&#x200B;设置您的云资源后，已成功添加到Cloud Manager产品配置文件的&#x200B;*开发人员*&#x200B;和&#x200B;*部署管理器*&#x200B;可以访问Cloud Manager并熟悉如何继续其学习路径。

## 其他资源 {#additional-resources}

请查看其他资源以了解：

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Cloud Manager产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Admin Console身份概述](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
