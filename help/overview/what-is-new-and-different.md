---
title: Adobe Experience Manager是Cloud Service
description: '不同和新—Adobe Experience Manager(AEM)作为Cloud Service。 '
translation-type: tm+mt
source-git-commit: 98514867fba8c998cb653abea059e15a99cbd007
workflow-type: tm+mt
source-wordcount: '1875'
ht-degree: 10%

---


# 新增功能与不同功能 {#what-is-new-and-what-is-different}

多年来，AEM一直可用于以下两方面：

* On-Premise

* 作为托管服务

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
>这些概述并非详尽无遗，但旨在介绍一下。

>[!NOTE]
>
>有关内部部署和托管服务版本的更多详细信息，请参阅AEM [6.5文档集](https://helpx.adobe.com/cn/support/experience-manager/6-5.html)。

## 架构 {#architecture}

>[!NOTE]
>
>有关更多详细信息，请 [参阅架构](/help/core-concepts/architecture.md)。

AEM 云服务现在具有：

* 具有可变数量的 AEM 图像的动态架构。

![动态架构](assets/introduction-03.png "动态架构")

此架构：

* 可根据&#x200B;*实际*&#x200B;流量和&#x200B;*实际*&#x200B;活动进行缩放。

* 各个实例仅在需要时运行。

* 使用模块化应用程序。

* 默认具有创作聚类；这可避免执行维护任务时出现停机。

此项可为不同的使用模式启用自动缩放功能：

![针对不同使用模式的自动缩放](assets/introduction-04.png "针对不同使用模式的自动缩放")


## AEM更新 {#upgrades}

>[!NOTE]
>有关更多详细信息，请 [参阅AEM版本更新](/help/implementing/deploying/aem-version-updates.md)。

AEM作为Cloud Service现在使用连续集成和连续投放(CI/CD)来确保您的项目处于最新的AEM版本。

这意味着生产实例和舞台实例将更新为最新的AEM版本，不会中断用户的服务。

>[!NOTE]
> 如果对生产环境的更新失败，Cloud Manager将自动回滚阶段环境。 这会自动完成，以确保更新完成后，阶段和生产环境都使用相同的AEM版本。

AEM版本更新有两种类型：

* **推送更新**

   * 可以每天发布。
   * 主要是维护，包括最新的错误修复和安全更新。

      由于更改会定期应用，因此影响会逐渐增加，从而减少对服务的影响。

* **新增功能更新**

   * 通过可预测的月度计划发布。

## Cloud Manager {#cloud-manager}

Adobe云管理器是AEM作为Cloud Service的持续升级方法的一个组成部分，因为它控制对您实例的所有更新——这是强制性的。

当有新版本的云服务可用时，更新可通过Adobe触发。 或者，您也可以使用Cloud Manager提供的管道触发应用程序更新。

云管理器包括：

* 用于管理AEM项目和环境,

* aem作为Cloud Service的基本组成部分；首先为每个新租户配置Cloud Manager访问权限，

* 为您的运营和开发人员提供单一入口点。

具体而言，可从云管理器创建的AEM项目的数量和类型可以派生：

* 从客户许可协议，

* 当AEM作为Cloud Service用于启用或培训时，从内部驱动型演员开始，

* 来自外部驱动的流程，如从Adobe.com开始的试用。

Cloud Manager已演变为自助门户，可在此创建和配置AEM作为Cloud Service的主要组件：

* 创建和管理新项目。 有关更多 [详细信息，请参阅了解项目](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) 和项目类型。

* 在这些项目中创建和管理AEM环境。 有关更多 [详细信息](/help/implementing/cloud-manager/manage-environments.md) ，请参阅管理环境。

* 创建并管理将客户代码和相关配置部署到特定环境的管道。 有关更 [多详细信息，请参阅配置CI-CD管道](/help/implementing/cloud-manager/configure-pipeline.md) 。

* 收到这些组件的重要生命周期事件的通知（例如，产品更新）。

目前，Cloud Manager能够在3个地理区域创建环境（下面还有更多区域）:

* 美国（东部）

* EMEA（荷兰）

* APAC（澳大利亚）

>[!NOTE]
>请参阅 [将Experience Manager作为Cloud Service访](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md) 问，以便在AEM将Cloud管理器作为Cloud Service入门。

## 入门 {#onboarding}

>[!NOTE]
>
>有关更多详细信息，请 [参阅入门](/help/onboarding/home.md)。

如果将AEM用作云服务作为Adobe负责许多方面，启动和管理AEM项目很简单：

* 基线AEM图像针对特定用例进行了优化。

* 许多手动配置任务已变得冗余。

与现在的情况也大不相同：

* 评估阶段，确保满足所有先决条件；包括，例如：

   * 法律要求

   * 合同协议

   * 对客户自定义的任何现有内容和／或代码的技术要求

* 部署要求：

   * 代码更新；任何为AEM的先前版本开发的客户应用程序都需要进行审核并可能进行更新。

   * 内容迁移

## 开发 {#developing}

>[!NOTE]
>
>有关更多详细信息，您可以 [开始开发](/help/implementing/developing/introduction/development-guidelines.md) 指 [南和开发- WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)。

支持AEM作为Cloud Service的新体系结构涉及对整体开发人员体验的一些关键更改。 AEM作为Cloud Service的主要目标之一是允许经验丰富的客户(在事先或在Adobe Managed Services的上下文中使用AEM)尽快迁移到AEM作为Cloud Service，而无需重写其大量自定义代码。 但是，可能仍需要做出一些调整。

### 云开发 {#aem-as-a-cloud-service-developing-cloud-development}

对于要在AEM上作为Cloud Service运行的现有AEM应用程序，需要执行以下步骤：

* 应用程序代码和配置必须存储在关联的Cloud Manager项目的Git代码存储库中。
* 应用程序代码和配置必须与最新版本的基准AEM映像兼容（可能每天都在更改）。
   * 必须使用与Cloud Manager环境关联的Cloud Manager管道构建和部署客户应用程序。
* 客户应用程序必须通过管道中强制实施的所有代码质量、安全性和性能门。
* 为客户应用程序构建的映像必须通过Cloud Manager管道进行部署。

此过程通常称为云优先开发。 由于端到端的持续时间预计需要几分钟（从20分钟到50分钟，具体取决于应用程序的复杂性），因此在云中尝试挂起的代码和配置更改之前，必须采用快速开发方法。

Web控制台(管理OSGI包及其关联配置，以前是AEM QuickStart的一部分)不再作为Cloud Service环境直接供AEM用户访问。 此界面仍可通过使用新的开发人员控制台以只读模式访问。 借助此控制台，开发人员可以选择创作或发布服务的任何特定节点并直接登录，然后访问默认阻止的区域。

>[!NOTE]
>
>另请参阅 [OSGi配置](/help/implementing/deploying/overview.md#osgi-configuration)

开发人员的另一个常见要求是快速访问各种环境的日志文件。 以AEM为Cloud Service，创作和发布节点中不同节点的日志文件可通过云管理器（可下载的文件形式或通过API）使用。

由于代码和内容的清晰分离，开发人员可以使用特定流程来更新内容作为部署的一部分。 可变内容的典型用例有：

* 属于 *客户* 项目的标准默认内容(例如，文件夹、模板、工作流等)

* 搜索索引定义

* ACL和权限

* 服务用户和用户组

### 本地开发 {#aem-as-a-cloud-service-developing-local-development}

为了支持快速迭代和开发，还可以在AEM之外开发AEM应用程序作为Cloud Service上下文。 为此，开发人员可以使用以下对象：

* AEM作为Cloud Service快速入门：最新 `.jar` AEM代码库的基于的独立安装程序，具有相同的功能和API界面。

* AEM作为Cloud Service调度程序SDK:在本地测试和验证调度程序配置的基于映像的过程

>[!NOTE]
>
>应该指出，云快速入门不允许所有AEM Sites和AEM Assets功能。 它包含一个简单的创作环境，在该环境中可以开发和测试大多数扩展。

## 操作和性能 {#operations-and-performance}

>[!NOTE]
>
>有关更多详细信息，请参阅[备份](/help/operations/backup.md)、[索引](/help/operations/indexing.md)和[其他维护任务](/help/operations/maintenance.md)。

以AEM为Cloud Service，此类操作可以自动执行，因此不再需要任何服务中断。

在以下方面：

* 许多任务已实现自动化。

* 拓扑优化以实现最大的恢复力和效率；例如，二进制复制是默认的。

* 重负载任务(如队列、作业和批量处理任务)已从核心AEM实例中移出，由共享和专用微服务处理。

AEM作为Cloud Service的操作还支持新的监视、报告和警报基础结构。 这使AdobeSRE（现场可靠性工程师）能够主动地保持服务的健康。 该建筑的各种元素都配备了各种健康检查。 如果由于某种原因认为体系结构的某个特定节点不健康，则从服务中删除该节点，并将其静默替换为新的、健康的节点。

## 身份管理 {#identity-management}

>[!NOTE]
>
>有关更多详细信息， [请参阅安全- IMS支持](/help/security/ims-support.md)。

对AEM作为Cloud Service的一个重大改变是完全集成地使用AdobeID访问创作层。

这需要使用Adobe [管理控制台](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 来管理用户和用户组。 用户帐户使您的用户能够访问Adobe产品和服务，因为用户档案信息集中在AdobeIdentity Management系统(IMS)中，以便在所有云服务中共享。 一旦为AEM分配了访问权限，用户帐户就可以作为Cloud Service在AEM中引用（如之前）;例如，用于从AEM Security用户界面定义角色和权限。

这综合了以下优点：

* 使用AdobeIdentity Management系统(IMS)在所有Adobe云应用程序中提供单一登录。

* 作为Cloud Service,AEM的每个特定实例的用户首选项仍为本地。

## 创作用户界面 {#authoring-user-interface}

>[!NOTE]
>
>有关更多细节， [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md) 是一个不错的起点。

对于站点和资产，创作用户界面(UI)的基本原则对于过去使用AEM的任何人来说都很熟悉。

主要区别在于UI完全支持触控；经典UI不再可用。 否则，基本内容将保持不变，只显示少量更改。

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites作为Cloud Service，通过将AEM内容管理系统的强大功能与AEM数字资产管理相结合，您可以为客户提供个性化、内容主导的体验。

有关详细信息，请参阅对 [站点的更改概述](/help/sites-cloud/sites-cloud-changes.md)。

## AEM Assets {#aem-assets}

Adobe Experience Manager资产作为Cloud Service优惠，为企业提供云本地SaaS解决方案，不仅可以快速、有效地执行数字资产管理和动态媒体操作，还可以在始终处于最新状态、始终可用且始终处于学习状态的系统中使用下一代智能功能，如AI/ML。

资产产品包括云中的下一代资产处理以及高性能的资产获取和搜索。

有关详细信息，请 [参阅概述和资产Cloud Service简介](/help/assets/overview.md)。

## 了解 Adobe Experience Manager 云服务 {#getting-to-know-aem-as-cloud-service}

有关更多信息，请参阅：

* [Adobe Experience Manager 云服务简介](/help/overview/introduction.md)
* Adobe Experience Manager 云服务[架构](/help/core-concepts/architecture.md)
* [对 AEM 云服务的显著更改（发行说明）](/help/release-notes/aem-cloud-changes.md)
* [对 AEM Sites 云服务的显著更改](/help/sites-cloud/sites-cloud-changes.md)
* [对 AEM Assets 云服务的显著更改](/help/assets/assets-cloud-changes.md)
* [将AEM Assets作为Cloud Service](/help/assets/overview.md)
* [Adobe Experience Manager 云服务教程](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)
