---
title: 作为Experience Manager迁移到Cloud Service
description: 作为Experience Manager迁移到Cloud Service
translation-type: tm+mt
source-git-commit: 3c1ff52d58f64d351507d20e4368a6aeb1bf6339
workflow-type: tm+mt
source-wordcount: '2070'
ht-degree: 8%

---


# 作为Cloud Service迁移到Adobe Experience Manager{#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration-overview"
>title="迁移到AEM作为云服务"
>abstract="概括介绍从过渡部署到Experience Manager(作为Cloud Service)的Experience Manager客户的建议分阶段方法，并帮助现有客户提供连贯、连续的体验"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en" text="新增功能和不同功能"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en" text="AEM as a Cloud Service 简介."

Adobe Experience Manager(AEM)作为Cloud Service优惠，构建在基于容器的基础架构、API驱动型开发和指导型DevOps流程之上的重新构建Experience Manager基础，使营销人员和开发人员始终在客户体验管理创新中处于领先地位。

Cloud Service将Adobe Experience Manager丰富的开箱即用功能和可扩展性与现代云本机架构的灵活性结合在一起，使品牌能够满足不断变化的消费者需求。

此单页机概括了从过渡部署到Experience Manager(作为Cloud Service)，为客户推荐的分阶段方法，并帮助现有客户在这个专为体验管理而构建的现代化平台上提供连贯、连续的体验。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

<br>

## Adobe Experience ManagerCloud Service入门{#getting-started}

| 有什么不同？ | 架构概述 |
|--------------------------|--------------------------|
| <ul><li>[现代建筑](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[自动更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=en#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)</li><li>[Asset Microservices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html)</li><li>[直接访问二进制文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=en#asset-upload-with-direct-binary-access)</li><li>[代码和内容的分离](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[复制为服务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=en)</li><li>[管理控制台、组／用户成员资格和ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li></ul> | <ul><li>[AEM体系架构简介](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[环境堆栈](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[创作层](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[发布层](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) </li><li>[云管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) (CI/CD)</li><li>[通过管](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) 理控制台 [进行身份管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li><li>[asset compute服务](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - 运行时架构](/help/core-concepts/assets/concepts-03.png "AEM as a Cloud Service - 运行时架构")

<br>

## 作为Cloud Service的Adobe Experience Manager开发者旅程{#developer-journey}

### 开发

与Adobe Experience Manager内部部署和Managed Services解决方案相比，Adobe Experience Manager的代码开发基础在Cloud Service上是相似的。

开发者编写代码并在本地进行测试，然后将它作为Cloud Service环境推送到远程Adobe Experience Manager。

查看有关将Experience Manager作为Cloud Service实施的自助资源，了解如何将Experience Manager自定义为Cloud Service部署。

| 本地开发设置 | 开始前要了解的事情 |
|-----------|------------|
| <ol><li>请查阅[Adobe Experience ManagerSDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)文档以了解更多信息。</li><li>观看[安装调度程序SDK](https://video.tv.adobe.com/v/30601?captions=chi_hans)以了解如何安装调度程序SDK</li><li>观看[配置调度程序SDK](https://video.tv.adobe.com/v/30602?captions=chi_hans)以了解如何配置调度程序SDK</li><li>查看[本地开发设置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)文档以了解更多信息</li><li>配置对Experience Manager[遍历](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)的访问</li></ol> | <ol><li>[开发要素](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[开发指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)</li><li>[了解Experience Manager项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[数字基础蓝图](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[样式系统](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=en#authoring)</li><li>[叠加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/overlays.html?lang=en#developing)</li><li>[Experience Manager作为Cloud ServiceAPI参考](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/)</li></ol> |

>[!TIP]
> 请参阅有关如何在本地Experience ManagerSDK[上开发和部署WKND的教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

### 部署

开发人员编写代码并在本地测试它，然后将它作为Cloud Service环境推送到远程AEM。

Cloud Manager是Managed Services的可选内容投放工具，是必需的。 现在，这是将代码作为Cloud Service环境部署到AEM的唯一机制。

查看有关如何将AEM配置和部署为Cloud Service环境的自助资源。

1. [配置CM管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)
   * 生产管道
   * 仅限非生产和代码质量的管道
2. [部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)
3. [了解测试结果](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)
4. **访问日志**
   * [通过CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)
   * [通过Adobei/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [运营和维护](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/home.html?lang=en)
   * [配置OSGI配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#deploying)
   * [备份和恢复](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en)

>[!TIP]
> 请参阅有关如何[将WKND部署到Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/develop-wknd-tutorial.html?lang=en)的教程

### 帮助和资源

1. [调试提示与技巧](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [开发人员控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging) (仅适用于本地SDK和Experience Manager云开发环境)
4. [日志和日志记录](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM日志](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) （构建单元测试、代码扫描、构建映像、部署）
   * [Experience Manager Cloud Service日志](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror、aemaccess、aemrequest、aemdispatcher、httpderror、httpaccess)
   * 本地SDK日志（位于host:port/crx-quickstart/logs下）

>[!NOTE]
> 要获得更多帮助，您可能需要：
>1. [联系Experience Manager支持团队](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 浏览[Experience Manager社区和论坛](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## 作为Cloud Service移至Adobe Experience Manager{#move-to-cloud}

**Experience Manager作为Cloud Service为Experience Manager站点和资产提供了可扩展、安全、灵活的技术基础，使营销人员和IT人员能够专注于大规模提供有影响力的体验。**

以Experience Manager为Cloud Service，您的团队可以专注于创新而不是规划产品升级。 新产品功能经过全面测试并且可在无任何中断的情况下交付给团队，如此一来，您的团队便可以始终访问最先进的应用程序。

过渡到云服务的历程包括三个阶段 - 规划、执行和上线后。要成功、顺利的过渡，您应确保进行适当的规划并遵守本指南中概述的最佳实践。

下图显示了推荐的过渡到云服务的历程的示意图。

![图像](/help/move-to-cloud-service/assets/home-img1.png)

<br>

### 规划

在开始过渡Cloud Service之前，您应熟悉Experience Manager作为Cloud Service，并查看对其所做的显着更改，并查看已替换或已弃用的功能。

<table>
<tr>
<td>项目发现和评估</td>
<td><ul><li>请参阅<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">Experience Manager的显着变化(Cloud Service)</a>以了解Adobe Experience Manager作为Cloud Service与Experience Manager6.x之间的重要区别。</li><li>请参阅<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=en#deprecated-features">已弃用的功能</a>，进一步了解已标记为已弃用的功能和功能。</li><li>[仅适用于Cloud Service迁移]评估Cloud Service就绪性：在源环境上运行<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">最佳实践分析器(BPA)</a> </li><li>完成对Experience ManagerCS中显着更改和已弃用功能的评估</li></ul></td>
</tr>
<tr>
<td>审核</td>
<td><ul><li>基于发现、执行工作评估和资源调配练习</li></ul></td>
</tr>
<tr>
<td>度量</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">建立项目KPI</a>、成功标准和项目时间表</li></ul></td>
</tr>
</table>

>[!NOTE]
>最佳实践分析器报告通过提供本来必须手动收集和评估的信息，加快了估计过渡到AEM作为Cloud Service所需的时间和成本的过程。


<br>

### 执行

在开始项目的执行阶段之前，您应已装上木板，开始Cloud Service。 您还需要熟悉Cloud Manager。 这是将项目代码部署到Experience Manager Cloud Service实例的机制。

Cloud Manager使组织能够在云中自行管理Experience Manager。 它包含一个连续集成和连续投放([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=en#overview))框架，使IT团队和实施合作伙伴能够在不影响性能或安全性的情况下加快自定义或更新的投放。

#### 内容迁移

1. [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) :用于将现有内容从源AEM实例（内部部署或AMS）移至目标AEMCloud Service实例。
2. [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) :用于导入和导出存储库的可变内容。


#### 重构／优化

| 入门 | 审阅和重构代码 | 调度程序审阅 |
|---|---|---|
| <ul><li>[本地开发人员设置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[本地调度程序设置](https://video.tv.adobe.com/v/30602/?captions=chi_hans)</li><li>[使用SDK API jar编译代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[查看AEM开发指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>后台任务和长时间运行的作业</li><li>Sling调度程序</li><li>输入流使用等</li></ul></li></ul> | <ul><li>在源环境上运行[最佳实践分析器(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)。[**仅迁移**]<ul><li>项目结构考虑事项（基于[云原型](https://github.com/adobe/aem-project-archetype)）<ul><li>代码和内容的分离（可变与不可变）</li><li>[自定义索引定义](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#indexing)</li><li>[自定义运行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)</li></ul></li></ul></li><li>检查并执行必要的更改</li><li>[在本](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) 地SDK上部署</li><li>通过AEM SDK执行烟雾测试</li></ul> | <ul><li>查看[调度程序配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#local-validation-of-dispatcher-configuration)以进行重构</li><li>酌情利用[调度程序转换器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en#introduction-dispatcher)工具。 [**仅迁移**]</li><li>测试可使用[调度程序SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)进行</li></ul> |

>[!TIP]
> 资产客户：使用[Asset Cloud迁移](https://github.com/adobe/aem-cloud-migration)工具审核和重构资产工作流


#### 部署／上线

1. [部署到云管](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=en#managing-code) 理器
2. 通过[云管理器质量管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)运行客户代码
3. [部署到开发环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**仅迁**] 移使用包或内容 [传输工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md)(CTT)进行内容传输
5. 执行建议的测试周期（烟雾、QA等）
6. 提升到Cloud Manager Production Pipeline
7. 烟雾测试验证
8. Go-Live

<br>

### 上线后

在上线后阶段，您应确保清理临时文件，审查持续开发的最佳实践并管理日志。

>[!TIP]
> 工具可用于作为Cloud Service环境对AEM进行疑难解答
>1. [开发人员控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#aem-as-a-cloud-service-development-tools)
>2. [CRX/DE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging)
>3. [管理日志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)


<br>

### 工具和资源

| 评估 | 重构 | Experience Manager现代化 | 内容迁移 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[最佳实践分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)</li></li> | <ul><li>[统一体验插件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#refactoring-tools)</li></ul> | <ul><li>[静态模板到可编辑模板](https://opensource.adobe.com/aem-modernize-tools/pages/tools/page-structure.html)</li><li>[设计配置到策略](https://opensource.adobe.com/aem-modernize-tools/pages/tools/policy-importer.html) <li>[基础组件到核心组件](https://opensource.adobe.com/aem-modernize-tools/pages/tools/component.html)</li><li>[经典 UI 到触控式 UI](https://opensource.adobe.com/aem-modernize-tools/pages/tools/dialog.html)</li></ul> | <ul><li>[内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration)</li><li>[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> 要获得更多帮助，您可能需要：
>1. [联系Experience Manager支持团队](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 浏览[Experience Manager社区和论坛](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

