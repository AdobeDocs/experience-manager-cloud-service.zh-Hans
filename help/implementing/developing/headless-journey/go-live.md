---
title: 如何与无外设应用程序一起使用
description: 在AEM无外设开发人员历程的这一部分中，了解如何通过将您的本地代码以Git格式存放并移至Cloud Manager Git，以便利用CI/CD渠道，实时部署无外设应用程序。
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
source-git-commit: 309fae113f98111e8dc548226a7fba1b72f16248
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 0%

---

# 如何与无外设应用程序共存{#go-live}

>[!CAUTION]
>
>正在进行中的工作 — 此文档的创建正在进行中，不应理解为完整或明确，也不应将其用于生产目的。

在[AEM无头开发人员历程的这一部分中，](overview.md)了解如何通过将您的本地代码以Git格式保存并移至Cloud Manager Git（用于CI/CD管道）来实时部署无头应用程序。

## 迄今为止的故事{#story-so-far}

在AEM无头旅程的上一个文档中，[如何将一切结合在一起 — 您的应用程序和您的内容在AEM无头中](put-it-all-together.md)您学会了如何准备您自己的AEM无头项目上线，现在您应：

* 了解上线的要求。

本文基于这些基础知识，因此您了解如何实际实施AEM无外设项目。

## 目标 {#objective}

此文档可帮助您了解AEM无头发布管道以及在应用程序上线之前需要注意的性能注意事项。

* 了解AEM SDK和所需的开发工具
* 设置本地开发运行时，以在上线前模拟您的内容
* 了解AEM内容复制和缓存基础知识
* 在启动之前保护和扩展您的应用程序
* 监视性能和调试问题

## AEM SDK {#the-aem-sdk}

它包含以下伪像：

* 快速启动jar — 可执行的jar文件，可用于设置作者和发布实例
* 调度程序工具 — 针对基于Windows和UNIX系统的调度程序模块及其依赖项
* Java API Jar - Java Jar/Maven依赖关系，它公开可用于针对AEM进行开发的所有允许的Java API
* Javadocjar - Javadocs for the Java API jar

## 开发工具 {#development-tools}

除了AEM SDK，您还需要其他工具，以便在本地开发和测试代码和内容：

* Java
* AEM SDK
* Git
* 阿帕奇·马文
* Node.js库
* 您选择的IDE

由于AEM是Java应用程序，您需要安装Java和Java SDK以支持将AEM作为Cloud Service进行开发。

AEM SDK用于构建和部署自定义代码。 它是您在上线前测试无外设应用程序所需的主要工具。

Git是您用来管理源代码控制以及将更改签入到Cloud Manager，然后将其部署到生产实例的工具。

AEM使用Apache Maven构建从AEM Maven Project原型生成的项目。 所有主要IDE都为Maven提供集成支持。

Node.js是一个JavaScript运行时环境，用于处理AEM项目的ui.front子项目的前端资源。 Node.js与npm一起分发，它是事实上的Node.js包管理器，用于管理JavaScript依赖关系。

## AEM系统组件概览{#components-of-an-aem-system-at-a-glance}

完整的AEM环境由作者、发布和调度程序组成。 这些相同的组件将在本地开发运行时中提供，以便您在上线前更轻松地预览代码和内容。

* **创作服** 务是内部用户创建、管理和预览内容的场所。

* **发布服** 务被视为“实时”环境，通常是最终用户与之交互的内容。内容在创作服务上经过编辑和批准后，将分发到发布服务。 AEM无外设应用程序的最常见部署模式是让应用程序的生产版本连接到AEM发布服务。

* **Dispatcher是** 一个静态Web服务器，它通过AEM调度程序模块进行了扩展。它缓存由发布实例生成的网页以提高性能。

## 本地开发工作流{#the-local-development-workflow}

本地开发项目以Apache Maven为构建基础，并使用Git进行源代码控制。 为了更新项目，开发人员可以使用他们的首选集成开发环境，如Eclipse、Visual Studio代码或IntelliJ等。

要测试将由您的无外设应用程序摄取的代码或内容更新，您需要将更新部署到本地AEM运行时，其中包括AEM创作和发布服务的本地实例。

请务必注意本地AEM运行时中每个组件之间的区别，因为在最重要的位置测试更新非常重要。 例如，在创作时测试内容更新或在发布实例上测试新代码。

在生产系统中，调度程序和http Apache服务器始终位于AEM发布实例前面。 它们为AEM系统提供缓存和安全服务，因此测试针对调度程序的代码和内容更新也至关重要。

在您确保所有内容都经过测试并正常运行后，即可将代码更新推送到Cloud Manager中的集中式Git存储库。

在将更新上传到Cloud Manager后，可以使用Cloud Manager的CI/CD管道将这些更新部署到AEM作为Cloud Service。

## 使用本地开发环境{#previewing-your-code-and-content-locally-with-the-local-development-environment}在本地预览您的代码和内容

为了准备启动您的AEM无外设项目，您需要确保项目的所有组成部分运行正常。

为此，您需要将所有内容整合在一起：代码、内容和配置，并在本地开发环境中测试它，以实现实时就绪。

地方发展环境由三个主要领域组成：

1. AEM项目 — 其中将包含AEM开发人员将要处理的所有自定义代码、配置和内容
1. 本地AEM运行时 — 将用于部署AEM项目代码的AEM作者和发布服务的本地版本
1. 本地调度程序运行时 — Apache httpd web服务器的本地版本，包括调度程序模块

设置本地开发环境后，您可以通过在本地部署静态节点服务器来模拟向React应用程序提供服务的内容。

要更深入地了解设置本地开发环境以及内容预览所需的所有依赖项，请参阅[使用AEM发布服务的生产部署](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites)。

## 部署到生产{#deploy-to-production}

在本地测试所有代码和内容后，即可开始使用AEM进行生产部署。

您可以通过利用Cloud Manager CI/CD管道来开始部署代码，该管道在[此处](/help/implementing/deploying/overview.md)中有广泛介绍。

## 准备AEM无外设应用程序以投入使用{#prepare-your-aem-headless-application-for-golive}

现在，您应该遵循下面概述的最佳实践，为启动准备AEM无外设应用程序。

### 在启动{#secure-and-scale-before-launch}之前保护和扩展您的无头应用程序

1. 配置[基于令牌的身份验证](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
1. 安全Webhooks
1. 配置缓存和可伸缩性

### 模型结构与GraphQL输出{#structure-vs-output}

* 避免创建输出超过15kb JSON的查询（gzip压缩）。 长JSON文件占用大量资源，客户端应用程序需要进行解析。
* 避免片段层次的嵌套级别超过五个。 其他级别使内容作者很难考虑其更改的影响。
* 使用多对象查询，而不是在模型内使用依赖关系层次来建模查询。 这样，无需进行大量内容更改，就可以在重构JSON输出方面具有更大的长期灵活性。

### 最大化CDN缓存命中率{#maximize-cdn}

* 请勿使用直接GraphQL查询，除非您从表面请求实时内容。
   * 请改用持久查询。
   * 提供600秒以上的CDN TTL，以便CDN可以缓存它们。
   * AEM可以计算模型更改对现有查询的影响。
* 在低和高内容更改率之间拆分JSON文件/GraphQL查询，以减少CDN的客户端流量并分配更高的TTL。 这样可最大限度地减少CDN通过来源服务器重新验证JSON。
* 要主动使CDN中的内容失效，请使用软清除。 这样，CDN可以重新下载内容，而不会导致缓存丢失。

### 缩短下载无外设内容{#improve-download-time}的时间

* 确保HTTP客户端使用HTTP/2。
* 确保HTTP客户端接受gzip的标头请求。
* 最小化用于托管JSON和引用对象的域数。
* 利用`Last-modified-since`刷新资源。
* 在JSON文件中使用`_reference`输出，无需解析完整的JSON文件即可开始下载资产。

## 性能监视{#performance-monitoring}

为使用户在使用AEM无外设应用程序时获得最佳体验，您务必要监控关键性能指标，如下所述：

* 验证预览和应用程序的生产版本
* 验证AEM状态页的当前服务可用性状态
* 访问性能报告
   * 投放性能
      * 快速(CDN) — 检查呼叫数、缓存率、错误率、负载流量
      * 来源服务器 — 呼叫数、错误率、CPU负载、负载流量
   * 作者性能
      * 检查用户数、请求数和加载数
* 访问特定于应用程序和空间的性能报告
   * 服务器启动后，检查常规指标是否为绿色/橙色/红色，然后确定特定应用程序问题
   * 打开以上已筛选到应用程序/空间的相同报表(即Photoshop桌面、付费专区等)
   * 使用Splunk日志API访问服务和应用程序性能
   * 如果存在其他问题，请与客户支持联系。

## 疑难解答 {#troubleshooting}

### 调试 {#debugging}

按照以下最佳做法，作为调试的一般方法：

* 使用预览版本的应用程序验证功能和性能
* 使用应用程序的生产版本验证功能和性能
* 使用内容片段编辑器的JSON预览验证
* Inspect客户端应用程序中的JSON，用于检查客户端应用程序或投放问题是否存在
* Inspect使用GraphQL检查是否存在与缓存内容或AEM相关的问题

### 使用支持{#logging-a-bug-with-support}记录错误

为了在您需要进一步帮助时通过支持有效记录错误，请执行以下步骤：

* 如有必要，获取问题的截屏
* 文档重现问题的方法
* 文档期刊复制的内容
* 通过AEM支持门户以适当的优先级记录问题

## 下一步是什么{#what-is-next}

现在您已完成了AEM Headless Developer历程的这一部分，您应：

* 了解AEM内容复制和缓存基础知识。
* 了解如何为无外设应用程序配置模拟上线所需的工具。
* 了解如何在启动之前保护和扩展您的应用程序。
* 了解如何监视性能和调试问题。

您应继续您的AEM无头旅程，接下来查看文档[启动后](post-launch.md)，了解如何保持无头体验。

## 其他资源 {#additional-resources}

* [设置本地AEM环境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [AEM作为Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [部署到AEM作为Cloud Service概述](/help/implementing/deploying/overview.md)
* [使用Cloud Manager部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [将Cloud Manager Git存储库与外部Git存储库集成，并将项目部署到AEM作为Cloud Service](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/master/help/implementing/developing/headless-journey/access-your-content.md)