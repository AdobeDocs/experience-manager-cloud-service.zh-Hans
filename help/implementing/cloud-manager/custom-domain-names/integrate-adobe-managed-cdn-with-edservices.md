---
title: 在Cloud Manager中将Edge Delivery Services与Adobe托管的CDN集成
description: null
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: 71ea3b810d4145d5581c29e26db9bc157c425a15
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# 在Cloud Manager中将Edge Delivery Services与Adobe托管的CDN集成 {#integrate-adbe-cdn-with-edservices-in-cm}

Adobe Managed CDN (AMC-D)与Edge Delivery Services本机集成，为您提供针对Adobe Experience Manager (AEM)站点的高性能、全球分布式体验。

它们一起为您提供了以下好处：

* 由Adobe管理的一整套企业级CDN。
* 现代化的边缘交付层，可加快请求速度、优化缓存并抵御常见攻击。
* 适用于域管理、SSL证书和管道驱动部署的统一Cloud Manager工作流程。

<!--
Adobe's Edge Delivery Services (EDS) can take advantage of an Adobe managed CDN. EDS is a framework that optimizes website delivery for speed, simplicity, and scalability by pushing content closer to the user through edge nodes. It is not a replacement for a CDN, but rather a way to enhance content delivery, especially when you use the Adobe managed CDN. It offers you the following benefits:

* Adobe-Managed CDN: EDS can use an Adobe-managed CDN, offering features like self-service CDN management and automatic certificate renewal. 
* EDS and AEM: EDS is a feature of AEM as a Cloud Service and works alongside the AEM authoring environment. 
* Performance enhancement: EDS, in conjunction with an Adobe Managed CDN, improves website performance by caching content at edge locations closer to users, reducing latency. 
* Flexibility: EDS provides flexibility in content delivery, allowing your organization to choose between the Adobe-managed CDN or their own CDN setup, based on their needs and existing infrastructure. 
Self-Service CDN Management:
Adobe-managed CDN within EDS enables self-service configuration and management tasks like SSL certificate setup. 
 
Use Cases:
EDS with CDN integration is beneficial for various scenarios, including e-commerce storefronts and websites requiring high performance and scalability. -->

## Cloud Manager中的Adobe Managed CDN中的Edge Delivery Services部署选项 {#deployment-options}

本主题将介绍两种在Cloud Manager中的Adobe Managed CDN上部署Edge Delivery Services的方式，并且同样重要的是，还可帮助您确定哪种选项最适合您的用例。

可以使用以下两个选项之一设置Edge Delivery Services。 每个版本都有不同的功能。

|  | 部署选项 | 关键文档 | 功能 | 最适合 |
| --- | --- | --- | --- | --- |
| 选项1 | *具有*&#x200B;现有AEM as a Cloud Service (AEMaaCS)环境 | [从现有环境设置代理](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment) | 配置管道通常适用于AEMaaCS环境 | 已在Cloud Manager中运行Sites并希望快速低风险地提高性能的团队。 |
| 选项2 | *不带*&#x200B;现有AEMaaCS环境；称为独立的“Edge环境”。 | [在没有现有环境的情况下设置Edge Delivery站点](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment) | 配置管道目前仅通过有限的Beta计划可用于Edge环境。<br>查看[添加Edge Delivery配置管道](help/implementing/cloud-manager/release-notes/current.md##add-eds-pipeline)。 | 希望采用完整Edge Delivery架构和精细路由的新构建或迁移。 |

<!-- Ultimately this URL above will need to be updated on GA -->

| 选项 | 摘要 | 最适合 | 关键文档 |
| --- | --- | --- | --- |
| Adobe Managed CDN代理 | Adobe Managed CDN面向现有AEM Sites环境。 您当前的Sites管道仍为“原点”，而AMC-D处理边缘缓存和TLS终止。 | 已在Cloud Manager中运行Sites并希望快速低风险地提高性能的团队。 | 设置AMC-D代理 |
| 使用originSelectors配置管道 | 专用的Edge Delivery配置管道将静态和动态内容直接发布到边缘。 `originSelectors`在AMC-D和AEM创作/发布层之间路由流量。 | 希望采用完整Edge Delivery架构和精细路由的新构建或迁移。 | 配置Edge Delivery管道 |

>[!TIP]
>
>不确定选择哪条路径？ 有关决策准则，请参阅下面的[选择部署模型](#choose-deployment-model)。

## 选择部署模型 {#choose-deployment-model}

这两种模型可以在同一Cloud Manager项目中并存，允许分阶段迁移。

| 如果您…… | 然后使用…… |
| :--- | :--- |
| 需要快速的、更改最少的转出，并且已在Cloud Manager中托管站点 | AMC-D代理 |
| 计划为Edge Delivery重构内容，或者希望在多个源之间实现细粒度路由 | 配置Edge交付管道+ `originSelectors` |

## 先决条件 {#prerequisites}

1. 在Cloud Manager中载入您的站点 — 两种部署模型均需要。 关注载入AEM站点。

2. 自带Git (BYOG)（可选） — 如果您在Adobe Git之外存储网站代码，请完成BYOG载入。

3. Edge Delivery许可证 — 确保您的项目已获得Edge Delivery Services许可。


