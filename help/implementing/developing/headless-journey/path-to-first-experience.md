---
title: 使用AEM无外设获得第一次体验的途径
description: 在AEM无外设开发人员历程的这一部分中，您将了解在AEM中实施第一个无外设体验的步骤，包括规划考虑事项，并学习最佳实践，以尽可能顺利地实现您的路径。
hide: true
hidefromtoc: true
index: false
exl-id: 257fc173-6bfb-4b60-b66c-6d6bdd5cf13f
translation-type: tm+mt
source-git-commit: 635768f63c604d1c1892de57c55693da6a0fe954
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 0%

---

# 使用AEM Headless {#path-to-first-experience}的初次体验路径

>[!CAUTION]
>
>正在进行中的工作 — 此文档的创建正在进行中，不应理解为完整或明确，也不应将其用于生产目的。

在[AEM无外设开发者历程](overview.md)的这一部分中，您将了解在AEM中实施第一个无外设体验的步骤，包括规划注意事项，并学习最佳实践，以尽可能顺利地实现您的路径。

## 迄今为止的故事{#story-so-far}

在AEM无头旅程的上一个文档中，[将AEM无头作为Cloud Service入门](getting-started.md)您学习了无头CMS的基本理论，现在您应：

* 了解AEM无外设功能的基础知识。
* 了解使用AEM无外设功能的先决条件。
* 了解AEM无外设集成级别。
* 能够根据范围定义您的项目。

本文以这些基础为基础，因此您了解如何准备自己的AEM无头项目。

## 目标 {#objective}

此文档可帮助您了解实施第一个项目所需的步骤。 读完后，您应：

* 了解设计内容时的重要规划注意事项。
* 了解在AEM中实现无外设的步骤。
* 了解需要哪些必要的工具和AEM配置。
* 了解最佳实践，让您的无头旅程变得顺畅、保持内容生成高效并确保内容快速交付。

## 要求{#requirements}

在继续此文档之前，请确保已查看AEM无头开发人员历程[AEM无头入门Cloud Service](getting-started.md)中以前的文档，确保您：

* 满足所列要求。
* 已考虑过您自己的项目定义，包括范围、角色和绩效。

## 成功计划{#planning-for-success}

要开始您的第一个AEM无头项目，您需要确保拥有一个内容模型，该模型支持您要在所有渠道中进行的个性化和更新。

与AEM分开，如果要构建客户端应用程序，您还希望确保设置了适当的开发环境，以便能够针对对AEM作为Cloud Service的API调用测试客户端。

### 定义内容模型和API {#defining-models}

您希望跨渠道提供一致的体验并管理个性化的活动，因此您可以将每个渠道和界面视为其要交付的独特内容结构。 然而，让每个渠道都有自己的内容模型，将很难维护。

相反，您应根据组织原则(如品牌和产品层次、商品或表面类别或客户旅程中的步骤)考虑不同表面上的内容如何相关。 例如，如果您有一组表面支持您制造的特定品牌汽车，您可能希望使用内容模型进行开始，以获得适用于整个汽车的常规信息，然后具有更多特定于上下文的元素，例如汽车启动时到出现服务问题时所需的内容。 这种模式将强制实施对一般汽车品牌内容的继承，同时允许根据所需的特定上下文进行转换。 它还有助于将来管理此内容的更新，因为您可以根据角色来实施控制，例如整个汽车品牌的整体营销人员或产品经理与负责“起跑车”体验的作者。

在您对需要呈现内容的各种客户端建立内容模型并清除视图后，您需要确保与访问各种内容模型相关的GraphQL/API会发布到需要这些内容的所有客户端。 如何访问某些内容有不同的选项。 您可以请求静态的特定内容片段，以便缓存内容和提高性能。 您还可以请求动态生成的内容，这将需要进行更多处理。 确保客户能够利用最有效满足其业务需要的API。

## 了解您的环境{#understanding-environments}

在AEM中，有三种环境:开发、升级和生产。

开发环境（您可以有多个应用程序）是进行试验和尝试想法的安全场所。 在项目的初始阶段，Adobe建议使用开发环境来尝试各种内容模型，并查看哪些内容为表面提供了预期输出。

无外设项目的暂存环境用于在新的AEM产品版本推出到生产之前对其进行验证。 在那里保持生产内容模型和内容子集的最新列表，因此您可以渲染JSON文件以比较它们，但在您进行更改或AEM版本引入更改时，仍提供相同的输出

内容作者在生产中创建和管理其实际内容。 生产中的模型更改必须谨慎进行，并且要考虑到向后兼容性。

在开发阶段，建议您使用开发和阶段环境。 当您转到性能测试时，您将希望转到生产环境。

### 开发人员与内容作者的合作{#cooperation}

开发人员需要使用填充的内容模型设置AEM开发环境。 开发人员开发的客户端将从AEM无头中消费内容，因为内容作者仍在创建内容。 这就是API定义真正重要的原因。 通过利用AEM SDK，开发人员可以创建测试挂接，以便创建客户端和单元测试以确保客户端能够正确呈现内容。

内容作者根据已在暂存环境中定义的内容模型创建内容。 使用内容片段创作工具，作者将创建新内容片段或编辑现有内容片段。 在发布之前，作者可以与开发人员合作将内容模型推上开发，或为作者设置开发人员环境以预览其在客户端的显示方式，从而预览其在客户端的显示方式。

## 设置 {#setup}

在AEM中开始使用无外设之前，您需要确保已启用所有必需的功能。 本节概述了所需内容。 实现这些步骤的实际步骤将在[AEM无头开发者历程中详细介绍。](#overview.md)

您还可以选择参阅[其他资源](#additional-resources)以了解有关各个主题的详细信息。

### 配置 {#configuration}

1. 启用内容片段
1. 启用GraphQL
1. 设置无外设SDK

## 实施您的第一个AEM无外设应用程序

这是使用AEM交付内容来实施您的第一个无外设应用程序所需内容的概述。 如何执行这些步骤将在无头开发人员历程的后半部分中详细介绍。

1. 创建内容片段模型
1. 创建内容片段
1. 使用GraphQL查询内容

## 最佳实践 {#best-practices}

一个无头项目之所以成功，不仅是因为技术得以实施，还因为良好的规划和项目治理。 以下是内容作者和开发人员在规划项目时要牢记的许多最佳实践。

### 组织内容{#organizing-content}

* 使结构尽可能复杂，但尽可能简单。 更简单的内容结构有助于简化内容管理并提高系统性能。
* 在您的战略中优先重用内容。 创建子模型和内容引用，它们可以跨多个更高级模型和渠道重复使用。
* 使内容结构尽可能自我解释，使内容作者能够快速学习和适应创作任务。
* 如果您具有访问限制，请尝试使您的内容模型与访问要求保持一致。
* 当您有访问要求时，这些要求将推动您的内容层次结构。 将由同一组人员编辑的内容分组在一起。
* 将类似内容分组到文件夹中。
   * 内容作者更有可能复制并粘贴现有内容以创建新内容。 因此，在同一文件夹中执行此操作可提高效率。
   * AEM允许为每个文件夹设置允许的模型，因此&#x200B;**“新建**”按钮将仅显示该位置支持的模型。
* 如果在模型中设置了根文件夹，则可以简化新内容片段的串联内容片段编辑器创建。 然后，从业者不必选择位置，只需提供名称即可开始编辑新参考。

### 创作内容 {#authoring}

* 对于渠道特定的内容版本，请考虑使用内容片段变量。 根据内容主控同步变量以简化内容更改管理。
* 邀请其他内容制作者审阅内容并提供注释和注释反馈，这些注释和注释可在内容片段编辑器中使用，并可在内容片段管理控制台中全局跨片段使用。
* 尽可能少的必备元素，让一切保持运转。 必选元素可以阻止工作流。

### 创作全局内容{#localization}

* 建立内容翻译的规则和管理。 要减少系统负载，请将转换建立为可以以较长时间间隔运行的异步进程。 为本地化质量控制和错误修复留出时间。
* 利用您的翻译技术系统提供的所有功能，这些功能可以与AEM集成，如翻译记忆库。
* 了解富媒体内容（如图像和视频）是否需要本地化。

## 下一步是什么{#what-is-next}

现在您已完成了AEM Headless Developer历程的这一部分，您应：

* 了解设计内容时的重要规划注意事项。
* 了解在AEM中实现无外设的步骤。
* 了解需要哪些必要的工具和AEM配置。
* 了解最佳实践，让您的无头旅程变得顺畅、保持内容生成高效并确保内容快速交付。

我们希望您以此基础知识为基础，充分了解AEM Headless的强大功能和灵活性，以便您能够将其用于您自己的项目。 为此，您有选择。

### 选择您自己的冒险{#choose-your-path}

无论您的学习风格如何，Adobe都希望您能够成功地开始使用AEM无头项目。

* 如果您希望&#x200B;**继续学习无头概念和AEM无头技术**，则应继续您的AEM无头旅程，方法是阅读文档[如何将您的内容建模为AEM内容模型](model-your-content.md)，从中学习如何在AEM中建模您的内容结构。
* 如果您希望&#x200B;**通过执行**&#x200B;来学习，您可以跳到[AEM无头动手教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)入门，在该教程中，您将通过实施一个简单项目来公开AEM无头内容，直接进入AEM无头开发。

## 其他资源 {#additional-resources}

尽管建议您通过查看文档[如何将您的内容建模为AEM内容模型，](model-your-content.md)来进入无头开发旅程的下一部分，但以下是一些附加的可选资源，可以更深入地了解本文档中提到的某些概念，但无需继续无头开发旅程。

* [作为Cloud Service的AEM Sites无头开发](/help/implementing/developing/headless/introduction.md)  — 快速介绍如何为AEM无头开发人员提供必要功能
* [AEM无头Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 使用这些实践教程探索如何使用AEM将内容交付到无头端点的各种选项并选择适合您的选项。
* [无外设内容管理使用](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) GraphQL API — 请通过本课程概述在AEM中实现的GraphQL API。需要通过AdobeID进行身份验证。
* [AEM指南WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  — 此GitHub项目包括高亮显示AEM GraphQL API的示例应用程序。
* [介绍Adobe Experience Manager的体系结构作为Cloud Service](/help/core-concepts/architecture.md) - AEM体系结构的完整概述
* [无头入门指南](/help/implementing/developing/headless/introduction.md#getting-started)  — 快速介绍AEM无头功能，面向已经了解AEM的用户。
* [创建内容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 有关内容片段模型的技术文档
* [创建内容片段](/help/assets/content-fragments/content-fragments.md)  — 有关内容片段的技术文档
* [查询包含GraphQL的内容](/help/assets/content-fragments/graphql-api-content-fragments.md) - GraphQL API的技术文档
