---
title: 实施 AEM 连接器
description: 实施 AEM 连接器
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 8%

---


实施 AEM 连接器
=============================

下面提供了构建 [AEM 连接器](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html)的有用参考，应结合有关[提交](submit.md)和[维护](maintain.md)连接器的指导阅读这些参考。

请注意，可通过Adobe Exchange项目获取AEM的开 [发人员许可证](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html)。

常见集成模式
---------------------------

AEM是一款先进的Web体验管理解决方案，它优惠了许多潜在的集成领域。 常见集成模式包括：

* 将外部系统中的数据拉入AEM。 例如，从CRM导出联系信息，使访问AEM支持的网站的更广大受众都可以使用这些信息。  实施应使用Sling的 [Scheduled Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，这保证即使容器下线，也执行作业。 代码应设计为假定作业可能被多次触发。
* 将数据从AEM导出到外部系统。 例如，在以AEM为后盾的网站上提交到CRM的Newsletter订阅设置。
* 从AEM检索资产。 例如，引用存储在AEM资产中的资产的外部内容管理系统(CMS)。 或者作为另一个示例，PIM系统链接到AEM资产中的图像。
* 在AEM基础结构中存储资产。 例如，营销资源管理(MRM)系统在AEM资产中存储已批准的资产。
* 配置和呈现自定义UI组件。 例如，允许作者拖放视频组件并配置特定视频以在实时站点上播放。
* 通过合作伙伴服务处理资产。 例如，在发布页面时将资产发送到视频平台。
* 在AEM管理控制台中分析站点、页面或资产。 例如，为现有或未发布的页面进行SEO推荐。
* 对由外部服务维护的用户数据的页面级访问。 例如，利用人口统计信息来个性化网站体验。 阅读ContextHub，它是一个用于存储、操作和呈现上下文数据的框架。
* 转换站点副本或资产元数据。 请参 [阅AEM Translation Framework Bootstrap Connector](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) ，以获取使用AEM Translation Framework（翻译连接器的首选实现）的示例代码。


实用文档
--------------------

Experience Manager作为云服务文档 [提供](../overview/introduction.md) 了有关在AEM中进行开发的宝贵见解。 以下是实施AEM连接器时可能有用的一些特定技术主题和参考：

* Adobe Consulting Services(ACS)AEM [示例](http://adobe-consulting-services.github.io/acs-aem-samples/) ，用于获得有条理的代码，以帮助教育AEM开发人员
* 本文“常见集成模式”部分中的各种文档链接

社区资源
--------------------

除了上述静态文档之外，Adobe和AEM社区优惠资源还可帮助将连接器推向市场：

* Adobe社区的AEM论 [坛是](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) 一个活跃的站点，您的同行在该站点提问并回答问题
* 某些合作伙伴级别提供其他Adobe技术资源。 进一步了 [解Adobe Exchange项目](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html)。
* 如果贵组织希望获得实施帮助，请考虑 Adobe 的[专业服务](http://www.adobe.com/cn/marketing-cloud/service-support/professional-consulting-training.html)团队或参阅[解决方案合作伙伴查找器](https://solutionpartners.adobe.com/home/partnerFinder.html)，获取 Adobe 全球合作伙伴列表

包结构规则
-----------------------

为了支持滚动部署，AEM作为云服务包（其中连接器为示例），在“不可变”和“可变”内容之间有严格的分隔。 包应在以下两者之间清晰地分开：

* `/apps`
* `/content` 和 `/conf`

连接器应遵守本文所述的这些包装 [准则](/help/implementing/developing/introduction/aem-project-content-package-structure.md)。 还应重新调整现有连接器的结构，以符合要求。

此外，只有Adobe才应将代码写入， `/libs`客户和合作伙伴应将代码写入 `/apps`。

可能还需要重构现有连接器，才能移动任何曾经被放置到其他顶级文件夹 `/etc` 中的配置，例如 `/conf`。 这在AEM文档中 [有介绍](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)。

建议将大多数连接器代码放在下面，以便为 `/apps/connectors/<vendor>` 具有多个连接器的客户提供干净的存储库结构。

云服务配置
-----------------------------

连接器实现的一个方面是支持连接器配置的代码。 此代码会导致在“工具”>“操作”>“云服务”下显示带有连接器名称的卡。 单击时，将弹出一个配置浏览器，客户从中选择要包含连接器配置的父文件夹。 连接器的代码应生成一个包含所有必须配置的属性的表单，最终将这些值存储在配置文件夹下 `/conf`。 以后可以在站点属性选项卡或资产属性选项卡下选择此文件夹。


上下文感知配置
-----------------------------

[上下文感知配置](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 允许跨不同文件夹(包括下面的文件夹、子文 `/libs`件 `/apps`夹和子文 `/conf` 件夹)进行图层 `/conf`配置。 它支持继承，这样客户可以配置全局配置，同时对每个微型站点进行特定更改。 由于此功能可用于云服务配置，因此连接器代码应使用上下文感知配置API引用配置，而不是引用特定配置节点。

如果连接器中使用了修改后的配置，请设计连接器以处理将来对连接器提供的默认配置的任何更新与任何客户配置一起进行包括／合并。 请记住，未经客户警告和同意而更改自定义（如客户更改的）内容或配置，可能会使用其连接器中断（或造成意外行为）。

编码最佳实践
----------------------

由于AEM是云服务，它是云本机解决方案，因此有一些准则可能会影响连接器的代码策略。 有关 [更多详细信息，请参阅AEM](/help/implementing/developing/introduction/development-guidelines.md) a Cloud Service Development Guidelines。

测试AEM连接器
-------------------------

应使用本地环境开发技术创建新连接器（或修改现有连接器）。 合作伙伴团队将为ISV合作伙伴提供沙箱环境，在沙箱中，他们可以将AEM Connector部署到香草应用程序，以确保其正常工作。
