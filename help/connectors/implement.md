---
title: 实施AEM Connector
description: 实施AEM Connector
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f

---


实施AEM Connector
=============================

下面提供了构建 [AEM Connectors的有用参考](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) ，应结合提交和维护连接器的指导 [一起阅读](submit.md)[这些参考](maintain.md) 。

请注意，可通过 [Adobe Exchange计划获得AEM的开发人员许可证](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html)。

常见集成模式
---------------------------

AEM是一款先进的Web体验管理解决方案，它提供许多潜在的集成领域。 常见集成模式包括：

* 将外部系统中的数据拉入AEM。 例如，从CRM导出联系信息，以便向访问以AEM为后盾的网站的更多受众提供该信息。  实施应使用Sling的 [Scheduled Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，这保证即使容器关闭也执行作业。 代码应设计为假定作业可能多次被触发。
* 将数据从AEM导出到外部系统。 例如，新闻稿订阅设置已在以AEM为后盾的网站上提交到CRM。
* 从AEM检索资产。 例如，引用存储在AEM资产中的资产的外部内容管理系统(CMS)。 或者，作为另一个示例，PIM系统链接到AEM资产中的图像。
* 在AEM基础结构中存储资产。 例如，将已批准的资产存储在AEM资产中的Marketing Resource Management(MRM)系统。
* 配置和呈现自定义UI组件。 例如，允许作者拖放视频组件并配置特定视频以在实时站点上播放。
* 使用合作伙伴服务处理资产。 例如，在发布页面时将资产发送到视频平台。
* 在AEM管理控制台中分析站点、页面或资产。 例如，为现有或未发布的页面提供SEO推荐。
* 对由外部服务维护的用户数据的页面级访问。 例如，利用人口统计信息来个性化网站体验。 阅读ContextHub，这是一个用于存储、操作和呈现上下文数据的框架。
* 翻译站点副本或资产元数据。 请参阅 [AEM Translation Framework Bootstrap Connector](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) ，以了解使用AEM Translation Framework（这是翻译连接器的首选实现）的示例代码。


实用文档
--------------------

Experience Manager作为云服务文档 [提供](../overview/introduction.md) AEM中开发的宝贵洞察。 以下是实施AEM连接器时可能会发现有用的一些特定技术主题和参考：

* Adobe Consulting Services(ACS) [AEM示例](http://adobe-consulting-services.github.io/acs-aem-samples/) ，用于获得注释良好的代码以帮助教育AEM开发人员
* 本文“常见集成模式”部分中的各种文档链接

社区资源
--------------------

除了上述静态文档之外，Adobe和AEM社区还提供资源，帮助将连接器推向市场：

* Adobe社区的 [AEM论坛](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) ，是一个活跃的站点，您的同行在该站点上提问并回答问题
* 某些合作伙伴级别提供其他Adobe技术资源。 进一步了解 [Adobe Exchange计划](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html)。
* 如果贵组织希望获得实施帮助，请考虑Adobe的 [Professional Services](http://www.adobe.com/marketing-cloud/service-support/professional-consulting-training.html) Team或查看 [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html) （解决方案合作伙伴查找器），获取Adobe全球合作伙伴列表

包结构规则
-----------------------

为了支持滚动部署，AEM作为云服务包（例如，连接器），在“不可变”和“可变”内容之间有严格的分隔。 应将包完全分开，它们包括：

* `/apps`
* `/content` 和 `/conf`

连接器应遵守本文所述的这些封装 [准则](/help/implementing/developing/introduction/aem-project-content-package-structure.md)。 现有连接器也应进行重构以符合要求。

此外，只有Adobe才应将代码写入， `/libs`客户和合作伙伴应将代码写入 `/apps`。

可能还需要重构现有连接器以移动任何可能已放入其他顶级文件夹 `/etc` 的配置，例如 `/conf`。 AEM文档中对此进 [行了说明](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)。

建议将大部分连接器代码放在下面，以便为具有多 `/apps/connectors/<vendor>` 个连接器的客户提供简洁的存储库结构。

云服务配置
-----------------------------

连接器实现的一个方面是支持连接器配置的代码。 此代码会导致在“工具”>“操作”>“云服务”下显示具有连接器名称的卡。 单击后，将弹出一个配置浏览器，客户在其中选择要包含连接器配置的父文件夹。 连接器的代码应生成一个包含必须配置的所有属性的表单，最终将这些值存储在下的配置文件夹中 `/conf`。 稍后可以在站点属性选项卡或资产属性选项卡下选择此文件夹。


上下文感知配置
-----------------------------

[上下文感知配置](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) ，允许跨不同文件夹（包括下面的文件夹、子文件夹和子文件夹） `/libs`进行图层配置 `/apps``/conf``/conf`。 它支持继承，这样客户就可以在为每个微型站点进行特定更改时配置全局配置。 由于可以将此功能用于云服务配置，因此连接器代码应使用上下文感知配置API引用配置，而不是引用特定配置节点。

如果连接器中使用了经过修改的配置，则应构建连接器以处理将来对连接器提供的默认配置的任何更新与任何客户配置进行包括／合并。 请记住，未经客户警告和同意而更改自定义（如客户更改）内容或配置可能会使用其Connector中断（或创建意外行为）。

编码最佳实践
----------------------

由于AEM作为云服务是云本机解决方案，因此存在一些可能影响连接器代码策略的准则。 有关更 [多详细信息，请参阅AEM云服务开发指南](/help/implementing/developing/introduction/development-guidelines.md) 。

测试AEM Connector
-------------------------

应使用本地环境开发技术创建新连接器（或修改现有连接器）。 合作伙伴团队将为ISV合作伙伴提供沙箱环境，在沙箱环境中，他们可以将其AEM Connector部署到vanila应用程序，以确保其正常工作。
