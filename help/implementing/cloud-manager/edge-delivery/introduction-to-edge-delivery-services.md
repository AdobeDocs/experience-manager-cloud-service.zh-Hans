---
title: Cloud Manager中的Edge Delivery Services简介
description: 了解如何使用Edge Delivery Services交付Cloud Manager项目。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 6%

---

# Cloud Manager中的Edge Delivery Services简介 {#edge-delivery-services}

Edge Delivery Services 是一组可组合的服务，通过这些服务，可非常灵活地在网站上创作内容。此功能允许您执行以下操作：

* 使用完美的Lighthouse分数创建快速站点。
* 通过RUM（实时监控）持续监控性能。
* 通过分离内容源提高创作效率。

您可以通过通用编辑器和基于文档的创作，同时使用AEM内容管理和WYSIWYG创作。

AEM as a Cloud Service中的Cloud Manager允许您为项目启用Edge Delivery服务。

>[!TIP]
>
>有关Edge Delivery Services以及如何将其用于AEM的详细信息，请参阅[Edge Delivery Services概述](/help/edge/overview.md)。

<!-- RELEASED TO GA SEPTEMBER 5, 2024
>[!NOTE]
>
>This feature is only available to [the early adopter program](/help/implementing/cloud-manager/release-notes/current.md#early-adoption). -->


## 关于Cloud Manager中的Edge Delivery Services {#edge-in-cloud-manager}

如果您已将许可Edge Delivery Services作为Adobe Experience Manager Sites的一部分，则可以直接在Cloud Manager中使用Edge Delivery Services载入您的网站，并使用引导式自助服务体验[上线](/help/implementing/cloud-manager/managing-code/private-repositories.md)。

此外，您可以访问用于管理所有AEM属性的统一体验，同时确保关键工作流之间的一致性。 这些功能包括域名管理、SSL证书管理和CDN映射。

## 将Edge Delivery Services添加到生产程序或沙盒程序

要添加或编辑程序，您必须是&#x200B;**业务负责人**&#x200B;角色的成员或拥有执行此操作所需的权限。

您的组织必须具有一个未使用的Edge Delivery Services许可证，然后才能将其应用于生产程序。

>[!NOTE]
>
>将Edge Delivery Services许可证应用于程序或从程序中删除后，更改将立即生效，而无需运行管道。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

根据您的用例，执行以下操作之一：

| 用例 | 描述 |
| --- | --- |
| 我想将Edge Delivery Services添加到新的生产程序。 | 请参阅[创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。<br>在向导的&#x200B;**解决方案和加载项**&#x200B;选项卡下，选择&#x200B;**Edge Delivery Services**。 |
| 我要将Edge Delivery Services添加到现有的生产程序。 | 请参阅[编辑程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。<br>在&#x200B;**编辑程序**&#x200B;对话框的&#x200B;**解决方案和加载项**&#x200B;选项卡下，选择&#x200B;**Edge Delivery Services**。 |
| 我要将Edge Delivery站点添加到Cloud Manager | 请参阅[添加Edge Delivery站点](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)。 |
| 我要将Edge Delivery Services添加到新的或现有的沙盒程序。 | 请参阅[创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)。<br>创建沙盒程序时，默认情况下会将Edge Delivery Services添加到该程序中；无需选择它。<br>在Edge Delivery正式发布之前存在沙盒程序，将自动继承Edge Delivery Services。 |

## 为签约客户Adobe推荐的路径 {#recommended-path-eds}

作为签约客户，请通过Cloud Manager访问和使用Edge Delivery Services许可证，确保您从Adobe中获得最大利益。 此方法允许您使用[Adobe托管CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)，并利用诸如自助CDN管理等关键优势，包括配置和添加DV证书。 此外，创建DV证书后，除非将其删除，否则Adobe会每三个月自动更新一次。 如果您没有具有Adobe的Edge Delivery Services许可证，但决定绕过这些权益，则只能使用客户管理的CDN。 此设置必须在`aem.live`平台上。

如果您已签订合同，具有AEM as a Cloud Service SitesEdge Delivery Services许可证，请登录Cloud Manager以确保能够执行以下操作：

* 使用您选择的程序上的许可证。
* 利用[API-1](https://developer.adobe.com/experience-cloud/experience-manager-apis/)的优势执行CRUD（创建、读取、更新、删除）操作。
<!-- REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+Self-service+access+to+Edge+Delivery+Services+and+Adobe+Managed+CDN * Access to license dashboard and reporting -->
* 访问SLA报告（*即将推出*） <!-- ADD LINK TO IT WHEN FINALLY ADDED -->
* 获得Adobe支持。 确保您的Edge Delivery Services站点是通过Cloud Manager中的生产程序注册的，以获得Adobe的正确识别和支持。


## 关于Edge Delivery待办事项列表 {#ed-todo-list}

**Edge Delivery待办事项列表**&#x200B;是一个入门任务核对清单，旨在指导您完成入门培训、管理Edge Delivery网站直到[上线](/help/journey-onboarding/go-live-checklist.md)。

![Edge Delivery网站待办事项列表](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|  | 任务 | 描述 |
| --- | --- | --- |
| 1 | 加入产品协作渠道 | 单击&#x200B;**立即提交请求**&#x200B;将向Adobe提交一个请求，以便为贵公司创建渠道。 如果该渠道已存在，则将您转发到公司的渠道。 |
| 2 | 完成先决条件 | 单击&#x200B;**查看入门教程**，会将您引导至[快速入门 — 开发人员教程](https://www.aem.live/developer/tutorial)。 |
| 3 | 添加Edge Delivery站点 | 请参阅[添加Edge Delivery站点](#eds-add-site)。 |
| 4 | 添加域 | 请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 |
| 5 | 添加 SSL 证书 | 请参阅[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 |
| 6 | 配置Edge Delivery站点的CDN | 请参阅[添加CDN配置](#add-cdn)。 |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

<!--
Edge Delivery Services can be enabled when adding a new production program or editing an existing one.

![Add production program with Edge Delivery Services](assets/add-production-program-with-edge.png)

For more information about adding programs, see the following:

* [Create Production programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Create Sandbox programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) -->
