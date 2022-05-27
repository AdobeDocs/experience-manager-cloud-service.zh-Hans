---
title: 如何使用您的无头应用程序
description: 在AEM无头开发人员历程的这一部分中，了解如何通过在Git中提取本地代码并将其移至Cloud Manager Git以用于CI/CD管道来实时部署无头应用程序。
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# 如何使用您的无头应用程序 {#go-live}

在 [AEM Headless开发人员历程](overview.md)，了解如何在Git中获取本地代码并将其移至Cloud Manager Git以用于CI/CD管道，从而实时部署无头应用程序。

## 迄今为止的故事 {#story-so-far}

在AEM无头历程的上一个文档中， [如何将所有内容整合在一起 — 在AEM Headless中查看您的应用程序和内容](put-it-all-together.md) 您学习了如何使用AEM开发工具将项目的所有方面整合在一起。

本文基于这些基础知识，以便您了解如何准备自己的AEM无头项目以投入使用。

## 目标 {#objective}

本文档可帮助您了解AEM无头发布管道以及在使用应用程序之前必须注意的性能注意事项。

* 在启动之前保护并扩展您的应用程序
* 监视性能和调试问题

<!-- Alexandru: this is a bit redundant, to review again later

## Prepare your AEM Headless Application for Go-Live {#prepare-your-aem-headless-application-for-golive}

-->
要使您的AEM无头应用程序准备好启动，请遵循下面概述的最佳实践。

## 在启动之前保护和扩展您的无头应用程序 {#secure-and-scale-before-launch}

1. 配置 [基于令牌的身份验证](/help/headless/security/authentication.md) 使用GraphQL请求
1. 配置 [缓存](/help/implementing/dispatcher/caching.md).

## 模型结构与GraphQL输出 {#structure-vs-output}

* 避免创建输出超过15kb JSON（gzip压缩）的查询。 较长的JSON文件是需要大量资源才能解析客户端应用程序。
* 避免片段层级的嵌套级别超过5个。 其他级别使内容作者很难考虑其更改的影响。
* 使用多对象查询，而不是在模型内使用依赖关系层次结构建模查询。 这样，在重构JSON输出方面就具有了更大的长期灵活性，而无需进行大量内容更改。

## 最大化CDN缓存点击率 {#maximize-cdn}

* 除非您从表面请求实时内容，否则请勿使用直接GraphQL查询。
   * 尽可能使用持久查询。
   * 为CDN提供超过600秒的CDN TTL，以便CDN进行缓存。
   * AEM可以计算模型更改对现有查询的影响。
* 在低内容更改率和高内容更改率之间拆分JSON文件/GraphQL查询，以减少客户端对CDN的流量并分配更高的TTL。 这样可以最大限度地减少CDN使用源服务器重新验证JSON的情况。
* 要主动使来自CDN的内容失效，请使用软清除。 这样，CDN便可重新下载内容，而不会导致缓存丢失。

## 缩短下载无头内容的时间 {#improve-download-time}

* 确保HTTP客户端使用HTTP/2。
* 确保HTTP客户端接受gzip的标头请求。
* 最大限度地减少用于托管JSON和引用对象的域数。
* 利用 `Last-modified-since` 刷新资源。
* 使用 `_reference` JSON文件中的输出，以便开始下载资产，而无需解析完整的JSON文件。

## 部署到生产环境 {#deploy-to-production}

确保所有内容均已测试并正常运行后，即可将代码更新推送到 [Cloud Manager中的集中式Git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

将更新上传到Cloud Manager后，可以使用将这些更新部署到AEMas a Cloud Service [Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

您可以利用Cloud Manager CI/CD管道来开始部署代码，该管道已得到广泛介绍 [此处](/help/implementing/deploying/overview.md).

## 性能监控 {#performance-monitoring}

为使用户在使用AEM无头应用程序时获得最佳体验，您务必要监控关键性能量度，如下所述：

* 验证应用程序的预览和生产版本
* 验证AEM状态页面以了解当前服务可用性状态
* 访问性能报告
   * 交付性能
      * CDN（快速）性能 — 检查调用数、缓存率、错误率和有效负载流量
      * 源服务器 — 调用数、错误率、CPU负载、负载流量
   * 创作性能
      * 检查用户数、请求数和加载数
* 访问特定于应用程序和空间的性能报表
   * 服务器启动后，检查常规量度是否为绿色/橙色/红色，然后确定特定的应用程序问题
   * 打开上面按应用程序或空间过滤的相同报表(例如Photoshop桌面版、付费专区)
   * 使用Splunk日志API访问服务和应用程序性能
   * 如果存在其他问题，请联系客户支持。

## 疑难解答 {#troubleshooting}

### 调试 {#debugging}

按照以下最佳实践作为调试的一般方法：

* 使用应用程序的预览版本验证功能和性能
* 使用应用程序的生产版本验证功能和性能
* 使用内容片段编辑器的JSON预览进行验证
* Inspect客户端应用程序中的JSON，以检查客户端应用程序或交付问题是否存在
* Inspect使用GraphQL检查是否存在与缓存内容或AEM相关的问题

### 记录支持的错误 {#logging-a-bug-with-support}

为了在您需要进一步帮助时，通过支持部门高效地记录错误，请执行以下步骤：

* 如有必要，请拍摄问题的屏幕截图
* 记录重现问题的方法
* 记录问题所重现的内容
* 通过具有相应优先级的AEM支持门户记录问题

## 历程结束了？ {#journey-ends}

恭喜！ 您已完成AEM Headless开发人员历程! 您现在应该了解：

* 无头内容和有头内容交付之间的区别。
* AEM无头功能。
* 如何组织和AEM Headless项目。
* 如何在AEM中创建无标题内容。
* 如何在AEM中检索和更新无标题内容。
* 如何使用AEM Headless项目进行实时。
* 上线后该怎么办。

您已经启动了您的第一个AEM Headless项目，或者现在掌握了执行此操作所需的所有知识。 干得好！

### 浏览单页应用程序 {#explore-spa}

不过，AEM中的无头店不需要停在这里。 您可能记得 [入门指南部分](getting-started.md#integration-levels) 我们简要讨论了AEM如何不仅支持无头交付和传统的全栈模型，而且还支持结合两者优点的混合模型。

如果您的项目需要这种灵活性，请继续进行历程的可选附加部分， [如何使用AEM创建单页应用程序(SPA)。](create-spa.md)

## 其他资源 {#additional-resources}

* [部署到AEMas a Cloud Service概述](/help/implementing/deploying/overview.md)
* [使用Cloud Manager部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [将Cloud Manager Git存储库与外部Git存储库集成，并将项目部署到AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)
