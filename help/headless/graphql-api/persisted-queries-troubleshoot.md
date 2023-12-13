---
title: 持久的GraphQL查询疑难解答
description: 了解如何对Adobe Experience Manager as a Cloud Service中的持久GraphQL查询问题进行故障诊断。
feature: Content Fragments,GraphQL API
source-git-commit: c8ea9846600d1773e6f269973635f5338f31906f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# 持久的GraphQL查询疑难解答 {#troubleshoot-persisted-graphql-queries}

此 [操作中心](/help/operations/actions-center.md) 包括 **GraphQL持久查询错误** 警报。 这意味着当您的某个GraphQL持久查询引发错误时，系统会通知您。

为了帮助您排除和解决此类问题，我们对 *最常见* 失败的原因以及如何修复它们的步骤。

## 对内容片段模型的更改 {#changes-to-content-fragment-model}

如果GraphQL持久查询基于已过时的GraphQL类型，则查询可能会失败，通常是因为基础内容片段模型发生了更改。

出现这种情况有多种原因。 例如，当内容模型作者执行以下操作时：

* 删除或重新命名字段
* 更新为片段引用定义的允许模型
* 取消发布由其他模型引用的模型
* 其他行动和原因

要解决此问题，请执行以下操作之一：

* 应更新失败的持久查询以适应内容片段模型上的更改
* 或者应该还原导致问题的模型上的更改

## 未配置GraphQL端点 {#graphql-endpoint-not-configured}

当持久查询返回 `400` 或 `500` 错误代码，以及信息 `No suitable endpoint found`，这意味着在AEM环境中未配置任何GraphQL端点。

要更正此问题，请按照启用和发布端点的步骤进行操作 [在AEM中管理GraphQL端点](/help/headless/graphql-api/graphql-endpoint.md).

## GraphQL持久查询URL中缺少路径 {#missing-path-query-url}

如果持久查询返回 `400` 或 `500` 包含信息的错误代码 `Suffix: '/' does not contain a path`，则在调用GraphQL servlet时没有路径后缀。

模式应为 `/graphql/execute.json/thePath`.

## 由于IP允许列表而被阻止 {#blocked-due-to-ip-allow-list}

在这种情况下，查询将返回 `405` 错误代码。

这不是特定于GraphQL的内容。 请参阅知识库文章 [不允许出现405错误](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-20824.html).

## 被Dispatcher阻止 {#blocked-dispatcher}

如果GraphQL端点返回 `404` 发布以下内容时出错： `POST` 请求，这意味着GraphQL查询在Dispatcher级别被阻止，并且端点需要手动启用。

默认情况下不应出现这种情况，但自定义Dispatcher配置可能会导致此问题。 查看下的更多信息 [Dispatcher — 使用AEM Headless进行端点配置](/help/headless/deployment/dispatcher.md).
