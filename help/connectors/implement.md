---
title: 实施 AEM 连接器
description: 实施 AEM 连接器
translation-type: tm+mt
source-git-commit: b77113ccc55f2063c684d49e2babdd7563b9d6fc
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 8%

---


实施 AEM 连接器
=============================

下面提供了构建 [AEM 连接器](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html)的有用参考，应结合有关[提交](submit.md)和[维护](maintain.md)连接器的指导阅读这些参考。

请注意，可以通过[AdobeExchange项目](https://partners.adobe.com/exchangeprogram/experiencecloud)获取AEM的开发人员许可证。

常见集成模式
---------------------------

AEM是一款先进的Web体验管理解决方案，可优惠许多潜在的集成领域。 常见集成模式包括：

* 将数据从外部系统拉入AEM。 例如，从CRM导出联系信息，以便更广泛的受众访问AEM支持的网站。  实施应使用Sling的[计划作业](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，这保证即使容器关闭也执行作业。 代码应设计为假定可以多次触发作业。
* 将数据从AEM导出到外部系统。 例如，在以AEM为后盾的网站上向CRM提交的Newsletter订阅设置。
* 从AEM检索资产。 例如，引用存储在AEM Assets中的资产的外部内容管理系统(CMS)。 或者，作为另一个示例，PIM系统链接到AEM Assets中的图像。
* 将资源存储在AEM基础结构中。 例如，营销资源管理(MRM)系统在AEM Assets中存储已批准的资产。
* 配置和渲染自定义UI组件。 例如，允许作者拖放视频组件并配置要在实时站点上播放的特定视频。
* 通过合作伙伴服务处理资产。 例如，在发布页面时向视频平台发送资产。
* 在AEM管理控制台中分析站点、页面或资产。 例如，为现有或未发布的页面进行SEO推荐。
* 对由外部服务维护的用户数据的页面级访问。 例如，利用人口统计信息来个性化网站体验。 阅读有关ContextHub的信息，ContextHub是用于存储、操作和呈现上下文数据的框架。
* 正在翻译网站副本或资产元数据。 有关使用AEM Translation Framework（首选实现的翻译连接器）的示例代码，请参阅[AEM Translation FrameworkBootstrap连接器](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector)。


实用文档
--------------------

Experience Manager作为Cloud Service[文档](../overview/introduction.md)提供了在AEM中开发的宝贵洞察。 以下是实施AEM连接器时可能会发现有用的一些特定技术主题和参考：

* Adobe咨询服务(ACS)[AEM示例](http://adobe-consulting-services.github.io/acs-aem-samples/)，以获取有关可帮助教育AEM开发人员的注释良好的代码
* 本文“常用集成模式”部分中的各种文档链接

社区资源
--------------------

除了上述静态文档之外，Adobe和AEM社区优惠资源还可帮助将连接器推向市场：

* Adobe社区的[AEM论坛](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html)是一个活动站点，您的同行在该站点上提问并回答问题
* 某些合作伙伴级别还提供其他Adobe技术资源。 了解有关[AdobeExchange项目](https://partners.adobe.com/exchangeprogram/experiencecloud)的更多信息。
* 如果贵组织希望获得实施帮助，请考虑 Adobe 的[专业服务](http://www.adobe.com/cn/marketing-cloud/service-support/professional-consulting-training.html)团队或参阅[解决方案合作伙伴查找器](https://solutionpartners.adobe.com/home/partnerFinder.html)，获取 Adobe 全球合作伙伴列表

包结构规则
-----------------------

为了支持滚动部署，AEM作为Cloud Service包（其中连接器为示例）在“不可变”和“可变”内容之间有严格的分隔。 软件包应完全分开，其中包括：

* `/apps`
* `/content` 和 `/conf`

连接器应遵守这些封装准则，本文[](/help/implementing/developing/introduction/aem-project-content-package-structure.md)中对这些准则进行了说明。 还应重新调整现有连接器的结构以符合要求。

此外，只有Adobe才应将代码写入`/libs`，客户和合作伙伴应将代码写入`/apps`。

可能还需要重构现有连接器，以将曾经放置`/etc`的任何配置移动到其他顶级文件夹，如`/conf`。 此重组是作为AEM 6.5的一部分完成的，在[AEM 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)中有介绍。

建议将大多数连接器代码放在`/apps/connectors/<vendor>`下，以便为具有多个连接器的客户提供简洁的存储库结构。

Cloud Services配置
-----------------------------

连接器实现的一个方面是支持连接器配置的代码。 此代码使具有连接器名称的卡显示在“工具”>“操作”>“Cloud Services”下。 单击后，将弹出[配置浏览器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)，客户选择父文件夹以包含连接器配置。 连接器的代码应生成一个包含所有必须配置的属性的表单，最终将这些值存储在`/conf`下的配置文件夹中。 以后可以在站点属性选项卡或资产属性选项卡下选择此文件夹。


上下文感知配置
-----------------------------

[上下文感知配](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 置 — 跨不同文件夹(包括下面的子文件夹 `/libs`、 `/apps`和子文 `/conf` 件夹)进行图层配 `/conf`置。它支持继承，以便客户在对每个微型站点进行特定更改时配置全局配置。 由于可以将此功能用于Cloud Services配置，因此连接器代码应使用上下文感知配置API引用配置，而不是引用特定配置节点。

如果连接器中使用了修改的配置，请设计连接器以处理将来对连接器提供的默认配置的任何更新包括/合并到任何客户配置。 请记住，未经客户警告和同意而更改自定义（如客户更改的）内容或配置可能会使用其连接器中断（或造成意外行为）。

编码最佳实践
----------------------

由于AEM作为Cloud Service是云本机解决方案，因此有一些准则可能会影响连接器的代码策略。 有关更多详细信息，请参阅[AEM作为Cloud Service开发准则](/help/implementing/developing/introduction/development-guidelines.md)。

测试AEM Connector
-------------------------

应使用本地环境开发技术创建新连接器（或修改现有连接器）。 合作伙伴团队将为ISV合作伙伴提供沙箱环境，在沙箱中，他们可以将AEM Connector部署到vanilla应用程序，以确保其正常工作。
