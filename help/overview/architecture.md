---
title: Adobe Experience Manager as a Cloud Service 的架构简介
description: Adobe Experience Manager as a Cloud Service 的架构简介。
exl-id: 3fe856b7-a0fc-48fd-9c03-d64c31a51c5d
source-git-commit: b610de53d1bd1b120a2642336aac1713444bfd3e
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 14%

---

# Adobe Experience Manager as a Cloud Service 的架构简介 {#an-introduction-to-the-architecture-adobe-experience-manager-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="intro_aem_cloudservice_architecture"
>title="AEM as a Cloud Service 架构简介"
>abstract="在此选项卡中，您可以查看 AEM as a Cloud Service 的新架构并了解更改。AEM 带来了具有可变数量图像的动态架构，因此花时间了解云架构是很重要的。"
>additional-url="https://video.tv.adobe.com/v/330542/" text="架构概述"

Adobe Experience Manager (AEM) as a Cloud Service提供了一组可组合服务，用于创建和管理高影响力的体验。

本页介绍了AEMas a Cloud Service的逻辑架构、服务架构、系统架构和开发架构。

## 逻辑架构 {#logical-architecture}

AEMas a Cloud Service由AEM Sites、AEM Assets和AEM Forms等高级解决方案组成。 这些服务是单独许可的，但可以协作使用。 每个解决方案分别使用由AEMas a Cloud Service提供的可组合服务，具体取决于其各自的用例。

### 项目 {#programs}

AEM应用程序以 [项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 根据您的许可授权，在Cloud Manager应用程序中创建的这些权限。 在特定项目上下文中，这些程序可让您完全控制如何命名、配置关联的AEM应用程序以及如何分配权限。

作为客户，Adobe通常将您标识为 **租户**，也称为 *IMS组织* (Identity Management)。 租户可以拥有所需数量的项目并获得许可。 例如，经常会看到AEM Assets的中心程序，而AEM Sites可能会用在对应于多个在线体验的多个程序中。

>[!NOTE]
>
>AEMEdge Delivery Services在Cloud Manager中作为顶级解决方案显示，同时从许可的角度看是其他主要解决方案的一部分。 例如，AEM Sites与Edge Delivery Services。

可以为项目配置高级解决方案的任意组合，并且每个解决方案都支持一对多插件。 例如，Commerce或Screens for AEM Sites、Dynamic Media或Brand Portal for AEM Assets。

![AEMas a Cloud Service — 程序](assets/architecture-aem-edge-programs.png "AEMas a Cloud Service — 部署架构")

### 环境 {#environments}

使用AEM Sites、AEM Assets或AEM Forms解决方案创建项目后，关联的AEM实例将在此项目中以AEM环境的形式表示。

有四种类型 [环境](/help/implementing/cloud-manager/manage-environments.md) 适用于AEMas a Cloud Service：

* 生产环境：

   * 生产环境为业务从业者托管应用程序并运行实时体验。

* 暂存环境：

   * 暂存环境通常以1:1的关系与生产环境成对出现。
   * 暂存环境主要用于在对应用程序所做的更改推送到生产环境之前进行自动测试。
      * 这与Adobe在维护更新时启动的更改无关，也与代码部署启动的更改无关。
      * 在部署代码的情况下，您还可以执行手动测试。
   * 使用自助内容复制功能，暂存环境的内容通常与生产内容保持同步。
* 开发环境：
   * 开发环境允许开发人员在与暂存环境和生产环境相同的运行时条件下实施和测试AEM应用程序。
   * 更改通过部署管道，允许与生产部署管道相同的代码质量和安全审核。
* 快速开发环境(RDE)：
   * 在将新代码或现有代码部署到RDE实例中时，RDE环境允许快速开发迭代，而无需通过常规开发环境中找到的正式部署管道。

### Edge Delivery Services {#logical-architecture-edge-delivery-services}

AEM程序可以使用 [Edge Delivery Services](/help/edge/overview.md) 也一样。

配置完毕后，AEM可以引用用于通过Edge Delivery Services构建体验的GitHub代码存储库。 因此，新的配置选项将可用于关联的体验。 这些功能包括设置Adobe管理的CDN，以及访问许可指标或SLA报告。

## 服务架构 {#service-architecture}

AEMas a Cloud Service中的高级可组合服务列表可以用两个区段表示 — 内容管理和Experience Delivery：

![AEM as a Cloud Service 概述 - 带 Edge Delivery Services](assets/architecture-aem-edge.png "AEM as a Cloud Service 概述 - 带 Edge Delivery Services")

对于内容管理，有两个用于创作内容的主要服务集，它们分别表示为 *内容源*：

* AEM创作层：提供基于Web的界面（以及关联的API），用于管理Web内容。 这适用于两种方法：
   * Headful — 通过页面编辑器和通用编辑器
   * Headless — 通过内容片段编辑器
* 基于文档的创作层：允许您使用标准应用程序创作内容，例如：
   * Microsoft Word和Excel — 通过SharePoint
   * Google文档和工作表 — 通过Google Drive

对于体验交付，在使用AEM Sites或AEM Forms时，还有两组主要服务，它们不互斥，并且作为不同的源在Adobe管理的共享CDN（内容交付网络）下运行：

* AEM发布层：
   * 运行一个标准AEM发布者和Dispatcher场，允许动态呈现与已发布内容组合在一起的网页和API内容(例如，GraphQL)。
   * 主要基于服务器端应用程序逻辑。
* 边缘交付发布层：
   * 允许动态呈现来自各种内容源(如AEM创作层或基于文档的创作层)的网页和API内容。
   * 基于客户端应用程序逻辑，旨在实现最高性能。

还有关键的相邻服务：

* 边缘交付资产层：
   * 允许从AEM Assets投放已批准和已发布的媒体项目。 例如，图像和视频。
   * 媒体项目通常引用自AEM发布层或Edge Delivery发布层上运行的体验，或者引用自与AEM Assets集成的任何其他Adobe Experience Cloud应用程序。
* AEM预览层和Edge Delivery Services预览层：
   * 此外，还适用于分别使用AEM发布层或边缘交付发布层构建的体验。
   * 允许内容作者在发布操作之前预览上下文中的内容。

>[!NOTE]
>
>默认情况下，仅资产程序既没有发布层，也没有预览层。

还有其他相邻的服务：

* 复制服务：
   * 位于内容管理层和体验交付层之间。
   * 负责处理 *发布* 由内容作者发布的操作，然后将已发布的内容提供给发布层(AEM或Edge交付)。

  >[!NOTE]
  >与AEM 6.x版本相比，复制服务进行了彻底的重新设计，因为不再使用AEM早期版本的复制框架发布内容。
  >
  >最新的体系结构基于 *发布和订阅* 基于云的内容队列的方法。 对于AEM发布层，它允许可变数量的发布者订阅发布内容，并且是实现AEMas a Cloud Service的真正快速自动缩放的重要组成部分

* 内容存储库服务：
   * 由AEM创作层使用。
   * 是一个符合JCR的内容存储库的基于云的实例，由Apache Oak技术实现。
   * 内容的持久性主要基于基于blob的云存储。
* CI/CD服务：
   * 表示专门用于管理到AEM环境的部署管道的Cloud Manager功能的子集。
* 测试服务：
   * 表示用于执行的基础结构：
      * 功能测试，
      * UI测试：例如，基于Selenium或Cypress脚本，
      * 体验审核测试：例如Lighthouse分数、

     作为到AEM环境的部署管道的一部分，或作为到边缘投放代码存储库的GitHub拉取请求的一部分。
* 数据服务：
   * 负责公开客户数据，如许可指标（如内容请求、存储、用户）或使用报告（如上传和下载的次数）。
   * 客户数据可以通过API在产品用户界面（例如Cloud Manager）中公开。
* Real-User Metric (RUM)服务：
   * 负责从客户体验中收集关键量度（例如页面查看次数、核心Web重要事件、转化事件），并响应关联的查询（例如，过去7天内给定域的热门页面查看次数）。
* 资产计算服务：
   * 负责处理上传的图像、视频和文档；例如PDF和Adobe Photoshop文件。 处理过程可以使用Adobe Sensei提取图像和视频元数据（例如描述性标记或主色调），然后生成演绎版（例如不同大小或格式），进而访问诸如Adobe Photoshop和Adobe Lightroom API之类的API。
* Identity Management服务(IMS)：
   * 是负责管理和验证给定Adobe Experience Cloud应用程序(例如，Cloud Manager或AEM创作层)的用户和用户组的中心位置。
   * 通过Adobe Admin Console访问。

## 系统架构 {#system-architecture}

### AEM创作、预览和发布层 {#aem-author-preview-publish-tiers}

AEM创作层和发布层作为一组Docker容器实施，由标准Container Orchestration服务操作。 生成的容器化架构意味着一个完全动态的系统，该系统具有可变数量的pod，具体取决于实际活动（用于内容管理）和实际流量（用于体验交付）。 这使得AEMas a Cloud Service能够在流量模式发生更改时对其进行调整。

AEM创作层作为共享单个内容存储库的AEM创作pod集群运行。 在维护任务正在运行或部署过程正在进行时，至少两个Pod允许业务连续性。

AEM发布层作为AEM发布实例场运行，每个实例都有自己的已发布内容内容存储库。 每个发布者都耦合到配备有AEM Dispatcher模块的单个Apache实例，用于内容的具体化视图，用作Adobe管理的CDN的原点。 至少两个Pod也允许业务连续性，但在高流量期间此数量不断增加的情况并不少见。

AEM预览层由单个AEM节点组成。 这用于在发布到发布层之前保证内容质量。 偶尔可能会出现停机时间，尤其是在部署期间，这会发生在预览层上。

### Edge Delivery Services {#system-architecture-edge-delivery-services}

这些Edge Delivery Services在CDN和无服务器基础架构的基础上运行，以最高效的方式组装页面。 当请求资源时，无服务器基础架构负责将已发布的内容转换为语义HTML，并充当CDN的原点。

从AEM创作层或基于文档的创作环境提供的已发布HTML到语义内容的转换。

下图说明了如何在Microsoft Word（基于文档的创作）中编辑站点内容并发布到Edge Delivery。 其中还展示使用各种编辑器的传统 AEM 发布方法。

![AEM Sitesas a Cloud Service — 带Edge Delivery Services](assets/architecture-aem-edge-author-publish.png "AEM Sitesas a Cloud Service — 带Edge Delivery Services")

由于Edge Delivery Services是Adobe Experience Manager的一部分，因此Edge Delivery、AEM Sites和AEM Assets可以共存于同一个域中。 这是大型网站的常见用例。例如，客户可能希望将流量较大的特定页面迁移到Edge Delivery Services，而所有其他页面可能保留在AEM发布层。

## 开发架构 {#development-architecture}

### 代码存储库 {#code-repositories}

AEM项目的代码和配置存储在代码存储库中，进行更改时会从中发布部署管道。 有不同类型的代码存储库：

* AEM全栈：
   * 用于存储AEM创作层和发布层的服务器端Java代码和OSGI配置。
* AEM前端：
   * 用于存储AEM创作层和发布层的客户端JS、CSS和HTML代码。
有关clientlibs的更多详细信息，请参阅 [在AEMas a Cloud Service上使用客户端库。](/help/implementing/developing/introduction/clientlibs.md)
* AEM Web层：
   * 存储AEM发布层的Dispatcher配置文件。
* AEM配置：
   * 允许存储AEM发布层和Edge Delivery Services发布层的各种配置选项（如CDN设置或维护任务设置）。
* AEM Edge投放：
   * 用于存储使用Edge Delivery Services构建的站点的客户端JS、CSS和HTML代码

### 部署管道 {#deployment-pipelines}

开发人员和管理员可使用Cloud Manager提供的连续集成/连续交付(CI/CD)服务管理AEMas a Cloud Service应用程序。 Cloud Manager还会公开与监控、维护、故障诊断（例如，访问日志文件）和许可相关的任何内容。

![AEM as a Cloud Service - 部署架构](assets/architecture-aem-edge-deployment-pipelines.png "AEM as a Cloud Service - 部署架构")

Cloud Manager将管理对AEMas a Cloud Service实例的所有更新。 这是强制性的，并且是构建、测试客户应用程序并将其部署到创作层、预览层和发布层的唯一方法。 这些更新可以由Adobe(当AEM Cloud Service的新版本准备就绪时)触发，也可以由您自己（当应用程序的新版本准备就绪时）触发。

这是通过部署管道实现的，与项目中的每个环境耦合。 当 Cloud Manager 管道运行时，它将为创作层和发布层创建客户应用程序的新版本。这可通过将最新的客户包与最新的基准 Adobe 图像相结合来实现。

当客户更改代码或Adobe部署新的维护版本时，将触发部署管道。

在这两种情况下，将执行同一组自动测试。 它由测试组成：

* Adobe为确保产品完整性作出的贡献
* 客户提供的测试
   * 功能测试：通过向AEM创作层或发布层发送http请求
   * UI测试：基于Selenium或Cypress技术

这些自动测试在暂存环境中运行，这就是为什么务必要使暂存环境内容尽可能接近生产实例上的内容的原因。

所有测试成功通过后，新代码将部署到生产环境。

### 滚动更新 {#rolling-updates}

Cloud Manager通过使用滚动更新模式更新所有服务节点，完全自动转换为最新版本的AEM应用程序。 这意味着 **无停机时间** 用于创作或发布服务。

## 自AEM 6.x以来的主要创新 {#major-innovations-since-aem-6x}

与前几代(AEM 6.x及更早版本)相比，AEMas a Cloud Service的最新架构引入了一些根本性的变化和创新：

* 所有文件都直接从云数据存储上传和提供。 关联的位流永远无需经过 AEM 创作和发布服务的 JVM。因此，AEM创作和发布服务的节点可以更小，从而更符合快速自动缩放的需求。 对于业务从业者而言，这可以加快上传和下载图像、视频和其他任务的体验。

* 现在，包括发布内容的所有操作都包含一个遵循订阅模式的管道。已发布内容会推送到管道中的各个队列，发布服务的所有节点都会订阅这些队列。因此，创作层无需了解发布服务中的节点数；这样可以快速自动缩放发布层。

* 该架构将应用程序内容与应用程序代码和配置完全分离。所有代码和配置几乎都不可更改，并且都植入到用于创建各种创作和发布服务节点的基准图像中。因此，可以绝对保证每个节点都相同，并且只能通过运行 Cloud Manager 管道在全局范围内对代码和配置进行更改。

* 该体系结构包括基于无服务器技术构建的多个微服务，特别是使用Adobe I/O运行时

## 更多信息 {#further-information}

另请参阅：

* Edge Delivery Services:

   * [AEM as a Cloud Service 概述 - 带 Edge Delivery Services](/help/edge/overview.md)
   * [使用 Edge Delivery Services](/help/edge/using.md)
   * [探索带 Edge Delivery Services 的 AEM as a Cloud Service 的底层架构和重要部分](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/introduction/architecture.html?lang=zh-Hans)
