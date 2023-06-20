---
title: 就绪阶段
description: 了解您需要执行的步骤，以便确保AEM安装已准备好移至云中
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 8%

---

# 就绪阶段 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="规划过渡"
>abstract="在开始过渡到 Cloud Service 的历程之前，您应该熟悉 AEM as a Cloud Service，并查看已对它所做的显著更改以及已替换或已弃用的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Best Practices Analyzer"

在AEMas a Cloud Service迁移历程的这一阶段，您将熟悉AEMas a Cloud Service、审查引入的显着更改并了解成功迁移到云需要做哪些规划。

## 迄今为止的故事 {#story-so-far}

上一份文件， [AEMas a Cloud Service迁移入门](/help/journey-migration/getting-started.md)，概述了迁移到AEMas a Cloud Service所需经历的阶段列表，以及这样做的优势。

## 目标 {#objective}

本文档有助于您了解必须考虑的因素，这样您才能确保AEM安装已准备好迁移到云：

* 了解显着更改和已弃用的功能
* 了解如何规划迁移到AEMas a Cloud Service

## 查看AEMas a Cloud Service架构中的显着更改 {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service 为管理 AEM 项目提供了许多新功能和可能性。

随着这些改进，与AEMas a Cloud Service相比，AEM和Adobe Managed Services的内部部署安装存在一些差异。

下表中的项目列表是与迁移到AEMas a Cloud Service最相关的更改的子集。 您可以查阅重要更改的完整列表 [此处](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>更改了哪些内容？</th>
    <th>引用</th>
    <th>主要技巧</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>将可变和不可变过滤器分隔到相应的包中</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">AEMas a Cloud Service显着更改</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">适用于AEM的AEM项目结构as a Cloud Service</a></td>
    <td>可部署到AEMas a Cloud Service的单个包可以具有子包，主要用于包含分隔到其自己的包中的可变和不可变内容。</td>
  </tr>
  <tr>
    <td>存储库初始</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Apache Sling RepoInit文档</a></td>
    <td>Repoinit脚本是创建任何初始节点结构、用户、组或服务用户的最佳实践。 由于这些脚本可以通过运行模式定位，并通过代码包部署进行管理，因此它们提供了很大的灵活性来实现存储库初始化任务。</td>
  </tr>
  <tr>
    <td>不允许自定义运行模式</td>
    <td></td>
    <td>仅支持随AEMas a Cloud Service一起提供的现成运行模式。<br>添加其他开发环境后，所有这些环境都会绑定到“开发”运行模式。</td>
  </tr>
  <tr>
    <td>Cloud Manager管道执行是部署的唯一方法</td>
    <td></td>
    <td>在AEMas a Cloud Service中，不允许访问/system/console，因此所有OSGi配置都必须是代码的一部分，并且应该作为代码部署。<br>OSGi配置以只读模式提供，以便通过Cloud Manager在开发人员控制台中查看</td>
  </tr>
  <tr>
    <td>复制代理已由Sling Content Distribution替换</td>
    <td></td>
    <td>Sing Content Distribution取代了复制代理的概念。 如果存在利用复制代理的自定义，则必须重新设计它们。<br>不支持反向复制</td>
  </tr>
  <tr>
    <td>CRX/DE和包管理器</td>
    <td></td>
    <td>CRX/DE仅允许在开发环境中使用。<br>包管理器可在所有创作实例上访问，但即将部署的包必须仅包含可变内容（例如： /content或/conf）</td>
  </tr>
  <tr>
    <td>内置CDN并获取您自己的CDN</td>
    <td></td>
    <td>AEMas a Cloud Service包含适用于所有环境的CDN，针对大多数用例进行了优化。<br>如果您希望设置自己的CDN，则必须向Adobe支持提交请求才能获得批准。<br>如果获得批准，CDN将指向Fastly，而不是任何环境中的AEM实例。</td>
  </tr>
  <tr>
    <td>长时间运行的作业</td>
    <td></td>
    <td>避免执行长时间运行的作业（如Sling调度程序或Cron作业），因为容器中执行的AEM实例可以随时来来去去。<br>重新思考这些功能以将其卸载到Adobe I/O。</td>
  </tr>
  <tr>
    <td>切换到异步操作</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">配置异步操作</a></td>
    <td>为了提高环境的整体性能，某些操作会在异步模式下执行。 当系统资源可用时，异步作业将排队并运行。</td>
  </tr>
  <tr>
    <td>基于令牌的身份验证和集成策略</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">为服务器端API生成访问令牌</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication">基于令牌的身份验证教程</a></td>
    <td>AEM外部的系统通常会尝试在AEM中执行HTTP操作。<br>建议的方法是实施此处概述的策略，而不是依赖在AEM中使用密码创建本地用户名。</td>
  </tr>
  <tr>
    <td>文件IO/磁盘使用情况</td>
    <td></td>
    <td>由于无法保证分配了多少磁盘空间以及容器中的实例来来去去，因此不建议使用文件I/O操作从附加到AEM实例的磁盘中写入或读取。</td>
  </tr>
  <tr>
    <td>DAM更新资产工作流</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">asset compute服务</a></td>
    <td>DAM更新资源工作流中的媒体处理步骤现在由Asset compute服务替换</td>
  </tr>
  <tr>
    <td>AEMas a Cloud Service中的资源上传方法和支持的工作流流程步骤</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">上传API比较和支持的WF流程步骤</a></td>
    <td>在AEMas a Cloud Service中，在上传或下载资源期间，资源将直接流入或流出二进制存储。</br>AEMaaCS并不支持所有工作流流程步骤。</td>
  </tr>
  <tr>
    <td>工作流启动器</td>
    <td></td>
    <td>从代码中删除任何触发OOTB或自定义DAM更新资产工作流的工作流启动器。</br>Asset Processing Service将处理上传到AEMas a Cloud Service的所有资源。 有关自定义步骤，请参阅 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> 后处理工作流</a> 介绍如何设置和配置后处理工作流。</td>
  </tr>
  <tr>
    <td>自定义演绎版步骤</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=en#manage">处理配置文件</a></td>
    <td>必须通过创建相应的处理配置文件，将任何自定义演绎版生成、图像转换或视频编码卸载到资产处理服务。</td>
  </tr>
  <tr>
    <td>内容搜索与索引</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en">内容搜索和索引更改</a></td>
    <td>索引的基础处理及其生效时间发生了重大变化。<br>在您将部署的代码中管理Oak索引之前，请完全了解并重新重构这些索引。</td>
  </tr>
  <tr>
    <td>并非所有维护任务都是可配置的</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=en">AEMas a Cloud Service维护任务</a></td>
    <td>您只能使用AEMas a Cloud Service配置某些维护任务。</td>
  </tr>
  <tr>
    <td>对发布存储库的更改</td>
    <td></td>
    <td>不允许直接更改发布存储库，但/home下的更改除外。 始终建议对作者进行更改并分发这些更改。 所有代码和配置更改必须通过相应的Cloud Manager管道部署。</td>
  </tr>
  <tr>
    <td>Dispatcher配置和缓存</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery">云中的调度程序</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/caching.html?lang=en#other-content">缓存管理<br></td>
    <td>Dispatcher配置必须遵循特定结构。<br>配置必须作为代码的一部分进行管理，并通过Cloud Manager管道进行部署。</td>
  </tr>
  <tr>
    <td>备份和恢复</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en">AEMas a Cloud Service备份和恢复</a></td>
    <td></td>
  </tr>
  <tr>
    <td>身份验证更改</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hans">AEM as a Cloud Service 的 IMS 支持</td>
    <td>如果在迁移到Cloud Service之前，您之前在author和publish上使用SAML 2.0集成，则主要更改是AEMas a Cloud ServiceAuthor仅与Adobe IMS集成。 但是，AEMas a Cloud Service发布层仍可以使用SAML或其他身份验证集成。 AEM as a Cloud Service 仅为作者、管理员和开发人员用户提供 IMS 身份验证支持。IMS身份验证不支持客户站点（如站点访客）的外部最终用户。</td>
  </tr>
</tbody>
</table>

## 已弃用功能 {#deprecated-features}

Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。

我们建议您查阅 [已弃用功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) 熟悉Experience Manageras a Cloud Service中标记为已弃用的特性和功能，并了解对您的AEM部署有何影响。

## 计划审查AEM安装 {#review-planning}

在您已经习惯了使用AEMas a Cloud Service引入的更改后，现在应该开始计划审查您的现有安装。 这样做有助于您衡量将其移动到云所需的更改级别。

下图显示了审查阶段涉及的关键步骤：

![图像](/help/journey-migration/assets/planning-phaseimg1.png)

接下来，我们将详细探究每个步骤的含义。

### 评估云服务准备情况 {#assess-cloud-readiness}

第一步是评估您是否已准备好从现有AEM版本迁移至Cloud Service，并确定需要重构才能与AEMas a Cloud Service兼容的区域。

您需要根据显着更改和已弃用功能对当前AEM源代码进行全面评估，以确定过渡历程中预期的工作量。

调查结果的数量将直接影响时间表和项目的整体成功。 因此，建议尽可能多地探索如何计划交付或开始重新设计符合AEMas a Cloud Service最佳实践所需的任何自定义项所需的对话。

**Best Practice Analyzer**

您可以针对当前AEM版本运行最佳实践分析器，以加快评估速度。 很好地了解它的工作原理是加快评估计划的关键。

您可以参阅 [最佳实践分析器](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 文档。

**创建云就绪性评估报告**

下一步是根据迄今为止获得的所有知识编写报告。 为此，您可以从暂存和生产实例生成最佳实践分析器报告， [然后将其上传到Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) 操作项的可消化报告。

典型报表应包含以下输入内容：

* 详细说明特定AEM安装的功能集的文档
* 有关您的AEM自定义配置和代码的详细信息
* 生产Dispatcher配置
* CDN配置（如果有）

**使报表社会化**

Best Practices Analyzer报告完成后，请与相关团队共享这些报告，以便您可以确认调查结果并规划后续步骤。 根据偏好，您还可以使用以下方式分发报告的打印版本 [打印预览](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### 审查资源计划 {#review-resource-planning}

一旦评估了迁移至Cloud Service所需的工作量，您就应该确定资源、创建团队并为过渡流程规划角色和职责。

### 建立 KPI {#establish-kpis}

如果您以前尚未建立关键绩效指标(KPI)，则建议为您的AEM实施建立KPI，以帮助您的团队专注于最重要的事情。

参见 [开发KPI](https://guided.adobe.com/welcome/aem/part6.html) 以了解如何为您的业务目标选择合适的KPI。

## 后续内容 {#what-is-next}

一旦您了解了迁移到AEMas a Cloud Service所需的更改范围，就可以开始 [使您的代码和内容云就绪](/help/journey-migration/implementation.md) 才能实际执行迁移。

## 其他资源 {#additional-resources}

* [Cloud Acceleration Manager快速入门](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md)  — 有关如何使用Cloud Acceleration Manager加快迁移到云的综合指南
* [AEMas a Cloud Service：简介、架构和思维方式不同](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEMCloud Service主页](/help/overview/home.md)  — 有关Experience Manageras a Cloud Service文档的概述，请从此处开始。
* [AEMas a Cloud Service概述](/help/overview/home.md)  — 本指南提供了Experience Manageras a Cloud Service的概述，包括简介、术语和架构。
* [载入历程](/help/journey-onboarding/overview.md) — 本指南概述了如何开始使用Experience Manageras a Cloud Service，包括如何获取访问权限和设置团队
