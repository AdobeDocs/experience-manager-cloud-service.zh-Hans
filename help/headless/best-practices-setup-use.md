---
title: 设置 AEM GraphQL 并将其与内容片段结合使用的最佳实践
description: 了解推荐的有关设置 AEM GraphQL 并将其与内容片段结合使用的最佳实践。
exl-id: 4d6a5aaa-c8be-4858-ad07-085dc4fb77e7
feature: Headless
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: ht
source-wordcount: '702'
ht-degree: 100%

---

# 设置 AEM GraphQL 并将其与内容片段结合使用的最佳实践{#best-practices-setup-use-aem-graphql-content-fragments}

这些指南汇总了推荐的有关设置、配置 AEM 以及将 AEM 与 GraphQL 和内容片段结合使用的最佳实践。

## 快速入门 {#getting-started}

以下内容可帮助您快速入门。

* [什么是 Headless？](/help/headless/what-is-headless.md)
* AEM [架构](/help/headless/deployment/architecture.md)中的各种环境的概述

## 设置 {#setup}

要安全地设置 AEM GraphQL 以便与内容片段和您的应用程序结合使用，您需要配置各种组件。

### GraphQL 端点创建（包括安全性） {#graphql-endpoint-creation}

端点是 AEM 用于访问 GraphQL 的路径。需要创建和发布这些端点，以便安全地访问它们。

#### 详细信息 {#details-graphql-endpoint-creation}

[在 AEM 中管理 GraphQL 端点](/help/headless/graphql-api/graphql-endpoint.md)

#### 环境 {#environments-graphql-endpoint-creation}

需要为以下环境配置端点：

* 创作
* 预览
* 发布

适用环境：

* 开发
* 测试
* 生产

### AEM Dispatcher 缓存 {#dispatcher-caching}

>[!NOTE]
>如果在 Dispatcher 中启用了缓存，则不需要 [CORS 设置](#cors-setup)，并且可以忽略该部分。

默认情况下，Dispatcher 中未启用持久化查询的缓存。无法实施默认启用，因为对多个源使用 CORS（跨源资源共享）的客户需要检查并（可能需要）更新其 Dispatcher 配置。

#### 详细信息 {#details-dispatcher-caching}

[GraphQL 持久化查询 - 在 Dispatcher 中启用缓存](/help/headless/deployment/dispatcher-caching.md)

#### 环境 {#environments-dispatcher-caching}

通常为以下项配置 Dispatcher：

* 发布：生产

### CORS 设置 {#cors-setup}

>[!NOTE]
>如果在 [AEM Dispatcher](#dispatcher-caching) 中启用了缓存，则不需要 CORS 设置，并且可以忽略该部分。

要访问 GraphQL 端点，必须配置 CORS 策略并添加到通过 Cloud Manager 部署到 AEM 的 AEM 项目。此操作可通过为所需端点添加相应的 OSGi CORS 配置文件来完成。

#### 详细信息 {#details-cors-setup}

[跨源资源共享 (CORS) 配置](/help/headless/deployment/cross-origin-resource-sharing.md)

#### 环境 {#environments-cors-setup}

通常为以下项配置 CORS：

* 发布：生产

### 身份验证 {#authentication}

用于内容片段投放的 Adobe Experience Manager as a Cloud Service (AEM) GraphQL API 的主要用例是接受来自第三方应用程序或服务的远程查询。这些远程查询可能需要经过身份验证的 API 访问，以保护 Headless 内容投放。

#### 详细信息 {#details-authentication}

[对内容片段的远程 AEM GraphQL 查询的身份验证](/help/headless/security/authentication.md)

#### 环境 {#environments-authentication}

通常为以下项配置身份验证：

* 预览
* 发布

适用环境：

* 开发
* 测试
* 生产

### 权限 {#permissions}

使用 Headless 实施，需要解决多个不同的安全和权限领域。根据 AEM 环境&#x200B;**创作**&#x200B;或&#x200B;**发布**，可以广泛地考虑权限和角色。每个环境包含不同的角色并有不同的需求。

#### 详细信息 {#details-permissions}

[Headless 内容的权限注意事项](/help/headless/security/permissions.md)

#### 环境 {#environments-permissions}

通常为以下项配置权限：

* 创作
* 预览
* 发布

适用环境：

* 开发
* 测试
* 生产

### 使用内容分发网络 (CDN) {#cdn}

在使用 CDN 时，如果目标为 `GET` 请求，则可以缓存 GraphQL 查询及其 JSON 响应。相比之下，未缓存的请求可能耗费大量资源且处理速度慢，同时可能对来源的资源产生更多不利影响。

#### 详细信息 {#details-cdn}

[AEM as a Cloud Service 中的 CDN](/help/implementing/dispatcher/cdn.md)

#### 环境 {#environments-cdn}

通常为以下项配置 CDN：

* 发布：生产

### 配置和创建内容片段 {#cconfigure-create-content-fragments}

AEM GraphQL 用于从内容片段中检索信息。需要配置这些项，再定义结构和位置，之后才能创建内容。

#### 详细信息 {#details-content-fragments}

* [创建配置](/help/headless/setup/create-configuration.md)
* [创建内容片段模型](/help/headless/setup/create-content-model.md)
* [创建资源文件夹](/help/headless/setup/create-assets-folder.md)
* [创建和编辑内容片段](/help/headless/setup/create-content-fragment.md)

#### 环境 {#eenvironments-content-fragments}

为以下项定义、创作、测试、发布和访问内容片段：

* 创作
* 预览
* 发布

适用环境：

* 开发
* 测试
* 生产

## 使用 AEM GraphQL {#use-aem-graphql}

### 优化 GraphQL 查询 {#optimize-graphql-queries}

这些准则旨在帮助防止 GraphQL 查询出现性能问题。

#### 详细信息 {#details-optimize-graphql-queries}

[优化 GraphQL 查询](/help/headless/graphql-api/graphql-optimization.md)

>[!NOTE]
>
>优化准则涵盖了已在[设置](#setup)中包含的缓存配置。

### 从您的应用程序访问 GraphQL {#access-graphql-from-your-apps}

AEM Headless CMS 使开发人员能够随意使用他们熟悉的语言、框架和工具构建和交付卓越体验。

#### 详细信息 {#details-your-apps}

* [安装并使用 AEM SDK 以进行开发](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=zh-Hans)
* [AEM Headless 开发人员资源](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
* 示例，包括 [React](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/react-app.html?lang=zh-Hans)、[Next.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/next-js.html?lang=zh-Hans)、[Node.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/server-to-server-app.html?lang=zh-Hans) 等

#### 环境 {#environments-your-apps}

通常为以下项开发、测试和使用应用程序：

* 预览
* 发布

适用环境：

* 开发
* 测试
* 生产

### 其他资源

有关 AEM GraphQL 和内容片段的更多详细信息，请参阅下面：

* [用于内容片段的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [使用 GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md)
* [AEM Headless 开发人员资源](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
