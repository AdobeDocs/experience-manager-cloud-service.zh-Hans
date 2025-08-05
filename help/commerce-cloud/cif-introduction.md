---
title: 介绍 AEM Commerce Integration Framework (CIF)
description: 了解如何通过CIF使用和管理Experience Manager Content和Commerce as a Cloud Service。
thumbnail: introducing-aem-commerce.jpg
feature: Commerce Integration Framework
role: Admin
source-git-commit: 127c4acae76c4875bfaffe8b2da0c86c3205beba
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 61%

---


# 介绍 AEM Commerce Integration Framework (CIF) {#cif-intro}

商务解决方案可以是从商业解决方案（如 Adobe Commerce Cloud）到一组自定义商务服务的任何内容。集成在很大程度上取决于用例和生态系统。 它通常影响各种系统，并有许多不同的种类：

* 复杂且动态的生态系统（例如产品目录）的集成
* 企业必须以高效、全渠道的方式管理其自身生命周期中的产品内容
* 为各种头构建复杂、个性化的购物历程
* 能够在后端和前端快速适应并进行创新
* 运行可扩展且稳定的E2E基础架构，该基础架构专为提供卓越性能（闪购、黑色星期五……）而构建，包括统一的搜索和缓存管理

这种复杂性会导致出现潜在故障点、增加 TCO、产生延迟和减少实现的价值。这些原因促使开发 Commerce Integration Framework (CIF)，它是 Experience Manager 的加载项。CIF 利用商务功能扩展 Experience Manager，并实施与商务引擎的集成的标准化。结果是提供经得起未来考验的稳定且可扩展的解决方案，并且总拥有成本(TCO)更低。 它通过敏捷的工具和无缝集成的功能解锁技术和业务创新，从而构建引人入胜的商务体验。

![CIF 元素](./assets/CIF/CIF_Overview.png)

## CIF 好处 {#cif-benefits}

CIF 提供现成的商务核心组件，可减少对自定义代码的需求，从而加快品牌的上市速度。所有核心组件都与 Adobe 的客户端数据层即时集成以补充客户配置文件（例如，统一配置文件）。此配置文件详细捕获访客行为，可用于实时预测和个性化设置客户历程。

CIF 加载项将产品上下文引入 Experience Manager 中，并提供产品控制台和产品/类别选取器等创作工具，使营销人员能够在 Experience Manager 中创建和交付可购买的体验，而无需依靠开发人员。优势包括：

* [引人入胜的体验](#experiences)
* [更快的价值实现](#ttv)
* [强大的集成](#integrations)

### 体验 {#experiences}

利用 AEM 中功能强大的 CIF 工具，内容创建者能够以可扩展且与交付无关的方式快速构建丰富且个性化的商务体验来抓住商机。

![CIF 元素](./assets/CIF/CIF_Product_Experience_Management.png)

### 价值实现时间 (TTV) {#ttv}

CIF通过[AEM核心组件](https://www.aemcomponents.dev/)、[AEM Venia引用店面](https://github.com/adobe/aem-cif-guides-venia)、[AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)以及PWA（Headless内容和商务）的集成模式来加快项目开发。

CIF通过始终保持最新的附加组件为持续创新而构建，可让您访问新的改进功能。

### 集成 {#integrations}

使用 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)（一项基于微服务的无服务器 PaaS）和 [CIF 的引用实施](https://github.com/adobe/commerce-cif-graphql-integration-reference)，将生态系统（例如商务解决方案）与 Experience Cloud 互联。

## 经过验证的模式和最佳实践 {#proven}

CIF通过基于最佳实践的标准化集成模式为您提供支持。 这有助于您现在取得成功，并且可灵活地随您的发展壮大并适应未来的需求：

* 消除围绕产品目录集成可能出现的典型挑战，例如：
   * 目录量或复杂性增加所带来的性能问题
   * 无法访问暂存数据
   * 需要实时产品数据和体验
* 数字成熟度的不断增长导致了对体验管理的需求
* 
   * CIF 附带产品体验管理功能，无需额外的 IT 工作即可逐步整合这些功能。
* 全渠道就绪
   * CIF通过模式、加速器和核心组件支持各种接触点技术（服务器端、混合型、客户端）。

## 历程 {#journey}

如果您正在进行 Commerce 历程，请转到下一步：

* [AEM 内容作者历程](/help/commerce-cloud/commerce-journeys/aem-commerce-content-author/getting-started.md)
