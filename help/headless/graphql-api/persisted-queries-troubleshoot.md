---
title: 持久的GraphQL查询疑难解答
description: 了解如何对Adobe Experience Manager as a Cloud Service中的持久GraphQL查询问题进行故障诊断。
feature: Headless, Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 持久的GraphQL查询疑难解答 {#troubleshoot-persisted-graphql-queries}

[操作中心](/help/operations/actions-center.md)包含&#x200B;**GraphQL持久查询错误**&#x200B;警报。 这意味着当您的某个GraphQL持久查询引发错误时，系统会通知您。

为了帮助您排除和解决此类问题，本页介绍了&#x200B;*最常见的*&#x200B;失败原因以及如何修复它们的步骤。

## 对内容片段模型的更改 {#changes-to-content-fragment-model}

如果GraphQL持久查询基于已过时的GraphQL类型，则查询可能会失败，通常是因为基础内容片段模型发生了更改。

发生此类错误的原因有很多。 示例包括（此列表并非详尽无遗），当创作内容片段模型时：

* 删除或重新命名字段
* 更新定义允许片段引用的模型的&#x200B;**模型类型**
* 取消发布由其他模型引用的模型

要解决此类错误，您应：

* 更新无法容纳对内容片段模型所做的更改的持久查询
* 恢复导致问题的模型上的更改

## 未配置GraphQL端点 {#graphql-endpoint-not-configured}

当持久查询返回`404`错误代码以及信息`No suitable endpoint found`时，这意味着在AEM环境中未配置任何GraphQL端点。

要更正此问题，请按照从[在AEM中管理GraphQL端点](/help/headless/graphql-api/graphql-endpoint.md)启用和发布端点的步骤进行操作。

## GraphQL持久查询URL中缺少路径 {#missing-path-query-url}

如果持久查询返回带有信息`Suffix: '/' does not contain a path`的`400`错误代码，则调用GraphQL servlet时没有路径后缀。

模式应为`/graphql/execute.json/thePath`。

## 由于IP允许列表而被阻止 {#blocked-due-to-ip-allow-list}

在这种情况下，查询返回`405`错误代码。

此类错误并非特定于GraphQL。 请参阅知识库文章[405不允许错误](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-20824)。

## 被Dispatcher阻止 {#blocked-dispatcher}

如果GraphQL端点在发布`POST`请求时返回`404`错误，这意味着在Dispatcher级别阻止GraphQL查询，并且需要手动启用端点。

默认情况下不应出现这种情况，但自定义Dispatcher配置可能会导致此问题。 在[Dispatcher — 使用AEM Headless的端点配置](/help/headless/deployment/dispatcher.md)下查看更多。
