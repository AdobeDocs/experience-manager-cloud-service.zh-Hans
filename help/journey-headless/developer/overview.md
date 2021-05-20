---
title: AEM Headless开发人员历程
description: 从此处开始，您可以逐步了解AEM强大而灵活的无外设功能、其功能，以及如何在您的第一个开发项目中利用这些功能。
source-git-commit: 1ac93a066f808e7dd2ed7e34aa7635e9914a4ea9
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 1%

---


# AEM Headless开发人员历程{#aem-headless-developer-journey}

从此处开始，您可以体验AEM强大而灵活的无头功能、其功能，以及如何在您的第一个无头开发项目中利用这些功能。

## 简介 {#introduction}

无头实施对于向受众提供体验（无论这些体验位于何处，也不论渠道如何）越来越重要。

与全栈解决方案中的传统方式一样，无头实施可用于页面和组件管理，并且重点关注创建不依赖于渠道、可重复使用的内容片段及其跨渠道交付。 它是一种用于实施Web体验的现代化、动态开发模式。

本指南将引导您完成最重要的主题，以便您在完成该工作后：

* 充分了解无头内容交付的含义及其好处。
* 了解AEM无头功能以及它们如何协同工作来提供无头体验。
* 能够采取实施首个AEM无头项目的首要步骤。

## 受众 {#audience}

此历程专为开发人员角色设计，从开发人员的角度阐述AEM Headless项目的要求、步骤和方法。 历程将定义其他角色，开发人员必须与这些角色进行交互才能使项目取得成功，但历程的视点是开发人员的角色。

此历程中的信息当然对其他角色很有用，但某些信息对于某些角色来说将是多余的。 请继续关注即将发布的涉及其他角色的历程。

## 无头开发人员历程{#the-journey}

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
| 6 | [如何通过AEM资产API更新内容](update-your-content.md) | 了解如何使用REST API访问和更新内容片段内容。 |
| 7 | [如何将所有内容整合在一起 — 在AEM Headless中查看您的应用程序和内容](put-it-all-together.md) | 了解如何获取您的AEM项目并为使用AEM Headless SDK进行上线做准备。 |
| 8 | [如何使用无头应用程序](go-live.md) | 了解如何在Git中实时部署应用程序并获取本地代码，然后将其移至Cloud Manager Git for CI/CD管道。 |
| 9 | [可选 — 如何使用AEM创建单页应用程序(SPA)](create-spa.md) | 了解AEM无头功能后，请了解如何结合使用无头和无头交付，并了解如何使用AEM SPA编辑器框架创建可编辑的SPA。 |

## 下一步是什么{#what-is-next}

现在，您已准备好开始AdobeHeadless历程。 我们建议您继续阅读本历程的下一部分，并阅读文章[了解CMS无头开发。](learn-about.md)

### 选择您自己的冒险{#choose-your-path}

但是，无论您的学习风格如何，Adobe都希望您在开始使用AEM Headless项目时取得成功。 所以请考虑这两个选项。

* 如果您希望继续&#x200B;**了解无头概念和AEM无头技术**，则应继续按照建议进行的AEM无头历程，方法是接下来查看文档[如何将内容建模为AEM内容模型](model-your-content.md)，在该文档中，您将了解如何在AEM中对内容结构进行建模。
* 如果您希望&#x200B;**通过执行**&#x200B;来学习，可以跳转到[AEM Headless无头入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)，在该教程中，您将通过实施一个简单的项目来公开AEM无头内容，直接进入AEM无头开发。
