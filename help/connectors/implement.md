---
title: 实施 AEM 连接器
description: 实施 AEM 连接器
translation-type: tm+mt
source-git-commit: 69756d6831678151b0e8eb73db81113d49f17447
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 8%

---


实施 AEM 连接器
=============================

下面提供了构建 [AEM 连接器](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html)的有用参考，应结合有关[提交](submit.md)和[维护](maintain.md)连接器的指导阅读这些参考。

请注意，可以通过AEM交换项目获 [取Adobe的开发人员许可证](https://partners.adobe.com/exchangeprogram/experiencecloud)。

常见集成模式
---------------------------

AEM是一款先进的Web体验管理解决方案，它优惠了许多潜在的集成领域。 常见集成模式包括：

* 将数据从外部系统拉入AEM。 例如，从CRM导出联系信息，以便更广泛的受众访问AEM支持的网站。  实施应使用Sling的 [Scheduled Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)，这保证即使容器下线，也执行作业。 代码应设计为假定作业可能被多次触发。
* 将数据从AEM导出到外部系统。 例如，在AEM支持的网站上向CRM提交新闻稿订阅设置。
* 从AEM检索资产。 例如，引用存储在AEM Assets的资产的外部内容管理系统(CMS)。 或者作为另一个示例，PIM系统链接到AEM Assets的图像。
* 在AEM基础架构中存储资产。 例如，营销资源管理(MRM)系统在AEM Assets存储已批准的资产。
* 配置和呈现自定义UI组件。 例如，允许作者拖放视频组件并配置特定视频以在实时站点上播放。
* 通过合作伙伴服务处理资产。 例如，在发布页面时将资产发送到视频平台。
* 在AEM admin console中分析站点、页面或资产。 例如，为现有或未发布的页面进行SEO推荐。
* 对由外部服务维护的用户数据的页面级访问。 例如，利用人口统计信息来个性化网站体验。 阅读ContextHub，它是一个用于存储、操作和呈现上下文数据的框架。
* 转换站点副本或资产元数据。 请参阅AEM [Translation FrameworkBootstrap连接器](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) ，以了解使用AEM Translation Framework（这是翻译连接器的首选实现）的示例代码。


实用文档
--------------------

Experience Manager作为Cloud Service文 [档](../overview/introduction.md) ，为AEM的开发提供宝贵的洞察。 以下是实施AEM连接器时可能有用的一些特定技术主题和参考：

* Adobe咨询服务(ACS)AEM [示例](http://adobe-consulting-services.github.io/acs-aem-samples/) ，获得有条理的代码，帮助教育AEM开发人员
* 本文“常见集成模式”部分中的各种文档链接

社区资源
--------------------

除了上述静态文档之外，Adobe和AEM社区优惠资源还有助于将连接器推向市场：

* Adobe社区的AEM [论坛](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) 是一个活跃的站点，您的同行可在此提问并回答问题
* 某些合作伙伴级别提供其他Adobe技术资源。 进一步了解 [AdobeExchange项目](https://partners.adobe.com/exchangeprogram/experiencecloud)。
* 如果贵组织希望获得实施帮助，请考虑 Adobe 的[专业服务](http://www.adobe.com/cn/marketing-cloud/service-support/professional-consulting-training.html)团队或参阅[解决方案合作伙伴查找器](https://solutionpartners.adobe.com/home/partnerFinder.html)，获取 Adobe 全球合作伙伴列表

包结构规则
-----------------------

为了支持滚动部署，AEM作为Cloud Service包（其中连接器为示例），在“不可变”和“可变”内容之间有严格的分隔。 包应在以下两者之间清晰地分开：

* `/apps`
* `/content` 和 `/conf`

连接器应遵守本文所述的这些包装 [准则](/help/implementing/developing/introduction/aem-project-content-package-structure.md)。 还应重新调整现有连接器的结构，以符合要求。

此外，只有Adobe才应将代码写入， `/libs`客户和合作伙伴应将代码写入 `/apps`。

可能还需要重构现有连接器，才能移动任何曾经被放置到其他顶级文件夹 `/etc` 中的配置，例如 `/conf`。 AEM文档中对此进 [行了说明](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)。

建议将大多数连接器代码放在下面，以便为 `/apps/connectors/<vendor>` 具有多个连接器的客户提供干净的存储库结构。

Cloud Services配置
-----------------------------

连接器实现的一个方面是支持连接器配置的代码。 此代码会使具有连接器名称的卡显示在“工具”>“操作”>“Cloud Services”下。 单击时，将弹 [出一个配置](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) 浏览器，客户从中选择要包含连接器配置的父文件夹。 连接器的代码应生成一个包含所有必须配置的属性的表单，最终将这些值存储在配置文件夹下 `/conf`。 以后可以在站点属性选项卡或资产属性选项卡下选择此文件夹。


上下文感知配置
-----------------------------

[上下文感知配置](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 允许跨不同文件夹(包括下面的文件夹、子文 `/libs`件 `/apps`夹和子文 `/conf` 件夹)进行图层 `/conf`配置。 它支持继承，这样客户可以配置全局配置，同时对每个微型站点进行特定更改。 由于可以将此功能用于Cloud Services配置，因此连接器代码应使用上下文感知配置API引用配置，而不是引用特定配置节点。

如果连接器中使用了修改后的配置，请设计连接器以处理将来对连接器提供的默认配置的任何更新与任何客户配置一起进行包括／合并。 请记住，未经客户警告和同意而更改自定义（如客户更改的）内容或配置，可能会使用其连接器中断（或造成意外行为）。

编码最佳实践
----------------------

由于AEM作为Cloud Service是云本机解决方案，因此有一些准则可能会影响连接器的代码策略。 有关更 [多详细信息，请参阅AEM](/help/implementing/developing/introduction/development-guidelines.md) a s a A Pro开发指南。

测试AEM连接器
-------------------------

应使用本地环境开发技术创建新连接器（或修改现有连接器）。 合作伙伴团队将为ISV合作伙伴提供沙箱环境，在沙箱中，他们可以将AEM连接器部署到vanilla应用程序，以确保其正常工作。
