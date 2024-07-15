---
title: AEM Headless CMS 开发人员历程
description: 了解通过将 Adobe Experience Manager (AEM) 用作 Headless CMS 进行的 Headless 开发。了解如何使用内容模型、内容片段和 GraphQL API 等功能来增强 Headless 内容交付。
landing-page-description: 了解 Headless 内容交付和实施。详细了解如何在您的企业内制定策略。
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 100%

---

# AEM Headless CMS 开发人员历程 {#aem-headless-developer-journey}

欢迎使用面向 Adobe Experience Manager Headless CMS 新手开发人员的文档！

了解强大而灵活的 Headless 特性、它们的功能以及如何在您的第一个 Headless 开发项目中利用它们。此历程为您提供了开发第一个 Headless 应用程序所需的所有信息。

{{headless-trials-promotion}}

>[!CONTEXTUALHELP]
>id="aemcloud_headless_developer_resources"
>title="AEM Headless 开发人员资源和高级文档"
>abstract="了解 AEM Headless CMS 以及构建和交付更好的应用程序和更快的体验所需的一切。"
>additional-url="https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans" text="AEM Headless 开发人员资源"

## 简介 {#introduction}

AEM 的 Headless 实施使用内容片段模型和内容片段来专注于创建结构化的、渠道中性的、可重用的内容片段，以及它们的跨渠道交付。为了实现这一点，它放弃了传统的全栈解决方案中的页面和组件管理。这是一种现代化的动态开发模式，用于实施数字体验。

本指南将引导您了解 AEM 中的 Headless 实施主题，因此当您完成后，您可以：

* 完全了解 Headless 内容交付的含义和好处。
* 了解 AEM 的 Headless 功能以及它们如何协作以提供 Headless 体验。
* 迈出实施您的第一个 AEM Headless 项目的第一步。

>[!TIP]
>
> 如果您更喜欢&#x200B;**通过实践学习**&#x200B;并且已具备 AEM 的现有知识，请访问 AEM Headless 教程，这些教程按 API 和框架进行编排，并包含在本文档末尾的[“其他资源”部分](#additional-resources)中。

## 受众 {#audience}

此历程专为开发人员角色设计，从开发人员的角度阐释了 AEM Headless 项目的要求、步骤和方法。此历程将定义开发人员为成功实施项目而必须与之互动的其他角色，但历程的观点是开发人员的观点。

以下是在此历程中互动的角色。

| 角色 | 描述 | 此历程中的角色 |
|---|---|---|
| 开发人员（目标受众） | 拥有开发使用不同来源内容的 Headless 应用程序的经验 | 此历程的目标受众 |
| 内容作者 | 创建和管理以 Headless 方式交付的内容 | 内容作者创建开发人员以 Headless 方式交付的内容。 |
| 管理员 | 管理 AEM 的基本设置和配置 | 开发人员与管理员合作以进行开发所需的配置更改。 |
| 内容架构师 | 分析必须以 Headless 方式交付的数据的要求并定义此数据的结构 | 开发人员与内容架构师合作，了解数据结构和以 Headless 方式交付数据的要求。 |

## Headless 开发人员历程 {#the-journey}

我们将在此历程中涵盖许多主题，您可从中了解 AEM 中的 Headless 的基础知识。

虽然您可以直接进入历程的特定部分，但许多概念都是基于之前文章中的概念来构建的。Adobe 建议您从头开始，然后循序渐进。

| # | 文章 | 描述 |
|---|---|---|
| 0 | AEM Headless 开发人员历程 | 本文档 |
| 1 | [了解 CMS Headless 开发](learn-about.md) | 了解 Headless 技术以及何时使用它。 |
| 2 | [AEM Headless as a Cloud Service 快速入门](getting-started.md) | 了解 AEM Headless 先决条件 |
| 3 | [首次 AEM Headless 使用体验的路径](path-to-first-experience.md) | 设置您的开发环境并了解如何将简单的应用程序与 AEM Headless 集成 |
| 4 | [如何为您的内容建模](model-your-content.md) | 了解如何为您的内容结构建模。 |
| 5 | [如何通过 AEM 交付 API 访问您的内容](access-your-content.md) | 了解如何使用 GraphQL 查询来访问您的内容片段内容。 |
| 6 | [如何通过 AEM Assets API 更新您的内容](update-your-content.md) | 了解如何使用 REST API 来访问和更新您的内容片段内容。 |
| 7 | [如何汇总您的应用程序和 AEM Headless 中的内容](put-it-all-together.md) | 了解如何获取您的 AEM Project 并准备好使用 AEM Headless SDK 上线。 |
| 8 | [如何使用 Headless 应用程序上线](go-live.md) | 了解如何实时部署应用程序，以及如何在 Git 中获取本地代码并将它移至 CI/CD 管道的 Cloud Manager Git。 |
| 9 | [可选 – 如何使用 AEM 创建单页应用程序 (SPA)](create-spa.md) | 探究如何结合使用 Headful 和 Headless 交付，并了解如何使用 AEM 的 SPA 编辑器框架来创建可编辑的 SPA。 |

{style="table-layout:auto"}

## 后续内容 {#what-is-next}

首先，阅读下一篇文章：[了解 CMS Headless 开发。](learn-about.md)

### 选择您自己的冒险 {#choose-your-path}

您喜欢按照自己的节奏学习吗？查看这些选项：

* 如果您更喜欢继续&#x200B;**了解 Headless 概念和 AEM 的 Headless 技术**，您应按照建议继续您的 AEM Headless 历程，即接下来查看文档[如何将内容建模为 AEM 内容模型](model-your-content.md)，您可从中了解如何在 AEM 中为内容结构建模。
* 如果您更喜欢&#x200B;**通过实践学习**，则可以跳转到 [AEM Headless 快速入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=zh-Hans)，在该教程中，您将实施一个简单项目来公开 AEM Headless 内容，从而直接跳转到 AEM Headless 开发。

## 其他资源 {#additional-resources}

文档历程将提供叙述来指导您完成相关流程和使用相关功能，从而向您说明 AEM 如何解决业务问题。历程说明了多项功能如何协作以满足单一业务需求。

查看这些附加历程，详细了解 AEM 的强大功能如何协作。

* [AEM 开发人员门户](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
* [AEM Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans) – 如果您更喜欢通过实践来学习并具备 AEM 知识基础，请参阅我们的按 API 和框架编排的实践教程，这些教程探究了如何创建和使用基于 AEM Headless 构建的应用程序。
* [AEM Headless 翻译历程](/help/journey-headless/translation/overview.md) – 此文档历程可让您全面了解 Headless 技术、AEM 如何提供 Headless 内容以及如何翻译 Headless 内容。
* [Headless 创作历程](/help/journey-headless/author/overview.md) – 从这里开始，引导您了解 AEM 强大而灵活的 Headless 特性、它们的功能以及如何在您的第一个 Headless 项目中为内容建模。
* [Headless 架构师历程](/help/journey-headless/architect/overview.md) – 从这里开始了解 Adobe Experience Manager as a Cloud Service 强大而灵活的 Headless 功能，以及如何对项目内容进行建模。
* [AEM as a Cloud Service 技术文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) – 如果您已对 AEM 和 Headless 技术有一定的了解，请参阅深入的技术文档。
   * [AEM as a Headless CMS 简介](/help/headless/introduction.md)
