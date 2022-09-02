---
title: 实施 AEM 连接器
description: 实施 AEM 连接器
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: ht
source-wordcount: '968'
ht-degree: 100%

---

实施 AEM 连接器
=============================

以下提供了构建 [AEM 连接器](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html)的有用参考，应结合有关[提交](submit.md)和[维护](maintain.md)连接器的指导阅读这些参考。

请注意，可以通过 [Adobe Exchange Program](https://partners.adobe.com/exchangeprogram/experiencecloud) 获取 AEM 的开发人员许可证。

常见集成模式
---------------------------

AEM 是一个前沿的 Web 体验管理解决方案，提供了许多潜在的集成领域。常见集成模式包括：

* 将数据从外部系统提取到 AEM 中。例如，从 CRM 导出联系信息，以供访问 AEM 支持的网站的更广泛受众使用。实施应使用 Sling 的[计划作业](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，从而确保即使容器发生故障也能执行作业。代码应设计为假设作业可能会被多次触发。
* 将数据从 AEM 导出到外部系统中。例如，在 AEM 支持的网站上提交给 CRM 的新闻稿订阅设置。
* 从 AEM 中检索资产。例如，引用存储在 AEM Assets 中的资产的外部内容管理系统 (CMS)。或者，作为另一个示例，链接到 AEM Assets 中的图像的 PIM 系统。
* 将资产存储在 AEM 基础架构中。例如，营销资产管理 (MRM) 系统将批准的资产存储在 AEM Assets 中。
* 配置和呈现自定义 UI 组件。例如，允许作者拖放视频组件并将特定视频配置为在实时站点上播放。
* 使用合作伙伴服务对资产执行操作。例如，在发布页面时将资产发送到视频平台。
* 在 AEM Admin Console 中分析站点、页面或资产。例如，提供针对现有页面或未发布的页面的 SEO 建议。
* 对由外部服务维护的用户数据的页面级访问。例如，利用人口统计信息来个性化站点体验。了解 ContextHub，它是一个用于存储、操作和呈现上下文数据的框架。
* 翻译站点副本或资产元数据。请参阅 [AEM 翻译框架引导连接器](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector)，查看使用 AEM 翻译框架的示例代码，它是翻译连接器的首选实施。


有用的文档
--------------------

Experience Manager as a Cloud Service [文档](../overview/introduction.md)提供了有关在 AEM 中进行开发的有价值见解。以下是一些特定的技术主题和参考，您在实施 AEM 连接器时会发现它们很有用：

* 具有良好注释的代码的 Adobe Consulting Services (ACS) [AEM 示例](https://adobe-consulting-services.github.io/acs-aem-samples/)，可帮助指导 AEM 开发人员
* 本文的“常见集成模式”部分中的各种文档链接

社区资源
--------------------

除了上述静态文档之外，Adobe 和 AEM 社区还提供了资源来帮助将连接器推向市场：

* Adobe 社区的 [AEM 论坛](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html)是一个活动站点，您的同行可以在这里提出和回答问题
* 为某些合作伙伴级别提供了其他 Adobe 技术资源。了解有关 [Adobe Exchange Program](https://partners.adobe.com/exchangeprogram/experiencecloud) 的更多信息。
* 如果您的组织希望获得实施帮助，请考虑 Adobe 的[专业服务](https://www.adobe.com/marketing-cloud/service-support/professional-consulting-training.html)团队或参阅[解决方案合作伙伴查找器](https://solutionpartners.adobe.com/home/partnerFinder.html)，获取 Adobe 全球合作伙伴列表

包结构规则
-----------------------

为了支持滚动部署，AEM as a Cloud Service 包（以连接器为例）在“不可变”和“可变”内容之间有严格的区分。应按包中的以下内容来明确区分各个包：

* `/apps`
* `/content` 和 `/conf`

连接器应遵守[本文](/help/implementing/developing/introduction/aem-project-content-package-structure.md)中所述的这些打包指南。现有连接器也应重构以符合要求。

此外，只有 Adobe 应将代码写入 `/libs`，而客户和合作伙伴则应将代码写入 `/apps`。

现有连接器可能也需要重构，以将可能曾放置 `/etc` 的任何配置移动到其他顶级文件夹中，例如 `/conf`。此重构是作为 AEM 6.5 的一部分完成的，并在 [AEM 6.5 文档](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)中进行了描述。

建议将大多数连接器代码放在 `/apps/connectors/<vendor>` 下，以便为具有多个连接器的客户提供干净的存储库结构。

云服务配置
-----------------------------

连接器实施的一个方面是支持连接器配置的代码。此代码会导致带有连接器名称的信息卡出现在“工具”>“操作”>“云服务”下。在单击时，会弹出一个[配置浏览器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)，客户可在其中选择要包含连接器配置的父文件夹。连接器的代码将生成一个包含所有必须配置的属性的表单，最终将值存储在 `/conf` 下的配置文件夹中。稍后可以在“站点属性”选项卡或“资产属性”选项卡下选择此文件夹。


上下文感知配置
-----------------------------

[上下文感知配置](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)允许跨不同的文件夹对配置进行分层，包括 `/libs`、`/apps`、`/conf` 以及 `/conf` 下的子文件夹。它支持继承，因此客户可以配置全局配置，同时对每个微型网站进行特定更改。由于可以将此功能用于云服务配置，因此，连接器代码应使用上下文感知配置 API 引用配置，而不是引用特定的配置节点。

如果在连接器中使用修改后的配置，则构建连接器以包含/合并对连接器提供的默认配置的任何未来更新与任何客户配置。请记住，在没有客户警告和同意的情况下更改自定义（如由客户更改的）内容或配置可能会破坏其连接器（或产生意外行为）。

编码最佳实践
----------------------

由于 AEM as a Cloud Service 是一种云原生解决方案，因此有一些准则可能会影响连接器的代码策略。有关更多详细信息，请参阅 [AEM as a Cloud Service 开发准则](/help/implementing/developing/introduction/development-guidelines.md)。

测试 AEM 连接器
-------------------------

应使用本地环境开发技术来创建新的连接器（或修改现有连接器）。合作伙伴团队将为 ISV 合作伙伴提供沙盒环境，他们可以在其中将 AEM 连接器部署到 vanilla 应用程序以确保它正常工作。
