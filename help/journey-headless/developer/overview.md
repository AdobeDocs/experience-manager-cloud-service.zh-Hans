---
title: AEM Headless开发人员历程
description: 从此处开始，您可以逐步了解AEM强大而灵活的无外设功能、其功能，以及如何在您的第一个开发项目中利用这些功能。
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
source-git-commit: bc56a739d8aa59d8474f47c9882662baacfdda84
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 1%

---

# AEM Headless开发人员历程 {#aem-headless-developer-journey}

从此处开始，您可以体验AEM强大而灵活的无头功能、其功能，以及如何在您的第一个无头开发项目中利用这些功能。

## 简介 {#introduction}

无头实施对于向受众提供体验（无论这些体验位于何处，也不论渠道如何）越来越重要。

与全栈解决方案中的传统方式一样，无头实施可用于页面和组件管理，并且重点关注创建不依赖于渠道、可重复使用的内容片段及其跨渠道交付。 它是一种实现数字体验的现代化、动态的开发模式。

本指南将引导您完成最重要的主题，以便您在完成该工作后：

* 充分了解无头内容交付的含义及其好处。
* 了解AEM无头功能以及它们如何协同工作来提供无头体验。
* 能够采取实施首个AEM无头项目的首要步骤。

## AEM文档历程 {#documentation-journeys}

[文档历程](/help/journey-documentation/home.md) 将许多不同且可能复杂的主题和功能结合在一起，提供了一种说明，帮助对AEM不熟悉、从头到尾理解和解决业务问题的读者，同时尽可能少地了解以前的主题或AEM知识。

文档历程围绕最佳实践原则进行设计，根据Adobe的最新研究、Adobe顾问的成熟实施经验以及客户项目的反馈提供信息。

如果您想了解Adobe如何建议如何使用AEM解决无头业务案例，可从AEM无头历程开始。

## 受众 {#audience}

此历程专为开发人员角色设计，从开发人员的角度阐述AEM Headless项目的要求、步骤和方法。 历程定义了其他角色，开发人员必须与这些角色进行交互才能使项目取得成功，但历程的视角是开发人员的视角。

以下是此历程中交互的角色。

| 角色 | 描述 | 角色在历程 |
|---|---|---|
| 开发人员 | 具有开发无头应用程序的经验，这些应用程序使用来自不同来源的内容 | 此历程的目标受众 |
| 内容作者 | 创建并管理无头投放的内容 | 内容作者创建开发人员随意交付的内容。 |
| 管理员 | 管理AEM的基本设置和配置 | 开发人员与管理员合作，进行开发所需的配置更改。 |
| 内容架构师 | 对必须无头传送的数据要求进行分析，并定义此数据的结构 | 开发人员与内容架构师合作，以了解数据的结构和无头提供数据的要求。 |
| 翻译专家 | 定义应翻译的内容并管理这些工作流 | 翻译专家会与内容架构师合作来定义内容的初始组织，并且可能需要与开发人员合作，以满足任何特定于翻译的要求。 |

此历程中的信息当然对所有角色都有用，但某些信息对某些角色可能是多余的。 请继续关注即将发布的涉及其他角色的历程。](/help/journey-documentation/home.md#journeys)[

## 无头开发人员历程 {#the-journey}

您将在此历程中探索许多主题。 以下文章为您提供了有关AEM中无头的基础知识，并链接到详细的技术文档。

尽管您可以直接转到历程的特定部分，但许多概念都基于之前文章中的概念进行构建。 因此，如果您是初次接触AEM中的无头用户，我们建议您从头开始，然后按顺序前进。

| # | 文章 | 描述 |
|---|---|---|
| 0 | AEM Headless开发人员历程 | 本文档 |
| 1 | [了解CMS无头开发](learn-about.md) | 了解无头技术以及何时使用它。 |
| 2 | [AEM Headless as aCloud Service入门](getting-started.md) | 了解AEM Headless先决条件 |
| 3 | [使用AEM Headless获得首个体验的路径](path-to-first-experience.md) | 设置开发环境，并了解如何将简单的应用程序与AEM Headless集成 |
| 4 | [如何对内容进行建模](model-your-content.md) | 了解如何对内容结构进行建模。 然后，使用内容片段模型和内容片段实现Adobe Experience Manager(AEM)的结构，以便跨渠道重复使用。 |
| 5 | [如何通过AEM交付API访问您的内容](access-your-content.md) | 了解如何使用GraphQL查询访问内容片段内容。 |
| 6 | [如何通过AEM Assets API更新内容](update-your-content.md) | 了解如何使用REST API访问和更新内容片段内容。 |
| 7 | [如何将所有内容整合在一起 — 在AEM Headless中查看您的应用程序和内容](put-it-all-together.md) | 了解如何获取您的AEM项目并为使用AEM Headless SDK进行上线做准备。 |
| 8 | [如何使用无头应用程序](go-live.md) | 了解如何在Git中实时部署应用程序并获取本地代码，然后将其移至Cloud Manager Git for CI/CD管道。 |
| 9 | [可选 — 如何使用AEM创建单页应用程序(SPA)](create-spa.md) | 了解AEM无头功能后，请了解如何结合使用无头和无头交付，并了解如何使用AEM SPA编辑器框架创建可编辑的SPA。 |

## 下一步 {#what-is-next}

现在，您已准备好开始AdobeHeadless历程。 我们建议您继续阅读本历程的下一部分，并阅读文章[了解CMS无头开发。](learn-about.md)

### 选择您自己的冒险 {#choose-your-path}

但是，无论您的学习风格如何，Adobe都希望您在开始使用AEM Headless项目时取得成功。 所以请考虑这两个选项。

* 如果您希望继续&#x200B;**了解无头概念和AEM无头技术**，则应继续按照建议进行的AEM无头历程，方法是接下来查看文档[如何将内容建模为AEM内容模型](model-your-content.md)，在该文档中，您将了解如何在AEM中对内容结构进行建模。
* 如果您希望通过执行&#x200B;**来学习**，则可以跳转到[AEM Headless动手入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)，在该教程中，您将通过实施一个简单的项目来公开AEM Headless内容，直接进入AEM Headless开发。

## 其他资源 {#additional-resources}

文档历程向您展示了AEM如何通过提供说明来解决业务问题，说明如何指导您完成复杂且相互关联的流程和功能。 历程说明了多个功能如何协同工作来满足单个业务需求。

因此，这些旅程旨在独立进行。 但是，其中的许多内容可以相互关联。 请查看这些其他历程，了解有关AEM强大功能如何协同工作的更多信息。

* [AEM无头翻译历程](/help/journey-headless/translation/overview.md)  — 此文档历程让您对无头技术、AEM如何提供无头内容以及如何翻译这些内容有了广泛的了解。
