---
title: 功能测试
description: 了解AEM as a Cloud Service部署过程中内置的三种不同类型的功能测试，确保代码的质量和可靠性。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 7a370ee0ab77046d128ae260af2575d50e655254
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 3%

---


# 简介 {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能测试"
>abstract="了解AEM as a Cloud Service部署过程中内置的三种不同类型的功能测试，确保代码的质量和可靠性。"

发现[AEM as a Cloud Service部署流程](/help/implementing/cloud-manager/deploy-code.md)中可用的质量关卡以及各种类型的内置功能测试。 了解如何在全面的测试策略框架内贡献并优化其使用。

## 概述

下图提供了整体测试策略和[AEM as a Cloud Service部署过程](/help/implementing/cloud-manager/deploy-code.md)上下文中的可用管道的整体概述。

![AEM Cloud Service部署质量关卡](assets/functional-testing/quality-gates-compact.svg)

## 用途

AEM Cloud Service部署管道的用途是在开发和AEM产品发布生命周期的各个阶段促进可靠且安全的部署。 这些管道包含位于不同级别的多个质量审核，以确保您的AEM应用程序更改和AEM产品更新的部署的完整性和安全性。

Adobe提供了多个内置的质量关卡，而其他质量关卡则需要您的干预才能实施和配置。 这些质量关卡具有通用性，可在不同的生命周期阶段应用，并可直接集成到开发设置和CI/CD流程中。

内置的质量关卡主要在AEM应用程序的上下文中验证AEM产品的功能。 相反，您设置的自定义质量审核旨在验证应用程序的关键功能和用户交互是否按预期执行。 总而言之，这两组质量审核可以共同工作，确保代码修改和AEM产品更新的自动部署可靠且安全。

请务必注意，这些质量关卡并非旨在作为整个测试策略的全面测试框架。 AEM产品在进入AEM Cloud Service部署过程之前会经过大量测试。 同样，您的应用程序在到达部署阶段之前应该已经处于高质量。 这种方法确保质量关卡专注于其保护部署过程的主要目标，而不是取代完整的测试方案。

## 质量审核

下图提供了可用质量审核及其在整体测试策略和[AEM as a Cloud Service部署过程](/help/implementing/cloud-manager/deploy-code.md)中的使用的详细视图。

![AEM Cloud Service部署质量关卡](assets/functional-testing/quality-gates-overview.svg)

### 汇总客户提供的质量审核

|                               | 单元测试 | 自定义<br/>功能测试 | 自定义<br/>用户界面测试 | 客户<br/>验证 | 手动<br/>测试 |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **生产管道** | 是<br/>正在阻止<br/> | 是<br/>阻止<br/>60m超时 | 是<br/>阻止<br/>30m超时 | 否 | 否 |
| **非生产管道** | 是<br/>正在阻止<br/> | 选择加入<br/>正在阻止<br/>60m超时 | 选择加入<br/>正在阻止<br/>30m超时 | 否 | 否 |
| **Adobe内部验证** | 是<br/>正在阻止<br/> | 是<br/>阻止<br/>60m超时 | 是<br/>阻止<br/>30m超时 | 否 | 否 |
| **客户CI/CD** | 是 | 是 | 是 | 是 | 是 |
| **客户本地开发人员** | 是 | 是 | 是 | 是 | 是 |

### 单元测试

建议您为AEM应用程序提供单元测试，这是每个测试策略的基础。 它们旨在快速且频繁地运行，并尽早提供快速反馈。 它们紧密集成到开发人员工作流、您自己的CI/CD和AEM云服务部署管道中。

它们使用JUnit实现，并使用Maven执行。 请参阅AEM项目原型](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/using#unit-tests)的[核心模块，了解AEM的单元测试示例和入门。

### 代码质量

此质量审核是现成配置的，并对AEM应用程序代码运行静态代码分析。

有关详细信息，请参阅[代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)和[自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

### 产品测试

产品功能测试是核心AEM功能（包括创作和复制任务）的稳定HTTP集成测试(IT)。 Adobe开箱即用地提供和维护这些组件。 它们旨在防止在破坏AEM产品中的核心功能的情况下部署对自定义应用程序代码所做的更改。

它们使用JUnit进行实施，与Maven一起运行，并依赖官方的[AEM测试客户端](https://github.com/adobe/aem-testing-clients)。 产品测试套件维护为
[开源项目](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)遵循最佳实践，可视为实施测试的良好起点。

### 自定义功能测试

与产品测试类似，客户功能测试是使用JUnit实现的HTTP集成测试(IT)，使用Maven运行，并构建在官方[AEM测试客户端](https://github.com/adobe/aem-testing-clients)之上。

>[!NOTE]
>
>可在用于AEM应用程序更改部署和AEM产品推送更新的生产和非生产（选择加入）管道中运行的自定义功能测试。 它们在确保应用程序正常运行以及增强发布安全性方面起着关键作用。 客户功能测试还在每个客户的内部预发行版验证管道中执行，这有助于提供早期反馈。

为了保持高效的管道运行，Adobe建议重点关注关键功能和主用户交互流程，旨在确保大约15分钟或更短的功能测试运行时间。 超过此时间的完整功能测试套件应在开发过程中作为常规客户验证管道的一部分执行。

有关示例，请参阅[开源产品测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)或AEM项目原型](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests)的[it.tests模块。

有关更多信息，请参阅 [Java 功能测试。](/help/implementing/cloud-manager/java-functional-testing.md)

### 自定义用户界面测试

为了最大程度地控制特定于客户的开发的风险，Adobe鼓励您将关键UI测试捕获到AEM as a Cloud Service中。 保持这些受限制的体验，但侧重于最大限度地提高它们对客户体验的影响。

测试封装在Docker图像中 — 设计为尽可能易变(支持Cypress、Selenium、Java和JavaScript)。 它们遵循与自定义功能测试相同的特性和目的。

>[!NOTE]
>
>自定义UI测试在用于AEM应用程序更改部署和AEM产品推送更新的生产和非生产（选择加入）管道中执行。 它们对于确保应用程序的正常运行以及增强发布安全性至关重要。 客户UI测试还在每个客户的内部预发行验证管道中执行，这有助于提供早期反馈。
>
>非Selenium容器应根据[UI测试部分](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)中的环境变量，使用HTTP代理执行测试。

为了保持管道执行的有效性，Adobe建议重点关注关键功能和主要用户交互流程。 超出此质量关卡的完整UI测试包应作为常规客户验证管道的一部分执行。 将它们整合到客户的开发流程中。

有关示例，请参阅[开源示例测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/)或AEM项目原型](/help/implementing/cloud-manager/ui-testing.md)的[ui.tests模块。

有关详细信息，请参阅[自定义 UI 测试。](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)

### 体验审核

体验审核质量关卡正在对客户的网页执行[Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/)审核。

此质量关卡由AEM现成提供，但不会阻止部署管道。 默认情况下，将对发布实例的根页面(`/`)执行审核。 您可通过配置考虑进行审核的最多25个自定义路径来投稿。

有关详细信息，请参阅[体验审核测试](/help/implementing/cloud-manager/experience-audit-dashboard.md)。

### 客户验证

客户验证质量关卡是客户自己的测试策略和工作的占位符，在客户的应用程序更改到达AEM云部署管道之前执行。

您可以在此处选择喜欢的工具和框架。 与客户功能测试和自定义UI测试相比，没有与AEM as a Cloud Service相关的限制。 因此，Adobe建议您在此处执行长时间运行的功能和UI测试。

虽然您可以选择任何工具和框架，但Adobe建议将基于HTTP的集成和UI测试与自定义功能和UI测试质量审核中使用的工具和框架保持一致。 此外，Adobe建议将[快速开发环境(RDE)](/help/implementing/developing/introduction/rapid-development-environments.md)并入您的本地测试策略以密切镜像AEM云环境。

### 手动测试

手动测试质量关卡是执行手动测试的客户的占位符。 由于AEM云管道不支持手动测试，因此必须将其包含在您的本地测试策略中。

对于手动测试，与附加的AEM Cloud Service开发环境集成会很有用。
