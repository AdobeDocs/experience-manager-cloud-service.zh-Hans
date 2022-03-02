---
title: 在 AEM 中使用 GraphiQL IDE
description: 了解如何在 Adobe Experience Manager 中使用 GraphiQL IDE。
feature: Content Fragments,GraphQL API
source-git-commit: c4490690edb1ec0e2a6b8cca724fe9c290650bc8
workflow-type: ht
source-wordcount: '226'
ht-degree: 100%

---


# 使用 GraphiQL IDE {#graphiql-ide}

标准 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE 的实施可用于 AEM GraphQL。这可以[随 AEM 安装](#installing-graphiql-ide)。

>[!NOTE]
>
>GraphiQL 绑定全局端点（不可用于特定 Sites 配置的其他端点）。

GraphiQL 工具允许您直接输入、测试和调试查询。GraphiQL 还提供了对文档的轻松访问，使其可以轻松地学习和了解有哪些方法可用。

例如：

* `http://localhost:4502/content/graphiql.html`

这提供了诸如语法突出显示、自动完成、自动建议等功能，以及历史记录和在线文档：

![GraphiQL 接口](assets/cfm-graphiql-interface.png "GraphiQL 接口")

## 安装 AEM GraphiQL IDE {#installing-graphiql-ide}

GraphiQL IDE 是一种开发工具，仅在开发实例或本地实例等低级环境中需要。因此，它不包括在 AEM 项目中，但作为可以临时安装的单独软件包提供。

1. 导航到&#x200B;**[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)** > **AEM as a Cloud Service**。
1. 搜索“GraphiQL”（请确保包括了 **GraphiQL** 中的 **i**）。
1. 下载最新的 **GraphiQL Content Package v.x.x.x**。
1. 从 **AEM 开始**&#x200B;菜单，导航到&#x200B;**工具** > **部署** > **软件包**。
1. 单击&#x200B;**上传软件包**，然后选择在之前步骤中下载的软件包。单击&#x200B;**安装**&#x200B;可安装软件包。

