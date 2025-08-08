---
title: 创建环境
description: 了解如何使用 Cloud Manager 创建您的首批环境。
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
feature: Onboarding
source-git-commit: 9c5838a01ceecf094aea19578e6560a5e5ca8c4c
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 62%

---

# 创建环境 {#create-environments}

在[加入历程](overview.md)的这一部分中，您将了解如何使用 Cloud Manager 创建第一个环境。

## 目标 {#objective}

在阅读了本次加入历程的前一篇文档[创建程序](create-program.md)后，您现在拥有了自己的 Cloud Manager 程序。 现在，您可以了解如何使用Cloud Manager为该程序创建首批环境。

阅读本文档后，您将：

* 了解什么是环境。
* 了解不同环境之间的差异。
* 能够创建自己的环境。

## 什么是环境？ {#environments}

环境位于 Cloud Manager 层次结构中程序的下方。 虽然程序允许您组织解决方案并授予特定团队成员访问这些程序的权限，但环境属于特定程序，是这些程序中 Adobe 解决方案的单个实例。环境用于特定目的，如创作内容或测试新开发。 Cloud Manager的CI/CD管道便于将代码从Git存储库部署到这些环境。

如果您回想一下理论上的WKND旅游和冒险企业示例，它们是专注于旅游相关媒体的租户。 他们可能有两个程序。即为WKND Magazine部门创建一个Sites项目，为WKND Media部门创建一个Assets项目。 每个程序可能都有两个环境，例如一个生产环境（为 Site 的实际流量提供服务）和一个开发环境（用于测试新的应用程序代码）。

有五种不同类型的环境：

* **生产和暂存** – 生产和暂存环境成对可用，分别用于生产和测试目的。
* **开发** – 开发环境可以创建用于开发和测试目的，并且只能与非生产管道相关联。
* **快速开发** — 快速开发环境(RDE)允许开发人员快速部署和审查更改。 它最大限度地减少了测试经验证可在本地开发环境中工作的功能所需的时间。
* **专业测试环境** — 提供专用空间，用于在接近生产环境的情况下验证功能，非常适合于压力测试和高级部署前检查。

出于此加入历程的目的，为了从最基础的级别开始，您会创建一个开发环境，用于探索 AEM as a Cloud Service 的功能。

## 创建环境 {#creating-environments}

>[!NOTE]
>
>系统将创建环境的用户记录为其创建者。 由于删除的用户有时可以恢复，因此请仔细选择环境创建者。

**创建环境：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 选择要为其添加环境的程序。

1. 要添加环境，请从&#x200B;**项目概述**&#x200B;页面的&#x200B;**环境**&#x200B;信息卡上，选择&#x200B;**添加环境**&#x200B;选项。

   ![环境信息卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **添加环境**&#x200B;选项也可在&#x200B;**环境**&#x200B;选项卡上使用。

     ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab.png)

   * **添加环境**&#x200B;选项可能由于缺少权限或根据许可的资源而被禁用。

1. 在&#x200B;**添加环境**&#x200B;对话框中，执行以下操作：

   * 选择&#x200B;**环境类型**。
      * 可用/使用的环境数显示在开发环境类型后面的括号中。
   * 提供&#x200B;**环境名称**。
   * 提供&#x200B;**环境描述**。
   * 选择&#x200B;**云区域**。

   ![添加环境对话框](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 单击&#x200B;**保存**&#x200B;来添加指定环境。

环境可用后，分配给&#x200B;**开发人员**&#x200B;产品配置文件的组织成员可以登录Cloud Manager并管理Cloud Manager Git存储库。

## 后续内容 {#whats-next}

既然您已经阅读了加入历程的这一部分，您应该：

* 了解什么是环境。
* 了解不同环境之间的差异。
* 能够创建自己的环境。

您的团队现在可以访问您创建的云资源。 作为系统管理员，您必须首先从 Adobe Admin Console 将团队成员分配到 AEM as a Cloud Service 产品配置文件，以便他们可访问这些资源。

因此，您应该继续您的入门培训历程，接下来查看文档[将团队成员分配给AEM as a Cloud Service产品配置文件](assign-profiles-aem.md)。 在该文档中，您将了解如何授予团队成员对新环境的权限。

## 其他资源 {#additional-resources}

如果您想了解加入历程以外的内容，以下是额外的可选资源。

* [管理环境](/help/implementing/cloud-manager/manage-environments.md) – 了解您可以创建的环境类型以及如何为 Cloud Manager 项目创建环境
* [使用 Adobe Cloud Manager – 环境](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/cloud-manager/environments) – 此视频概述了由 AEM 创作、发布和 Dispatcher 服务组成的 Cloud Manager 环境。了解不同的环境如何支持角色，以及如何使用不同的CI/CD管道与其互动。
* [快速开发环境](/help/implementing/developing/introduction/rapid-development-environments.md) - 请参阅该文档了解有关如何使用 RDE 的详细信息。
<!-- ERROR: Not Found (HTTP error 404) FIND AN ALTERNATE RESOURCE? * [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Watch this video for an overview of Cloud Manager environment types from an AEM champion. -->

