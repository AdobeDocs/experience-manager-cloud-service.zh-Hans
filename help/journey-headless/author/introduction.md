---
title: 创作AEM as a Headless CMS — 简介
description: 介绍如何使用Adobe Experience Manager as a Cloud Service的功能作为无头CMS来为项目创作内容。
exl-id: 065b00cb-a82d-4bcb-b2c9-44542cee6303
source-git-commit: 00ec09f327bc2f382d263970e690ed067aaa1355
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 3%

---

# 创作AEM as a Headless CMS — 简介 {#author-headless-introduction}

在 [AEM Headless内容创作历程](overview.md)，您可以学习在使用Adobe Experience Manager(AEM)as a Cloud Service作为无头CMS时，了解创作内容所需的（基本）概念和术语。 这涉及构建和创建用于无头内容交付的内容。

## 目标 {#objective}

* **受众**:初学者
* **目标**:介绍与无头创作相关的概念和术语。

## 内容管理系统(CMS) {#content-management-system}

什么是内容管理系统？

内容管理系统(CMS)就是它所说的 — 用于管理内容的计算机系统。 这有些笼统，因此更确切地说，它通常用于管理您希望在网站上提供的内容。

## Headless CMS {#headless-cms}

“无头”是一个术语，用于描述从在Web上显示内容的方式中有效分离内容的系统。

传统上，您会在CMS中管理内容，而同一CMS则负责在您的网页上渲染该内容。

现在，无头意味着可以在CMS中管理内容集，然后由一个或多个（独立）应用程序访问。

这意味着您的内容可以以各种格式传送到任何设备。 这使整个过程更加灵活，并且还意味着您无需担心布局和格式设置问题。

>[!NOTE]
>
>如果您想进一步了解无头CMS的技术详细信息，可以在“了解CMS无头开发”中阅读更多信息。

## Adobe Experience Manager as a Cloud Service {#aem-cloud-service}

那么什么是AEM?

首先，AEM是一个内容管理系统，具有多种功能，还可以根据您的需求进行自定义。

这一切都意味着它可用作：

* 无头CMS
   * 对于无头，您的内容可以创作为 **内容片段**.
这些是自包含的内容项，可由一系列应用程序直接访问，因为它们具有基于的预定义结构 **内容片段模型**.
这意味着您的内容可以访问各种设备、各种格式和多种功能。
(此外，如果您需要，还可以在构建AEM网页时使用这些片段，这是双重打击。)

* “传统”CMS
   * 内容是使用一系列组件为网页创作的，这些组件定义了内容在您的网站上的呈现方式。 即使在此，AEM也非常灵活，因为您的项目团队可以开发自定义组件。

## 内容建模 {#content-modeling}

因此，内容建模（也称为数据建模）是另一个技术术语，为什么作为作者，它会让您感兴趣？

要使无头应用程序能够访问您的内容并使用它执行一些操作，您的内容真正需要有一个预定义的结构。 你的内容可以是自由形式的，但它可以让你的生活 *非常* 应用程序非常复杂。

基本上，定义内容要遵循的结构的过程涉及设计模型 — 这称为数据建模。

对于AEM，内容架构师角色（通常是不同的人员）将执行数据建模以设计一系列 **内容片段模型**  — 然后，使用 **内容片段**.

>[!NOTE]
>
>如果您想进一步了解数据建模，可以在AEM Headless Content Architect历程下阅读更多内容。

## 下一步 {#whats-next}

既然您已经学习了概念和术语，下一步就是 [了解创作内容片段的基础知识](basics.md). 这将介绍AEM的基本操作以及如何创作内容片段。

## 其他资源 {#additional-resources}

* AEM Headless开发人员历程
   * [了解CMS无头开发](/help/journey-headless/developer/learn-about.md)
   * [了解如何对内容进行建模](/help/journey-headless/developer/model-your-content.md)

* AEM Headless 内容架构师历程

* AEM Headless内容翻译历程
