---
title: GraphQL 持久查询故障排除
description: 了解如何在 Adobe Experience Manager as a Cloud Service 中使用 GraphQL 持久查询排除故障。
feature: Headless, Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: ht
source-wordcount: '363'
ht-degree: 100%

---

# GraphQL 持久查询故障排除 {#troubleshoot-persisted-graphql-queries}

 [操作中心](/help/operations/actions-center.md) 包含 **GraphQL 持久查询错误** 警报。这意味着当您的某个 GraphQL 持久查询抛出错误时，您都会收到通知。

为了帮助您排除故障并解决此类问题，本页面介绍了 *最常见的* 故障原因以及如何修复这些问题的步骤。

## 内容片段模型的变更 {#changes-to-content-fragment-model}

当 GraphQL 持久查询基于过时的 GraphQL 类型时，它可能会失败，这通常是由于底层内容片段模型发生变化造成的。

此类错误可能因多种原因而发生。示例包括（该列表并不详尽），当内容片段模型的作者：

* 删除或重命名字段
* 更新 **模型类型** ，该模型类型定义了允许片段引用的模型
* 取消发布被其他模型引用的模型

要解决此类错误，您可以：

* 更新无法适应内容片段模型所做更改的持久查询
* 恢复导致该问题的模型更改

## GraphQL 端点未配置 {#graphql-endpoint-not-configured}

当持久查询返回 `404` 错误代码，以及信息 `No suitable endpoint found`，这意味着 AEM 环境上未配置 GraphQL 端点。

要解决此问题，请按照从中启用和发布端点的步骤进行操作 [在 AEM 中管理 GraphQL 端点](/help/headless/graphql-api/graphql-endpoint.md)。

## GraphQL 持久查询 URL 中缺少路径 {#missing-path-query-url}

如果持久查询返回 `400` 错误代码及信息 `Suffix: '/' does not contain a path`，调用 GraphQL servlet 时没有路径后缀。

模式应该是 `/graphql/execute.json/thePath`。

## 由于 IP 允许列表而被阻止 {#blocked-due-to-ip-allow-list}

在这种情况下，查询返回 `405` 错误代码。

这样的错误并不是 GraphQL 所特有的。请参阅 KB 文章 [405 错误不允许](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-20824)。

## 被 Dispatcher 阻止 {#blocked-dispatcher}

如果 GraphQL 端点在发布`POST`请求时返回 `404`错误，这意味着 GraphQL 查询在 Dispatcher 级别被阻止，需要手动启用端点。

默认情况下不应出现这种情况，但自定义 Dispatcher 配置可能会导致此问题。请参阅[Dispatcher - 使用 AEM Headless 进行端点配置](/help/headless/deployment/dispatcher.md)了解详情。
