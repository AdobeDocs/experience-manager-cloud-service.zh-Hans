---
title: AEMas a Cloud Service术语
description: 在登录AEMaCS之前，了解系统的一些术语及其基本结构会有所帮助。
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 18%

---


# AEMas a Cloud Service术语 {#terminology}

在 [入门历程，](overview.md) 您将学习AEM as a Cloud Service的一些术语及其基本结构。

## 目标 {#objective}

现在，您已通过阅读文档了解导致载入流程的原因 [入门准备、](preparation.md) 登录前，了解系统的一些术语及其基本结构将会有所帮助。

AEMas a Cloud Service是一款功能强大且灵活的工具，可用于使用您应该熟悉其组织以及用于描述该工具的术语和语言的任何工具。 本文档概述了在开始使用系统之前您需要了解的一些关键术语。

阅读本文档后，您将了解：

* AEMaCS的不同层。
* 每个层所做工作的基础知识。

## AEMaCS结构 {#structure}

在此入门历程中，无需完全了解AEM as a Cloud Service的结构。 但是，熟悉以下概念将更便于在历程的后续过程中遵循。

![Cloud Manager 结构](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **租户** – 每个客户均配有一个租户。租户也称为IMS组织（在此历程的后面部分有关IMS的更多信息）
* **项目** – 每个租户都有一个或多个项目，这些项目通常反映了客户的许可解决方案。
* **环境** – 每个项目都有多个环境，例如用于实时内容的生产环境、一个用于暂存的环境，一个用于开发的环境。
* **存储库**  — 环境具有一个或多个维护应用程序和前端代码的git存储库。
* **工具和工作流** – 管道管理从存储库到环境的代码部署。

示例通常有助于将此层级置于上下文中。

* WKND 旅游和冒险企业可能是专注于旅游相关媒体的&#x200B;**租户**。
* WKND Travel and Adventure Enterprises租户可能有两个 **项目**:
   * 其WKND杂志部的一个站点计划
   * WKND媒体部的一个资产计划
* WKND杂志和WKND媒体程序都将具有开发、暂存和制作功能 **环境**.
* **存储库** 用于维护WKND Magazine和WKND Media的自定义代码和应用程序。
* 各种 **工具和工作流** 跨repo工作以使用CI/CD管道部署代码、访问日志、访问AEM等。

## 下一步 {#what-is-next}

现在，您已完成AEM入门历程的这一部分，您应该了解：

* AEMaCS的不同层。
* 每个层所做工作的基础知识。

在此知识的基础上，通过下一次阅读文档，继续您的AEM入门历程 [访问Admin Console](admin-console.md)，您将在此处了解如何访问控制台并以系统管理员身份验证您的状态。
