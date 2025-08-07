---
title: Cloud Manager 中的 Edge Delivery Services 简介
description: 了解如何使用 Edge Delivery Services 传递您的 Cloud Manager 项目。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 040c8af18353cbcb9242570e6bb3bac73928e2fa
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 97%

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

## 使用 Adobe 推荐的 Edge Delivery Services 路径的益处 {#recommended-path-eds}

通过 Cloud Manager 访问和使用您的 Edge Delivery Services 许可证，最大化您从 Adobe 获得的利益。这样做可以让您享受到几个关键的好处。

* [在您选择的程序上使用您的许可证](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)，或者[更新其他程序](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md)，或者两者都进行。
* 利用 [API 优先](https://developer.adobe.com/experience-cloud/experience-manager-apis/)的优势，执行 CRUD（创建、读取、更新、删除）操作。
* [访问 SLA 报告](/help/implementing/cloud-manager/sla-reporting.md)（*即将推出*）
* 为您注册的生产程序[获取 Adobe 支持](/help/edge/overview.md#support-ticket)。

如果您拥有 Edge Delivery Services（EDS）许可证，则可以为您的 Edge Delivery Site 使用 [Adobe 管理的 CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)，并利用自助 CDN 管理和每三个月自动续订 DV 证书（除非删除）等功能。

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

>[!NOTE]
>
>* 要添加或编辑程序，您必须是&#x200B;**业务负责人**&#x200B;角色的成员，或者被赋予相应的权限。
>* 您的组织必须拥有一个未使用的 Edge Delivery Services 许可证，才能将其应用于生产程序。
>* 一旦将 Edge Delivery Services 许可证应用于某个程序或从程序中移除，更改将立即生效，无需运行管道。


## 关于 Cloud Manager 中的 Edge Delivery 待办事项列表 {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

Cloud Manager 中的 **Edge Delivery 待办事项列表**&#x200B;是一份加入任务清单，旨在引导您完成加入流程，管理您的 Edge Delivery Site，直至[上线](/help/journey-onboarding/go-live-checklist.md)。

![Cloud Manager 中的 Edge Delivery Site 待办事项列表](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)。

|   | 任务 | 描述 |
| --- | --- | --- |
| 1 | 加入产品协作渠道 | 单击&#x200B;**立即提交请求**&#x200B;向 Adobe 提交请求，为您的公司创建一个渠道。如果该渠道已经存在，您将被转到您公司的渠道。 |
| 2 | 完成前提条件 | 请参阅[查看快速入门教程](https://www.aem.live/developer/tutorial)。 |
| 3 | 添加 Edge Delivery Site 或<br>立即创建 Site | 请参阅[添加 Edge Delivery Site](#eds-add-site)。<br>查看[在 Cloud Manager 中创建 Edge Delivery Site](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)。 |
| 4 | 配置Edge Delivery站点以使用外部Git存储库 | 请参阅[将Edge Delivery站点配置为使用外部Git存储库](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md)。 |
| 5 | 添加域 | 请参阅[添加自定义域名称](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 |
| 6 | 添加 SSL 证书 | 请参阅[添加 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 |
| 7 | 配置 Edge Delivery Site 的内容传递网络 | 请参阅[添加域映射](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。 |
| 8 | 设置推送验证 | 请参阅[为 Edge Delivery Site 设置推送验证](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md)。 |
| 9 | 上线 | 请参阅[上线清单](/help/edge/docs/go-live-checklist.md)。 |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## 记录支持工单 {#eds-support-ticket}

{{support-ticket}}



