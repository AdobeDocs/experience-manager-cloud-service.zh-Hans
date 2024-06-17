---
title: 持久的GraphQL查询疑难解答
description: 了解如何对Adobe Experience Manager as a Cloud Service中的持久GraphQL查询问题进行故障诊断。
feature: Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
source-git-commit: 736fbc28c800c1c181721df7e0d7feed143642d9
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 持久的GraphQL查询疑难解答 {#troubleshoot-persisted-graphql-queries}

此 [操作中心](/help/operations/actions-center.md) 包括 **GraphQL持久查询错误** 警报。 这意味着当您的某个GraphQL持久查询引发错误时，系统会通知您。

为了帮助您排除和解决此类问题，本页涵盖 *最常见* 失败的原因以及如何修复它们的步骤。

## 对内容片段模型的更改 {#changes-to-content-fragment-model}

如果GraphQL持久查询基于已过时的GraphQL类型，则查询可能会失败，通常是因为基础内容片段模型发生了更改。

发生此类错误的原因有很多。 示例包括（此列表并非详尽无遗），当创作内容片段模型时：

* 删除或重新命名字段
* 更新 **模型类型** 用于定义允许片段引用的模型
* 取消发布由其他模型引用的模型

要解决此类错误，您应：

* 更新无法容纳对内容片段模型所做的更改的持久查询
* 恢复导致问题的模型上的更改

## 未配置GraphQL端点 {#graphql-endpoint-not-configured}

当持久查询返回 `404` 错误代码，以及信息 `No suitable endpoint found`，这意味着在AEM环境中未配置任何GraphQL端点。

要更正此问题，请按照启用和发布端点的步骤进行操作 [在AEM中管理GraphQL端点](/help/headless/graphql-api/graphql-endpoint.md).

## GraphQL持久查询URL中缺少路径 {#missing-path-query-url}

如果持久查询返回 `400` 包含信息的错误代码 `Suffix: '/' does not contain a path`，则在调用GraphQL servlet时没有路径后缀。

模式应为 `/graphql/execute.json/thePath`.

## 由于IP允许列表而被阻止 {#blocked-due-to-ip-allow-list}

在这种情况下，查询将返回 `405` 错误代码。

此类错误并非特定于GraphQL。 请参阅知识库文章 [不允许出现405错误](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-20824).

## 被Dispatcher阻止 {#blocked-dispatcher}

如果GraphQL端点返回 `404` 发布以下内容时出错： `POST` 请求，这意味着GraphQL查询在Dispatcher级别被阻止，并且端点需要手动启用。

默认情况下不应出现这种情况，但自定义Dispatcher配置可能会导致此问题。 查看下的更多信息 [Dispatcher — 使用AEM Headless进行端点配置](/help/headless/deployment/dispatcher.md).
