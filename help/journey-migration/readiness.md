---
title: 就绪阶段
description: 了解您需要采取哪些步骤来确保AEM安装已准备就绪，可将其移至云
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 7%

---

# 就绪阶段 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="规划过渡"
>abstract="在开始过渡到 Cloud Service 的历程之前，您应该熟悉 AEM as a Cloud Service，并查看已对它所做的显著更改以及已替换或已弃用的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Best Practices Analyzer"

在AEMas a Cloud Service迁移历程的此阶段，您将熟悉AEMas a Cloud Service，查看其引入的显着更改，并了解成功迁移到云所需的计划。

## 迄今为止的故事 {#story-so-far}

上一份文件， [迁移到AEM as a Cloud Service](/help/journey-migration/getting-started.md)，概述了迁移到AEMas a Cloud Service所需执行的阶段列表以及执行此操作的好处。

## 目标 {#objective}

本文档可帮助您了解为确保AEM安装已准备就绪，可将其移至云，您必须考虑哪些因素：

* 了解显着更改和已弃用功能
* 了解如何规划迁移到AEMas a Cloud Service

## 查看AEMas a Cloud Service架构中的显着更改 {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service 为管理 AEM 项目提供了许多新功能和可能性。

与AEMas a Cloud Service相比，AEM和Adobe Managed Services的内部部署安装与这些改进还引入了一些差异。

下表中的项目列表是与迁移到AEMas a Cloud Service最相关的更改的子集。 您可以查阅显着更改的完整列表 [此处](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>更改了哪些内容？</th>
    <th>引用</th>
    <th>主要优点</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>将可变和不可变过滤器分离到相应的包中</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">AEMas a Cloud Service显着更改</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">适用于AEM的AEM项目结构as a Cloud Service</a></td>
    <td>可部署到AEMas a Cloud Service的单个包可以具有子包，主要用于包含分隔到其自身包中的可变和不可变内容。</td>
  </tr>
  <tr>
    <td>Repo Init</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Apache Sling RepoInit文档</a></td>
    <td>重新指向脚本是创建任何初始节点结构、用户、组或服务用户的最佳实践。 由于这些脚本可以通过运行模式进行定位，并且可通过代码包部署进行管理，因此它们在实现存储库初始化任务方面具有很大的灵活性。</td>
  </tr>
  <tr>
    <td>不允许自定义运行模式</td>
    <td></td>
    <td>仅支持随AEMas a Cloud Service提供的开箱即用运行模式。<br>添加其他开发环境后，所有环境都将绑定到“开发”运行模式。</td>
  </tr>
  <tr>
    <td>Cloud Manager管道执行是部署的唯一方法</td>
    <td></td>
    <td>在AEMas a Cloud Service中，不允许访问/system/console，因此所有OSGi配置都必须包含在代码中，并且应作为代码部署。<br>OSGi配置以只读模式提供，可通过Cloud Manager在开发人员控制台中查看</td>
  </tr>
  <tr>
    <td>复制代理由Sling内容分发取代</td>
    <td></td>
    <td>复制代理的概念被Sing Content Distribution所取代。 如果存在利用复制代理的自定义项，则必须重新设计这些自定义项。<br>不支持反向复制</td>
  </tr>
  <tr>
    <td>CRX/DE和包管理器</td>
    <td></td>
    <td>CRX/DE仅在开发环境中允许。<br>包管理器可在所有创作实例上访问，但要部署的包必须只包含可变内容(例如：/content或/conf</td>
  </tr>
  <tr>
    <td>内置CDN并获取您自己的CDN</td>
    <td></td>
    <td>AEM as a Cloud Service包含适用于所有环境的CDN，这些环境已针对大多数用例进行了优化。<br>如果您要设置自己的CDN，则必须向Adobe支持部门提交请求，以便获得批准。<br>如果获得批准，CDN将快速指向，而不是任何环境中的AEM实例。</td>
  </tr>
  <tr>
    <td>长时间运行的作业</td>
    <td></td>
    <td>避免执行长时间运行的作业（如Sling调度程序或Cron作业），因为在容器中执行的AEM实例可能会在任何时间点来回运行。<br>重新思考这些功能，将其卸载到Adobe I/O。</td>
  </tr>
  <tr>
    <td>切换到异步操作</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">配置异步操作</a></td>
    <td>为了提高环境的整体性能，某些操作会在异步模式下执行。 当系统资源可用时，异步作业将排入队列并执行。</td>
  </tr>
  <tr>
    <td>基于令牌的身份验证和集成策略</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">为服务器端API生成访问令牌</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication">基于令牌的身份验证教程</a></td>
    <td>AEM外部的系统通常会尝试在AEM中执行HTTP操作。<br>推荐的方法是实施此处概述的策略，而不是依赖在AEM中使用密码创建本地用户名。</td>
  </tr>
  <tr>
    <td>文件IO/磁盘使用情况</td>
    <td></td>
    <td>由于无法保证分配了多少磁盘空间以及容器中的实例来回移动，因此建议不使用文件I/O操作从附加到AEM实例的磁盘中写入或读取。</td>
  </tr>
  <tr>
    <td>DAM更新资产工作流</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">asset compute服务</a></td>
    <td>作为DAM更新资产工作流一部分的媒体处理步骤现在由Asset compute服务取代</td>
  </tr>
  <tr>
    <td>AEMas a Cloud Service中的资产上传方法和支持的工作流流程步骤</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">上载API比较和支持的WF流程步骤</a></td>
    <td>在AEMas a Cloud Service中，在上传或下载资产期间，资产会直接流入或流出二进制存储。</br>AEMaCS并非支持所有工作流流程步骤。</td>
  </tr>
  <tr>
    <td>工作流启动器</td>
    <td></td>
    <td>从您的代码中删除任何触发OOTB或自定义DAM更新资产工作流的工作流启动器。</br>上传到AEMas a Cloud Service的所有资产都将由资产处理服务进行处理。 有关自定义步骤，请参阅 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> 后处理工作流</a> 了解如何设置和配置后处理工作流。</td>
  </tr>
  <tr>
    <td>自定义演绎版步骤</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=en#manage">处理配置文件</a></td>
    <td>必须通过创建相应的处理配置文件，将任何自定义呈现版本生成、图像转换或视频编码卸载到资产处理服务。</td>
  </tr>
  <tr>
    <td>内容搜索与索引</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en">内容搜索和索引更改</a></td>
    <td>索引的基础处理以及何时启动都发生了很大的变化。<br>在将要部署的代码中管理Oak索引之前，请完全了解并重构索引。</td>
  </tr>
  <tr>
    <td>并非所有维护任务都可配置</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=en">AEMas a Cloud Service维护任务</a></td>
    <td>您只能使用AEMas a Cloud Service配置某些维护任务。</td>
  </tr>
  <tr>
    <td>对发布存储库的更改</td>
    <td></td>
    <td>不允许直接更改发布存储库，但/home下的除外。 始终建议对作者进行更改并分发这些更改。 所有代码和配置更改都必须通过相应的Cloud Manager管道进行部署。</td>
  </tr>
  <tr>
    <td>调度程序配置和缓存</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery">云中的调度程序</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/caching.html?lang=en#other-content">缓存管理<br></td>
    <td>Dispatcher配置必须遵循特定结构。<br>配置必须作为代码的一部分进行管理，并通过Cloud Manager管道进行部署。</td>
  </tr>
  <tr>
    <td>备份和恢复</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en">AEMas a Cloud Service备份和恢复</a></td>
    <td></td>
  </tr>
  <tr>
    <td>对身份验证的更改</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hans">AEM as a Cloud Service 的 IMS 支持</td>
    <td>如果您之前在移动到Cloud Service之前在创作和发布中都使用了SAML 2.0集成，则主要更改是AEMas a Cloud Service作者仅与Adobe IMS集成。 但是，AEMas a Cloud Service发布层仍然可以利用SAML或其他身份验证集成。 AEM as a Cloud Service 仅为作者、管理员和开发人员用户提供 IMS 身份验证支持。IMS身份验证不为客户站点（如站点访客）的外部最终用户提供支持。</td>
  </tr>
</tbody>
</table>

## 已弃用功能 {#deprecated-features}

Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。

我们建议您查阅 [已弃用的功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) 了解在Experience Manageras a Cloud Service中标记为已弃用的特性和功能，并了解这对AEM部署有何影响。

## 计划查看AEM安装 {#review-planning}

在您习惯了AEM as a Cloud Service中引入的更改后，便可以开始规划对现有安装的审查，以便衡量将其移动到云所需的更改级别。

下图显示了审阅阶段涉及的关键步骤：

![图像](/help/journey-migration/assets/planning-phaseimg1.png)

接下来，我们将详细探讨这些步骤中每个步骤的含义。

### 评估云服务准备情况 {#assess-cloud-readiness}

第一步是评估您从现有AEM版本移动到Cloud Service的准备情况，并确定需要重构才能与AEMas a Cloud Service兼容的区域。

您需要根据显着更改和已弃用的功能对当前AEM源代码进行全面评估，以确定过渡历程中预期的工作量。

调查结果的数量将直接影响时间表和项目总体成功。 因此，建议尽可能地发现计划投放或启动重新设计任何符合AEMas a Cloud Service最佳实践所需的自定义设置所需的对话。

**最佳实践分析器**

您可以针对当前的AEM版本运行“最佳实践分析器”，以加快评估。 要加快评估规划，必须充分了解其工作方式。

您可以通过咨询 [Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 文档。

**创建云就绪性评估报告**

下一步是根据迄今获得的所有知识创建报告。 您可以通过从暂存和生产实例生成最佳实践分析器报告来执行此操作， [然后将它们上传到Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) 可操作项目的可编辑报表。

典型报表应包含以下输入：

* 详细介绍特定AEM安装功能集的文档
* 有关AEM自定义配置和代码的详细信息
* 生产调度程序配置
* CDN配置（如果有）

**将报表社交化**

在“最佳实践分析器”报告完成后，请与相关团队共享这些报告，以确认您的发现并规划您的后续步骤。 根据偏好，您还可以使用 [打印预览](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### 审查资源计划 {#review-resource-planning}

在估算了迁移到Cloud Service所需的工作量后，您应该确定资源、创建团队并为过渡过程规划角色和职责。

### 建立 KPI {#establish-kpis}

如果您之前尚未建立关键绩效指标(KPI)，则建议为AEM实施建立KPI，以帮助您的团队专注于最重要的内容。

请参阅 [制定KPI](https://guided.adobe.com/welcome/aem/part6.html) 了解如何为您的业务目标选择适当的KPI。

## 下一步 {#what-is-next}

了解移动到AEMas a Cloud Service所需更改的范围后，便可以 [使代码和内容云就绪](/help/journey-migration/implementation.md) 执行迁移之前。

## 其他资源 {#additional-resources}

* [Cloud Acceleration Manager快速入门](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md)  — 有关如何使用Cloud Acceleration Manager加快云迁移的全面指南
* [AEMas a Cloud Service:导言、架构与思维的不同](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEM a Cloud Service主页](/help/overview/home.md)  — 有关Experience Manageras a Cloud Service文档的概述，请单击此处开始。
* [AEMas a Cloud Service概述](/help/overview/home.md)  — 本指南概述了Experience Manageras a Cloud Service，包括简介、术语和架构。
* [入门历程](/help/journey-onboarding/overview.md) — 本指南概述了如何开始使用Experience Manageras a Cloud Service，包括如何获取访问权限和设置您的团队
