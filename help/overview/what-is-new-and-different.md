---
title: 不同功能与新增功能 – Adobe Experience Manager as a Cloud Service
description: 不同功能与新增功能 – Adobe Experience Manager (AEM) as a Cloud Service。
exl-id: d1ce126e-960c-4367-b741-af709dd81010
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: ht
source-wordcount: '1904'
ht-degree: 100%

---

# 新增功能与不同功能 {#what-is-new-and-what-is-different}

多年来，AEM 提供有两种版本：

* 内部部署

* 作为托管服务

以前的这些方法与 AEM as a Cloud Service 存在本质上的区别：

* [架构](#architecture)
* [升级](#upgrades)
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
>这些概述并未说明全部内容，而是用于提供一个介绍。

>[!NOTE]
>
>有关内部部署和托管服务版本的详细信息，请参阅 [AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans) 的文档集。

## 架构 {#architecture}

>[!NOTE]
>
>有关详细信息，请参阅[架构](/help/overview/architecture.md)。

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


## AEM 更新 {#aem-updates}

>[!NOTE]
>有关详细信息，请参阅 [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)。

AEM as a Cloud Service 现在使用连续集成和连续投放 (CI/CD)，以确保您的项目使用的是最新的 AEM 版本。这意味着生产实例和暂存实例均会更新到最新 AEM 版本而无需中断用户的服务。

>[!NOTE]
> 如果对生产环境的更新失败，Cloud Manager 将自动回滚到暂存环境。此操作自动完成，以确保在更新完成后，暂存环境和生产环境均采用同一个 AEM 版本。

AEM 版本更新分为两种类型：

* **AEM 推送更新**

   * 可以每日发布。
   * 主要是用于维护，包括最新的错误修复和安全更新。

      由于定期应用更改，因此其影响是增量式的，因此减少了对您服务的影响。

* **新增功能更新**

   * 按照可预测的每月计划发布。

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager 是 AEM as a Cloud Service 连续升级方法的组成部分，它控制对实例的所有更新，这一点是必需的。

在有新版本的 Cloud Service 可用时，Adobe 会触发更新。此外，您可以使用 Cloud Manager 提供的管道触发应用程序更新。

Cloud Manager：

* 用于管理 AEM 程序和环境，

* 是 AEM as a Cloud Service 的必要组件；每个新租户都要首先预配 Cloud Manager 访问权限，

* 是运营员工和开发员工的单一入口点。

具体来说，可从 Cloud Manager 创建的 AEM 程序的数量和类型派生自：

* 客户授予许可协议，

* 内部驱动的操作者（当 AEM as a Cloud Service 用于能力培养或培训时），

* 外部驱动的流程，例如从 Adobe.com 启动的试用。

Cloud Manager 已经演变成为自助服务门户，在其中可以创建和配置 AEM as a Cloud Service 的主要组件：

* 创建和管理新程序。有关详细信息，请参阅[了解程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)。

* 在这些程序中创建和管理 AEM 环境。有关详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md)。

* 创建和管理管道，用于将客户代码以及相关配置部署到特定环境。有关详细信息，请参阅[配置 CI-CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

* 获得有关这些组件的重要生命周期事件（例如，产品更新）的通知。

Cloud Manager 在跨多个地域的数据中心内创建环境，实现全球覆盖。CDN Points of Presence (PoP) 确保为全球各地的客户提供低延迟的内容投放。


## 入门 {#onboarding}

使用 AEM as a Cloud Service 启动和管理 AEM 项目都非常直接，因为 Adobe 负责处理以下许多方面：

* 基准 AEM 映像针对特定用例进行了优化。

* 许多手动配置任务已经变得多余。

其很大的差别还在于现在：

* 有评估阶段，能够确保满足所有先决条件；例如，包括：

   * 法律要求

   * 合约协议

   * 任何现有内容的技术要求和/或客户自定义的代码

* 有部署要求：

   * 代码更新；任何为以前版本的 AEM 开发的客户应用程序都将需要审核并可能需要更新。

   * 内容迁移

>[!TIP]
>
>有关载入流程的完整概述，请参阅 [入门历程。](/help/journey-onboarding/overview.md)

## 开发 {#developing}

>[!NOTE]
>
>有关详细信息，您可通过[开发指南](/help/implementing/developing/introduction/development-guidelines.md)和[部署 – WKND 教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)来开始了解。

支持 AEM as a Cloud Service 的新架构涉及到对整体开发人员体验的一些关键改变。AEM as a Cloud Service 的主要目标之一是允许经验丰富的客户（曾在内部部署或者在 Adobe Managed Service 环境中使用 AEM）尽可能快地迁移到 AEM as a Cloud Service，而无需重新编写大量的自定义代码。不过，可能仍然需要进行一些调整。

### 云开发 {#aem-as-a-cloud-service-developing-cloud-development}

现有 AEM 应用程序如果要在 AEM as a Cloud Service 上运行，则需要完成以下步骤：

* 应用程序代码和配置必须存储在所关联 Cloud Manager 程序的 Git 代码存储库中。
* 应用程序代码和配置必须与最新版本的基准 AEM 映像（可能会每日更改）兼容。
   * 在构建和部署客户应用程序时，必须使用与 Cloud Manager 环境关联的 Cloud Manager 管道。
* 客户应用程序必须通过在管道中强制进行的所有代码质量、安全和性能审核。
* 为客户应用程序构建的映像必须由 Cloud Manager 管道部署。

此流程通常称为云优先的开发。由于端到端持续时间预计需要很多分钟（根据应用程序的复杂性，可能需要 20 到 50 分钟），在云中尝试挂起的代码和配置更改之前，务必要采用快速开发方法。

用于管理 OSGI 捆绑包及其关联配置的 Web 控制台（以前是 AEM 快速入门的一部分）在 AEM as a Cloud Service 中不再可用。新的开发人员控制台为大多数运行时信息提供了一个只读界面。 通过这个控制台，开发者可以直接选择并登录作者或发布服务的任何特定节点，并查看相关信息。

>[!NOTE]
>
>另请参阅 [OSGi 配置](/help/implementing/deploying/overview.md#osgi-configuration)

开发人员的另一个常见要求是快速访问不同环境的日志文件。使用 AEM as a Cloud Service，创作和发布节点中不同节点的日志文件通过 Cloud Manager，以可供下载的文件格式或者通过 API 提供。

由于代码和内容的明确分离，开发人员在部署过程中可以使用特定流程来更新内容。可变内容的典型用例包括：

* 属于客户项目的标准&#x200B;*默认* 内容（例如，文件夹、模板、工作流等）

* 搜索索引定义

* ACL 和权限

* 服务用户和用户组

### 本地开发 {#aem-as-a-cloud-service-developing-local-development}

为了支持快速迭代和开发，还可以在 AEM as a Cloud Service 环境之外开发 AEM 应用程序。出于此目的，向开发人员提供了以下工件：

* AEM as a Cloud Service QuickStart：最新 AEM 代码库的独立安装程序，它基于 `.jar`，具有相同的功能和 API 表面。

* AEM as a Cloud Service Dispatcher SDK：基于映像的流程，用于在本地测试和验证 Dispatcher 配置。

>[!NOTE]
>
>需要注意的是，并非所有AEM Sites 和 AEM Assets 功能均允许云 QuickStart。它包括一个简单的创作环境，可以开发和测试大多数扩展功能。

## 操作和性能 {#operations-and-performance}

>[!NOTE]
>
>有关更多详细信息，请参阅[备份](/help/operations/backup.md)、[索引](/help/operations/indexing.md)和[其他维护任务](/help/operations/maintenance.md)。

使用 AEM as a Cloud Service 时，此类操作会自动完成，因此不再需要中断服务。

在这些领域：

* 许多任务已经自动化。

* 拓扑进行了优化以尽可能提高弹性和效率；例如，默认使用非二进制复制。

* 重负载任务，例如排队、作业和批量处理任务移出了核心 AEM 实例，由共享和专用的微服务处理。

新的监控、报告和警报基础设施也支持 AEM as a Cloud Service 的操作。这使得 Adobe SRE（网站可靠性工程师）可以主动确保服务正常运行。架构中的不同元素都配备了各种运行状况检查。如果由于某种原因将架构的某个具体节点视为不健康，则会将其从服务中移出，并使用新的健康节点静默替换。

## Identity Management {#identity-management}

>[!NOTE]
>
>有关详细信息，请参阅[安全性 – IMS 支持](/help/security/ims-support.md)。

对 AEM as a Cloud Service 的一项重大更改是完全集成使用 Adobe ID 来访问创作层。

这需要使用 [Adobe Admin console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 来管理用户和用户组。用户可以利用用户帐户来访问 Adobe 产品和服务，因为用户配置文件信息集中存储在 Adobe Identity Management System (IMS) 中，可供所有 Cloud Service 共享。分配了对 AEM 的访问权限之后，可以在 AEM as a Cloud Service 中引用用户帐户（与以前一样）；例如，用于从 AEM Security 用户界面定义角色和权限。

这集合了下列好处：

* 使用 Adobe Identity Management System (IMS) 在所有 Adobe 云应用程序之间提供单点登录。

* 对于 AEM as a Cloud Service 的每个具体实例，用户偏好设置保留在本地。

## 创作用户界面 {#authoring-user-interface}

>[!NOTE]
>
>如需了解详细信息，[基本处理](/help/sites-cloud/authoring/getting-started/basic-handling.md)是一个很好的起点。

对于站点和 Assets，以前使用过 AEM 的任何用户都会非常熟悉创作用户界面 (UI) 的基本原则。

主要差别在于 UI 完全支持触摸；经典 UI 不再可用。除此之外，基本的东西保持不变，只有一些明显的小变化。

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites as a Cloud Service 使您可以将 AEM Content Management System 与 AEM 数字资产管理的强大功能结合起来，向客户提供以内容引导的个性化体验。

有关详细信息，请参阅[对站点的更改](/help/sites-cloud/sites-cloud-changes.md)概述。

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Cloud Service 为企业提供了云原生的 PaaS 解决方案，不仅可用于快速执行其数字资源管理和 Dynamic Media 运营来实现影响力，而且还可在始终最新、始终可用和不断学习的系统中使用新一代智能功能，例如 AI/ML。

Assets 产品包括云中的新一代资源处理以及高性能资源引入和搜索。

有关详细信息，请参阅 [Assets as a Cloud Service 概述和简介](/help/assets/overview.md)。

## 了解 Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

有关更多信息，请参阅：

* [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)
* Adobe Experience Manager as a Cloud Service 的[架构](/help/overview/architecture.md)
* [对 AEM as a Cloud Service 的重要更改（发行说明）](/help/release-notes/aem-cloud-changes.md)
* [对 AEM Sites as a Cloud Service 的重要更改](/help/sites-cloud/sites-cloud-changes.md)
* [对 AEM Assets as a Cloud Service 的重要更改](/help/assets/assets-cloud-changes.md)
* [AEM Assets as a Cloud Service 简介](/help/assets/overview.md)
* [Adobe Experience Manager as a Cloud Service 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=zh-Hans)

>[!TIP]
>
>在大致了解 AEM as a Cloud Service 后，您可以查看[入门培训历程](/help/journey-onboarding/overview.md)来快速入门。
>
>已完成入门培训或准备开始深入测试 AEM 的功能？安装 [AEM 参考演示加载项](/help/journey-sites/demos-add-on/overview.md)，使用丰富的示例探究 AEM 的强大功能。
