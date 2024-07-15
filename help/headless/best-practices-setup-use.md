---
title: 设置和将AEM GraphQL与内容片段一起使用的最佳实践
description: 了解设置和将AEM GraphQL与内容片段一起使用的推荐最佳实践。
exl-id: 4d6a5aaa-c8be-4858-ad07-085dc4fb77e7
feature: Headless
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 29%

---

# 设置和将AEM GraphQL与内容片段一起使用的最佳实践{#best-practices-setup-use-aem-graphql-content-fragments}

这些准则汇总了将AEM与GraphQL和内容片段设置、配置和使用的推荐最佳实践。

## 快速入门 {#getting-started}

为了帮助您快速掌握：

* [什么是Headless？](/help/headless/what-is-headless.md)
* AEM [架构](/help/headless/deployment/architecture.md)中各种环境的概述

## 设置 {#setup}

要安全设置AEM GraphQL以与内容片段和您的应用程序一起使用，您需要配置各种组件。

### GraphQL端点创建（包括安全性） {#graphql-endpoint-creation}

端点是 AEM 用于访问 GraphQL 的路径。需要创建和发布这些端点，以便可以安全地访问它们。

#### 详细信息 {#details-graphql-endpoint-creation}

[在 AEM 中管理 GraphQL 端点](/help/headless/graphql-api/graphql-endpoint.md)

#### 环境 {#environments-graphql-endpoint-creation}

端点需要配置于：

* 创作
* 预览
* 发布

对于：

* 开发
* 测试
* 生产

### AEM Dispatcher缓存 {#dispatcher-caching}

>[!NOTE]
>如果启用了Dispatcher中的缓存，则不需要使用[CORS设置](#cors-setup)，因此可以忽略。

默认情况下，Dispatcher 中未启用持久化查询的缓存。无法实施默认启用，因为对多个源使用 CORS（跨源资源共享）的客户需要检查并（可能需要）更新其 Dispatcher 配置。

#### 详细信息 {#details-dispatcher-caching}

[GraphQL 持久化查询 - 在 Dispatcher 中启用缓存](/help/headless/deployment/dispatcher-caching.md)

#### 环境 {#environments-dispatcher-caching}

Dispatcher通常配置为执行以下操作：

* Publish：生产

### CORS设置 {#cors-setup}

>[!NOTE]
>如果启用了[AEM Dispatcher](#dispatcher-caching)中的缓存，则不需要CORS设置，因此可以忽略此部分。

要访问GraphQL端点，必须配置CORS策略并添加到通过Cloud Manager部署到AEM的AEM项目。 此操作可通过为所需端点添加相应的OSGi CORS配置文件来完成。

#### 详细信息 {#details-cors-setup}

[跨源资源共享 (CORS) 配置](/help/headless/deployment/cross-origin-resource-sharing.md)

#### 环境 {#environments-cors-setup}

CORS通常配置为用于：

* Publish：生产

### 身份验证 {#authentication}

用于内容片段投放的Adobe Experience Manager as a Cloud Service (AEM) GraphQL API的主要用例是接受来自第三方应用程序或服务的远程查询。 这些远程查询可能需要经过身份验证的 API 访问，以保护 Headless 内容投放。

#### 详细信息 {#details-authentication}

[对内容片段的远程 AEM GraphQL 查询的身份验证](/help/headless/security/authentication.md)

#### 环境 {#environments-authentication}

身份验证通常配置为执行以下操作：

* 预览
* 发布

对于：

* 开发
* 测试
* 生产

### 权限 {#permissions}

使用 Headless 实施，需要解决多个不同的安全和权限领域。根据 AEM 环境&#x200B;**创作**&#x200B;或&#x200B;**发布**，可以广泛地考虑权限和角色。每个环境包含不同的角色并有不同的需求。

#### 详细信息 {#details-permissions}

[Headless 内容的权限注意事项](/help/headless/security/permissions.md)

#### 环境 {#environments-permissions}

权限通常配置为用于：

* 创作
* 预览
* 发布

对于：

* 开发
* 测试
* 生产

### 使用内容交付网络(CDN) {#cdn}

使用CDN时，如果定位为`GET`请求，则可以缓存GraphQL查询及其JSON响应。 相比之下，未缓存的请求可能非常（资源）昂贵且处理缓慢，有可能对源头资源造成进一步的有害影响。

#### 详细信息 {#details-cdn}

[AEM as a Cloud Service 中的 CDN](/help/implementing/dispatcher/cdn.md)

#### 环境 {#environments-cdn}

CDN通常配置为执行以下操作：

* Publish：生产

### 配置和创建内容片段 {#cconfigure-create-content-fragments}

AEM GraphQL用于从您的内容片段中检索信息。 需要配置这些内容，然后定义结构和位置，然后才能创建内容。

#### 详细信息 {#details-content-fragments}

* [创建配置](/help/headless/setup/create-configuration.md)
* [创建内容片段模型](/help/headless/setup/create-content-model.md)
* [创建Assets文件夹](/help/headless/setup/create-assets-folder.md)
* [创建和编辑您的内容片段](/help/headless/setup/create-content-fragment.md)

#### 环境 {#eenvironments-content-fragments}

在以下位置定义、创作、测试、发布和访问内容片段：

* 创作
* 预览
* 发布

对于：

* 开发
* 测试
* 生产

## 使用AEM GraphQL {#use-aem-graphql}

### 优化GraphQL查询 {#optimize-graphql-queries}

提供这些准则是为了帮助防止GraphQL查询出现性能问题。

#### 详细信息 {#details-optimize-graphql-queries}

[优化 GraphQL 查询](/help/headless/graphql-api/graphql-optimization.md)

>[!NOTE]
>
>优化准则涵盖已在[设置](#setup)中涵盖的缓存配置。

### 从您的应用程序访问GraphQL {#access-graphql-from-your-apps}

AEM Headless CMS使开发人员能够自由地使用他们已熟悉的语言、框架和工具构建和提供卓越的体验。

#### 详细信息 {#details-your-apps}

* [安装并使用AEM SDK进行开发](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html)
* [AEM Headless开发人员资源](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
* 示例，包括[React](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/react-app.html)、[Next.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/next-js.html)、[Node.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/server-to-server-app.html)等

#### 环境 {#environments-your-apps}

应用程序通常在以下环境中开发、测试和使用：

* 预览
* 发布

对于：

* 开发
* 测试
* 生产

### 其他资源

有关AEM GraphQL和内容片段的更多详细信息，请参阅以下内容：

* [用于内容片段的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [使用 GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md)
* [AEM Headless开发人员资源](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
