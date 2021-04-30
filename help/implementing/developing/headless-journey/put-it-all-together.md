---
title: 如何将一切结合在一起 — 您的应用程序和内容以AEM无外设
description: 在AEM无外设开发人员历程的这一部分中，了解如何将您的AEM项目（包括内容片段）、您的GraphQL调用、您的REST API调用和您的应用程序)准备好投入使用。
hide: true
hidefromtoc: true
index: false
exl-id: 254fb9dd-36c8-43ce-aaea-ceb4d079503d
translation-type: tm+mt
source-git-commit: e8eb9d2c96d24601e50c48f6846a8c8bac8b0252
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 0%

---

# 如何将一切结合在一起 — 您的应用程序和您的内容放在AEM Headless {#put-it-all-together}中

>[!CAUTION]
>
>正在进行中的工作 — 此文档的创建正在进行中，不应理解为完整或明确，也不应将其用于生产目的。

在[AEM无外设开发人员历程的这一部分中，](overview.md)了解如何将您的AEM项目（包括内容片段）、您的GraphQL调用、您的REST API调用和您的应用程序)准备好并投入使用。

## 迄今为止的故事{#story-so-far}

在AEM无头旅程的上一个文档中，[如何通过AEM Assets API更新您的内容](update-your-content.md)您学会了如何通过API在AEM中更新现有无头内容，您现在应：

* 了解AEM Assets HTTP API。

本文以这些基础为基础，因此您了解如何准备自己的AEM无头项目投入使用。

## 目标 {#objective}

* 了解什么是AEM的本地开发工作流程
* 安装AEM SDK以获取可用于在
* 了解在本地开发运行时旁边使用所需的开发工具

## 本地开发工作流{#the-local-development-workflow}

本地开发项目以Apache Maven为构建基础，并使用Git进行源代码控制。 为了更新项目，开发人员可以使用他们的首选集成开发环境，如Eclipse、Visual Studio代码或IntelliJ等。

要测试将由您的无外设应用程序摄取的代码或内容更新，您需要将更新部署到本地AEM运行时，该运行时包括AEM作者实例和发布实例的本地实例。

请务必注意本地AEM运行时中每个组件之间的区别，因为在最重要的位置测试更新很重要 — 例如，在创作时测试内容更新或在发布实例上测试新代码。

在生产系统中，调度程序和http Apache服务器始终位于AEM发布实例前面。 它们为AEM系统提供缓存和安全服务，因此测试针对调度程序的代码和内容更新也至关重要。

在您确保所有内容都经过测试并正常运行后，即可将代码更新推送到Cloud Manager中的集中式Git存储库。

在将更新上传到Cloud Manager后，可以使用Cloud Manager的CI/CD管道将这些更新部署到AEM作为Cloud Service。


## AEM SDK {#the-aem-sdk}

AEM SDK用于构建和部署自定义代码。 它包含以下伪像：

* 快速启动jar — 可执行的jar文件，可用于设置作者和发布实例
* 调度程序工具 — 针对基于Windows和UNIX系统的调度程序模块及其依赖项
* Java API Jar - Java Jar/Maven依赖关系，它公开可用于针对AEM进行开发的所有允许的Java API
* Javadocjar - Javadocs for the Java API jar

## 本地开发环境设置{#local-development-environment}

为了准备启动您的AEM无外设项目，您需要确保项目的所有组成部分运行正常。

为此，您需要将所有内容（代码、内容和配置）整合在一起，并在本地开发环境中测试，以实现实时就绪。

地方发展环境由三个主要领域组成：

1. AEM项目 — 其中将包含AEM开发人员将要处理的所有自定义代码、配置和内容
1. 本地AEM运行时 — 将用于部署AEM项目代码的AEM作者和发布服务的本地版本
1. 本地调度程序运行时 — Apache httpd web服务器的本地版本，包括调度程序模块

## 开发工具 {#development-tools}

除了AEM SDK，您还需要其他工具，以便在本地开发和测试代码和内容：

* Java
* Git
* 阿帕奇·马文
* Node.js库
* 您选择的IDE

由于AEM是Java应用程序，您需要安装Java和Java SDK以支持将AEM作为Cloud Service进行开发。

Git是您用来管理源代码控制、检入对Cloud Manager的更改，然后将其部署到生产实例的工具。

AEM使用Apache Maven构建从AEM Maven Project原型生成的项目。 所有主要IDE都为Maven提供集成支持。

Node.js是一个JavaScript运行时环境，用于处理AEM项目的ui.front子项目的前端资源。 Node.js与npm一起分发，它是事实上的Node.js包管理器，用于管理JavaScript依赖关系。

## 下一步是什么{#what-is-next}

您应该继续您的AEM无头旅程，接下来查看文档[如何使用您的无头应用程序](go-live.md)实现您的AEM无头项目！

## 其他资源 {#additional-resources}

* [本地开发环境设置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-dispatcher-runtime)  — 了解如何安装为AEM开发开始所需的工具
* [AEM作为Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)  — 深入了解AEM SDK