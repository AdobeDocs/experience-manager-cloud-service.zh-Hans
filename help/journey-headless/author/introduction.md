---
title: AEM Headless内容创作历程
description: 介绍Adobe Experience Manager as a Cloud Service强大、灵活、无头的功能，以及如何为项目创作内容。
exl-id: 065b00cb-a82d-4bcb-b2c9-44542cee6303
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 3%

---

# 使用 AEM 为 Headless 创作 - 简介 {#author-headless-introduction}

在 [AEM Headless内容创作历程](overview.md)，您可以学习必要的（基本）概念和术语，以了解使用Adobe Experience Manager(AEM)as a Cloud Service进行无头内容交付的创作内容。

## 目标 {#objective}

* **受众**:初学者
* **目标**:介绍与无头创作相关的概念和术语。

## 内容管理系统(CMS) {#content-management-system}

什么是内容管理系统？

A Content Management System (CMS) is just what it says it is - a computer system used to manage content. 这有些笼统，因此更确切地说，它通常用于管理您希望在网站上提供的内容。

## 无头CMS {#headless-cms}

“无头”是一个术语，用于描述从在Web上显示内容的方式中有效分离内容的系统。

Traditionally you would manage your content in a CMS, and the same CMS would be responsible for rendering that content on your webpages.

现在，无头意味着可以在CMS中管理内容集，然后由一个或多个（独立）应用程序访问。

这意味着您的内容可以以各种格式传送到任何设备。 This makes the whole process much more flexible, and also means that you do not need to worry about layout and formatting.

>[!NOTE]
>
>如果您想进一步了解无头CMS的技术详细信息，可以在“了解CMS无头开发”中阅读更多信息。

## Adobe Experience Manager as a Cloud Service {#aem-cloud-service}

So what is AEM?

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

For the headless applications to be able to access your content, and do something with it, your content really needs to have a predefined structure. It would be possible to have your content as free-form, but it would make life *very* complicated for the applications.

Basically the process of defining the structure for your content to adhere to involves designing a model - and this is called data modeling.

For AEM the Content Architect role (often a different person) will perform the data modeling to design a range of **Content Fragment Models** - that you then use as a basis for your content by using **Content Fragments**.

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
