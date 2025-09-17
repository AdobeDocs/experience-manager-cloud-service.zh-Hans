---
title: AEM as a Cloud Service 上线历程简介
description: 您可以在此处了解 AEM as a Cloud Service 上线历程的指导概述。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
recommendations: noDisplay
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 841e30bc279a3859ce9a302b18ddf566d8163100
workflow-type: ht
source-wordcount: '1348'
ht-degree: 100%

---


# 上线历程 {#onboarding-journey}

恭喜您选择 AEM as a Cloud Service！ 本文档是指导您整个上线历程的起点。 无论您是部署新的应用程序还是迁移现有的应用程序，此加入历程都会为您的团队提供帮助。它确保他们可以访问 AEM as a Cloud Service。

## 简介 {#introduction}

Adobe Experience Manager 是一组功能强大的可组合内容服务，它在任何渠道上都快速地投放极具影响力的个性化体验，从而为所有人展示各种内容。**Edge Delivery Services** 是 Adobe Experience Manager 中最新的创新，通过它，可极快地投放内容并打造卓越的体验。通过查阅 [Edge Delivery Services 概述](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/overview)，了解如何开始使用 Edge Delivery Services。要了解如何使用 Edge Delivery Services，请参阅[开发人员教程](https://www.aem.live/developer/tutorial)页面。

入门培训是所指派的系统管理员为您的组织设置 AEM as a Cloud Service 的过程。这个过程包括云资源的初始配置，以及根据用户的工作职责为其分配角色。因此，每个成员都可以登录和访问其 AEM as a Cloud Service 资源。

![加入历程](/help/journey-onboarding/assets/onboarding-journey.png)。

本指南将引导您了解最重要的载入主题，以便在完成后，您将具有：

* 全面了解载入流程中涉及的不同术语、服务和用户。
* 使您的团队能够启动并运行，开始学习如何为 AEM as a Cloud Service 应用程序编写和开发内容。

因此：

* 您的团队经过设置，可以访问云资源。
* AEM 作者将有权访问 AEM as a Cloud Service，并可以开始创建内容。
* AEM 开发人员和部署管理员将有权访问 AEM as a Cloud Service，并可以开始创建和部署自定义应用项目。

## 概念和目标 {#concepts}

<!-- Although there may appear to be a lot to learn when getting started with AEM as a Cloud Service, conceptually there are only a few, logical pieces.-->

AEM as a Cloud Service 的加入历程围绕着以下几个核心要素：

* **合同** - 查看您的 Adobe 合同，了解加入流程的重要详情。
* **Experience Hub** - 使用 [experience.adobe.com](https://experience.adobe.com/) 作为 AEM 功能的中心入口点。Experience Hub 可适应您的角色和权利，使您能高效工作。从这里导航至：
   * **Admin Console** - 管理用户并分配角色。
   * **Cloud Manager** - 设置程序和环境、访问 Git，以及创建管道来管理和部署自定义代码。
   * **Sites** - 创建、管理和传递数字体验。（基于许可证的权利）
   * **Assets** - 组织、存储和分发您的数字资产。（基于许可证的权利）
   * **Forms** - 创建和管理自适应和响应式表单。（基于许可证的权利）

这些概念会在此次加入历程中详细阐述。目标是在历程结束时，您可以做到以下几点：

* 授予必要的用户访问 AEM as a Cloud Service 的权限。
* 为您的项目设置了第一个云资源.
* 知道如何部署第一个代码并创作第一个内容。

基本上，您可以将新 AEM as a Cloud Service 项目投入使用！

## 受众 {#audience}

该加入历程是专门为新加入 AEM as a Cloud Service 和 AEM 的客户的&#x200B;**系统管理员**&#x200B;编写的。系统管理员是在您签署 AEM as a Cloud Service 后 Adobe 最首先联系的个人他们通常是第一个在 AEM as a Cloud Service 上访问和设置您的资源的人。如果您正在阅读本主题，您很可能是系统管理员。

系统管理员管理其组织的 AEMaaCS 用户的各个方面，从访问到权限。 然而，系统管理员必须在此过程中与其他角色进行交互。

| 角色 | 描述 | 历程中的角色 |
| --- | --- | --- |
| 系统管理员 | 此历程的目标是提供云资源的初始配置，并根据用户的工作职责将其分配给适当的角色。 | 角色可以帮助您管理用户的从访问到权限的各个方面。 |
| 内容作者 | 创建并查看 AEM 中的内容。 | 由系统管理员授予权限后，作者就可以开始自己的内容创作之旅。 |
| 开发人员 | 开发使用不同来源内容的 AEM 应用程序。 | 由系统管理员授予权限后，开发人员就可以启动自己的解决方案开发之旅。 |
| 部署管理员 | 添加或更新环境，运行管道，并将代码部署到 AEM 环境或代码质量。 | 由系统管理员授予权限后，部署管理员就可以开始自己管理部署的历程。 |

本载入指南说明了作为系统管理员载入的完整过程。 作为历程的附加可选部分，对 AEM 用户、开发人员和部署管理员的角色进行了简要探讨。

>[!TIP]
>
>如果您是 AEM as a Cloud Service 的新手，并且熟悉 AEM，并且正在从内部部署或 Adobe Managed Services 迁移，请查看 [AEM as a Cloud Service](/help/journey-migration/getting-started.md) 迁移历程。

## 上线历程概述 {#overview}

以下文章详细描述了核心载入概念，并为您提供了 AEM as a Cloud Service 的基本知识。 虽然您可以直接进入历程的特定部分，但许多概念都是基于之前文章中的概念来构建的。因此，如果您是新手，Adobe 建议您从头开始，然后循序渐进。

| | 文章 | 描述 | 受众 |
| --- | --- | --- | --- |
| 0 | 上线历程 | 本文档 | 系统管理员 |
| 1 | [载入准备](preparation.md) | 在载入流程开始之前，系统管理员必须了解一些步骤或准备步骤，然后才能登录系统。 | 系统管理员 |
| 2 | [AEM as a Cloud Service 术语](terminology.md) | 在首次登录 AEMaaCS 之前，了解系统的一些术语及其基本结构会很有帮助。 | 系统管理员 |
| 3 | [Admin Console](admin-console.md) | 了解什么是 Admin Console，如何登录，以及如何以系统管理员身份验证您的配置文件。 | 系统管理员 |
| 4 | [分配 Cloud Manager 产品配置文件](assign-profiles-cloud-manager.md) | 查看 Cloud Manager 产品配置文件，了解如何将团队成员分配给 Cloud Manager 产品配置文件。 | 系统管理员 |
| 5 | [访问 Experience Hub](/help/experience-hub.md) | 使用 Experience Hub 作为 AEM 生态系统的统一的个性化入口点。 | AEM 用户 |
| 6 | [访问 Cloud Manager](cloud-manager.md) | 了解如何访问 Cloud Manager，以便您可以设置项目资源。 | 系统管理员 |
| 7 | [创建项目](create-program.md) | 了解如何使用 Cloud Manager 创建项目。 | 系统管理员 |
| 8 | [创建环境](create-environments.md) | 了解如何使用 Cloud Manager 创建环境。 | 系统管理员 |
| 9 | [分配 AEM 产品配置文件](assign-profiles-aem.md) | 了解系统管理员如何将您的团队成员分配给 AEM as a Cloud Service 中的产品配置文件。 | 系统管理员 |
| 10 | [开发人员和部署管理员任务](developers.md) | 可选 - 作为开发人员，了解如何访问和管理 Cloud Manager Git。作为部署管理员，了解如何在 Cloud manager 中设置管道并部署代码。 | 开发人员和部署管理员 |
| 11 | [AEM 用户任务](aem-users.md) | 可选 – 了解作为 AEM 作者如何访问 AEM as a Cloud Service 实例，并熟悉 AEM as a Cloud Service.的创作内容。 | AEM 用户 |

## 后续内容 {#what-is-next}

您现在已经准备好开始您的 AEM as a Cloud Service 上线历程。 我们鼓励您继续此历程的下一部分，并阅读[入门准备](preparation.md)一文

## AEM 文档历程 {#documentation-journeys}

[文档历程](/help/journey-documentation/documentation-journeys.md)会将许多不同的、复杂的主题和功能联系在一起。其中提供的内容可以帮助新接触 AEM 的读者从头到尾理解和解决业务问题，同时假定读者不了解先前的主题或 AEM 知识。

文档历程是根据最佳实践原则设计的。他们利用 Adobe 的最新研究、Adobe 顾问提供的经过验证的实施经验以及来自客户项目的反馈来获取信息。

如果您想知道 Adobe 建议怎样将您的团队加入到全新的 AEM as a Cloud Service 应用项目，请从这里开始！

## 其他资源 {#additional-resources}

如果您想了解上线历程以外的内容，以下是额外的可选资源。

* [加入 AEM as a Cloud Service 入门培训](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/migration/moving-to-aem-as-a-cloud-service/onboarding) - 这段简短的视频概述 AEM 的云服务入门过程。
