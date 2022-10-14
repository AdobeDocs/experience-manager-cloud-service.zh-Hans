---
title: AEM as a Cloud Service 术语
description: 在登录 AEMaaCS 之前，了解系统的一些术语及其基本结构会很有帮助。
exl-id: d02776a7-836a-4894-a5d5-ae88cc7e4e76
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 100%

---

# AEM as a Cloud Service 术语 {#terminology}

在[入门培训历程](overview.md)这一部分，您将了解 AEM as a Cloud Service 的一些术语及其基本结构。

## 目标 {#objective}

现在，通过阅读文档[入门准备](preparation.md)，您已经了解载入的原因，在登录之前，了解一些系统术语及其基本结构是很有帮助的。

AEM as a Cloud Service 是一种强大而灵活的工具，要使用任何工具，您都应该熟悉其组织结构以及用于描述它的术语和语言。本文档总结了开始使用系统之前需要理解的一些关键术语。

阅读本文档后，您将了解：

* 构成 AEMaaCS 的不同层。
* 每个层的基本功能。

## AEMaaCS 结构 {#structure}

就此次入门培训历程而言，不需要完全了解 AEM as a Cloud Service 的结构。 但是，熟悉以下概念将使以后的历程更容易理解。

![Cloud Manager 结构](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **租户** – 每个客户均配有一个租户。租户也称为 IMS 组织（稍后将介绍 IMS）
* **项目** – 每个租户都有一个或多个项目，这些项目通常反映了客户的许可解决方案。
* **环境** – 每个项目都有多个环境，例如用于实时内容的生产环境、一个用于暂存的环境，一个用于开发的环境。
* **存储库** – 这些环境具有一个或多个 Git 存储库，可在其中维护应用程序和前端代码。
* **工具和工作流** – 管道管理从存储库到环境的代码部署。

示例通常有助于将此层级置于上下文中。

* WKND 旅游和冒险企业可能是专注于旅游相关媒体的&#x200B;**租户**。
* “WKND 旅游和冒险企业”租户可能有两个&#x200B;**程序**：
   * WKND 杂志部门的 Sites 程序
   * WKND 媒体部门的 Assets 程序
* WKND 杂志和 WKND 媒体项目都具有开发、暂存和生产&#x200B;**环境**。
* **存储库**&#x200B;用于维护 WKND 杂志和 WKND 媒体的自定义代码和应用程序。
* 各种&#x200B;**工具和工作流**&#x200B;在整个存储库中使用 CI/CD 管道、访问日志、访问 AEM 等部署代码。

## 后续内容 {#what-is-next}

现在您已完成 AEM 入门培训历程的这一部分，您应该了解：

* 构成 AEMaaCS 的不同层。
* 每个层的基本功能。

在这些知识的基础上，继续您的 AEM 入门培训历程，接下来阅读文档[访问 Admin Console](admin-console.md)，您将了解如何访问控制台并验证您作为系统管理员的状态。
