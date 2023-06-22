---
title: 面向合作伙伴的 Experience Manager as a Cloud Service 迁移指南
description: 面向合作伙伴的 Experience Manager as a Cloud Service 迁移指南
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: d925310603961f1f3721c283fc247105459e9c0f
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 21%

---

# Adobe Experience Manager as a Cloud Service合作伙伴迁移指南 {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="迁移至 AEM as a Cloud Service"
>abstract="概述推荐的分阶段方法，将客户从各种 Experience Manager 部署过渡到 Experience Manager as a Cloud Service，并帮助现有客户提供无中断的互联体验"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html" text="新增功能和不同功能"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html" text="AEM as a Cloud Service 简介."

Adobe Experience Manager (AEM) as a Cloud Service提供了重新构建的Experience Manager基础，它基于基于容器的基础架构、API驱动的开发和引导式DevOps流程而构建，允许营销人员和开发人员始终在客户体验管理创新方面保持领先。

Cloud Service将Adobe Experience Manager丰富的开箱即用功能和可扩展性与现代云原生架构的灵活性结合在一起，使品牌能够满足不断变化的消费者需求。

这份单页宣传材料概述了推荐的分阶段方法，用于将客户从各种 Experience Manager 部署过渡到 Experience Manager as a Cloud Service，并帮助现有客户在这个专门构建的现代化体验管理平台上提供无中断的互联体验。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

有关迁移历程的一般描述，请参阅下图。

![图像](/help/journey-migration/assets/migration-process.png)

## Adobe Experience Manager as a Cloud Service快速入门 {#getting-started}

| 有什么不同呢？ | 架构概述 |
|--------------------------|--------------------------|
| <ul><li>[现代建筑](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[自动更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)</li><li>[资源微服务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[直接访问二进制文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=en)</li><li>[代码和内容分离](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[复制即服务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=zh-Hans)</li><li>[Admin Console、组/用户成员资格和ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li></ul> | <ul><li>[AEM架构简介](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[环境栈栈](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[创作层](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[发布层](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hans) via [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li><li>[asset compute服务](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - 运行时架构](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - 运行时架构")

<br>

## Adobe Experience Manager as a Cloud Service中的开发人员历程 {#developer-journey}

### 开发

与Adobe Experience Manager On Premise和Adobe Experience Manager as a Cloud Service解决方案相比，Managed Services中的代码开发基础知识类似。

开发人员编写代码并在本地对其进行测试，然后将该代码推送到远程Adobe Experience Manager as a Cloud Service环境。

请参阅有关Experience Manageras a Cloud Service实施的自助资源，了解如何自定义Experience Manageras a Cloud Service部署。

| 本地开发设置 | 开始前须知 |
|-----------|------------|
| <ol><li>审核 [ADOBE EXPERIENCE MANAGER SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en) 文档，以了解更多信息。</li><li>观看 [安装Dispatcher SDK](https://video.tv.adobe.com/v/30601) 了解如何安装Dispatcher SDK</li><li>观看 [配置Dispatcher SDK](https://video.tv.adobe.com/v/30602) 了解如何配置Dispatcher SDK</li><li>审核 [本地开发设置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) 文档，以了解更多信息</li><li>配置对Experience Manager的访问权限 [演练](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Development Essentials](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[开发准则](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)</li><li>[了解Experience Manager项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[数字基础Blueprint](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[样式系统](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=en)</li><li>[叠加](/help/implementing/developing/introduction/overlays.md)</li><li>[Experience Manageras a Cloud ServiceAPI参考](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> 请参阅教程，了解如何 [在本地Experience ManagerSDK上开发和部署WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)

### 部署

开发人员编写代码并在本地进行测试，然后将代码推送到远程 AEM as a Cloud Service 环境。

需要使用 Cloud Manager，它是 Managed Services 的一个可选内容交付工具。现在，这是用于将代码部署到 AEM as a Cloud Service 环境的唯一机制。

请参阅有关如何配置和部署到AEMas a Cloud Service环境的自助资源。

1. [配置CM管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=en)
   * 生产管道
   * 仅非生产和代码质量管道
2. [部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en)
3. [了解测试结果](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en)
4. **访问日志**
   * [通过CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)
   * [通过Adobei/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [运行和维护](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=en)
   * [配置OSGI配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en)
   * [备份和恢复](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=en)

>[!TIP]
> 请参阅教程，了解如何 [将WKND部署到Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)

### 帮助及资源

1. [调试提示和技巧](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [开发人员控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en) (仅在本地SDK和Experience Manager云开发环境中可用)
4. [日志和日志记录](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM日志](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) （构建单元测试、代码扫描、构建映像、部署）
   * [Experience Manager Cloud Service日志](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror、aemaccess、aemrequest、aemdispatcher、httpderror、httpcaccess)
   * 本地SDK日志（位于host：port/crx-quickstart/logs下）

>[!NOTE]
> 要获得其他帮助，您可能需要：
>1. [联系Experience Manager支持团队](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索 [Experience Manager社区和论坛](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

<br>

## 迁移至 Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="迁移至 Adobe Experience Manager as a Cloud Service"
>abstract="这份单页宣传材料概述了推荐的分阶段方法，用于将客户从各种 Experience Manager 部署过渡到 Experience Manager as a Cloud Service，并帮助现有客户在这个专门构建的现代化体验管理平台上提供无中断的互联体验。"

**Experience Manageras a Cloud Service为Experience Manager Sites和Assets提供了可扩展、安全且敏捷的技术基础，使营销人员和IT人员能够专注于大规模提供有影响力的体验。**

借助Experience Manageras a Cloud Service，您的团队可以专注于创新而不是规划产品升级。 新产品功能经过全面测试，并在无任何中断的情况下交付给您的团队，以便他们始终可以访问一流的应用程序。

过渡到云服务的历程包括三个阶段 - 规划、执行和上线后。要成功、顺利的过渡，您应确保进行适当的规划并遵守本指南中概述的最佳实践。

下图显示了建议的Cloud Service过渡历程的高级呈现。

![图像](/help/journey-migration/assets/home-img1.png)

<br>

### 规划

在开始过渡到Cloud Service的过程之前，您应该熟悉Experience Manageras a Cloud Service，并查看已对它所做的显着更改，以及已替换或已弃用的功能。

<table>
<tr>
<td>项目发现和评估</td>
<td><ul><li>请参阅 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=zh-Hans">对Experience Manageras a Cloud Service的重要更改</a> 了解Adobe Experience Manager as a Cloud Service与Experience Manager6.x之间的重要差异。</li><li>请参阅 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=en">已弃用功能</a> 详细了解已标记为已弃用的特性和功能。</li><li>[仅适用于Cloud Service迁移]评估Cloud Service就绪性：运行 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en">Best Practices Analyzer(BPA)</a> 在源环境中 </li><li>针对Experience ManagerCS中的显着更改和已弃用功能完成评估</li></ul></td>
</tr>
<tr>
<td>审核</td>
<td><ul><li>根据发现，执行工作估算和资源配置练习</li></ul></td>
</tr>
<tr>
<td>衡量</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">建立项目KPI</a>，成功标准和项目时间表</li></ul></td>
</tr>
</table>

>[!NOTE]
>最佳实践分析器报告通过提供原本必须手动收集和评估的信息，加快了迁移到AEMas a Cloud Service所需的时间和成本的评估过程。


<br>

### 执行

在项目的执行阶段开始之前，您应该先开始Cloud Service。 您还需要熟悉Cloud Manager。 这是将项目代码部署到Experience Manager Cloud Service实例的机制。

Cloud Manager使组织能够在Cloud中自行管理Experience Manager。 它包括持续集成和持续交付([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=en))框架，使IT团队和实施合作伙伴能够在不影响性能或安全性的情况下快速交付自定义项或更新。

#### 内容迁移

1. [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) ：用于将现有内容从源AEM实例（内部部署或AMS）移动到目标AEM Cloud Service实例。
2. [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) ：用于导入和导出存储库的可变内容。


#### 重构/优化

| 快速入门 | 审查和重构代码 | Dispatcher审核 |
|---|---|---|
| <ul><li>[本地开发设置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[本地Dispatcher设置](https://video.tv.adobe.com/v/30602/)</li><li>[使用SDK API jar编译代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[查看AEM开发准则](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)<ul><li>后台任务和长时间运行的作业</li><li>Sling调度程序</li><li>输入流使用情况等</li></ul></li></ul> | <ul><li>运行 [Best Practices Analyzer(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) 在源环境中。[**仅迁移**]<ul><li>项目结构化注意事项(基于 [云原型](https://github.com/adobe/aem-project-archetype))<ul><li>代码和内容分离（可变与不可变）</li><li>[自定义索引定义](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en)</li><li>[自定义运行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=en)</li></ul></li></ul></li><li>审查并执行必要的更改</li><li>[部署](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) 它位于本地SDK上</li><li>通过AEM SDK执行烟雾测试</li></ul> | <ul><li>审核 [Dispatcher配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en) 用于重构</li><li>使用 [Dispatcher转换器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en) 工具（如果适用）。 [**仅迁移**]</li><li>可以使用进行测试 [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> 资产客户：使用审查和重构资产工作流 [资产云迁移](https://github.com/adobe/aem-cloud-migration) 工具


#### 部署/上线

1. [部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=en) git
2. 通过运行客户代码 [Cloud Manager质量管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=en)
3. [部署到开发环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**仅迁移**] 使用包或进行内容传输 [内容传输工具](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. 执行建议的测试周期（抽烟、QA等）
6. 提升至Cloud Manager生产管道
7. 烟雾试验验证
8. 上线

<br>

### 上线后

在上线后阶段，您应确保清理临时文件，审查持续开发的最佳实践并管理日志。

>[!TIP]
> 提供了用于对AEMas a Cloud Service环境进行故障排除的工具
>1. [开发人员控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)
>2. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en)
>3. [管理日志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)

<br>

### 工具和资源

| 评估 | 重构 | Experience Manager现代化 | 内容迁移 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en)</li></li> | <ul><li>[Unified Experience Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=en)</li></ul> | <ul><li>[静态模板到可编辑模板](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[设计配置到策略](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[基础组件到核心组件](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[经典 UI 到触控式 UI](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans)</li><li>[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> 要获得其他帮助，您可能需要：
>1. [联系Experience Manager支持团队](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索 [Experience Manager社区和论坛](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)
