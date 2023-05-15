---
title: 创建环境
description: 了解如何使用 Cloud Manager 创建您的首批环境。
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 53%

---

# 创建环境 {#create-environments}

在 [入门历程，](overview.md) 您将了解如何使用Cloud Manager创建您的第一个环境。

## 目标 {#objective}

在阅读了本次入门培训历程的前一篇文档[创建程序](create-program.md)后，您现在拥有了自己的 Cloud Manager 程序。 现在您可以了解如何使用 Cloud Manager 为该程序创建您的首批环境。

阅读本文档后，您将：

* 了解什么是环境。
* 了解不同环境之间的差异。
* 能够创建自己的环境。

## 什么是环境？ {#environments}

环境位于 Cloud Manager 层次结构中程序的下方。 虽然程序允许您组织解决方案并授予特定团队成员访问这些程序的权限，但环境属于特定程序，是这些程序中 Adobe 解决方案的单个实例。环境用于特定目的，如创作内容或测试新开发。 Cloud Manager 的 CI/CD 管道便于将代码从 Git 存储库部署到这些环境。

如果您回顾WKND旅游和冒险企业理论的例子，他们是一家致力于旅游相关媒体的租户，他们可能有两个项目。 即其WKND杂志部的一个站点计划和WKND媒体部的一个资产计划。 每个程序可能都有两个环境，例如一个生产环境（为站点的实际流量提供服务）和一个开发环境（用于测试新的应用程序代码）。

环境有四种类型：

* **生产和暂存** – 生产和暂存环境成对可用，分别用于生产和测试目的。
* **开发**  — 开发环境可用于开发和测试目的，并且只能与非生产管道关联。
* **快速开发**  — 快速开发环境(RDE)允许开发人员快速部署和审查更改，将经过验证可在本地开发环境中工作的功能的测试时间降至最低。

就本入门历程而言，为了以最低的成本入门，您需要创建一个开发环境，以便您能够使用该环境来探索AEM as a Cloud Service的功能。

## 创建环境 {#creating-environments}

1. 登录到Cloud Manager: [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织。

1. 选择要为其添加环境的程序。

1. 要添加环境，请从 **计划概述** 页面，在 **环境** 卡片，选择 **添加环境**.

   ![环境信息卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **添加环境**&#x200B;选项也可在&#x200B;**环境**&#x200B;选项卡上使用。

      ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab.png)

   * **添加环境**&#x200B;选项可能由于缺少权限或根据许可的资源而被禁用。

1. 在出现的&#x200B;**添加环境**&#x200B;对话框中：

   * 选择&#x200B;**环境类型**。
      * 可用/使用的环境数显示在开发环境类型后面的括号中。
   * 提供&#x200B;**环境名称**。
   * 提供&#x200B;**环境描述**。
   * 选择&#x200B;**云区域**。

   ![添加环境对话框](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 单击&#x200B;**保存**&#x200B;来添加指定环境。

环境可用后，分配给&#x200B;**开发人员**&#x200B;的组织成员可以登录 Cloud Manager 并管理 Cloud Manager Git 存储库。

## 后续内容 {#whats-next}

既然您已经阅读了入门培训历程的这一部分，您应该：

* 了解什么是环境。
* 了解不同环境之间的差异。
* 能够创建自己的环境。

您的云资源已创建，可以由您的团队访问。 作为系统管理员，您必须首先将团队成员分配给Adobe Admin Console中的AEMas a Cloud Service产品配置文件，以便他们能够访问这些资源。

因此，您应通过下一步审阅文档来继续入门历程 [将团队成员分配给AEMas a Cloud Service产品配置文件](assign-profiles-aem.md). 在该文档中，您将了解如何授予团队成员访问新环境的权限。

## 其他资源 {#additional-resources}

如果您希望不仅仅访问载入历程的内容，还可以选择使用以下其他资源。

* [管理环境](/help/implementing/cloud-manager/manage-environments.md)  — 了解可以创建的环境类型以及如何为Cloud Manager项目创建环境
* [使用AdobeCloud Manager — 环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) - Cloud Manager环境由AEM创作、发布和调度程序服务组成。 了解不同的环境如何支持角色，以及如何使用不同的 CI/CD 管道互动。
* [快速开发环境](/help/implementing/developing/introduction/rapid-development-environments.md)  — 有关如何使用RDE的详细信息，请参阅此文档

<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Watch this video for an overview of Cloud Manager environment types from an AEM champion. -->

