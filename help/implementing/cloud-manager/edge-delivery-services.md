---
title: Cloud Manager 中的 Edge Delivery Services 支持
description: 了解如何使用Edge Delivery Services交付Cloud Manager项目。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: dda5444ccfced079125c358f65f0dae43293ae55
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 5%

---

# Cloud Manager 中的 Edge Delivery Services 支持 {#edge-delivery-services}

了解如何使用您的Edge Delivery Services许可证来创建Edge Delivery Services站点。

<!-- RELEASED TO GA SEPTEMBER 5, 2024
>[!NOTE]
>
>This feature is only available to [the early adopter program](/help/implementing/cloud-manager/release-notes/current.md#early-adoption). -->

## 简要Edge Delivery Services {#edge-overview}

Edge Delivery Services 是一组可组合的服务，通过这些服务，可非常灵活地在网站上创作内容。此功能允许您执行以下操作：

* 使用完美的Lighthouse分数创建快速站点。
* 通过RUM（实时监控）持续监控性能。
* 通过分离内容源提高创作效率。

您可以通过通用编辑器和基于文档的创作，同时使用AEM内容管理和WYSIWYG创作。

AEM as a Cloud Service中的Cloud Manager允许您为项目启用Edge Delivery服务。

>[!TIP]
>
>有关Edge Delivery Services以及如何将其用于AEM的详细信息，请参阅文档[Edge Delivery Services概述](/help/edge/overview.md)。

## Cloud Manager中的Edge Delivery Services {#edge-in-cloud-manager}

如果您已将许可Edge Delivery Services作为Adobe Experience Manager Sites的一部分，则可以直接在Cloud Manager中使用Edge Delivery Services载入您的网站，并使用引导式自助服务体验[上线](/help/implementing/cloud-manager/managing-code/private-repositories.md)。

此外，您可以访问用于管理所有AEM属性的统一体验，同时确保关键工作流之间的一致性。 这些功能包括域名管理、SSL证书管理和CDN映射。

## 将Edge Delivery Services添加到生产或沙盒程序

要添加或编辑程序，您必须是&#x200B;**业务负责人**角色的成员或拥有执行此操作所需的权限。
您的组织必须具有一个未使用的Edge Delivery Services许可证，然后才能将其应用于生产程序。

>[!NOTE]
>
>将Edge Delivery Services许可证应用于程序或从程序中删除后，更改将立即生效，而无需运行管道。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

根据您的用例，执行以下操作之一：

| 用例 | 描述 |
| --- | --- |
| 我想将Edge Delivery Services添加到新的生产程序。 | 请参阅[创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。<br>在向导的&#x200B;**解决方案和加载项**&#x200B;选项卡下，选择&#x200B;**Edge Delivery Services**。 |
| 我要将Edge Delivery Services添加到现有的生产程序。 | 请参阅[编辑程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。<br>在&#x200B;**编辑程序**&#x200B;对话框的&#x200B;**解决方案和加载项**&#x200B;选项卡下，选择&#x200B;**Edge Delivery Services**。 |
| 我要将Edge Delivery Services添加到新的或现有的沙盒程序。 | 请参阅[创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)。<br>创建沙盒程序时，默认情况下会将Edge Delivery Services添加到该程序中；无需选择它。<br>现有沙盒程序自动继承Edge Delivery Services。 |

## 为签约客户Adobe推荐的路径 {#recommended-path-eds}

作为签约客户，请通过Cloud Manager访问和使用Edge Delivery Services许可证，确保您从Adobe中获得最大利益。 此方法允许您使用[Adobe托管CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)，并利用自助服务CDN管理等关键优势，包括DV或EV/OV证书的配置和安装。 如果您没有具有Adobe的Edge Delivery Services许可证，但决定绕过这些权益，则只能使用客户管理的CDN。 此设置必须在aem.live平台上。

如果您已签订合同，具有AEM as a Cloud Service SitesEdge Delivery Services许可证，请登录Cloud Manager以确保能够执行以下操作：

* 使用您选择的程序上的许可证。
* 利用[API-1](https://developer.adobe.com/experience-cloud/experience-manager-apis/)的优势执行CRUD（创建、读取、更新、删除）操作。
<!-- REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+Self-service+access+to+Edge+Delivery+Services+and+Adobe+Managed+CDN * Access to license dashboard and reporting -->
* 访问SLA报告（*即将推出*） <!-- ADD LINK TO IT WHEN FINALLY ADDED -->
* 获得Adobe支持。 确保您的Edge Delivery Services站点是通过Cloud Manager中的生产程序注册的，以获得Adobe的正确识别和支持。

## 添加Edge Delivery站点 {#eds-add-site}

将Edge Delivery Services添加到生产程序后，您的Edge Delivery Services许可证将应用于该程序。

“概述”页面上显示名为&#x200B;**Edge Delivery**&#x200B;的可单击选项卡。 单击选项卡会显示一个表格，其中列出了您已添加的每个Edge Delivery站点。 在左侧导航面板的&#x200B;**服务**&#x200B;分组下，注意名为&#x200B;**Edge Delivery Sites**&#x200B;的菜单选项。

![概述页面在左侧导航面板中显示Edge Delivery Sites，并在“Publish交付”选项卡右侧显示Edge Delivery选项卡](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**添加Edge Delivery站点：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择适当的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择已配置Edge Delivery Services的程序，并从中添加Edge Delivery站点。
1. 执行以下任一操作：
   * 从&#x200B;**项目概述**&#x200B;页面，单击&#x200B;**Edge Delivery**&#x200B;选项卡。 然后，在页面的右下角附近，单击&#x200B;**添加Edge Delivery站点**。

     ![从Edge Delivery选项卡添加Edge Delivery站点](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     **Edge Delivery待办事项列表**&#x200B;是可选的入门清单指南，旨在帮助您开始使用Edge Delivery，如上图所示。 请参阅[关于Edge Delivery待办事项列表](#ed-todo-list)。

   * 在页面的左上角，单击汉堡图标以显示左侧导航菜单。 在&#x200B;**服务**&#x200B;标题下，单击&#x200B;**Edge Delivery站点**。 在页面的右上角附近，单击&#x200B;**添加站点**。

     ![从Edge Delivery站点添加Edge Delivery站点按钮](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. 在&#x200B;**添加Edge Delivery站点**&#x200B;对话框中，执行以下操作：

   | 文本字段 | 要做什么 |
   | --- | --- |
   | 站点名称 | 输入要添加的Edge Delivery站点的名称。 该名称将用作Cloud Manager中站点的唯一标识符。 |
   | 存储库 URL | 此字段是指存储网站代码的Git存储库。<br>输入Git存储库的URL，该URL包含您的Edge Delivery站点所需的文件和资源(例如HTML、CSS、JavaScript和其他Web资源)。 这种安排允许Cloud Manager在部署过程中从该存储库中提取代码。 |
   | 网站描述（可选） | 输入要添加的Edge Delivery站点的简短说明。<br>此描述有助于识别和区分站点，使管理和识别您添加的其他站点更加容易。 您可能希望包括有关站点用途、内容的详细信息，或任何其他有助于阐明其功能或范围的相关信息。 |

1. 单击对话框右下角的&#x200B;**添加**。

1. 在&#x200B;**验证存储库所有权**&#x200B;对话框中，执行以下任一操作：

   | 步骤 | 描述 |
   | --- | --- |
   | 1 | 添加文件，该文件具有在&#x200B;**存储库URL**&#x200B;字段中列出的Git存储库的`main`分支的位置路径。 如有必要，请单击复制图标以将路径复制到剪贴板。<br>位置路径为：<br>`well-known/adobe/cloudmanager-challenge.txt`。<br><br>请&#x200B;*不*&#x200B;添加位置路径开头的句点，位于：<br>`.well-known/adobe/cloudmanager-challenge.txt` |
   | 2 | 将生成的代码添加到您在步骤1中创建的文件中。 如有必要，请单击复制图标以将代码复制到剪贴板。 |
   | 3 | 在Git存储库中，创建拉取请求，然后将其合并以提交代码。 |

1. 单击&#x200B;**验证**。 验证存储库后，其在Edge交付站点表格中的状态将更改为绿色圆圈，并在其内部显示白色复选标记。

## 关于Edge Delivery待办事项列表 {#ed-todo-list}

**Edge Delivery待办事项列表**&#x200B;是一个入门任务核对清单，旨在指导您完成入门培训、管理Edge Delivery网站直到[上线](/help/journey-onboarding/go-live-checklist.md)。

|  | 任务 | 描述 |
| --- | --- | --- |
| 1 | 加入产品协作渠道 | 单击&#x200B;**立即提交请求**&#x200B;将向Adobe提交一个请求，以便为贵公司创建渠道。 如果该渠道已存在，则将您转发到公司的渠道。 |
| 2 | 完成先决条件 | 单击&#x200B;**查看入门教程**，会将您引导至[快速入门 — 开发人员教程](https://www.aem.live/developer/tutorial)。 |
| 3 | 添加Edge Delivery站点 | 请参阅[添加Edge Delivery站点](#eds-add-site)。 |
| 4 | 添加域 | 请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 |
| 5 | 添加 SSL 证书 | 请参阅[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 |
| 6 | 配置Edge Delivery站点的CDN | 请参阅[添加CDN配置](#add-cdn)。 |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## 将CDN配置添加到您的Edge Delivery站点 {#add-cdn}

请参阅[添加CDN配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。

## 删除Edge Delivery站点 {#eds-site-delete}

>[!IMPORTANT]
>
>如果删除Edge Delivery Services站点，则任何关联的CDN配置也会被删除。 此操作中断自定义域与站点之间的连接。 有关详细信息，请参阅CDN配置。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**删除Edge Delivery站点：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择适当的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择已配置Edge Delivery Services的程序，并从中添加Edge Delivery站点。
1. 执行以下任一操作：
   * 从&#x200B;**项目概述**&#x200B;页面，单击&#x200B;**Edge Delivery**&#x200B;选项卡。 在Edge Delivery站点表中，单击要删除其站点的行末尾的省略号。 单击“**删除**”，然后再次单击“**删除**”以确认移除网站。

     ![从Edge Delivery选项卡添加Edge Delivery站点](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * 在页面的左上角，单击汉堡图标以显示左侧导航菜单。 在&#x200B;**服务**&#x200B;标题下，单击&#x200B;**Edge Delivery站点**。 在Edge Delivery站点表中，单击要删除其站点的行末尾的省略号。 单击“**删除**”，然后再次单击“**删除**”以确认移除网站。


     ![从Edge Delivery站点添加Edge Delivery站点按钮](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)


<!--
Edge Delivery Services can be enabled when adding a new production program or editing an existing one.

![Add production program with Edge Delivery Services](assets/add-production-program-with-edge.png)

For more information about adding programs, see the following:

* [Create Production programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Create Sandbox programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) -->
