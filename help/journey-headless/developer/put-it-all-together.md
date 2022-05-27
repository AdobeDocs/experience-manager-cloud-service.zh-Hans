---
title: 如何将所有内容整合在一起 — 在AEM Headless中查看您的应用程序和内容
description: 在AEM无头开发人员历程的这一部分中，了解如何获取您的AEM项目（包括内容片段、GraphQL调用、REST API调用和应用程序）并为其上线做准备。
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 7%

---

# 如何将所有内容整合在一起 — 在AEM Headless中查看您的应用程序和内容 {#put-it-all-together}

在 [AEM Headless开发人员历程](overview.md)，您可以了解如何使用AEM开发工具和Headless SDK将应用程序整合在一起。

## 迄今为止的故事 {#story-so-far}

在AEM无头历程的上一个文档中， [如何通过AEM Assets API更新您的内容](update-your-content.md) 您学习了如何通过API在AEM中更新现有无头内容，现在应该：

* 了解AEM Assets HTTP API。

## 目标 {#objective}

本文旨在帮助您了解如何通过以下方式将AEM无头应用程序整合在一起：

* 了解AEM Headless SDK和所需的开发工具
* 在上线前设置本地开发运行时以模拟内容
* 了解AEM内容复制基础知识

## AEM SDK {#the-aem-sdk}

AEM SDK用于构建和部署自定义代码。 它是您在开始使用之前开发和测试无头应用程序的主要工具。 它包含以下工件：

* 快速入门jar — 一个可执行的jar文件，可用于设置创作实例和发布实例
* 调度程序工具 — 基于Windows和UNIX®的系统的调度程序模块及其依赖项
* Java™ API Jar - Java™ Jar/Maven依赖项，它公开了可用于针对AEM进行开发的所有允许的Java™ API
* Javadoc jar - Java™ API Jar的javadoc

## AEM Headless SDK {#the-aem-headless-sdk}

与AEM SDK不同，AEM **无外设SDK** 是一组库，客户端可使用这些库通过HTTP快速轻松地与AEM Headless API交互。

有关AEM Headless SDK的更多信息，请参阅 [文档位于此处](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/how-to/aem-headless-sdk.html?lang=en).

## 其他开发工具 {#additional-development-tools}

除了AEM SDK之外，您还需要其他工具，以便在本地开发和测试代码和内容：

* Java™
* Git
* 阿帕奇·马文
* Node.js库
* 您选择的IDE

由于AEM是Java™应用程序，因此您需要安装Java™和Java™ SDK才能支持AEMas a Cloud Service的开发。

您将使用Git来管理源控件，并将更改签入到Cloud Manager中，然后将其部署到生产实例。

AEM使用Apache Maven生成从AEM Maven项目原型生成的项目。 所有主要IDE都为Maven提供集成支持。

Node.js是一个JavaScript运行时环境，用于处理AEM项目的前端资产 `ui.frontend` 子项目。 Node.js与npm一起分发，npm是事实上的Node.js包管理器，用于管理JavaScript依赖项。

## AEM系统组件概览 {#components-of-an-aem-system-at-a-glance}

接下来，让我们看一下AEM环境的组成部分。

完整的AEM环境由创作、发布和调度程序组成。 这些组件在本地开发运行时中可用，以便您在上线前更轻松地预览代码和内容。

* **Author 服务**&#x200B;是内部用户创建、管理和预览内容的地方。

* **Publish 服务**&#x200B;被视为“实时”环境，通常是最终用户与之交互的对象。在 Author 服务上编辑和审批之后的内容，分发到 Publish 服务。AEM Headless 应用程序最常见的部署模式是将应用程序的生产版本连接到 AEM Publish 服务。

* **调度程序** 是一种通过AEM Dispatcher模块增强的静态web服务器。 它会缓存由发布实例生成的网页，以提高性能。

## 本地开发工作流 {#the-local-development-workflow}

本地开发项目是基于Apache Maven构建的，并且使用Git进行源代码管理。 为了更新项目，开发人员可以使用他们首选的集成开发环境，例如Eclipse、Visual Studio代码或IntelliJ等。

要测试将由您的无头应用程序摄取的代码或内容更新，您必须将更新部署到本地AEM运行时，其中包括AEM创作和发布服务的本地实例。

请务必注意本地AEM运行时中每个组件之间的差异，因为在最重要的位置测试更新非常重要。 例如，在创作时测试内容更新或在发布实例中测试新代码。

在生产系统中，Dispatcher和http Apache服务器将始终位于AEM发布实例之前。 它们为AEM系统提供缓存和安全服务，因此，还必须针对Dispatcher测试代码和内容更新。

## 使用本地开发环境在本地预览代码和内容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

要为启动您的AEM无头项目做好准备，您需要确保项目的所有组成部分都正常运行。

为此，您必须将所有内容整合在一起：代码、内容和配置，并在本地开发环境中测试它，以便进行上线准备。

地方发展环境由三个主要领域组成：

1. AEM项目 — 其中将包含AEM开发人员将要处理的所有自定义代码、配置和内容
1. 本地AEM运行时 — AEM创作和发布服务的本地版本，将用于从AEM项目部署代码
1. 本地Dispatcher运行时 — Apache httpd Web服务器的本地版本，其中包含Dispatcher模块

设置本地开发环境后，您可以通过在本地部署静态节点服务器来模拟向React应用程序提供内容的过程。

要更深入地了解如何设置本地开发环境以及内容预览所需的所有依赖关系，请参阅 [生产部署文档](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## 接下来呢？ {#whats-next}

现在，您已完成AEM Headless开发人员历程的这一部分，接下来您应该：

* 熟悉AEM开发工具
* 了解本地开发工作流

您应该通过下一步审阅文档来继续您的AEM无头历程 [如何使用您的无头应用程序](/help/journey-headless/developer/go-live.md) 您实际将AEM Headless项目上线！

## 其他资源 {#additional-resources}

* [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [设置本地AEM环境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [适用于客户端浏览器的AEM Headless SDK(JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [AEM Headless SDK for server-side/Node.js(JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [AEM Headless SDK for Java™](https://github.com/adobe/aem-headless-client-java)

