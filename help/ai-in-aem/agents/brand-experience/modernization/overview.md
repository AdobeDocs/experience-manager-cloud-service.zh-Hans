---
title: Experience Modernization Agent概述
description: 了解Experience现代化代理如何借助人工智能将新网站载入Edge Delivery Services。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: c23a6f55-2ba8-4290-b7e8-06cad5de0fc8
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Experience Modernization Agent概述 {#experience-modernization-agent}

了解Experience现代化代理如何借助人工智能将网站载入Edge Delivery Services。

## 简介 {#introduction}

[作为Brand Experience Agent的一部分，](/help/ai-in-aem/agents/brand-experience/overview.md)Experience Modernization Agent通过自动执行网站迁移和基本站点设置，加快了Edge Delivery Services的入门培训。

它结合了[网站创建和迁移技能](#creation-migration)用于初始网站入门和[阻止开发功能](#block-development)以支持网站创建和迁移工作流。 此外，它还提供[体验现代化控制台](#console)作为基于Web的AI辅助开发环境，可直接提供给您。 虽然用户可以通过该控制台直接操作该代理，但开发人员可以完全控制所交付的产品。

对于复杂或高优先级的迁移，Adobe提供了[Agentic Output Engineer (AOE)交付模型，](#aoe-delivery)由工程部门牵头的服务，旨在使用Experience Modernization Agent交付可用于生产环境的Edge Delivery站点。

## 好处 {#benefits}

体验现代化代理可加快采用[Edge Delivery Services](/help/edge/overview.md)的价值实现速度，并让您能够灵活地调整品牌的Web体验。

* **高速**：与传统方法相比，AI自动化处理重复的迁移工作（内容导入、块映射、设计系统应用程序），压缩迁移时间线
* **注重效率**：自动化可减少重复工作，使团队能够专注于价值更高的实施工作
* **任何人都可以访问**：自然语言请求使技术含量较低的用户能够访问网站更改，并且可进行实时预览以立即验证更改
* **企业治理**：开发人员对与GitHub集成的审核工作流的运行保持完全的权威
* **迁移后的灵活性**：使团队能够使用Edge Delivery Services模式扩展和优化迁移的网站

## 站点创建和迁移技能 {#creation-migration}

Experience现代化代理提供了创建新的Edge Delivery Services站点和迁移现有网站的技能。 我们鼓励任何新的Edge Delivery Services站点或迁移都充分利用这些技能。

* 加快网站创建和从几个月到几周或几天的迁移，大大缩短采用Edge Delivery Services实现价值的时间
* 支持从各种CMS平台、旧版AEM或设计系统（如Figma）迁移到支持生产的Edge Delivery Services项目
* 支持符合Edge Delivery Services指导的最佳实践，以实现高性能、可访问性和响应式设计

详细技能包括页面迁移、批量导入、设计提取、导航设置和网页抓取。

## 块开发功能 {#block-development}

Experience现代化代理会利用服务于各种开发任务的一般Edge Delivery Services开发功能，在初始站点创建或迁移之外提供持续价值。

* 遵循内容驱动开发(CDD)方法以建立便于作者使用的内容模型
* 利用[块集合](https://www.aem.live/developer/block-collection)和[块参与方](https://www.aem.live/developer/block-party/)查找参考实施和最佳实践
* 支持测试和调试工作流，以便在部署之前验证更改

详细的功能包括块开发、内容建模、参考块发现、测试和调试。

## 体验现代化控制台 {#console}

Experience Modernization Agent为Edge Delivery Services提供基于Web的AI辅助开发环境，该环境在[`aemcoder.adobe.io`.](https://aemcoder.adobe.io)公开为Web界面

* 该控制台不需要任何本地设置即可让用户以自然语言立即开始提示更改。
* 通过实时AEM预览快速执行日常体验开发任务，并将内容同步到AEM。
* 该控制台通过标准GitHub审核工作流支持企业治理。

自助式Experience Modernization Console现已正式可用。 感兴趣的用户可以请求访问权限，以确保顺利入门体验。

Experience Modernization Console入门！

* 如果您正在通过定位文档创作来使您的网站现代化，请[从此处开始。](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md)
* 如果通过定位AEM创作来使您的网站现代化，请[从此处开始。](/help/ai-in-aem/agents/brand-experience/modernization/getting-started-aem-authoring.md)

## 代理结果工程师(AOE)交付 {#aoe-delivery}

对于复杂的迁移或加速的成果，Adobe提供了代理结果工程师(AOE)交付。 这是一项可选服务，Adobe工程师代表您操作Experience Modernization Agent，并将AI自动化与专家指导相结合，以大规模提供可用于生产的结果。 有关AOE交付的详细信息，请参阅文档[体验现代化代理的AOE交付。](/help/ai-in-aem/agents/brand-experience/modernization/aoe-delivery.md)

如果您对下次迁移的AOE模型感兴趣：

* 请联系您的Adobe代表或客户团队以开始设定范围和计划。
* Adobe将确认资格、估计参与并提议参与计划。

## 限制 {#limitations}

除了体验现代化代理的技能之外，以下用例还需要额外的实施工作。

刮擦技能不支持以下源。

* Intranet或受保护的源（如身份验证后的内容、 VPN或无法访问防火墙）
* 复杂的动态内容，例如需要复杂的用户交互才能在DOM中显示的内容。
   * 如果可以通过特定URL访问客户端渲染的内容，则支持该内容。
   * 还支持通过CSS隐藏但存在于DOM中的元素，例如选项卡、折叠或轮播。

代理不支持以下目标。

* 网站在其中使用基于HTL的交付的AEM发布环境
   * 这些技能仅针对Edge Delivery Services。
* Headless投放模式，如仅限API或基于SPA的投放（例如，Next.js）

以下要求不在专门的自动化技能涵盖范围内，需要手动操作。

* 严格像素完美
   * 只有实际的设计保真度是自动的
* 服务器或客户端第三方数据/服务的集成
* 商业或搜索功能的集成
* MarTech数据层或定位/试验
* 内容/体验片段的隔离
* 多站点继承(MSM)
* 自定义功能（例如，计算器、配置器）
* 自定义业务逻辑

## 后续步骤 {#next-steps}

使用文档[Experience现代化代理快速入门](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md)迁移网站以开始使用。
