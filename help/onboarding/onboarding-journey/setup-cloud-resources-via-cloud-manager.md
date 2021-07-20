---
title: 通过Cloud Manager设置云资源
description: 请阅读本页内容，了解如何通过Cloud Manager设置云资源
hide: true
hidefromtoc: true
index: false
source-git-commit: 021146e4e1d65c7fe81ed3dba70b32daf34b9704
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# 通过Cloud Manager设置云资源 {#setup-cloud-resources}

分配了“业务所有者”角色的系统管理员应该有权访问并登录Cloud Manager。 之后，分配给“业务所有者”产品配置文件的团队成员必须登录到Cloud Manager并创建您的云计划和环境，以便您的专家团队能够开始工作。

## 目标 {#objective}

本文档可帮助您了解云资源的创建方式以及谁可以执行此操作。

阅读此部分后，您应：

* 了解分配了“业务所有者”角色的系统管理员必须是第一个访问和登录Cloud Manager的管理员
* 了解云程序和环境的创建方式。

## 简介 {#introduction}

由分配给Cloud Manager业务所有者产品配置文件的团队成员通过Cloud Manager来添加云资源。 此人员通常是了解业务需求并完成初始Cloud Manager设置的人员。

请按照以下各节了解如何创建[云服务程序](#create-cloud-service-program)和[环境](#create-cloud-environments)。

### 先决条件 {#prerequisites}

* 分配了“业务所有者”角色的系统管理员应该有权访问并登录到Cloud Manager。

* 了解如何导航和登录Cloud Manager

* 熟悉Cloud Manager产品配置文件

* 了解创建程序时的注意事项。 请观看此视频以了解更多信息。

* 了解Cloud Manager程序和环境的概念

## 导航到Cloud Manager {#navigate-cloud-manager}

1. “业务所有者”用户将收到一封欢迎电子邮件，他们可以从中开始使用，或者如果找不到，则直接转到experience.adobe.com并使用您的Adobe ID登录。

1. 在Experience Cloud主页中，选择Experience Manager:


1. 这会将您转到AEM主页。 从此处，选择Cloud Manager:


1. 这会将您转到Cloud Manager登录页面，如下所示：


1. 现在，验证是否已为您分配了“业务所有者产品配置文件”。 为此，请选择右上角的用户档案，如下所示：


1. 现在，选择用户角色，并确保您已分配给业务所有者。


   干得好！ 您已以业务所有者身份成功登录Cloud Manager!

## 创建Cloud Service程序 {#create-cloud-service-program}


1. 导航到Cloud Manager登录页面，如下所示。

   >[!NOTE]
   >您必须是分配给Cloud Manager业务所有者产品配置文件的团队成员，才能成功完成此步骤。

1. 从此处，选择添加程序以启动添加程序向导。 请观看视频，了解如何创建AEMaCS项目以及在创建项目之前的重要注意事项。

1. 有关如何使用“添加程序”向导的分步说明，请转至此处。

   >[!CAUTION]
   >请记住，程序名称在创建后无法更改。 我们建议您确定您希望给程序提供什么名称。

   如果您必须更改项目名称，则需要通过Adobe支持部门打开一个案例，或者联系您的Adobe代表。 他们将协助有效删除该程序。 您必须重新开始工作，您的团队可能会失去工作。

1. 成功创建云程序后，您可以导航到程序以查看程序的概述页面，如下所示：

1. 如果您尚未执行此操作，现在是将开发人员成员添加到Cloud Manager团队的好时机，请转到将用户添加到开发人员产品配置文件并按照列出的步骤进行操作。

1. 分配给开发人员产品配置文件的成员可以登录到Cloud Manager和管理Cloud Manager Git。


   干得好！ 现在，您的程序已成功创建，您的Cloud Manager Git可供开发人员访问！


## 创建云环境 {#create-cloud-environments}

1. 成功创建云程序后，请通过导航到Cloud Manager概述页面并从环境卡中选择添加来创建云环境。

   >[!NOTE]
   >必须登录具有“业务所有者”或“部署管理器”角色的Cloud Manager用户，才能成功完成此步骤。

   此外，请观看快速视频教程，以了解Cloud Manager环境以及如何将这些环境添加到您的项目中。

1. 这将启动添加环境向导，该向导将指导您添加环境。 首先添加开发环境，以便您熟悉。

1. 如果您尚未执行此操作，则可以立即将开发人员成员添加到您的Cloud Manager团队，转到将用户添加到开发人员产品配置文件，然后按照列出的步骤操作。 这样，开发人员便可以开始导航到Cloud Manager并管理Cloud Manager Git。


   恭喜！ 现在，您的云程序环境已经创建完毕，并且开发人员已添加到团队中！

## 下一步 {#whats-next}

现在，您的团队成员必须获得对实例的权限，因为管理Cloud Manager的权限是不够的。 现在，您的云资源已创建完毕，并可供您的团队访问，系统管理员必须将您的团队成员作为Admin Console中的Cloud Service产品配置文件分配给AEM。

>[!NOTE]
>要获得AEM as a Cloud Service用户的访问权限，用户必须属于两个产品配置文件“AEM用户”或“AEM管理员”中的一个。 了解更多。

## 其他资源 {#additional-resources}

请查看其他资源以了解：

* 程序类型和添加程序
* 环境类型和添加环境
* 管理Cloud Manager Git
* 将对AEM的访问配置为从Admin ConsoleCloud Service
