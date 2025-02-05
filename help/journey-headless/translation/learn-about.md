---
title: 了解 AEM 中的 Headless 内容及其翻译方法
description: 了解 Headless 概念、它们如何映射到 AEM 以及 AEM 翻译理论。
exl-id: 72bb6646-e573-4576-8d17-49787d8c8c7f
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 92%

---

# 了解 AEM 中的 Headless 内容及其翻译方法 {#learn-about}

了解 Headless 概念、它们如何映射到 AEM 以及 AEM 翻译理论。

## 目标 {#objective}

本文档可帮助您了解 Headless 内容交付、AEM 支持 Headless 的方式以及如何翻译此内容。阅读本文档后，您应：

* 了解 Headless 内容交付的基本概念。
* 熟悉 AEM 支持 Headless 和翻译的方式。

## 全栈内容交付 {#full-stack}

自易于使用的大型内容管理系统 (CMS) 兴起以来，组织便已将其用作管理消息、品牌化和通信的中心位置。通过将 CMS 用作管理体验的中心点，消除了在不同的系统中重复任务的需求，从而提高了效率。

![经典全栈 CMS](/help/journey-headless/developer/assets/full-stack.png)

在全栈 CMS 中，用于操作内容的功能在 CMS 中。该系统的各种功能构成了 CMS 堆栈的不同组件。全栈解决方案有许多优点。

* 需要维护一个系统。
* 集中管理内容。
* 系统的所有服务都是集成的。
* 内容创作是无缝进行的。

因此，如果必须添加新渠道或需要支持新类型的体验，则可将一个（或多个）新组件插入到堆栈中，并且只有一处可作出更改。

![向堆栈添加新渠道](/help/journey-headless/developer/assets/adding-channel.png)

不过，当堆栈中的其他项目可能需要调整才能适应更改时，堆栈中依赖项的复杂性很快就会变得明显。

## Headless 中的头 {#the-head}

任何系统的头通常都是该系统的输出呈现器，通常采用 GUI 或其他图形输出的形式。

就 Headless CMS 而言，CMS 将管理内容并继续将内容交付给消费者。但是，通过仅以标准化方式交付&#x200B;**内容**，Headless CMS 会省略最终的输出呈现，而只保留要&#x200B;**呈现**&#x200B;给消费服务的内容。

![Headless CMS](/help/journey-headless/developer/assets/headless-cms.png)

消费服务，无论是 AR 体验、网上商店、移动体验、渐进式 Web 应用程序 (PWA) 等，都从 Headless CMS 摄入内容并提供其自己的呈现方式。它们负责为您的内容提供它们自己的头。

忽略头将消除复杂性，从而简化 CMS。这样做还会将呈现内容的责任转移到实际需要内容且通常更适合此类呈现的服务。

## 在 AEM 中翻译 Headless 内容 {#translating-in-aem}

除了提供功能强大的工具来以全栈方式创建、管理和交付传统网页之外，AEM 还可用于创作独立内容选择并以 Headless 方式提供这些内容。

利用 AEM 的强大功能，可通过 Headless 方式、全栈方式或同时在两个模型中交付内容。对于翻译专家来说，同一组翻译工具可应用于两种类型的内容，从而为您提供统一的内容翻译方法。

在继续此历程时，您将详细了解 AEM 如何翻译内容，但大致而言，这个概念比较简单：

1. 通过配置翻译集成框架来定义与翻译服务的连接。
1. 使用翻译规则定义应翻译的内容。
1. 创建翻译项目以收获内容，将该内容发送到翻译服务，并接收结果。
1. 检查和发布已翻译的内容。

## 后续内容 {#what-is-next}

感谢您开始 AEM Headless 翻译历程！现在您已阅读本文档，您应：

* 了解 Headless 内容交付的基本概念。
* 熟悉 AEM 支持 Headless 和翻译的方式。

在此知识的基础上继续您的 AEM Headless 翻译历程，接下来查看文档 [AEM Headless 翻译快速入门](getting-started.md)，大致了解 AEM 如何管理 Headless 内容并熟悉其翻译工具。

## 其他资源 {#additional-resources}

我们建议您查看文档[AEM headless翻译入门](getting-started.md)来继续无头翻译历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续无头翻译历程所必需的。

* [MSM 和翻译](/help/sites-cloud/administering/msm-and-translation.md) – AEM 的多站点管理器的详细信息及其使用翻译工具的方式
* [AEM as a Headless CMS 简介](/help/headless/introduction.md)
* [AEM 中的 Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans)