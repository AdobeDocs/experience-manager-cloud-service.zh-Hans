---
title: 不同之处和新增内容 — Adobe Experience Manager作为Cloud Service
description: 不同之处和新增内容 — Adobe Experience Manager(AEM)作为Cloud Service。
exl-id: d1ce126e-960c-4367-b741-af709dd81010
source-git-commit: 42c565c8c5a3300b95a9153cb402cdb3e847f6a2
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 10%

---

# 新增功能与不同功能 {#what-is-new-and-what-is-different}

多年来，AEM一直可用于：

* On-Premise

* as a Managed Service

以前的这些方法与AEM作为Cloud Service之间存在内在差异：

* [架构](#architecture)
* [升级次数](#upgrades)
* [Cloud Manager](#cloud-manager)
* [入门](#onboarding)
* [开发](#developing)
* [操作和性能](#operations-and-performance)
* [身份管理](#identity-management)
* [创作用户界面](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>这些概述内容虽不详尽，但旨在作一介绍。

>[!NOTE]
>
>有关内部部署版和托管服务版的更多详细信息，请参阅[AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)的文档集。

## 架构 {#architecture}

>[!NOTE]
>
>有关更多详细信息，请参阅[Architecture](/help/core-concepts/architecture.md)。

AEM as a Cloud Service 现在具有：

* 具有可变数量的 AEM 图像的动态架构。

![动态架构](assets/introduction-03.png "动态架构")

此架构：

* 可根据&#x200B;*实际*&#x200B;流量和&#x200B;*实际*&#x200B;活动进行缩放。

* 各个实例仅在需要时运行。

* 使用模块化应用程序。

* 默认具有创作聚类；这可避免执行维护任务时出现停机。

此项可为不同的使用模式启用自动缩放功能：

![针对不同使用模式的自动缩放](assets/introduction-04.png "针对不同使用模式的自动缩放")


## AEM更新 {#aem-updates}

>[!NOTE]
>有关更多详细信息，请参阅[AEM版本更新](/help/implementing/deploying/aem-version-updates.md)。

AEM as aCloud Service现在使用连续集成和连续交付(CI/CD)来确保您的项目处于最新的AEM版本。 这意味着，Production和Stage实例将更新到最新的AEM版本，而不会中断用户的服务。

>[!NOTE]
> 如果对生产环境的更新失败，Cloud Manager将自动回滚暂存环境。 此操作会自动完成，以确保更新完成后，暂存环境和生产环境都位于同一AEM版本上。

AEM版本更新有两种类型：

* **AEM推送更新**

   * 可以每天发布。
   * 主要是维护，包括最新的错误修复和安全更新。

      由于更改会定期应用，因此影响会是递增的，从而减少对服务的影响。

* **新增功能更新**

   * 通过可预测的每月计划发布。

## Cloud Manager {#cloud-manager}

AdobeCloud Manager是AEM as a Analytics的连续升级方法的一部分，因为它控制着实例的所有更新 — 这是强制性的。

当有新版本的云服务可用时，可能会通过Adobe触发更新。 或者，您也可以使用Cloud Manager提供的管道触发应用程序更新。

Cloud Manager是：

* 用于管理AEM程序和环境，

* AEM作为Cloud Service的基本组成部分；首先为Cloud Manager访问配置了每个新租户，

* 您的运营和开发人员的单一入口点。

具体而言，可以从Cloud Manager创建的AEM程序的数量和类型可以派生：

* 从客户许可协议，

* 当AEM as a Cloud Service用于启用或培训时，从内部驱动型参与者

* 来自外部驱动的流程(例如，试用从Adobe.com开始)。

Cloud Manager已演变为自助门户，在该门户中，可以创建和配置AEM as aCloud Service的主要组件：

* 创建和管理新项目。 有关更多详细信息，请参阅[了解程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/understand-program-types.md)。

* 在这些程序中创建和管理AEM环境。 有关更多详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md) 。

* 创建和管理管道以将客户代码和相关配置部署到特定环境。 有关更多详细信息，请参阅[配置CI-CD管线](/help/implementing/cloud-manager/configure-pipeline.md) 。

* 会收到这些组件的重要生命周期事件通知（例如，产品更新）。

Cloud Manager在跨多个地理区域的数据中心中创建环境，从而提供全球覆盖。 CDN存在点(PoP)可确保为遍布全球的客户提供低延迟的内容交付。

>[!NOTE]
>请参阅[以Cloud Service身份访问Experience Manager](/help/onboarding/what-is-required/accessing-aem-instance.md) ，以开始使用AEM中的Cloud Manager as aCloud Service。

## 入门 {#onboarding}

>[!NOTE]
>
>有关更多详细信息，请参阅[入门](/help/onboarding/home.md)。

在使用AEM as a Cloud Service时，启动和管理AEM项目非常简单，因为Adobe需要在许多方面负责：

* 基线AEM图像针对特定用例进行了优化。

* 许多手动配置任务已变得多余。

与现在的情况相比，它也存在显着的不同：

* 评估阶段，以确保满足所有先决条件；包括：

   * 法律要求

   * 合同协议

   * 客户自定义的任何现有内容和/或代码的技术要求

* 部署要求：

   * 代码更新；任何为以前版本的AEM开发的客户应用程序都需要进行审核，并可能会进行更新。

   * 内容迁移

## 开发 {#developing}

>[!NOTE]
>
>有关更多详细信息，您可以从[开发准则](/help/implementing/developing/introduction/development-guidelines.md)和[开发 — WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)开始。

支持将AEM作为Cloud Service的新架构涉及对整体开发人员体验进行一些关键更改。 AEM as a A Services的主要目标之一是，让经验丰富的客户(在内部部署或Adobe Managed Services的上下文中使用了AEM)尽快迁移到AEM作为Cloud Service，而无需重写其大量自定义代码。 但是，可能仍需要进行一些调整。

### 云开发 {#aem-as-a-cloud-service-developing-cloud-development}

对于要在AEM as a Cloud Service上运行的现有AEM应用程序，需要执行以下步骤：

* 应用程序代码和配置必须存储在关联的Cloud Manager程序的Git代码存储库中。
* 应用程序代码和配置必须与最新版本的基线AEM图像兼容（可能每天都在更改）。
   * 必须使用与Cloud Manager环境关联的Cloud Manager管道构建和部署客户应用程序。
* 客户应用程序必须传递管道中强制实施的所有代码质量、安全性和性能门。
* 为客户应用程序构建的映像必须通过Cloud Manager管道部署。

此过程通常称为云优先开发。 由于端到端持续时间预计需要几分钟（从20到50分钟，具体取决于应用程序的复杂性），因此在云中尝试对待处理的代码和配置进行更改之前，必须采用快速开发方法。

Web控制台(管理OSGi包及其关联配置，且此前是AEM快速入门的一部分)不再作为Cloud Service环境的用户直接访问。 仍可以使用新的开发人员控制台以只读模式访问此界面。 通过此控制台，开发人员可以选择创作或发布服务的任何特定节点并直接登录，然后访问默认阻止的区域。

>[!NOTE]
>
>另请参阅[OSGi配置](/help/implementing/deploying/overview.md#osgi-configuration)

开发人员的另一个常见要求是快速访问各种环境的日志文件。 以AEM为Cloud Service，创作和发布节点中不同节点的日志文件可通过Cloud Manager使用（以可下载文件的形式提供，或通过API提供）。

由于代码和内容之间有着明确的分离，开发人员可以在部署中使用特定流程来更新内容。 可变内容的典型用例包括：

* 属于客户项目的标准&#x200B;*默认*&#x200B;内容（例如，文件夹、模板、工作流等）

* 搜索索引定义

* ACL和权限

* 服务用户和用户组

### 地方发展 {#aem-as-a-cloud-service-developing-local-development}

为了支持快速的迭代和开发，还可以在AEM之外开发AEM应用程序作为Cloud Service上下文。 为此，开发人员可以使用以下工件：

* AEM as a AnalyticsCloud Service快速入门：基于`.jar`的最新AEM代码库独立安装程序，具有相同的功能和API界面。

* AEM as a Dispatcher SDK:在本地测试和验证Dispatcher配置的基于图像的流程

>[!NOTE]
>
>应该指出，云快速入门不允许使用AEM Sites和AEM Assets的所有功能。 它包含一个简单的创作环境，在该环境中，可以开发和测试大多数扩展。

## 操作和性能 {#operations-and-performance}

>[!NOTE]
>
>有关更多详细信息，请参阅[备份](/help/operations/backup.md)、[索引](/help/operations/indexing.md)和[其他维护任务](/help/operations/maintenance.md)。

以AEM为Cloud Service，此类操作会自动执行，因此不再需要任何服务中断。

在以下方面：

* 许多任务已自动完成。

* 拓扑经过优化，可实现最大可复原性和效率；例如，默认为无二进制复制。

* 大量负载任务（如队列、作业和批量处理任务）已从核心AEM实例中移出，以便由共享和专用的微服务处理。

新的监控、报告和警报基础架构还支持AEM as a Cloud Service的操作。 这使AdobeSRE（站点可靠性工程师）能够主动保持服务的健康。 该架构的各个元素都配备了各种健康检查。 如果由于某种原因，架构的某个特定节点被认为不正常，则该节点将从服务中删除，并静默地替换为新的、正常的节点。

## 身份管理 {#identity-management}

>[!NOTE]
>
>有关更多详细信息，请参阅[安全 — IMS支持](/help/security/ims-support.md)。

对AEM as a A A Service的主要更改是完全集成地使用AdobeID访问创作层。

这需要使用[Adobe管理控制台](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)管理用户和用户组。 AdobeIdentity Management系统(IMS)中集中了用户配置文件信息，以便在所有云服务之间共享，因此用户帐户可让您访问Adobe产品和服务。 一旦分配了对AEM的访问权限，用户帐户即可在AEM中作为Cloud Service引用（如之前）；例如，用于从AEM Security用户界面定义角色和权限。

这结合了以下优势：

* 使用AdobeIdentity Management系统(IMS)在所有Adobe云应用程序中提供单点登录。

* 作为Cloud Service的AEM的每个特定实例的用户首选项仍为本地。

## 创作用户界面 {#authoring-user-interface}

>[!NOTE]
>
>有关更多详细信息，[基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)是一个很好的起点。

对于过去使用过AEM的任何人而言，站点和资产的创作用户界面(UI)的基本原则都非常熟悉。

主要区别在于，UI完全支持触控；经典UI不再可用。 否则，基础知识将保持不变，只会显着做出细微的更改。

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites as a Analytics通过将AEM内容管理系统的强大功能与AEM数字资产管理相结合，使您能够为客户提供以内容为导向的个性化体验。

有关详细信息，请参阅[对Sites](/help/sites-cloud/sites-cloud-changes.md)的更改概述。

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Analytics为企业提供了一个云原生的PaaS解决方案，不仅可以快速高效地执行其数字资产管理和Dynamic Media操作，而且还可以在始终最新、始终可用且始终学习的系统中使用下一代智能功能，如AI/ML。

资产产品包括云中的下一代资产处理以及高性能资产摄取和搜索。

有关详细信息，请参阅[概述和资产as as aCloud Service简介](/help/assets/overview.md)。

## 了解 Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

有关更多信息，请参阅：

* [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)
* Adobe Experience Manager as a Cloud Service[架构](/help/core-concepts/architecture.md)
* [对 AEM as a Cloud Service 的显著更改（发行说明）](/help/release-notes/aem-cloud-changes.md)
* [对 AEM Sites as a Cloud Service 的显著更改](/help/sites-cloud/sites-cloud-changes.md)
* [对 AEM Assets as a Cloud Service 的显著更改](/help/assets/assets-cloud-changes.md)
* [将AEM Assets作为Cloud Service介绍](/help/assets/overview.md)
* [Adobe Experience Manager as a Cloud Service 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)
