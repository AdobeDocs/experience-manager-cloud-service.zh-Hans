---
title: 就绪阶段
description: 了解您必须执行的步骤，以便确保AEM安装已准备好移至云。
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1900'
ht-degree: 6%

---

# 就绪阶段 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="规划过渡"
>abstract="在开始过渡到云服务的历程之前，请先熟悉 AEM as a Cloud Service。查看对它作出的重大更改和被取代或弃用的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=zh-Hans" text="Best Practices Analyzer"

在AEM as a Cloud Service迁移历程的这一阶段，您可以熟悉AEM as a Cloud Service。 您可以查看引入的显着更改，并了解为成功迁移到云进行规划需要做哪些工作。

## 迄今为止的故事 {#story-so-far}

上一个文档[迁移到AEM as a Cloud Service快速入门](/help/journey-migration/getting-started.md)概述了您必须经历的阶段列表，以便您可以迁移到AEM as a Cloud Service。 它还概述了迁移的好处。

## 目标 {#objective}

本文档可帮助您了解必须考虑的因素，以便您能够确保AEM安装已准备好移动到云：

* 了解显着更改和已弃用的功能
* 了解如何规划迁移到AEM as a Cloud Service

## 查看AEM as a Cloud Service架构中的显着更改 {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service为管理AEM项目提供了许多新功能和可能性。

伴随着这些改进，与AEM as a Cloud Service相比，AEM的内部部署安装与AdobeManaged Services之间引入了几个差异。

下表中的项目列表是与迁移到AEM as a Cloud Service最相关的更改的子集。 您可以在[此处](/help/release-notes/aem-cloud-changes.md)查看重要更改的完整列表。

<table>
<thead>
  <tr>
    <th>更改了哪些内容？</th>
    <th>引用</th>
    <th>主要要点</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>将可变和不可变过滤器分隔到相应的包中</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html">AEM as a Cloud Service显着更改</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">适用于AEM as a Cloud Service的AEM项目结构</a></td>
    <td>可部署到AEM as a Cloud Service中的单个包可以具有子包，主要是为了将可变和不可变内容分隔到其自己的包中。</td>
  </tr>
  <tr>
    <td>存储库初始</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Apache Sling RepoInit文档</a></td>
    <td>Repoinit脚本是创建任何初始节点结构、用户、组或服务用户的最佳实践。 由于这些脚本可以通过运行模式定位，并通过代码包部署进行管理，因此它们提供了很大的灵活性来完成存储库初始化任务。</td>
  </tr>
  <tr>
    <td>不允许自定义运行模式</td>
    <td></td>
    <td>仅支持随AEM as a Cloud Service一起提供的现成运行模式。<br>添加其他开发环境时，所有环境都会绑定到“开发”运行模式。</td>
  </tr>
  <tr>
    <td>Cloud Manager Pipeline Execution是部署的唯一方法</td>
    <td></td>
    <td>在AEM as a Cloud Service中，不允许访问/system/console，因此所有OSGi配置都必须是代码的一部分，并且应该作为代码部署。<br>OSGi配置以只读模式提供，可通过Cloud Manager在Developer Console中查看</td>
  </tr>
  <tr>
    <td>复制代理已由Sling Content Distribution替换</td>
    <td></td>
    <td>Sing Content Distribution取代了复制代理的概念。 如果存在使用复制代理的自定义项，则必须重新设计它们。<br>不支持反向复制</td>
  </tr>
  <tr>
    <td>CRX/DE和包管理器</td>
    <td></td>
    <td>CRX/DE仅允许在开发环境中使用。<br>包管理器可在所有创作实例上访问，但即将部署的包只能包含可变内容（例如： /content或/conf）</td>
  </tr>
  <tr>
    <td>内置CDN并获取您自己的CDN</td>
    <td></td>
    <td>AEM as a Cloud Service包括适用于所有环境的CDN，这些环境针对大多数用例进行了优化。<br>如果要设置自己的CDN，则必须向Adobe支持提交请求才能获得批准。<br>如果获得批准，CDN将指向Fastly，而不是任何环境中的AEM实例。</td>
  </tr>
  <tr>
    <td>长时间运行的作业</td>
    <td></td>
    <td>避免长时间运行作业，例如Sling调度程序或Cron作业，因为运行在容器中的AEM实例可以随时来往往。<br>重新考虑这些功能，以便将其卸载到Adobe Developer。</td>
  </tr>
  <tr>
    <td>切换到异步操作</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/asynchronous-jobs.html#configuring-asynchronous-msm-operations">配置异步操作</a></td>
    <td>为了提高环境的整体性能，某些操作以异步模式运行。 当系统资源可用时，异步作业将排队并运行。</td>
  </tr>
  <tr>
    <td>基于令牌的身份验证和集成策略</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html#the-server-to-server-flow">为服务器端API生成访问令牌</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html#authentication">基于令牌的身份验证教程</a></td>
    <td>AEM外部的系统通常会尝试在AEM中执行HTTP操作。<br>建议的方法是实施此处概述的策略，而不是依赖在AEM中使用密码创建本地用户名。</td>
  </tr>
  <tr>
    <td>文件IO/磁盘使用情况</td>
    <td></td>
    <td>无法保证分配了多少磁盘空间，并且容器中的实例会来去去。 因此，不建议使用文件I/O操作来写入或读取连接到AEM实例的磁盘。</td>
  </tr>
  <tr>
    <td>DAM更新资产工作流</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html">asset compute服务</a></td>
    <td>DAM更新资产工作流中的媒体处理步骤现在由Asset compute服务替换</td>
  </tr>
  <tr>
    <td>AEM as a Cloud Service中的资产上传方法和支持的工作流流程步骤</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis.html#post-processing-workflows-steps">上传API比较和支持的WF流程步骤</a></td>
    <td>在AEM as a Cloud Service中，在上传或下载资源期间，资源将直接流入或流出二进制存储。 <br>AEMaaCS不支持所有工作流进程步骤。</td>
  </tr>
  <tr>
    <td>工作流启动器</td>
    <td></td>
    <td>从代码中删除触发现成或自定义DAM更新资产工作流的任意工作流启动器。 <br>上传到AEM as a Cloud Service的所有资源都将由资源处理服务进行处理。 有关自定义步骤，请参阅<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows"> Post处理工作流</a>，了解如何设置和配置后处理工作流。</td>
  </tr>
  <tr>
    <td>自定义演绎版步骤</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html">处理配置文件</a></td>
    <td>必须通过创建相应的处理配置文件，将任何自定义演绎版生成、图像转换或视频编码卸载到资产处理服务。</td>
  </tr>
  <tr>
    <td>内容搜索与索引</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html">内容搜索和索引更改</a></td>
    <td>索引的基础处理及其引入时间发生了显着变化。<br>在部署代码中管理Oak索引之前，请完全了解并重构这些索引。</td>
  </tr>
  <tr>
    <td>并非所有维护任务都可以配置</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/maintenance.html">AEM as a Cloud Service维护任务</a></td>
    <td>您只能使用AEM as a Cloud Service配置某些维护任务。</td>
  </tr>
  <tr>
    <td>对Publish存储库的更改</td>
    <td></td>
    <td>不允许直接更改Publish存储库，但/home下的更改除外。 始终建议分发对作者所做的任何更改。 所有代码和配置更改都必须通过相应的Cloud Manager管道进行部署。</td>
  </tr>
  <tr>
    <td>Dispatcher配置和缓存</td>
    <td>云中的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html">Dispatcher</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/caching.html#other-content">缓存管理<br></td>
    <td>Dispatcher配置必须遵循特定结构。<br>配置必须作为代码的一部分进行管理，并通过Cloud Manager管道进行部署。</td>
  </tr>
  <tr>
    <td>备份和恢复</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html">AEM as a Cloud Service备份和恢复</a></td>
    <td></td>
  </tr>
  <tr>
    <td>身份验证的更改</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html">AEM as a Cloud Service 的 IMS 支持</td>
    <td>如果您之前在迁移到Cloud Service之前在创作和发布网站上使用SAML 2.0集成，则主要更改是AEM as a Cloud Service Author仅与Adobe IMS集成。 但是，AEM as a Cloud Service Publish层仍可以使用SAML或其他身份验证集成。 AEM as a Cloud Service 仅为作者、管理员和开发人员用户提供 IMS 身份验证支持。IMS身份验证不为客户站点（如站点访客）的外部最终用户提供支持。</td>
  </tr>
</tbody>
</table>

## 已弃用功能 {#deprecated-features}

Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。

Adobe建议您查阅[已弃用的功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html#deprecated-features)，以了解Experience Manageras a Cloud Service中标记为已弃用的特性和功能。 查看对您的AEM部署有何影响。

## 规划您的AEM安装审查 {#review-planning}

在您已经习惯了使用AEM as a Cloud Service引入的更改后，现在就可以开始计划审查您的现有安装了。 这样做有助于您衡量将其移至云所需的更改级别。

下图显示了审查阶段涉及的关键步骤：

![图像](/help/journey-migration/assets/planning-phaseimg1.png)

接下来，您将详细探究每个步骤的含义。

### 评估Cloud Service准备情况 {#assess-cloud-readiness}

第一步是评估您是否已准备好从现有AEM版本迁移至Cloud Service，并确定需要重构才能与AEM as a Cloud Service兼容的区域。

根据显着更改和已弃用功能对当前AEM源代码进行全面评估，以确定过渡历程中预期的工作量。

发现结果的数量会直接影响时间表和项目的整体成功。 因此，Adobe建议您尽可能多地发现，以便可以计划投放。 或者，启动对话，以便您可以重新设计符合AEM as a Cloud Service最佳实践所需的任何自定义设置。

**最佳实践分析器**

您可以针对当前AEM版本运行Best Practices Analyzer以加快评估速度。 很好地了解它的工作原理是加快评估计划的关键。

您可以通过查阅[最佳实践分析器](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)文档来阅读其工作方式。

**创建云就绪性评估报告**

下一步是根据迄今为止获得的所有知识创建报告。 您可通过以下方式创建报告：从暂存实例和生产实例生成Best Practices Analyzer报告，[然后将其上传到Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam)，以获取可操作项目的可理解报告。

典型报表应包含以下输入内容：

* 详细说明特定AEM安装的功能集的文档
* 有关AEM自定义配置和代码的详细信息
* 生产Dispatcher配置
* CDN配置（如果有）

**使报告社会化**

在完成Best Practices Analyzer报告后，请与相关团队共享，以便您可以确认调查结果并规划后续步骤。 根据偏好，您还可以使用[打印预览](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam)分发打印的报告版本。

### 审查资源计划 {#review-resource-planning}

评估了迁移到Cloud Service所需的工作量后，您应该确定资源、创建团队并为过渡流程规划角色和职责。

### 建立KPI {#establish-kpis}

如果您以前尚未建立关键绩效指标(KPI)，则建议为AEM实施建立KPI，以帮助团队专注于最重要的事情。

请参阅[开发KPI](https://experienceleague.adobe.com/welcome/aem/part6.html)，以便了解如何为您的业务目标选择合适的KPI。

## 后续内容 {#what-is-next}

了解了迁移到AEM as a Cloud Service所需的更改范围后，应当[在实际执行迁移之前，让您的代码和内容云准备就绪](/help/journey-migration/implementation.md)。

## 其他资源 {#additional-resources}

* [Cloud Acceleration Manager快速入门](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) — 有关如何使用Cloud Acceleration Manager加快您向云移动速度的全面指南。
* [AEM as a Cloud Service：简介、架构和思维方式不同](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEMCloud Service主页](/help/overview/introduction.md) — 有关Experience Manageras a Cloud Service文档的概述，请从此处开始。
* [AEM as a Cloud Service概述](/help/overview/introduction.md) — 本指南提供了Experience Manageras a Cloud Service的概述，包括简介、术语和架构。
* [入门培训历程](/help/journey-onboarding/overview.md) — 本指南概述了如何开始使用Experience Manageras a Cloud Service，包括如何获取访问权限和设置团队。
