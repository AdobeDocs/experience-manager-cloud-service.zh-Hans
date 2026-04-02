---
title: Cloud Manager 中的 Edge Delivery Services 简介
description: 了解如何使用 Edge Delivery Services 传递您的 Cloud Manager 项目。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: fc9f7f10d1797bda5f31d82005b0afbb6ea1e644
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 73%

---


# Cloud Manager 中的 Edge Delivery Services 简介 {#edge-delivery-services}

Edge Delivery Services 是一组可组合的服务，使您在网站上创作内容时具有高度的灵活性。此功能允许您执行以下操作：

* 创建拥有完美灯塔评分的快速 Site。
* 通过操作遥测持续监测性能。
* 通过分离内容源来提高创作效率。

您可以使用通用编辑器和基于文档的创作来使用 AEM 内容管理和所见即所得创作。

AEM as a Cloud Service 中的 Cloud Manager 允许您为项目启用 Edge Delivery Service。

>[!TIP]
>
>有关 Edge Delivery Services 及其如何与 AEM 一起使用的详细信息，请参阅 [Edge Delivery Services 概述](/help/edge/overview.md)。

## 有关 Cloud Manager 中的 Edge Delivery Services {#edge-in-cloud-manager}

如果您已将 Edge Delivery Services 作为 Adobe Experience Manager Site 的一部分获得许可，您可以直接在 Cloud Manager 中为您的 Site 启用 Edge Delivery Services，并[通过引导式的自助服务体验快速上线](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。

此外，您可以在确保关键工作流一致性的同时，获得管理所有 AEM 属性的统一体验。这些工作流包括域名管理、SSL 证书管理以及 CDN 映射。

## 关于具有AEM创作功能的Edge Delivery Services (Beta) {#eds-aem-authoring}

>[!NOTE]
>
>此处介绍的灵活发布层和AEM创作交叉路线的功能位于Beta中。 要加入Beta，请使用您的Adobe组织ID和项目ID向[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)发送电子邮件。

现代Web体验要求高性能交付，但许多组织还依赖于现有的AEM创作工作流、治理和内容重用模式。 为了帮助您的团队在不中断创作的情况下实现交付现代化，Cloud Manager引入了可让您完成以下操作的功能：

* 使用Edge Delivery Services交付体验。
* 继续使用AEM Author创建内容。
* 仅配置您的体系结构所需的基础架构。

通过这些功能，组织可以逐步采用现代化的交付方式，而无需牺牲现有的工作流。

### Edge Delivery站点的创作选项

在Cloud Manager中创建Edge Delivery站点时，您可以选择首选的创作方法：

* 基于文档的创作 — 在Google Drive或SharePoint中创作内容。 不需要AEM环境。
* AEM创作 — 使用通用编辑器在AEM中创作内容。 此方法需要AEM创作环境。 利用此选项，在Edge Delivery处理内容交付时，不需要发布层。

组织可以在这两种方法之间进行选择，也可以根据工作流首选项逐步使用这两种方法。 查看[单击](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)即可创建您的第一个Edge Delivery网站。

### 灵活的发布层

Cloud Manager允许您配置是否为项目的环境配置了发布层。 并非所有体系结构都需要发布层，如下表所示：

| 架构 | 发布层 |
| --- | --- |
| 传统AEM Sites | 必需 |
| Headless/API优先 | 必需 |
| Edge Delivery Services | 不必需 |

通过在需要时启用发布层，团队可以更快地配置环境，简化基础架构，并减少不必要的组件。 请参阅[灵活发布层(Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)。

## 使用 Adobe 推荐的 Edge Delivery Services 路径的益处 {#recommended-path-eds}

通过 Cloud Manager 访问和使用您的 Edge Delivery Services 许可证，最大化您从 Adobe 获得的利益。这样做可以让您享受到几个关键的好处。

* [在您选择的程序上使用您的许可证](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)，或者[更新其他程序](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md)，或者两者都进行。
* 利用 [API 优先](https://developer.adobe.com/experience-cloud/experience-manager-apis/)的优势，执行 CRUD（创建、读取、更新、删除）操作。
* [访问 SLA 报告](/help/implementing/cloud-manager/reports/report-sla.md)
* 为您注册的生产程序[获取 Adobe 支持](/help/edge/overview.md#support-ticket)。

如果您拥有 Edge Delivery Services（EDS）许可证，则可为 Edge Delivery Site 使用 [Adobe 管理的 CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)。此操作将开启自助式 CDN 管理功能，并提供每三个月自动续订（除非手动删除）的 DV 证书。

或者，如果您选择使用您的 CDN（即非 Adobe 管理的 CDN），无论您的 Edge Delivery Services 许可如何，您都必须在 `aem.live` 平台上对其进行配置。请参阅 [BYO CDN 设置](https://www.aem.live/docs/byo-cdn-setup)。


## 关于将 Edge Delivery Services 添加到生产程序或沙盒程序中

根据您启动项目的方式或者当您要创建 Site 时，Edge Delivery Services 可以通过多种不同的方式添加。

| 用例 | 描述 |
| --- | --- |
| 我想将 Edge Delivery Services 添加到一个新的生产程序中。 | 请参阅[创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。<br>在向导中，选择&#x200B;**解决方案与附加组件**&#x200B;标签下的 **Edge Delivery Services**。 |
| 我想将 Edge Delivery Services 添加到一个现有的生产程序中。 | 请参阅[编辑程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。<br>在&#x200B;**编辑程序**&#x200B;对话框的&#x200B;**解决方案与附加组件**&#x200B;标签下，选择 **Edge Delivery Services**。 |
| 我想将 Edge Delivery Site 添加到 Cloud Manager 中  | 请参阅[添加 Edge Delivery Site](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)。 |
| 我现在想创建一个 Edge Delivery Site | 查看[通过单击按钮在 Cloud Manager 中快速创建 Edge Delivery Site](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)。 |
| 我想将 Edge Delivery Services 添加到一个新的或现有的沙盒程序中。 | 请参阅[创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)。<br>当您创建一个沙盒程序时，默认情况下，Edge Delivery Services 已被添加到该程序中；您无需手动选择它。<br>在 Edge Delivery 普遍可用之前，现有的沙盒程序会自动继承 Edge Delivery Services。 |
| 我想创建一个使用AEM创作的Edge Delivery站点 | 请参阅[创建Edge Delivery站点](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site)。 在将AEM创作与Edge Delivery结合使用时，发布层是可选的。 请参阅[灵活发布层(Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)。 |

>[!NOTE]
>
>* 要添加或编辑程序，您必须是&#x200B;**业务负责人**&#x200B;角色的成员，或者被赋予相应的权限。
>* 您的组织必须拥有一个未使用的 Edge Delivery Services 许可证，才能将其应用于生产程序。
>* 一旦将 Edge Delivery Services 许可证应用于某个程序或从程序中移除，更改将立即生效，无需运行管道。


## 关于 Cloud Manager 中的 Edge Delivery 待办事项列表 {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

Cloud Manager 中的 **Edge Delivery 待办事项列表**&#x200B;是一份加入任务清单，旨在引导您完成加入流程，管理您的 Edge Delivery 网站，直至[上线](/help/journey-onboarding/go-live-checklist.md)。

![Cloud Manager 中的 Edge Delivery 网站待办事项列表](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | 任务 | 描述 |
| --- | --- | --- |
| 1 | 加入产品协作渠道 | 单击&#x200B;**立即提交请求**&#x200B;向 Adobe 提交请求，为您的公司创建一个渠道。如果该渠道已经存在，您将被转到您公司的渠道。 |
| 2 | 完成前提条件 | 请参阅[查看快速入门教程](https://www.aem.live/developer/tutorial)。 |
| 3 | 添加 Edge Delivery Site 或<br>立即创建一个 Site | 请参阅[添加 Edge Delivery Site](#eds-add-site)。<br>查看[在 Cloud Manager 中创建 Edge Delivery Site](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)。 |
| 4 | 配置 Edge Delivery 网站以使用外部 Git 存储库 | 参见[配置 Edge Delivery 网站以使用外部 Git 存储库 &#x200B;](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md)。 |
| 5 | 添加域 | 请参阅[添加自定义域名称](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 |
| 6 | 添加 SSL 证书 | 请参阅[添加 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 |
| 7 | 配置 Edge Delivery Site 的内容传递网络 | 请参阅[添加域映射](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。 |
| 8 | 设置推送验证 | 请参阅[为 Edge Delivery Site 设置推送验证](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md)。 |
| 9 | 上线 | 请参阅[上线清单](https://www.aem.live/docs/go-live-checklist)。 |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## 记录支持工单 {#eds-support-ticket}

{{support-ticket}}



