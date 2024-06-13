---
title: 如何汇总您的应用程序和 AEM Headless 中的内容
description: 在 AEM Headless 开发人员历程的这一部分中，了解如何使用您的 AEM Project（包括内容片段）、GraphQL 调用、REST API 调用和您的应用程序，并为上线做好准备。
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
solution: Experience Manager
feature: Headless
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: ht
source-wordcount: '1061'
ht-degree: 100%

---

# 如何汇总您的应用程序和 AEM Headless 中的内容 {#put-it-all-together}

在 [AEM Headless 开发人员历程](overview.md)的这一部分中，您将熟悉如何使用 AEM 开发工具和 Headless SDK 将您的应用程序组合在一起。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 历程的上一个文档[如何通过 AEM Assets API 更新您的内容](update-your-content.md)中，您已了解如何通过 API 在 AEM 中更新现有 Headless 内容，您现在应该：

* 了解 AEM Assets HTTP API。

## 目标 {#objective}

本文旨在通过以下方式帮助您了解如何将 AEM Headless 应用程序组合在一起：

* 了解 AEM Headless SDK 和所需的开发工具
* 在上线前，设置本地开发运行时以模拟内容
* 了解 AEM 内容复制基础知识

## AEM SDK {#the-aem-sdk}

AEM SDK 用于构建和部署自定义代码。它是您在上线前开发和测试 Headless 应用程序所需的主要工具。它包含以下构件：

* 快速入门 jar – 可用于设置创作和发布实例的可执行的 jar 文件
* Dispatcher 工具 – Dispatcher 模块及其对基于 Windows 的系统和基于 Unix® 的系统的依赖项
* Java™ API Jar – Java™ Jar/Maven 依赖项，公开了所有允许的 Java™ API，它们可用于针对 AEM 进行开发
* Javadoc jar – Java™ API jar 的 javadoc

## AEM Headless SDK {#the-aem-headless-sdk}

与 AEM SDK 不同，AEM **Headless SDK** 是一组库，客户端可以使用这些库通过 HTTP 快速轻松地与 AEM Headless API 进行交互。

有关 AEM Headless SDK 的更多信息，请参阅[此处的文档](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html)。

## 其他开发工具 {#additional-development-tools}

除了 AEM SDK 之外，您还需要其他工具以加快在本地开发和测试您的代码和内容：

* Java™
* Git
* Apache Maven
* Node.js 库
* 您选择的 IDE

由于 AEM 是一个 Java™ 应用程序，因此，您需要安装 Java™ 和 Java™ SDK 以支持开发 AEM as a Cloud Service。

Git 可用于管理源代码管理和签入对 Cloud Manager 的更改，然后将它们部署到生产实例。

AEM 使用 Apache Maven 构建从 AEM Maven 项目原型生成的项目。所有主要 IDE 都提供对 Maven 的集成支持。

Node.js 是一个 JavaScript 运行时环境，用于处理 AEM 项目的 `ui.frontend` 子项目的前端资产。Node.js 与 npm 一起分发，实际上是 Node.js 包管理器，可用于管理 JavaScript 依赖项。

## AEM 系统组件概览 {#components-of-an-aem-system-at-a-glance}

接下来，让我们看看 AEM 环境的组成部分。

完整的 AEM 环境由创作、发布和 Dispatcher 构成。这些相同的组件在本地开发运行时中可用，以便您在上线前更轻松地预览您的代码和内容。

* **Author 服务**&#x200B;是内部用户创建、管理和预览内容的地方。

* **Publish 服务**&#x200B;被视为“实时”环境，通常是最终用户与之交互的对象。在 Author 服务上编辑和审批之后的内容，分发到 Publish 服务。AEM Headless 应用程序最常见的部署模式是将应用程序的生产版本连接到 AEM Publish 服务。

* **Dispatcher** 是一个通过 AEM Dispatcher 模块增强的静态 Web 服务器。它缓存由发布实例生成的网页以提高性能。

## 本地开发工作流 {#the-local-development-workflow}

本地开发项目基于 Apache Maven 构建，并使用 Git 进行源代码管理。若要更新项目，开发人员可以使用他们喜欢的集成开发环境，例如 Eclipse、Visual Studio Code 或 IntelliJ 等。

要测试 Headless 应用程序摄取的代码或内容更新，您必须将更新部署到本地 AEM 运行时，其中包括 AEM 创作和发布服务的本地实例。

请务必记下本地 AEM 运行时中每个组件之间的区别，因为在更新最起作用的位置测试更新是非常重要的。例如，在创作实例上测试内容更新或在发布实例上测试新代码。

在生产系统中，Dispatcher 和 http Apache 服务器将始终位于 AEM 发布实例的前面。它们为 AEM 系统提供缓存和安全服务，因此，针对 Dispatcher 测试代码和内容更新也至为重要。

## 使用本地开发环境在本地预览您的代码和内容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

若要准备启动 AEM Headless 项目，您需要确保项目的所有组成部分都运行良好。

为此，您必须将所有内容放在一起：代码、内容和配置，并在本地开发环境中测试这些内容以准备上线。

本地开发环境包含三个主要区域：

1. AEM 项目 – 该项目包含 AEM 开发人员将处理的所有自定义代码、配置和内容
1. 本地 AEM 运行时 – 本地版本的 AEM 创作和发布服务，用于从 AEM 项目部署代码
1. 本地 Dispatcher 运行时 – 包含 Dispatcher 模块的 Apache httpd Web 服务器的本地版本

在设置本地开发环境后，您可以通过本地部署静态节点服务器来模拟向 React 应用程序提供内容。

<!-- THIS TOPIC IS 404. IT DOES NOT APPEAR IN THE TOC OR ANYWHERE ELSE To get a more in-depth look at setting up a local development environment and all dependencies needed for content preview, see [Production Deployment documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/headless-tutorial/graphql/multi-step/production-deployment.html). -->

## 后续内容 {#whats-next}

现在您已完成 AEM Headless 开发人员历程的这一部分，您应：

* 熟悉 AEM 开发工具
* 了解本地开发工作流

继续您的 AEM Headless 历程，接下来查看文档[如何使用 Headless 应用程序上线](/help/journey-headless/developer/go-live.md)，您将在其中实际推出 AEM Headless 项目！

## 其他资源 {#additional-resources}

* [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [设置本地 AEM 环境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=zh-Hans)
* [适用于客户端浏览器的 AEM Headless SDK (JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [适用于服务器端/Node.js 的 AEM Headless SDK (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [适用于 Java™ 的 AEM Headless SDK](https://github.com/adobe/aem-headless-client-java)
* [AEM as a Headless CMS 简介](/help/headless/introduction.md)
* [AEM 开发人员门户](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
* [AEM 中的 Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans)
