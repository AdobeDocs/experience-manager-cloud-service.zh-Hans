---
title: What is Different and What is New - Adobe Experience Manager作为Cloud Service
description: 'What is Different and What is New - Adobe Experience Manager(AEM)作为Cloud Service。 '
translation-type: tm+mt
source-git-commit: d2786f51edcb84e3d206c400e4faaecb46a54981
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 10%

---


# 新增功能与不同功能 {#what-is-new-and-what-is-different}

多年来，AEM已同时提供：

* On-Premise

* 作为托管服务

以前的这些方法与AEM作为Cloud Service存在内在差异：

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
>这些概述并非详尽无遗，但旨在介绍一下。

>[!NOTE]
>
>有关内部部署和托管服务版本的更多详细信息，请参阅[AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html)的文档集。

## 架构 {#architecture}

>[!NOTE]
>
>有关更多详细信息，请参阅[架构](/help/core-concepts/architecture.md)。

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


## AEM更新{#aem-updates}

>[!NOTE]
>有关详细信息，请参阅[AEM版本更新](/help/implementing/deploying/aem-version-updates.md)。

AEM作为Cloud Service，现在使用“持续集成”和“持续投放”(CI/CD)来确保您的项目处于最新的AEM版本。 这意味着生产实例和舞台实例将更新为最新的AEM版本，而不会中断用户的服务。

>[!NOTE]
> 如果对生产环境的更新失败，Cloud Manager将自动回滚舞台环境。 这是自动完成的，以确保更新完成后，阶段和生产环境都使用相同的AEM版本。

AEM版本更新有两种类型：

* **AEM推送更新**

   * 可以每天发布。
   * 主要是维护，包括最新的错误修复和安全更新。

      由于会定期应用更改，因此影响会逐渐增加，从而减少对服务的影响。

* **新增功能更新**

   * 通过可预测的月度计划发布。

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager是AEM作为Cloud Service的持续升级方法的一部分，因为它控制了您实例的所有更新 — 这是强制性的。

当有新版本的云服务可用时，可通过Adobe触发更新。 或者，您也可以使用Cloud Manager提供的管道触发应用程序更新。

云管理器是：

* 用于管理AEM项目和环境,

* 作为AEM的重要组成部分；每个新租户首先为Cloud Manager访问设置

* 为您的运营和开发人员提供单一入口点。

具体而言，可以从云管理器创建的AEM项目的数量和类型可以派生：

* 从客户许可协议，

* 当AEM用作Cloud Service用于启用或培训时，

* 来自外部驱动的流程，如从Adobe.com开始的试用。

Cloud Manager已发展成为自助门户，可在此创建和配置AEM作为Cloud Service的主要组件：

* 创建和管理新项目。 有关详细信息，请参阅[了解项目和项目类型](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md)。

* 在这些项目中创建和管理AEM环境。 有关详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md)。

* 创建并管理将客户代码和相关配置部署到特定环境的管道。 有关详细信息，请参阅[配置CI-CD管道](/help/implementing/cloud-manager/configure-pipeline.md)。

* 获得有关这些组件的重要生命周期事件的通知（例如，产品更新）。

Cloud Manager可跨多个地理区域在数据中心创建环境，提供全球覆盖。 CDN存在点(PoP)确保为遍布全球的客户提供低延迟内容投放。

>[!NOTE]
>请参阅[将Experience Manager作为Cloud Service](/help/onboarding/what-is-required/accessing-aem-instance.md)访问，以开始将AEM中的Cloud Manager作为Cloud Service。

## 入门 {#onboarding}

>[!NOTE]
>
>有关详细信息，请参阅[入门](/help/onboarding/home.md)。

在将AEM用作云服务时，启动和管理AEM项目非常简单，因为Adobe负责许多方面：

* 基线AEM图像针对特定用例进行了优化。

* 许多手动配置任务已变得冗余。

与现在的情况相比，情况也明显不同：

* 一个评估阶段，以确保满足所有先决条件；包括，例如：

   * 法律要求

   * 合同协议

   * 客户自定义的任何现有内容和/或代码的技术要求

* 部署要求：

   * 代码更新；任何为AEM的早期版本开发的客户应用程序都需要进行审阅并可能进行更新。

   * 内容迁移

## 开发 {#developing}

>[!NOTE]
>
>有关更多详细信息，您可以使用[开发指南](/help/implementing/developing/introduction/development-guidelines.md)和[开发 — WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)进行开始。

支持AEM作为Cloud Service的新架构涉及对整体开发人员体验的一些关键更改。 AEM作为Cloud Service的主要目标之一是允许经验丰富的客户(在事先或在Adobe Managed Services的上下文中使用了AEM)尽可能快速迁移到AEM作为Cloud Service，而无需重写其大量自定义代码。 然而，可能仍需作一些调整。

### 云开发{#aem-as-a-cloud-service-developing-cloud-development}

要使现有的AEM应用程序作为Cloud Service在AEM上运行，需要执行以下步骤：

* 应用程序代码和配置必须存储在关联的Cloud Manager项目的Git代码存储库中。
* 应用程序代码和配置必须与最新版本的基线AEM图像兼容（可能每天都在更改）。
   * 必须使用与Cloud Manager环境关联的Cloud Manager渠道构建和部署客户应用程序。
* 客户应用程序必须通过管道中强制实施的所有代码质量、安全性和性能门。
* 为客户应用程序构建的映像必须通过Cloud Manager渠道进行部署。

此过程通常称为云优先开发。 由于端到端的持续时间预计需要几分钟（从20到50，具体取决于应用程序的复杂性），因此在尝试在云中更改挂起的代码和配置之前，必须采用快速开发方法。

Web控制台中管理OSGI包及其关联配置，而且之前是AEM QuickStart的一部分，因此AEM的用户不再作为Cloud Service环境直接访问它。 此界面仍可通过使用新的开发人员控制台以只读模式访问。 借助此控制台，开发人员可以选择创作或发布服务的任何特定节点并直接登录，然后访问默认阻止的区域。

>[!NOTE]
>
>另请参阅[OSGi Configuration](/help/implementing/deploying/overview.md#osgi-configuration)

开发人员的另一个常见要求是快速访问各种环境的日志文件。 以AEM为Cloud Service，创作和发布节点中不同节点的日志文件可通过云管理器使用，其形式可以是可下载的文件，也可以是通过API。

由于代码和内容的清晰分离，开发人员可以使用特定流程在部署过程中更新内容。 可变内容的典型用例有：

* 作为客户项目一部分的标准&#x200B;*默认*&#x200B;内容(例如，文件夹、模板、工作流等)

* 搜索索引定义

* ACL和权限

* 服务用户和用户组

### 本地开发{#aem-as-a-cloud-service-developing-local-development}

为了支持快速迭代和开发，还可以在AEM外部开发AEM应用程序作为Cloud Service上下文。 为此，开发人员可以使用以下对象：

* AEM作为Cloud Service快速入门：基于`.jar`、最新AEM代码库的独立安装程序，具有相同的功能和API界面。

* AEM作为Cloud Service Dispatcher SDK:在本地测试和验证调度程序配置的基于映像的过程

>[!NOTE]
>
>应当注意的是，云快速入门不支持所有AEM Sites和AEM Assets功能。 它包含一个简单的作者环境，可在其中开发和测试大多数扩展。

## 操作和性能{#operations-and-performance}

>[!NOTE]
>
>有关更多详细信息，请参阅[备份](/help/operations/backup.md)、[索引](/help/operations/indexing.md)和[其他维护任务](/help/operations/maintenance.md)。

以AEM为Cloud Service，这些操作是自动的，因此不再需要任何服务中断。

在这些领域：

* 许多任务已自动化。

* 拓扑优化以实现最大的恢复力和效率；例如，无二进制复制是默认值。

* 大负载任务(如队列、作业和批量处理任务)已从核心AEM实例中移出，由共享和专用微服务处理。

AEM作为Cloud Service的操作还支持新的监视、报告和警报基础结构。 这使AdobeSRE（站点可靠性工程师）能够主动保持服务的健康。 该建筑的各种元素都配备了各种健康检查。 如果由于某种原因认为体系结构的特定节点不健康，则从服务中删除该节点，并静默地替换为新的、健康的节点。

## 身份管理 {#identity-management}

>[!NOTE]
>
>有关详细信息，请参阅[安全 — IMS支持](/help/security/ims-support.md)。

对AEM作为Cloud Service的一个重大改变是完全集成地使用Adobe ID访问创作层。

这需要使用[Adobe管理控制台](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)管理用户和用户组。 用户帐户使您的用户能够访问Adobe产品和服务，因为用户用户档案信息集中在Adobe Identity Management系统(IMS)中，以便在所有云服务中共享。 一旦分配了对AEM的访问权限，用户帐户就可以作为Cloud Service在AEM中引用（如之前）；例如，用于从AEM Security用户界面定义角色和权限。

这结合了以下优势：

* 使用Adobe Identity Management系统(IMS)在所有Adobe云应用程序中提供单点登录。

* 作为Cloud Service,AEM的每个特定实例的用户首选项仍为本地。

## 创作用户界面{#authoring-user-interface}

>[!NOTE]
>
>有关更多详细信息，[基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)是一个不错的起点。

对于站点和资产，创作用户界面(UI)的基本原则对于过去使用过AEM的任何人来说都很熟悉。

主要区别在于UI完全支持触控；经典UI不再可用。 否则，基本内容将保持不变，只显示少量更改。

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites作为一个Cloud Service，通过将AEM 内容管理系统的强大功能与AEM数字资产管理相结合，使您能够为客户提供个性化的内容导向体验。

有关详细信息，请参阅[对站点](/help/sites-cloud/sites-cloud-changes.md)的更改概述。

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets作为一款Cloud Service优惠，为企业提供了云本地PaaS解决方案，不仅可以快速、有效地执行其数字资产管理和Dynamic Media操作，还可以在始终最新、始终可用和始终学习的系统中使用下一代智能功能，如AI/ML。

资产产品包括云中的下一代资产处理以及高性能资产获取和搜索。

有关详细信息，请参阅[概述和资产作为Cloud Service的介绍](/help/assets/overview.md)。

## 了解 Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

有关更多信息，请参阅：

* [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)
* Adobe Experience Manager as a Cloud Service[架构](/help/core-concepts/architecture.md)
* [对 AEM as a Cloud Service 的显著更改（发行说明）](/help/release-notes/aem-cloud-changes.md)
* [对 AEM Sites as a Cloud Service 的显著更改](/help/sites-cloud/sites-cloud-changes.md)
* [对 AEM Assets as a Cloud Service 的显著更改](/help/assets/assets-cloud-changes.md)
* [将AEM Assets作为Cloud Service](/help/assets/overview.md)
* [Adobe Experience Manager as a Cloud Service 教程](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)
