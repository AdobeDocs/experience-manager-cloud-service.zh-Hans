---
title: AEM Headless内容创作历程
description: 介绍Adobe Experience Manager作为Cloud Service的强大、灵活、无头的功能，以及如何为您的项目创作内容。
index: false
hide: true
hidefromtoc: true
source-git-commit: 41ad9e8ee77ae4494d28026b5ad9da45c06eaeaf
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---


# 使用AEM创作无头 — 简介 {#author-headless-introduction}

在[AEM无头内容创作历程](overview.md)的这一部分中，您可以学习必要的（基本）概念和术语，以便了解将Adobe Experience Manager(AEM)作为Cloud Service交付无头内容时的创作内容。

## 目标 {#objective}

* **受众**:初学者
* **目标**:介绍与无头创作相关的概念和术语。

## 内容管理系统(CMS) {#content-management-system}

什么是内容管理系统？

内容管理系统(CMS)就是它所说的 — 用于管理内容的计算机系统。 这有些笼统，因此更确切地说，它通常用于管理您希望在网站上提供的内容。

## 无头CMS {#headless-cms}

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
   * 对于无头，您的内容可以创作为&#x200B;**内容片段**。
这些是可由一系列应用程序直接访问的自包含内容项，因为它们具有基于**内容片段模型**的预定义结构。
这意味着您的内容可以访问各种设备、各种格式和多种功能。
(此外，如果您需要，还可以在构建AEM网页时使用这些片段，这是双重打击。)

* “传统”CMS
   * 内容是使用一系列组件为网页创作的，这些组件定义了内容在您的网站上的呈现方式。 即使在此，AEM也非常灵活，因为您的项目团队可以开发自定义组件。

## 内容建模 {#content-modeling}

因此，内容建模（也称为数据建模）是另一个技术术语，为什么作为作者，它会让您感兴趣？

要使无头应用程序能够访问您的内容并使用它执行一些操作，您的内容真正需要有一个预定义的结构。 您的内容可以自由格式，但这会使应用程序的生活&#x200B;*非常*&#x200B;变得复杂。

基本上，定义内容要遵循的结构的过程涉及设计模型 — 这称为数据建模。

对于AEM，内容架构师角色（通常是不同的人员）将执行数据建模以设计一系列&#x200B;**内容片段模型** — 然后，您使用&#x200B;**内容片段**&#x200B;来将这些模型用作内容的基础。

>[!NOTE]
>
>如果您想进一步了解数据建模，可以在AEM Headless Content Architect历程下阅读更多内容。

## 下一步 {#whats-next}

现在，您已经学习了概念和术语，接下来的步骤是[了解创作内容片段的基础知识](basics.md)。 这将介绍AEM的基本操作以及如何创作内容片段。

## 其他资源 {#additional-resources}

* AEM Headless开发人员历程
   * [了解CMS无头开发](/help/journey-headless/developer/learn-about.md)
   * [了解如何对内容进行建模](/help/journey-headless/developer/model-your-content.md)

* AEM Headless Content Architect历程

* AEM Headless内容翻译历程