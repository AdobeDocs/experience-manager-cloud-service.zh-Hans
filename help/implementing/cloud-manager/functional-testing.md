---
title: 功能测试
description: 了解 AEM as a Cloud Service 部署过程内置的三种不同类型的功能测试，确保代码的质量和可靠性。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: ad3a82919b2c0561742527b83af20cc89d8a243a
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 10%

---


# 简介 {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能测试"
>abstract="了解 AEM as a Cloud Service 部署过程内置的三种不同类型的功能测试，确保代码的质量和可靠性。"

了解中可用的质量关卡 [AEMas a Cloud Service部署过程](/help/implementing/cloud-manager/deploy-code.md)，以及内建的不同类型的功能测试、如何贡献以及如何在整个测试策略上下文中最好地利用它们。

## 概述

下图提供了整体测试策略背景下可用管道的高级概述，以及 [AEMas a Cloud Service部署过程](/help/implementing/cloud-manager/deploy-code.md).

![AEM Cloud Service部署质量审核](assets/functional-testing/quality-gates-compact.svg)

## 用途

AEM Cloud Service部署管道的用途是在开发和AEM产品发布生命周期的各个阶段促进可靠且安全的部署。 这些管道包含位于不同级别的多个质量审核，以确保您的AEM应用程序更改和AEM产品更新的部署的完整性和安全性。

Adobe提供了多个内置的质量关卡，而其他质量关卡则需要您的干预才能实施和配置。 这些质量审核具有通用性，其中一些可应用于生命周期的各个阶段，甚至可集成到您自己的开发设置和CI/CD流程中。

内置的质量关卡主要在AEM应用程序的上下文中验证AEM产品的功能。 相反，您设置的自定义质量审核旨在验证应用程序的关键功能和用户交互是否按预期执行。 总而言之，这两组质量审核可以共同工作，确保代码修改和AEM产品更新的自动部署可靠且安全。

请务必注意，这些质量关卡并非旨在作为整个测试策略的全面测试框架。 AEM产品在进入AEM Cloud Service部署过程之前会经过大量测试。 同样，您的应用程序在到达部署阶段之前应该已经处于高质量。 这种方法确保质量关卡专注于其保护部署过程的主要目标，而不是取代完整的测试方案。

## 质量审核

下图提供了可用质量审核及其在整体测试策略和 [AEMas a Cloud Service部署过程](/help/implementing/cloud-manager/deploy-code.md).

![AEM Cloud Service部署质量审核](assets/functional-testing/quality-gates-overview.svg)

### 汇总客户提供的质量审核

|                               | 单元测试 | 自定义<br/> 功能测试 | 自定义<br/> UI测试 | 客户<br/> 验证 | 手动<br/> 测试 |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **生产管道** | 是<br/>阻止<br/> | 是<br/>阻止<br/>6000万超时 | 是<br/>阻止<br/>6000万超时 | 否 | 否 |
| **非生产管道** | 是<br/>阻止<br/> | 选择加入<br/>阻止<br/>6000万超时 | 选择加入<br/>阻止<br/>6000万超时 | 否 | 否 |
| **Adobe内部验证** | 是<br/>阻止<br/> | 是<br/>阻止<br/>6000万超时 | 是<br/>阻止<br/>6000万超时 | 否 | 否 |
| **客户CI/CD** | 是 | 是 | 是 | 是 | 是 |
| **客户本地开发人员** | 是 | 是 | 是 | 是 | 是 |

### 单元测试

建议您为AEM应用程序提供单元测试，这是每个测试策略的基础。 它们旨在快速且频繁地运行，并尽早提供快速反馈。 它们紧密集成到开发人员工作流、您自己的CI/CD和AEM云服务部署管道中。

它们使用JUnit实现，并使用Maven执行。 请参阅 [AEM项目原型的核心模块](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/core.html#unit-tests) 有关AEM和入门的单元测试示例。

### 代码质量

此质量审核是现成配置的，并对AEM应用程序代码运行静态代码分析。

请参阅 [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md) 和 [自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md) 以了解更多信息。

### 产品测试

产品功能测试是 AEM 中核心功能（如创作和复制任务）的一组稳定 HTTP 集成测试 (IT)。Adobe开箱即用地提供和维护这些组件。 它们旨在防止在破坏AEM产品中的核心功能的情况下部署对自定义应用程序代码所做的更改。

它们使用Junit实现，使用Maven执行，并利用官方网站上的 [AEM测试客户端](https://github.com/adobe/aem-testing-clients). 产品测试套件将维护为 [开源项目](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)，遵循最佳实践，并可视为实施测试的良好起点。

### 自定义功能测试

与产品测试一样，客户功能测试是HTTP集成测试(IT)，并且使用Junit实施，使用Maven执行并构建在官方的基础之上 [AEM测试客户端](https://github.com/adobe/aem-testing-clients).

>[!NOTE]
>
>自定义功能测试在生产管道和非生产（选择加入）管道中执行，AEM应用程序使用这些管道更改部署和AEM产品推送更新，因此它是帮助确保应用程序正常运行并提高发布安全性的一个关键贡献。 客户功能测试还在每个客户的内部预发行版验证管道中执行，这有助于提供早期反馈。

为了保持管道执行高效，我们建议重点关注关键功能和主要用户交互流程。 建议将功能测试的执行时间设置为约15分钟或更短。 建议在客户开发流程期间，作为常规客户验证管道的一部分执行不符合此质量关卡的全功能测试包。

请参阅 [开源产品测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 或 [AEM项目原型的it.tests模块](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/ittests.html) 例如。

有关更多信息，请参阅 [Java 功能测试。](/help/implementing/cloud-manager/java-functional-testing.md)

### 自定义用户界面测试

为了最大程度地控制特定于客户的开发的风险，Adobe强烈建议您将关键UI测试捕获到AEMCS中。 虽然数量有限，但给客户体验带来的影响最大。

测试封装在Docker图像中 — 设计为尽可能易变（支持Cypress、Selenium、Java、Javascript等）。 它们遵循与自定义功能测试相同的特性和目的。

>[!NOTE]
>
>自定义UI测试在生产管道和非生产（选择加入）管道中执行，AEM应用程序使用这些管道更改部署和AEM产品推送更新，因此它是帮助确保应用程序正常运行并提高发布安全性的一个关键贡献。 客户UI测试还在每个客户的内部预发行验证管道中执行，这有助于提供早期反馈。

为了保持管道执行高效，我们建议重点关注关键功能和主要用户交互流程。 建议在客户开发流程期间，作为常规客户验证管道的一部分执行不符合此质量关卡的完整UI测试包。

请参阅 [开源示例测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/) 或 [AEM项目原型的ui.tests模块](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uitests.html) 例如。

有关详细信息，请参阅[自定义 UI 测试。](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)

### 体验审核

正在执行体验审核质量审核 [Google灯塔](https://developer.chrome.com/docs/lighthouse/overview/) 针对客户网页的审核。

此质量关卡由AEM现成提供，但不会阻止部署管道。 默认情况下，会针对根页面进行审核(`/`)。 您可通过配置考虑进行审核的最多25个自定义路径来投稿。

请参阅 [体验审核测试](/help/implementing/cloud-manager/experience-audit-testing.md) 以了解更多信息。

### 客户验证

客户验证质量关卡是客户自己的测试策略和工作的占位符，在客户的应用程序更改到达AEM云部署管道之前执行。

当然，您可以在此处选择您喜欢的工具和框架。 相对于客户功能测试和自定义UI测试，没有与AEMas a Cloud Service相关的限制，因此我们建议在此处执行长时间运行的功能和UI测试。

虽然您可以自由选择任何工具和框架，但我们建议您使基于HTTP的集成测试和UI测试与自定义功能测试和自定义UI测试质量审核中提供的工具和框架保持一致。 我们建议集成 [快速开发环境(RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) ，以便在尽可能接近AEM云环境的环境中进行测试。

### 手动测试

手动测试质量关卡是执行手动测试的客户的占位符。 AEM云管道不支持手动测试，因此这需要在您自己的本地测试策略中实现。

对于手动测试，与附加的AEM Cloud Service开发环境集成会很有用。
