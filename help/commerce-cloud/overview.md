---
title: AEM Commerce as aCloud Service简介
description: Experience Manager商务作为Cloud Service，由商务集成框架(CIF)组成，该框架是Adobe推荐的模式，用于将Magento和其他第三方商务解决方案的商务服务与Experience Cloud集成和扩展。
thumbnail: introducing-aem-commerce.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 1%

---


# 将AEM Commerce作为Cloud Service{#commerce-intro}

Experience Manager商务作为Cloud Service，由商务集成框架(CIF)组成，该框架是Adobe推荐的模式，用于将Magento和其他第三方商务解决方案的商务服务与Experience Cloud集成和扩展。 这使Adobe客户能够基于最新技术提供出众的个性化全渠道购物体验。

Commerce Integration Framework是一个附加模块，用于Experience Manager作为Cloud Service，并提供一组创作工具、组件和参考店面，以加速Experience Manager作为Cloud Service和商务解决方案之间的集成开发。

## CIF优势{#cif-benefits}

主要益处是：

* 该集成是一个抽象层，用于标准化和封装与多个系统的集成。

* CIF支持无外设／全渠道体验：

   * 单页应用程序和多页应用程序
   * GraphQL端点

* CIF为定制和扩展商务服务提供无服务器、基于微服务的流程和业务逻辑层。

* CIF提供与AEM和Magento等Adobe解决方案的即装即用集成

## CIF元素{#cif-elements}

![CIF Elements](/help/commerce-cloud/assets/cif-overview1.jpg)


### 用于创作工具的CIF加载项{#add-on-authoring-tools}

CIF加载项提供对商务创作工具(如产品控制台、产品和类别选择器或针对作者的产品搜索)的访问，使其能够创建包含营销和商务内容的丰富体验。 该加载项还通过GraphQL管理到Magento（或替代商务系统）的后端连接。 设置加载项后，它将作为Cloud Service环境自动部署在AEM上。

### AEM CIF核心组件{#aem-cif-core}

AEM CIF核心组件是服务器端和客户端呈现的组件，支持MagentoGraphQL。 他们习惯于基于AEM技术创建静态、可缓存和SEO友好型商务商店。

提供基本组件，这些组件在商务实施(如产品详细信息、产品列表、导航、搜索等)中很常见。 它们可以按原样使用或进行扩展。

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)的工作方式与[AEM Sites核心组件](https://github.com/adobe/aem-core-wcm-components)类似，但专门用于商务特定用例。

这些组件的主要优点是：

* 它们易于在您的项目中使用。
* 它们可以按原样使用，也可以进行非常小的修改。
* 它们提供通过GraphQL API或REST API与Magento连接的最佳实践

提供了产品Teaser和产品传送等组件，以使AEM作者能够在AEM中创建体验页面，并将营销和商务内容相结合。 这些组件可以轻松拖放到AEM中创建的内容页面，并使用CIF创作工具(如Cloud Service中的产品或类别选取器)链接到特定产品或类别。

所有组件均在[GitHub](https://github.com/adobe/aem-core-cif-components)上开放源。 这显示了将来所做的更改的完全透明度，并允许您非常轻松地获得最新版本。 您还可以提供可整合的提升请求和错误修复。

### AEM Venia Storefront {#aem-venia-storefront}

[AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia)是展示基本B2C商务旅程的现代生产就绪型参考店面。 它可用于启动商务项目，并使用AEM、CIF和Magento加速项目。 它演示了集成AEM和Magento的最佳实践，并演示了如何使用[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)和[AEM Sites核心组件](https://github.com/adobe/aem-core-wcm-components)并支持Adobe商务GraphQL端点。 它还为售前人员提供一个参考站点，以演示AEM与Magento之间的集成。

AEM Venia Storefront是一个混合页面应用程序，AEM拥有玻璃，Magento以无头方式为商务后端提供支持。 店面中同时使用服务器端渲染和客户端渲染。 服务器端渲染用于交付静态内容，客户端渲染用于交付动态内容。

产品和目录页面相对静态，并使用AEM CIF核心组件(如产品详细信息和产品列表)在AEM中创建的通用模板在服务器端呈现。 这些组件通过GraphQL API从Magento获取数据。
这些页面是动态创建的，呈现在服务器上，缓存在AEM调度程序上，然后交付到浏览器。
对于库存或价格等更动态属性，则使用客户端组件。 客户端组件或Web组件通过GraphQL API直接从Magento获取数据，然后内容在浏览器上呈现。

#### 签出 {#checkout}

此参考店面使用客户端购物车组件来呈现购物车和结帐表单，以展示完整的体验集成模式，您可以通过Magento以完全无头的方式运行和AEM拥有玻璃来提供商务体验。 建议使用所提供的抽象支付方法。 这使得浏览器客户端与支付网关提供商直接通信，从而Adobe云和Magento云都不会保存或传递PCI敏感数据。

#### 帐户管理{#account-management}

帐户管理由Magento处理，而参考店面利用基于客户端React的组件，使AEM能够为以下功能提供体验：创建帐户、登录和忘记密码。

AEM Venia Storefront项目是开放源，有关详细信息，请参阅[AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia)。

### AEM 项目原型 {#aem-project-archtype}

[AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)可用于创建基于最佳实践的最小Adobe Experience Manager项目，作为您自己的AEM项目的起点。 可选地，[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)可以包含在新生成的项目中。

### CIF扩展层{#cif-extension}

CIF扩展层是承载复杂业务逻辑的中间层。 它运行于Adobe I/O Runtime平台，该平台是Adobe的无服务器平台。 它允许您通过将业务和流程逻辑注入微服务级别来扩展端到端服务调用。 例如，业务逻辑将使用位置和渠道来确定库存策略。 例如，流程逻辑可以检索个性化信息。

### CIF集成层{#cif-integration-layer}

CIF集成层用于与其他商务解决方案的集成标准化。 它运行于Adobe I/O Runtime平台(Adobe的无服务器平台)上，通过映射第三方API与Adobe商务API，支持微服务级别的集成。 为了帮助您开始构建与AEM的第三方集成，我们创建了[引用实现](https://github.com/adobe/commerce-cif-graphql-integration-reference)，以演示如何通过Adobe商务API(MagentoGraphQL API)集成非Magento商务后端。

## AEM Commerce Integration Patterns {#aem-commerce-integration}

下面显示了一些常用的AEM Commerce集成模式。

![AEM CIF集成模式](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### 集成模式1 {#integration-pattern-one}

这是我们推荐的集成模式，AEM拥有整个玻璃，并通过Adobe商务GraphQL API集成商务服务。 这种模式使AEM能够完全灵活地跨设备定制富媒体站点设计。 这种集成模式被CIF作为现成的解决方案支持。


### 集成模式2 {#integration-pattern-two}

此模式描述了一种完全无头的内容和商务交付方式。 投放完全在客户端。 在此模式中，内容通过API提供，HTML和商务数据通过GraphQL提供。 目前，CIF现成版本不支持此模式。


### 集成模式3 {#integration-pattern-three}

在这种模式下，Magento拥有玻璃并嵌入AEM创作的内容。 AEM创作的内容可以通过体验片段或内容片段交付。 这种整合模式需要针对具体项目进行工作，不能与CIF一起开箱即用。


### 集成模式4 {#integration-pattern-four}

这是一个常见的集成模式，其中玻璃层或表示层在AEM和商务解决方案之间进行拆分。 通常，商务解决方案提供非营销页面（如结帐和我的帐户）,AEM提供营销页面和店面目录体验。 在这种模式下，您需要确保在两个系统之间正确处理购物车和用户会话，以避免用户体验脱节。 例如，Magento将购物车和用户会话存储在cookie中，可在AEM和Magento之间共享。 这种模式需要具体项目的工作，不能在CIF的开箱即用。
