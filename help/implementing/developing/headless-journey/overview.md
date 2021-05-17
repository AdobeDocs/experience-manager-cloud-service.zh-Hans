---
title: AEM无外设开发人员历程
description: 开始此处，引导您了解AEM强大而灵活的无外设功能、其功能以及如何将它们用于您的首个开发项目。
hide: true
hidefromtoc: true
index: false
exl-id: 4524c92a-8f19-497a-b4f2-c3e23f555d37
source-git-commit: 3554c4a4ea1858ea5b4ffbe0fd223a540261cb5c
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 2%

---

# AEM无外设开发者历程{#aem-headless-developer-journey}

>[!CAUTION]
>
>正在进行中的工作 — 此文档的创建正在进行中，不应理解为完整或明确，也不应将其用于生产目的。

开始此处，引导您了解AEM强大而灵活的无头功能、其功能以及如何将它们用于您的首个无头开发项目。

## 简介 {#introduction}

无外设实施对于向您的受众提供体验变得越来越重要，无论体验在何处，也不管渠道。

无外设实施可实现页面和组件管理，就像在完整堆栈解决方案中一样，侧重于创建渠道中立、可重用的内容片段及其跨渠道投放。 它是用于实施Web体验的现代、动态的开发模式。

本指南将引导您完成最重要的主题，以便您在完成后：

* 充分了解什么是无头内容投放及其优势。
* 了解AEM无外设功能以及它们如何协同工作以提供无外设体验。
* 能够采取实施您的第一个AEM无头项目的第一步。

## 无头历程{#the-journey}

您将在此旅程中探索许多主题。 以下文章为您提供了AEM中无外设的基本知识，并链接到详细的技术文档。

虽然您可以直接访问旅程中的特定部分，但许多概念都基于之前文章中的概念。 因此，如果您不熟悉AEM中的无头功能，我们建议您从头开始开始，然后按顺序进行。

| # | 文章 | 描述 |
|---|---|---|
| 0 | AEM无外设开发人员历程 | 此文档 |
| 1 | [了解CMS无外设开发](learn-about.md) | 了解无外设技术及其使用时间。 |
| 2 | [AEM Headless入门Cloud Service](getting-started.md) | 了解AEM Headless的先决条件 |
| 3 | [使用AEM Headless获得第一次体验](path-to-first-experience.md) | 设置开发环境并了解如何将简单应用程序与AEM无头集成 |
| 4 | [如何对内容进行建模](model-your-content.md) | 了解如何对内容结构建模。 然后，使用内容片段模型和内容片段实现Adobe Experience Manager(AEM)的结构，以便在渠道间重复使用。 |
| 5 | [如何通过AEM 投放 API访问您的内容](access-your-content.md) | 了解如何使用GraphQL查询访问内容片段内容。 |
| 6 | [如何通过AEM资产API更新您的内容](update-your-content.md) | 了解如何使用REST API访问和更新内容片段内容。 |
| 7 | [如何将所有内容整合在一起 — 您的应用程序和您的内容放在AEM Headless中](put-it-all-together.md) | 了解如何利用您的AEM项目（包括内容片段、GraphQL调用、您的REST API调用和您的应用程序），并为其上线做准备。 |
| 8 | [如何与无外设应用程序一起使用](go-live.md) | 了解如何实时部署应用程序并在Git中保存您的本地代码，然后将其移至Cloud Manager Git for CI/CD渠道。 |
| 9 | [启动后](post-launch.md) | 了解如何保持无外设体验。 |
| 10 | [可选 — 如何使用AEM创建单页应用程序(SPA)](create-spa.md) | 了解AEM无头功能后，了解如何结合使用无头和无头投放，并了解如何使用AEM SPA Editor框架创建可编辑的SPA。 |

## 下一步是什么{#what-is-next}

您现在已准备好开始Adobe无头之旅。 我们建议您继续下一步，阅读文章[了解CMS无外设开发。](learn-about.md)

### 选择您自己的冒险{#choose-your-path}

但是，Adobe希望您在开始使用AEM无头项目时取得成功，无论您的学习风格如何。 所以请考虑这两个选项。

* 如果您希望继续&#x200B;**了解无头概念和AEM无头技术**，则应继续按照建议的AEM无头旅程，方法是查看文档[如何将您的内容建模为AEM内容模型](model-your-content.md)，从中可了解如何在AEM中建模您的内容结构。
* 如果您希望&#x200B;**通过执行**&#x200B;来学习，您可以跳到[AEM无头动手教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)入门，在该教程中，您将通过实施一个简单项目来公开AEM无头内容，直接进入AEM无头开发。
