---
title: AEMas a Cloud Service载入历程简介
description: 您可以在此处了解 AEM as a Cloud Service 入门过程的指导概览。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 75c0e8cbaa409fa48750e794c27ace98eda107d0
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 入门培训历程 {#onboarding-journey}

恭喜您选择AEMas a Cloud Service! 本文档是引导式历程的入门指南。 无论您是要部署新应用程序还是迁移现有应用程序，此入门历程都可确保您的团队已设置并有权访问AEMas a Cloud Service。

## 简介 {#introduction}

载入是指指定系统管理员为您的组织设置AEMas a Cloud Service的过程。 这包括初始配置云资源，并根据用户的工作职责为用户分配角色。 因此，每个成员都能够登录并访问其AEMas a Cloud Service资源。

![入门历程](/help/journey-onboarding/assets/onboarding-journey.png)

本指南将引导您完成最重要的入门主题，以便您在完成后能够：

* 充分了解载入过程中涉及的不同术语、服务和用户。
* 使您的团队能够启动并运行，并采取首要步骤了解如何为您的AEMas a Cloud Service应用程序创作和开发内容。

因此：

* 您的团队将会进行设置，并有权访问云资源。
* AEM作者将有权访问AEMas a Cloud Service，并可以开始创建内容。
* AEM开发人员和部署经理将有权访问AEMas a Cloud Service，并可以开始创建和部署自定义应用程序。

## 概念和目标 {#concepts}

虽然在开始使用AEM时似乎有很多要学的东西，但从概念上讲，只有少数逻辑部分。

* **合同**  — 您需要熟悉您的Adobe合同，因为它定义了载入过程的各个方面。
* **Admin Console**  — 这是管理用户和分配角色的位置。
* **Cloud Manager**  — 这是设置资源（如方案和环境）的工具。 您还可以在该位置访问git并创建管道以管理和部署自定义代码。

这些概念将在此入门历程中详细阐述。 目标是在历程结束时，您：

* 已授予必要用户访问AEMaaCS的权限
* 为您的项目设置了第一个云资源
* 了解如何部署第一个代码并创作第一个内容。

基本上，您会使用新的AEMas a Cloud Service项目开始运行！

## 受众 {#audience}

入门历程专门为 **系统管理员** 客户对AEM as a Cloud Service和AEM的新增功能。 系统管理员是在您签署AEMas a Cloud Service合同后，Adobe首次联系到的个人，通常是访问和设置AEMas a Cloud Service资源的第一人。 如果您正在阅读此内容，则可能是系统管理员。

系统管理员可管理其组织内AEMaaCS用户（从权限到权限）的各个方面。 但是，系统管理员在过程中必须与其他角色进行交互。

| 角色 | 描述 | 历程中的角色 |
|---|---|---|
| 系统管理员 | 此历程的目标，提供云资源的初始配置以及根据用户的工作职责将用户分配给适当的角色 | 管理用户从访问权限到访问权限的所有方面 |
| 内容作者 | 在AEM中创建并审阅内容 | 系统管理员授予权限后，作者可以开始自己的历程创建内容 |
| 开发人员 | 开发使用来自不同来源的内容的AEM应用程序 | 一旦系统管理员授予了权限，开发人员便可以开始自己的历程来开发解决方案 |
| 部署管理器 | 添加或更新环境、运行管道以及将代码部署到AEM环境或代码质量。 | 在系统管理员授予权限后，部署经理便可以开始他们自己的历程管理部署 |

本入门指南说明了以系统管理员身份入门的完整过程。 简要地介绍了AEM用户、开发人员和部署经理的角色，作为历程中的其他可选部分。

>[!TIP]
>
>如果您是初次使用AEMas a Cloud Service，但已经熟悉AEM，并且是从内部部署或Adobe Managed Services迁移，请务必查看 [AEMas a Cloud Service迁移历程。](/help/journey-migration/getting-started.md)

## 入门历程概述 {#overview}

以下文章详细描述了核心入门概念，并为您提供了AEMas a Cloud Service的基础知识。 虽然您可以直接进入历程的特定部分，但许多概念都是基于之前文章中的概念来构建的。因此，如果您是初次入门，我们建议您从头开始，然后按顺序进行。

| # | 文章 | 描述 | 受众 |
|---|---|---|---|
| 0 | 入门培训历程 | 本文档 | 系统管理员 |
| 1 | [入门准备](preparation.md) | 在载入过程开始之前，系统管理员在登录系统之前必须了解一些数字或准备步骤。 | 系统管理员 |
| 2 | [AEMas a Cloud Service术语](terminology.md) | 在您首次登录AEMaCS之前，了解系统的一些术语及其基本结构会有所帮助。 | 系统管理员 |
| 3 | [Admin Console](admin-console.md) | 了解Admin Console是什么、如何登录以及如何以系统管理员身份验证您的用户档案。 | 系统管理员 |
| 4 | [分配Cloud Manager产品配置文件](assign-profiles-cloud-manager.md) | 查看Cloud Manager产品配置文件，并了解如何将团队成员分配给Cloud Manager产品配置文件。 | 系统管理员 |
| 5 | [访问 Cloud Manager](cloud-manager.md) | 了解如何访问Cloud Manager，以便设置项目资源。 | 系统管理员 |
| 6 | [创建项目](create-program.md) | 了解如何使用Cloud Manager创建程序。 | 系统管理员 |
| 7 | [创建环境](create-environments.md) | 了解如何使用Cloud Manager创建环境。 | 系统管理员 |
| 8 | [分配AEM产品配置文件](assign-profiles-aem.md) | 了解系统管理员如何将您的团队成员分配给AEMas a Cloud Service的产品配置文件。 | 系统管理员 |
| 9 | [开发人员和部署管理器任务](developers.md) | 可选 — 了解作为开发人员，您如何可以访问和管理Cloud Manager Git，以及作为部署管理器，您如何在Cloud Manager中设置管道和部署代码。 | 开发人员和部署管理器 |
| 10 | [AEM用户任务](aem-users.md) | 可选 — 了解作为AEM作者，您如何访问AEMas a Cloud Service实例并熟悉AEMas a Cloud Service的创作内容。 | AEM用户 |

## 下一步 {#what-is-next}

您现在可以开始AEMas a Cloud Service入门历程。 我们建议您继续进入历程的下一部分并阅读文章 [入门准备](preparation.md)

## AEM 文档历程 {#documentation-journeys}

[文档历程](/help/journey-documentation/documentation-journeys.md)通过提供叙述来帮助可能是 AEM 新手的读者彻底理解和解决业务问题，同时假定读者拥有最少的主题或 AEM 知识，从而将许多不同且可能复杂的主题和功能联系起来。

文档历程是围绕最佳实践准则而设计的，其中包含了 Adobe 的最新研究、Adobe 顾问提供的成熟实施经验以及来自客户项目的反馈。

如果您想了解Adobe如何建议如何将团队载入新的AEMas a Cloud Service应用程序，请从此处开始！
