---
title: 实施 AEM 连接器
description: 实施 AEM 连接器
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 10%

---

实施 AEM 连接器
=============================

下面提供了构建 [AEM 连接器](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html)的有用参考，应结合有关[提交](submit.md)和[维护](maintain.md)连接器的指导阅读这些参考。

请注意，可通过 [Adobe交换计划](https://partners.adobe.com/exchangeprogram/experiencecloud).

常见集成模式
---------------------------

AEM是一款先进的web体验管理解决方案，提供了许多潜在的集成领域。 常见的集成模式包括：

* 将数据从外部系统提取到AEM。 例如，从CRM导出联系信息，以将其提供给访问AEM支持的网站的更广泛受众。  实施应使用Sling [计划作业](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，这可保证即使容器关闭，也会执行作业。 代码应设计为假定该作业可能多次触发。
* 将数据从AEM导出到外部系统。 例如，在以AEM为后盾的网站上向CRM提交了新闻稿订阅设置。
* 从AEM检索资产。 例如，引用存储在AEM Assets中的资产的外部内容管理系统(CMS)。 或者，再比如PIM系统链接到AEM Assets中的图像。
* 在AEM基础架构中存储资产。 例如，在AEM Assets中存储已批准资产的营销资源管理(MRM)系统。
* 配置和渲染自定义UI组件。 例如，允许作者拖放视频组件并配置要在实时网站上播放的特定视频。
* 通过合作伙伴服务对资产执行操作。 例如，在发布页面时向视频平台发送资产。
* 在AEM管理控制台中分析网站、页面或资产。 例如，为现有页面或未发布页面提供SEO推荐。
* 对由外部服务维护的用户数据的页面级访问。 例如，利用人口统计信息对网站体验进行个性化。 阅读有关ContextHub的信息，ContextHub是用于存储、处理和呈现上下文数据的框架。
* 翻译网站副本或资产元数据。 请参阅 [AEM Translation FrameworkBootstrap连接器](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) 例如，使用AEM翻译框架的代码示例，这是翻译连接器的首选实施。


有用文档
--------------------

Experience Manageras a Cloud Service [文档](../overview/introduction.md) 为在AEM中进行开发提供了有价值的分析。 以下是在实施AEM连接器时可能会发现有用的一些特定技术主题和参考：

* Adobe咨询服务(ACS) [AEM示例](http://adobe-consulting-services.github.io/acs-aem-samples/) 提供了评论良好的代码以帮助教育AEM开发人员
* 本文“常用集成模式”部分中的各种文档链接

社区资源
--------------------

除了上述静态文档之外，Adobe和AEM社区还提供资源来帮助将连接器推向市场：

* Adobe社区 [AEM论坛](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) 是您的同行在其中提问和回答问题的活动网站
* 其他Adobe技术资源适用于特定合作伙伴级别。 进一步了解 [Adobe交换计划](https://partners.adobe.com/exchangeprogram/experiencecloud).
* 如果贵组织希望获得实施帮助，请考虑 Adobe 的[专业服务](http://www.adobe.com/cn/marketing-cloud/service-support/professional-consulting-training.html)团队或参阅[解决方案合作伙伴查找器](https://solutionpartners.adobe.com/home/partnerFinder.html)，获取 Adobe 全球合作伙伴列表

包结构规则
-----------------------

为了支持滚动部署，AEMas a Cloud Service包（例如连接器）在“不可变”和“可变”内容之间有严格的分隔。 应将包清晰地分隔为以下两个包：

* `/apps`
* `/content` 和 `/conf`

连接器应遵循这些包装准则，如 [本文](/help/implementing/developing/introduction/aem-project-content-package-structure.md). 还应对现有连接器进行重构以符合要求。

此外，只有Adobe才应将代码写入 `/libs`，客户和合作伙伴将向 `/apps`.

可能还需要重构现有连接器，以移动一旦放置好的任何配置 `/etc` 到其他顶级文件夹，例如 `/conf`. 此重组是作为AEM 6.5的一部分完成的，在 [AEM 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html).

建议将大多数连接器代码置于 `/apps/connectors/<vendor>` 为具有多个连接器的客户推广干净的存储库结构。

Cloud Services配置
-----------------------------

连接器实现的一个方面是支持连接器配置的代码。 此代码会导致在“工具”>“操作”>“Cloud Services”下显示带有连接器名称的信息卡。 单击后， [配置浏览器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) 弹出窗口，其中客户选择要包含连接器配置的父文件夹。 连接器代码应生成一个包含所有必须配置的属性的表单，最终将值存储在下的配置文件夹中 `/conf`. 稍后可以在站点属性选项卡或资产属性选项卡下选择此文件夹。


上下文感知配置
-----------------------------

[上下文感知配置](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 允许跨不同文件夹进行层配置，包括 `/libs`, `/apps`, `/conf` 子文件夹 `/conf`. 它支持继承，以便客户在对每个微型站点进行特定更改时能够配置全局配置。 由于此功能可用于Cloud Services配置，因此连接器代码应使用上下文感知配置API引用配置，而不是引用特定配置节点。

如果连接器中使用了经过修改的配置，请设计连接器以处理包括/合并连接器提供的默认配置的任何未来更新以及任何客户配置。 请记住，在未经客户警告和同意的情况下更改自定义（如客户更改的）内容或配置，可能会使用其Connector中断（或创建意外行为）。

编码最佳实践
----------------------

由于AEMas a Cloud Service是云原生解决方案，因此有一些准则可能会影响连接器的代码策略。 请参阅 [AEMas a Cloud Service开发准则](/help/implementing/developing/introduction/development-guidelines.md) 以了解更多详细信息。

测试AEM Connector
-------------------------

应使用本地环境开发技术创建新连接器（或修改现有连接器）。 合作伙伴团队将为ISV合作伙伴提供一个沙盒环境，在该环境中，他们可以将其AEM Connector部署到原版应用程序，以确保它正常工作。
