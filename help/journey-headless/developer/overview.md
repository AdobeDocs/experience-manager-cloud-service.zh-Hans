---
title: AEM无头CMS开发人员历程
description: 了解如何使用Adobe Experience Manager(AEM)作为无头CMS进行无头开发。 了解如何使用内容模型、内容片段和GraphQL API等功能来支持无头内容交付。
landing-page-description: 了解无头内容交付和实施。 了解有关在业务中制定战略的更多信息。
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
source-git-commit: 06aec2fa43db2393416dd5efab886d9c301ffdb2
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 16%

---

# AEM无头CMS开发人员历程 {#aem-headless-developer-journey}

欢迎阅读面向初次使用Adobe Experience Manager无头CMS的开发人员的文档！

了解强大而灵活的无头功能、其功能，以及如何在您的第一个无头开发项目中利用这些功能。 此历程为您提供开发首个无头应用程序所需的所有信息。

## 简介 {#introduction}

AEM的无头实施使用内容片段模型和内容片段，以专注于创建结构化、渠道中性、可重复使用的内容片段及其跨渠道交付。 要实现此目的，需要像在完整堆栈解决方案中一样，放弃页面和组件管理。 它是一种实现数字体验的现代化、动态的开发模式。

本指南将指导您在AEM中介绍无标题实施主题，因此在您完成后，您将：

* 充分了解无头内容交付的含义及其好处。
* 了解AEM无头功能以及它们如何协同工作来提供无头体验。
* 能够采取实施首个AEM无头项目的首要步骤。

>[!TIP]
>
> 如果您愿意 **学习** 并拥有AEM的现有知识，请访问AEM Headless教程，这些教程由API和框架组织，在 [“其他资源”部分](#additional-resources) 在本文档末尾。

## 受众 {#audience}

此历程专为开发人员角色设计，从开发人员的角度阐述AEM Headless项目的要求、步骤和方法。 历程定义了其他角色，开发人员必须与这些角色进行交互才能使项目取得成功，但历程的视角是开发人员的视角。

以下是在此历程中互动的角色。

| 角色 | 描述 | 此历程中的角色 |
|---|---|---|
| 开发人员（目标受众） | 具有开发无头应用程序的经验，这些应用程序使用来自不同来源的内容 | 此历程的目标受众 |
| 内容作者 | 创建并管理无头投放的内容 | 内容作者创建开发人员随意交付的内容。 |
| 管理员 | 管理 AEM 的基本设置和配置 | 开发人员与管理员合作，进行开发所需的配置更改。 |
| 内容架构师 | 对必须无头传送的数据要求进行分析，并定义此数据的结构 | 开发人员与内容架构师合作，以了解数据的结构和无头提供数据的要求。 |

## 无头开发人员历程 {#the-journey}

我们将介绍此历程中的许多主题，这些主题将为您提供AEM中无头的基础知识。

尽管您可以直接转到历程的特定部分，但许多概念都基于之前文章中的概念构建。 我们建议您从头开始，然后按顺序进行。

| # | 文章 | 描述 |
|---|---|---|
| 0 | AEM Headless开发人员历程 | 本文档 |
| 1 | [了解 CMS Headless 开发](learn-about.md) | 了解无头技术以及何时使用它。 |
| 2 | [AEM Headless as a Cloud Service 快速入门](getting-started.md) | 了解AEM Headless先决条件 |
| 3 | [首次 AEM Headless 使用体验的路径](path-to-first-experience.md) | 设置开发环境，并了解如何将简单的应用程序与AEM Headless集成 |
| 4 | [如何对内容进行建模](model-your-content.md) | 了解如何对内容结构进行建模。 |
| 5 | [如何通过 AEM 投放 API 访问您的内容](access-your-content.md) | 了解如何使用GraphQL查询访问内容片段内容。 |
| 6 | [如何通过 AEM Assets API 更新您的内容](update-your-content.md) | 了解如何使用REST API访问和更新内容片段内容。 |
| 7 | [如何将所有内容整合在一起 — 在AEM Headless中查看您的应用程序和内容](put-it-all-together.md) | 了解如何获取您的AEM项目并为使用AEM Headless SDK进行上线做准备。 |
| 8 | [如何使用 Headless 应用程序上线](go-live.md) | 了解如何在Git中实时部署应用程序并获取本地代码，然后将其移至Cloud Manager Git for CI/CD管道。 |
| 9 | [可选 — 如何使用AEM创建单页应用程序(SPA)](create-spa.md) | 了解如何结合使用头和无头交付，并了解如何使用AEM SPA Editor框架创建可编辑的SPA。 |

## 后续内容 {#what-is-next}

请参阅下一篇文章以开始操作： [了解CMS无头开发。](learn-about.md)

### 选择您自己的冒险 {#choose-your-path}

你喜欢按自己的节奏学习吗？ 请查看以下选项：

* 如果您希望继续 **了解无头概念和AEM无头技术**，则您应该继续您的AEM无头历程，方法是接下来查看文档 [如何将内容建模为AEM内容模型](model-your-content.md) 其中，您了解如何在AEM中构建内容结构模型。
* 如果您愿意 **学习**，您可以跳转到 [AEM Headless动手操作入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=zh-Hans) 在这里，您将通过实施一个简单的项目来公开AEM无头内容，从而直接进入AEM开发。

## 其他资源 {#additional-resources}

文档历程向您展示了AEM如何通过提供说明来解决业务问题，说明如何指导您完成相关流程和功能。 历程说明了多个功能如何协同工作来满足单个业务需求。

请查看这些其他历程，了解有关AEM强大功能如何协同工作的更多信息。

* [AEM Headless教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans)  — 如果您希望通过学习和掌握AEM的现有知识，请学习我们由API和框架组织的动手实践教程，这些教程将探索如何创建和使用基于AEM Headless构建的应用程序。
* [AEM无头翻译历程](/help/journey-headless/translation/overview.md)  — 此文档历程使您能够广泛了解无头技术、AEM如何提供无头内容以及如何翻译无头内容。
* [Headless 创作历程](/help/journey-headless/author/overview.md) – 从这里开始，引导您了解 AEM 强大而灵活的 Headless 特性、它们的功能以及如何在您的第一个 Headless 项目中为内容建模。
* [Headless 架构师历程](/help/journey-headless/architect/overview.md) – 从这里开始了解 Adobe Experience Manager as a Cloud Service 强大而灵活的 Headless 功能，以及如何对项目内容进行建模。
* [AEMas a Cloud Service技术文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已经对AEM和无头技术有了非常深入的了解，请查看我们的深入技术文档。
