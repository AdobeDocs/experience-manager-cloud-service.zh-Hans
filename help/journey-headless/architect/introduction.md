---
title: AEM Headless Content Architect历程
description: 介绍Adobe Experience Manager作为Cloud Service的强大、灵活、无头的功能，以及如何为项目建立内容模型。
index: false
hide: true
hidefromtoc: true
source-git-commit: 41ad9e8ee77ae4494d28026b5ad9da45c06eaeaf
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---


# 使用AEM实现无头内容建模 — 简介 {#architect-headless-introduction}

在[AEM Headless Content Architect历程](overview.md)的这一部分中，您可以学习必要的（基本）概念和术语，以了解将Adobe Experience Manager(AEM)作为Cloud Service进行无头内容交付的内容建模。

本文档可帮助您了解无头内容交付、AEM如何支持无头，以及如何为无头内容建模。 阅读后，您应该：

* 了解无头内容交付的基本概念。
* 熟悉AEM如何支持无头和内容建模。

## 目标 {#objective}

* **受众**:初学者
* **目标**:介绍与无头内容建模相关的概念和术语。

## 全栈内容交付 {#full-stack}

自从易于使用的大型内容管理系统(CMS)兴起以来，各公司一直利用它们作为管理报文传送、品牌推广和通信的中心位置。 将CMS用作管理体验的中心点，通过消除在不同系统中重复任务的需要，提高了效率。

![经典的全栈CMS](/help/journey-headless/developer/assets/full-stack.png)

在全栈CMS中，用于处理内容的所有功能都在CMS中。 系统的功能构成了CMS堆栈的不同组件。 全栈解决方案具有许多优势。

* 有一个系统需要维护。
* 内容是集中管理的。
* 系统的所有服务都已集成。
* 内容创作是无缝的。

因此，如果需要添加新渠道或支持新类型的体验，则可以在堆栈中插入一个（或多个）新组件，并且只有一个位置进行更改。

![向堆栈中添加新渠道](/help/journey-headless/developer/assets/adding-channel.png)

但是，堆栈中依赖项的复杂性会很快变得明显，因为堆栈中的其他项目需要调整以适应更改。

## 无头的头 {#the-head}

任何系统的头通常是该系统的输出渲染器，通常以GUI或其他图形输出的形式。

当我们讨论无头CMS时，CMS会管理内容并继续向消费者提供内容。 但是，无头CMS仅以标准化方式传送&#x200B;**内容**，从而忽略最终输出渲染，将内容的&#x200B;**表示**&#x200B;保留给消费服务。

![无头CMS](/help/journey-headless/developer/assets/headless-cms.png)

消费性服务(无论是AR体验、网店、移动体验、渐进式Web应用程序(PWA)等)从无头CMS中获取内容并提供自己的呈现。 他们负责为您的内容提供自己的头脑。

省略头部通过消除复杂性来简化CMS。 这样做还会将呈现内容的责任转移到实际需要内容且通常更适合此类呈现的服务上。

## 内容建模 {#content-modeling}

内容建模（也称为数据建模）是您的专长，因此在为无头进行建模时需要考虑哪些因素？

要使无头应用程序能够访问您的内容并使用它执行一些操作，内容真正需要具有预定义的结构。 您的内容可以自由格式，但这会使应用程序的生活&#x200B;*非常*&#x200B;变得复杂。

对于AEM，作为内容架构师，您将执行内容建模以设计一系列&#x200B;**内容片段模型**。 这些属性定义了内容作者创建包含内容的&#x200B;**内容片段**&#x200B;时使用的结构。

### 访问内容 {#access-content}

这更像是一个开发细节 — 但你可能会感兴趣，只是为了完成故事。

创建内容片段模型并且作者使用它们生成内容后，无标题应用程序将需要访问此内容。

Adobe Experience Manager(AEM)作为Cloud Service，可以使用AEM GraphQL API有选择地访问您的内容片段，以仅返回所需的内容。 使用API，开发人员可以制定用于选择特定内容的查询。此选择过程基于&#x200B;*您的*&#x200B;内容片段模型。

这意味着您的项目可以实现结构化内容的无头交付，以供在您的应用程序中使用。

## 下一步 {#whats-next}

现在，您已经学习了概念和术语，接下来的步骤是[了解使用内容片段模型进行建模的基础知识](basics.md)。

## 其他资源 {#additional-resources}

* AEM Headless开发人员历程
   * [了解CMS无头开发](/help/journey-headless/developer/learn-about.md)
   * [了解如何对内容进行建模](/help/journey-headless/developer/model-your-content.md)
