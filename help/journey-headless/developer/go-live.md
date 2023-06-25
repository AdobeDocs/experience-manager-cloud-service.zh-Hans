---
title: 如何使用 Headless 应用程序上线
description: 在 AEM Headless 开发人员历程的这一部分中，了解如何通过在 Git 中获取本地代码并将其移动到 CI/CD 管道的 Cloud Manager Git 来实时部署 Headless 应用程序。
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 94%

---

# 如何使用 Headless 应用程序上线 {#go-live}

在 [AEM Headless 开发人员历程](overview.md)的这一部分中，了解如何通过在 Git 中获取本地代码并将其移动到 CI/CD 管道的 Cloud Manager Git 来实时部署 Headless 应用程序。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 历程的上一个文档[如何融于一起 - 您的应用程序和 AEM Headless 中的内容](put-it-all-together.md) 中，您已了解如何使用 AEM 开发工具融合您项目的所有方面。

本文基于这些基础知识编写，以便您了解如何准备您自己的 AEM Headless 项目以上线。

## 目标 {#objective}

本文档可帮助您了解 AEM Headless 发布管道，以及在通过您的应用程序上线之前必须了解的性能注意事项。

* 在启动前保护和扩展您的应用程序
* 监控性能和调试问题

<!-- Alexandru: this is a bit redundant, to review again later

## Prepare your AEM Headless Application for Go-Live {#prepare-your-aem-headless-application-for-golive}

-->
要让您的 AEM Headless 应用程序准备好启动，请遵循下面概述的最佳实践。

## 在启动前保护和扩展您的 Headless 应用程序 {#secure-and-scale-before-launch}

1. 使用 GraphQL 请求配置[基于令牌的身份验证](/help/headless/security/authentication.md)
1. 配置[缓存](/help/implementing/dispatcher/caching.md)。

## 模型结构与 GraphQL 输出 {#structure-vs-output}

* 避免创建输出超过 15kb JSON（以 gzip 格式压缩）的查询。长 JSON 文件是客户端应用程序要分析的资源密集型文件。
* 避免超过五个嵌套级别的片段层级。其他级别会使内容作者难以考虑其更改产生的影响。
* 使用多对象查询而不是在模型中使用依赖项层级对查询进行建模。这允许具有更大的长期灵活性，无需更改许多内容，即可重新构建JSON输出。

## 最大程度地提高 CDN 缓存命中率 {#maximize-cdn}

* 不要使用直接 GraphQL 查询，除非您从表面请求实时内容。
   * 尽可能使用持久查询。
   * 提供超过 600 秒的 CDN TTL，以便 CDN 缓存它们。
   * AEM 可以计算模型更改对现有查询的影响。
* 在低内容更改率和高内容更改率之间拆分JSON文件/GraphQL查询，以便减少到CDN的客户端流量并分配更高的TTL。 这可以最大程度地减少使用源服务器重新验证 JSON 的 CDN。
* 要主动使来自 CDN 的内容无效，请使用软清除。这可让 CDN 重新下载内容，而不会导致缓存未命中。

## 缩短下载 Headless 内容的时间 {#improve-download-time}

* 确保 HTTP 客户端使用 HTTP/2。
* 确保 HTTP 客户端接受 gzip 的标头请求。
* 最大程度地减少用于托管 JSON 的域和引用的构件的数量。
* 利用 `Last-modified-since` 刷新资源。
* 使用 JSON 文件中的 `_reference` 输出开始下载资产，而无需分析完整的 JSON 文件。

## 部署到生产 {#deploy-to-production}

在确保一切都经过测试并正常工作后，即可将代码更新推送到 [Cloud Manager 中的集中式 Git 存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)。

在将更新上传到 Cloud Manager 后，可以使用 [Cloud Manager 的 CI/CD 管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)将这些更新部署到 AEM as a Cloud Service。

您可以利用 Cloud Manager CI/CD 管道开始部署您的代码，[此处](/help/implementing/deploying/overview.md)对这方面进行了广泛介绍。

## 性能监控 {#performance-monitoring}

要让用户在使用 AEM Headless 应用程序时获得最佳体验，请务必监控关键性能指标，详情如下：

* 验证应用程序的预览版和生产版
* 验证当前服务可用性状态的 AEM 状态页面
* 访问性能报告
   * 交付性能
      * CDN（快速）性能 – 检查调用次数、缓存率、错误率和负载流量
      * 源服务器 – 调用次数、错误率、CPU 负载、负载流量
   * 创作性能
      * 检查用户数、请求数和负载
* 访问应用程序和空间特定的性能报告
   * 在服务器启动后，检查一般指标是否为绿色/橙色/红色，然后识别具体的应用程序问题
   * 打开上面过滤到应用程序或空间的相同报告（例如，Photoshop 桌面、付费专区）
   * 使用 Splunk 日志 API 访问服务和应用程序性能
   * 如果还有其他问题，请联系客户支持。

## 疑难解答 {#troubleshooting}

### 调试 {#debugging}

将这些最佳实践用作常规调试方法：

* 使用应用程序的预览版本验证功能和性能
* 使用应用程序的生产版本验证功能和性能
* 使用内容片段编辑器的 JSON 预览版进行验证
* 检查客户端应用程序中的 JSON，确定是否存在客户端应用程序或交付问题
* 使用 GraphQL 检查 JSON，确认是否存在与缓存内容或 AEM 相关的问题

### 借助支持记录错误 {#logging-a-bug-with-support}

要在您需要进一步帮助的情况下通过支持高效地记录错误，请执行以下操作：

* 如有必要，可拍摄问题屏幕快照
* 记录重现问题的方法
* 记录问题重现的内容
* 通过 AEM 支持门户以适当的优先级记录问题

## 历程结束 - 是吗？ {#journey-ends}

恭喜！您已完成 AEM Headless 开发人员历程！您现在应了解以下内容：

* Headless 和 Headful 内容交付之间的区别。
* AEM 的 Headless 功能。
* 如何编排 AEM Headless 项目。
* 如何在 AEM 中创建 Headless 内容。
* 如何在 AEM 中检索和更新 Headless 内容。
* 如何使用 AEM Headless 项目上线。
* 上线后需要执行的操作。

您要么已启动第一个 AEM Headless 项目，要么已具备执行此操作所需的所有知识。做得好！

### 探究单页应用程序 {#explore-spa}

但 AEM 中的 Headless 存储不需要止步于此。您可能还记得，在[历程的快速入门部分](getting-started.md#integration-levels)中，我们简要讨论了 AEM 如何支持 Headless 交付和传统全栈模型，并支持结合了两者优点的混合模型。

如果您的项目需要这种灵活性，请继续进行历程的可选附加部分[如何使用 AEM 创建单页应用程序 (SPA)。](create-spa.md)

## 其他资源 {#additional-resources}

* [到 AEM as a Cloud Service 的部署概述](/help/implementing/deploying/overview.md)
* [使用 Cloud Manager 部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [将 Cloud Manager Git 存储库与外部 Git 存储库集成，并将项目部署到 AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=zh-Hans)
