---
title: 在AEM中使用GraphiQL IDE
description: 了解如何在Adobe Experience Manager中使用GraphiQL IDE。
feature: Content Fragments,GraphQL API
source-git-commit: c4490690edb1ec0e2a6b8cca724fe9c290650bc8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 3%

---


# 使用GraphiQL IDE {#graphiql-ide}

标准的实施 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE可与AEM GraphQL一起使用。 这可以是 [已安装AEM](#installing-graphiql-ide).

>[!NOTE]
>
>GraphiQL已绑定全局端点（并且不适用于特定Sites配置的其他端点）。

GraphiQL工具允许您直接输入、测试和调试查询。 GraphiQL还提供对文档的轻松访问，从而便于学习和了解可用的方法。

例如：

* `http://localhost:4502/content/graphiql.html`

这提供了语法突出显示、自动完成、自动建议等功能，以及历史记录和在线文档：

![GraphiQL接口](assets/cfm-graphiql-interface.png "GraphiQL接口")

## 安装AEM GraphiQL IDE {#installing-graphiql-ide}

GraphiQL IDE是一款开发工具，仅在开发或本地实例等较低级别环境中需要。 因此，它不会包含在AEM项目中，而是作为单独的包提供，可以临时安装。

1. 导航到 **[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)** > **AEMas a Cloud Service**.
1. 搜索“GraphiQL”(请务必包含 **i** in **GraphiQL**.
1. 下载最新版本 **GraphiQL内容包v.x.x.x**
1. 从 **AEM开始** 菜单导航到 **工具** > **部署** > **包**.
1. 单击 **上传包** 并选择在上一步骤中下载的包。 单击 **安装** 来安装包。

