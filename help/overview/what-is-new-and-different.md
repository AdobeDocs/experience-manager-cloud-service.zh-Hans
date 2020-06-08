---
title: 不同之处和新增功能- Adobe Experience Manager即云服务
description: '不同之处和新增功能- Adobe Experience Manager(AEM)即云服务。 '
translation-type: tm+mt
source-git-commit: 160db0dabc99eccdef5bd579f8ccc26a861b1380
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 7%

---


# 新增功能与不同功能 {#what-is-new-and-what-is-different}

多年来，AEM已同时提供：

* On-Premise

* 作为托管服务

以前的这些方法与AEM作为云服务存在内在差异：

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
>有关内部部署和托管服务版本的更多详细信息，请参阅AEM 6. [5文档集](https://helpx.adobe.com/cn/support/experience-manager/6-5.html)。

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


## 升级次数 {#upgrades}

>[!NOTE]
>
>有关更多详细信息，请参 [阅部署简介](/help/implementing/deploying/overview.md)。

AEM作为云服务，现在使用连续集成和连续投放(CI/CD)来确保您的项目完全处于最新状态。 这意味着所有升级操作都是完全自动化的，因此，用户无需中断任何服务。

Adobe会主动将服务的所有操作实例更新到最新版本的AEM代码库：

* 错误修复：

   * 可以每天发布。

   * 实例经常使用最新的错误修复进行更新。 由于更改会定期应用，因此影响会逐渐增加，从而减少对服务的影响。

   * 大多数更新是出于维护和安全原因。

* 新增功能：

   * 将通过可预测的月度计划发布。

>[!NOTE]
>
>有关更多详细信息，请 [参阅部署架构](/help/core-concepts/architecture.md#deployment-architecture)。

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager是AEM作为云服务的持续升级方法的一部分，因为它控制您实例的所有更新——这是强制性的。

当有新版本的云服务可用时，Adobe可以触发更新。 或者，您也可以使用Cloud Manager提供的管道触发应用程序更新。

云管理器包括：

* 用于管理AEM项目和环境,

* 作为云服务的AEM的基本组件； 首先为每个新租户配置Cloud Manager访问权限，

* 为您的运营和开发人员提供单一入口点。

具体而言，可以从云管理器创建的AEM项目的数量和类型可以派生：

* 从客户许可协议，

* 当AEM作为云服务用于启用或培训时，从内部驱动型演员开始，

* 从外部驱动的流程（如从Adobe.com开始的试用）。

Cloud Manager已演变为自助服务门户，在该门户中，可以创建和配置AEM的主要组件作为云服务：

* 创建和管理新项目。

* 在这些环境中创建和管理AEM项目。

* 创建并管理将客户代码和相关配置部署到特定环境的管道。

* 收到这些组件的重要生命周期事件的通知（例如，产品更新）。

目前，Cloud Manager能够在3个地理区域创建环境（下面还有更多区域）:

* 美国（东部）

* EMEA（荷兰）

* APAC（澳大利亚）

## 入门 {#onboarding}

>[!NOTE]
>
>有关更多详细信息，请 [参阅入门](/help/onboarding/home.md)。

在将AEM用作云服务时，启动和管理AEM项目很简单，因为Adobe负责许多方面：

* 基线AEM图像已针对特定用例进行优化。

* 许多手动配置任务已变得冗余。

与现在的情况也大不相同：

* 评估阶段，确保满足所有先决条件； 包括，例如：

   * 法律要求

   * 合同协议

   * 对客户自定义的任何现有内容和／或代码的技术要求

* 部署要求：

   * 代码更新； 需要审阅为AEM的早期版本开发的任何客户应用程序，并可能进行更新。

   * 内容迁移

## 开发 {#developing}

>[!NOTE]
>
>有关更多详细信息，您可以 [开始开发](/help/implementing/developing/introduction/development-guidelines.md) 指 [南和开发- WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)。

支持AEM作为云服务的新架构涉及对整体开发人员体验的一些关键更改。 AEM云服务的主要目标之一是允许经验丰富的客户（在预置型或Adobe Managed Services的上下文中使用过AEM）尽可能快地将AEM作为云服务迁移到AEM，而无需重写大量自定义代码。 但是，可能仍需要做出一些调整。

### 云开发 {#aem-as-a-cloud-service-developing-cloud-development}

对于要在AEM上以云服务形式运行的现有AEM应用程序，需要执行以下步骤：

* 应用程序代码和配置必须存储在关联的Cloud Manager项目的Git代码存储库中。
* 应用程序代码和配置必须与基线AEM图像的最新版本兼容（可能每天都在更改）。
   * 必须使用与Cloud Manager环境关联的Cloud Manager管道构建和部署客户应用程序。
* 客户应用程序必须通过管道中强制实施的所有代码质量、安全性和性能门。
* 为客户应用程序构建的映像必须通过Cloud Manager管道进行部署。

此过程通常称为云优先开发。 由于端到端的持续时间预计需要几分钟（从20分钟到50分钟，具体取决于应用程序的复杂性），因此在云中尝试挂起的代码和配置更改之前，必须采用快速开发方法。

AEM的用户不再可以作为云服务环境直接访问Web控制台，在该控制台中管理OSGI捆绑包及其关联的配置，以前也是AEM快速入门的一部分。 此界面仍可通过使用新的开发人员控制台以只读模式访问。 借助此控制台，开发人员可以选择创作或发布服务的任何特定节点并直接登录，然后访问默认阻止的区域。

>[!NOTE]
>
>另请参阅 [OSGi配置](/help/implementing/deploying/overview.md#osgi-configuration)

开发人员的另一个常见要求是快速访问各种环境的日志文件。 将AEM作为云服务，作者节点和发布节点中不同节点的日志文件可通过云管理器使用，形式可以是可下载的文件，也可以通过API使用。

由于代码和内容的清晰分离，开发人员可以使用特定流程来更新内容作为部署的一部分。 可变内容的典型用例有：

* 属于 *客户* 项目的标准默认内容(例如，文件夹、模板、工作流等)

* 搜索索引定义

* ACL和权限

* 服务用户和用户组

### 本地开发 {#aem-as-a-cloud-service-developing-local-development}

为了支持快速迭代和开发，还可以将AEM外的AEM应用程序作为云服务上下文进行开发。 为此，开发人员可以使用以下对象：

* AEM作为云服务快速入门： 最新 `.jar` AEM代码库的基于的独立安装程序，具有相同的功能和API界面。

* AEM作为Cloud Service Dispatcher SDK: 在本地测试和验证调度程序配置的基于映像的过程

>[!NOTE]
>
>请注意，云快速入门不允许所有AEM Sites和AEM Assets功能。 它包含一个简单的创作环境，在该环境中可以开发和测试大多数扩展。

## 操作和性能 {#operations-and-performance}

>[!NOTE]
>
>有关更多详细信息，请参阅[备份](/help/operations/backup.md)、[索引](/help/operations/indexing.md)和[其他维护任务](/help/operations/maintenance.md)。

将AEM作为云服务，这些操作将实现自动化，因此不再需要任何服务中断。

在以下方面：

* 许多任务已实现自动化。

* 拓扑优化以实现最大的恢复力和效率； 例如，二进制复制是默认的。

* 重负载任务(如队列、作业和批量处理任务)已从核心AEM实例中移出，以由共享和专用微服务处理。

新的监视、报告和警报基础架构也支持AEM云服务的操作。 这使Adobe SRE（站点可靠性工程师）能够主动保持服务的健康。 该建筑的各种元素都配备了各种健康检查。 如果由于某种原因认为体系结构的某个特定节点不健康，则从服务中删除该节点，并将其静默替换为新的、健康的节点。

## 身份管理 {#identity-management}

>[!NOTE]
>
>有关更多详细信息， [请参阅安全- IMS支持](/help/security/ims-support.md)。

对AEM作为云服务的一个重大更改是完全集成地使用Adobe ID访问创作层。

这需要使用Adobe [Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 来管理用户和用户组。 用户帐户使您的用户能够访问Adobe产品和服务，因为用户用户档案信息集中在Adobe身份管理系统(IMS)中，以便在所有云服务中共享。 在为AEM分配访问权限后，用户帐户可在AEM中作为云服务进行引用（如之前）; 例如，用于从AEM Security用户界面定义角色和权限。

这综合了以下优点：

* 使用Adobe Identity Management System(IMS)在所有Adobe云应用程序中提供单一登录。

* 作为云服务，AEM的每个特定实例的用户首选项仍为本地。

## 创作用户界面 {#authoring-user-interface}

>[!NOTE]
>
>有关更多细节， [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md) 是一个不错的起点。

对于过去使用过AEM的任何人，站点和资产的创作用户界面(UI)的基本原则都很熟悉。

主要区别在于UI完全支持触控； 经典UI不再可用。 否则，基本内容将保持不变，只显示少量更改。

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites作为云服务，通过将AEM内容管理系统的强大功能与AEM数字资产管理相结合，您可以为客户提供个性化的内容导向体验。

有关详细信息，请参阅对 [站点的更改概述](/help/sites-cloud/sites-cloud-changes.md)。

## AEM Assets {#aem-assets}

Adobe Experience Manager资产作为云服务，为企业优惠一种云本地SaaS解决方案，不仅可以快速、有影响地执行其数字资产管理和动态媒体操作，还可以在始终处于最新状态、始终可用且始终处于学习状态的系统中使用新一代智能功能，如AI/ML。

资产产品包括云中的下一代资产处理以及高性能的资产获取和搜索。

有关详细信息， [请参阅概述和资产（即云服务）的介绍](/help/assets/overview.md)。
