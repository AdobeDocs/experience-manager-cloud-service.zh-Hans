---
title: Cloud Manager 中的 Edge Delivery Services 简介
description: 了解如何使用 Edge Delivery Services 传递您的 Cloud Manager 项目。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0fb5476b4cff9e26971696bd8352181a71e7b3e4
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 89%

---


# Cloud Manager 中的 Edge Delivery Services 简介 {#edge-delivery-services}

Edge Delivery Services 是一组可组合的服务，使您在网站上创作内容时具有高度的灵活性。此功能允许您执行以下操作：

* 创建拥有完美灯塔评分的快速网站。
* 通过 RUM（实时使用监测）持续监测性能。
* 通过分离内容源来提高创作效率。

您可以使用通用编辑器和基于文档的创作来使用 AEM 内容管理和所见即所得创作。

AEM as a Cloud Service 中的 Cloud Manager 允许您为项目启用 Edge Delivery Service。

>[!TIP]
>
>有关 Edge Delivery Services 及其如何与 AEM 一起使用的详细信息，请参阅 [Edge Delivery Services 概述](/help/edge/overview.md)。

## 有关 Cloud Manager 中的 Edge Delivery Services {#edge-in-cloud-manager}

如果您已将 Edge Delivery Services 作为 Adobe Experience Manager Sites 的一部分获得许可，您可以直接在 Cloud Manager 中为您的网站启用 Edge Delivery Services，并[通过引导式的自助服务体验快速上线](/help/implementing/cloud-manager/managing-code/private-repositories.md)。

此外，您可以在确保关键工作流程一致性的同时，获得管理所有 AEM 属性的统一体验。这些工作流包括域名管理、SSL证书管理和CDN映射。

## 使用 Adobe 推荐的 Edge Delivery Services 路径的益处 {#recommended-path-eds}

通过 Cloud Manager 访问和使用您的 Edge Delivery Services 许可证，最大化您从 Adobe 获得的利益。这样做可以让您享受到几个关键的好处。

* [在您选择的程序上使用您的许可证](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)，或者[更新其他程序](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md)，或者两者都进行。
* 利用 [API 优先](https://developer.adobe.com/experience-cloud/experience-manager-apis/)的优势，执行 CRUD（创建、读取、更新、删除）操作。
* [访问 SLA 报告](/help/implementing/cloud-manager/sla-reporting.md)（*即将推出*）
* 为您注册的生产程序[获取 Adobe 支持](/help/edge/overview.md#support-ticket)。

此外，使用 Cloud Manager 可以让您为您的 Edge Delivery 网站使用 [Adobe 托管的内容传递网络](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)，并享受自助式内容传递网络管理（包括配置和添加 DV 证书）等关键优势。此外，在创建 DV 证书后，Adobe 会每三个月自动续期一次，除非该证书被删除。如果您没有 Adobe 的 Edge Delivery Services 许可证，并决定放弃这些优势，那么您只能使用您自己的自托管内容传递网络。此设置必须位于 [`aem.live` 平台](https://www.aem.live/docs/go-live-checklist#cdn-configuration)上。

## 关于将 Edge Delivery Services 添加到生产程序或沙盒程序中

根据您启动项目的方式，Edge Delivery Services 可以通过多种不同的方式添加。

| 用例 | 描述 |
| --- | --- |
| 我想将 Edge Delivery Services 添加到一个新的生产程序中。 | 请参阅[创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。<br>在向导中，选择&#x200B;**解决方案与附加组件**&#x200B;标签下的 **Edge Delivery Services**。 |
| 我想将 Edge Delivery Services 添加到一个现有的生产程序中。 | 请参阅[编辑程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。<br>在&#x200B;**编辑程序**&#x200B;对话框的&#x200B;**解决方案与附加组件**&#x200B;标签下，选择 **Edge Delivery Services**。 |
| 我想在 Cloud Manager 中添加一个 Edge Delivery 网站 | 请参阅[添加 Edge Delivery 网站](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)。 |
| 我想将 Edge Delivery Services 添加到一个新的或现有的沙盒程序中。 | 请参阅[创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)。<br>当您创建一个沙盒程序时，默认情况下，Edge Delivery Services 已被添加到该程序中；您无需手动选择它。<br>在 Edge Delivery 普遍可用之前，现有的沙盒程序会自动继承 Edge Delivery Services。 |

>[!NOTE]
>
>* 要添加或编辑程序，您必须是&#x200B;**业务负责人**&#x200B;角色的成员，或者被赋予相应的权限。
>* 您的组织必须拥有一个未使用的 Edge Delivery Services 许可证，才能将其应用于生产程序。
>* 一旦将 Edge Delivery Services 许可证应用于某个程序或从程序中移除，更改将立即生效，无需运行管道。


## 关于Cloud Manager中的Edge Delivery待办事项列表 {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

Cloud Manager中的&#x200B;**Edge Delivery待办事项列表**&#x200B;是一个入门任务核对清单，旨在指导您完成入门培训、管理Edge Delivery网站直到[上线](/help/journey-onboarding/go-live-checklist.md)。

Cloud Manager中的![Edge Delivery网站待办事项列表](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | 任务 | 描述 |
| --- | --- | --- |
| 1 | 加入产品协作渠道 | 点击&#x200B;**立即提交请求**&#x200B;向 Adobe 提交请求，为您的公司创建一个渠道。如果该渠道已经存在，您将被转到您公司的渠道。 |
| 2 | 完成先决条件 | 请参阅[查看入门教程](https://www.aem.live/developer/tutorial)。 |
| 3 | 添加 Edge Delivery 网站 | 请参阅[添加 Edge Delivery 网站](#eds-add-site)。 |
| 4 | 添加域 | 请参阅[添加自定义域名称](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 |
| 5 | 添加 SSL 证书 | 请参阅[添加 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 |
| 6 | 配置 Edge Delivery 网站的内容传递网络 | 请参阅[添加 CDN 配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。 |
| 7 | 设置推送验证 | 请参阅[为Edge Delivery站点设置推送验证](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md)。 |
| 8 | 上线 | 查看[上线清单](/help/edge/docs/go-live-checklist.md)。 |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## 记录支持工单 {#eds-support-ticket}

{{support-ticket}}



