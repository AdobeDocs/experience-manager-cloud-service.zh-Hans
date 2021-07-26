---
title: '将团队成员作为Cloud Service产品配置文件分配给AEM '
description: 可查看本页以了解如何将团队成员分配给AEM作为Cloud Service产品配置文件
hide: true
hidefromtoc: true
index: false
source-git-commit: c2301227eb65bedb77acd9754e2bc4b62527863d
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 1%

---


# 将团队成员作为Cloud Service产品配置文件分配给AEM {#assign-team-members-cloud-service}

## 目标 {#objective}

本文档可帮助您了解系统管理员为将团队成员分配为AEM as a Cloud Service产品配置文件所必须执行的步骤，以及为什么让AEM作者能够开始使用AEM的旅程至关重要。

阅读此部分后，您应该了解：

* 为何以及如何将您的团队成员作为Cloud Service产品配置文件分配给AEM。
* 如何将团队成员添加到AEM用户产品配置文件。
* 如何将团队成员添加到AEM Administrators产品配置文件。


## 简介 {#introduction}

要授予AEM作为Cloud Service用户的访问权限，用户必须属于两个产品配置文件之一，例如`AEM Users`或`AEM Administrators`。 您的团队成员必须获得对AEM实例的权限，因为管理Cloud Manager的权限是不够的。 了解更多。

>[!NOTE]
>系统管理员分配给AEM用户产品配置文件的每个用户都将拥有Cloud Manager的（只读）访问权限。

## 先决条件 {#prerequisites}

在开始阅读本节之前，您应当考虑以下先决条件：

* 了解[AEM as a Cloud Service产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)
* 熟悉[Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)
* 已根据需要将Cloud Manager产品配置文件分配给团队成员，并且已设置云资源
* 有关您的团队成员的详细信息：系统管理员必须具有姓名和电子邮件地址，以及需要作为Cloud Service访问AEM的团队成员的角色和职责。

   >[!NOTE]
   >为了入门，我们建议您最初添加将参与即时任务的用户，例如管理员、开发人员和内容作者。 您无需添加所有用户即可继续载入其余内容。 完成载入后，您可以稍后扩展到更多用户。


1. 登录到[Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)。 有关更多详细信息，请参阅登录Admin Console。

1. 查看[AEM as a Cloud Service产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)。

请按照以下步骤查看Adobe Admin Console中的Cloud Manager配置文件列表：

1. 登录Adobe Admin Console后，从“产品和服务”卡中选择Adobe Experience Manager as a Cloud Service :

1. 导航并选择实例（开发环境的创作实例），如下图所示。

   现在，您将能够看到AEM作为Cloud Service产品配置文件的列表，用户需要根据其角色对其进行分配。 要了解有关这些功能的更多信息，请转至AEM as a Analytics Product Profiles。


## 将团队成员添加到AEM用户或AEM管理员产品配置文件 {#add-team-members}

要授予AEM作为Cloud Service实例的访问权限，用户必须属于两个产品配置文件`AEM Users`或`AEM Administrators`中的一个。

>[!NOTE]
>您必须获得实例的权限，但管理Cloud Manager的权限是不够的。 了解更多。

以下步骤必须由同时具有“业务所有者”角色的系统管理员执行。

1. 在Cloud Manager中，导航到Cloud Manager，然后从感兴趣的环境的上下文中选择管理访问按钮，如下所示：

1. 单击“管理访问”后，新的选项卡会导航您到Admin Console，您可以从中访问环境的创作实例。 根据此人需要授予的权限，选择&#x200B;*AEM Administrators*&#x200B;或&#x200B;*AEM Users*。 了解有关[AEM as a Cloud Service产品配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)的更多信息。

1. 选择如下所示的添加用户并提交必要的详细信息以完成添加团队成员：


1. 如果您拥有需要访问的团队成员信息，则需要对所有环境（包括开发、暂存和生产）重复执行这些步骤。

   现在，您添加的用户将有权访问AEM作为Cloud Service创作服务！


## 下一步 {#whats-next}

现在，您为AEM as a Cloud Service产品配置文件分配的用户已准备好了解如何访问“创作”，并熟悉AEM as a Cloud Service中的页面创作。 您应该遵循该路径，方法是接下来查看文档“AEM用户学习路径”。

## 其他资源 {#additional-resources}

* [配置对AEM的访问权限](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [页面创作快速入门指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)
