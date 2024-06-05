---
title: 程序和程序类型
description: 了解 Cloud Manager 的层级，以及不同类型的程序如何适应其结构以及它们之间的差异。
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 93%

---


# 程序和程序类型 {#understanding-programs}

Cloud Manager 是围绕实体的层次结构构建的。这方面的细节对于您在 Cloud Manager 中的日常工作并不重要，但概述将有助于您了解程序并设置自己的程序。

![Cloud Manager 层级](assets/program-types1.png)

* **租户** – 这是层次结构的顶层。每个客户均配有一个租户。
* **程序** – 每个租户都有一个或多个项目，[这些项目通常反映了客户的许可解决方案](introduction-production-programs.md)。
* **环境** – 每个项目都有多个环境，例如用于实时内容的生产环境、一个用于暂存的环境，一个用于开发的环境。
   * 每个程序只能有一个生产环境，但可以有多个非生产环境。
* **存储库** – 程序有 Git 存储库，其中应用程序和前端代码被维护的环境。
* **工具和工作流程** – 管道管理从存储库到环境的代码部署，而其他工具允许访问日志、监控和环境管理。

示例通常有助于将此层级置于上下文中。

* WKND 旅游和冒险企业可能是专注于旅游相关媒体的&#x200B;**租户**。
* WKND 旅游和冒险企业租户可能具有两个&#x200B;**程序**：一个针对 WKND 杂志的 Sites 程序和一个针对 WKND 媒体的 Assets 程序。
* WKND 杂志和 WKND 媒体项目都具有开发、暂存和生产&#x200B;**环境**。

## 源代码存储库 {#source-code-repository}

Cloud Manager 程序将自动配置自己的 Git 存储库。

要访问Cloud Manager Git存储库，用户需要使用带有命令行工具的Git客户端、独立的可视Git客户端或用户选择的IDE，例如Eclipse、IntelliJ或NetBeans。

一旦设置了 Git 客户端，就可以从 Cloud Manager 用户界面管理 Git 存储库。要了解如何使用 Cloud Manager 用户界面管理 Git，请参阅[访问 Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)。

要开始开发 AEM Cloud 应用程序，必须通过将应用程序代码从 Cloud Manager 存储库签出到本地计算机上的某个位置来制作应用程序代码的本地副本。

```java
$ git clone {URL}
```

因此，该工作流程是一个标准的 Git 工作流程。

1. 用户克隆 Git 存储库的本地副本。
1. 用户在本地代码存储库中进行更改。
1. 准备就绪后，用户将更改提交回远程 Git 存储库。

唯一的区别是远程 Git 存储库是 Cloud Manager 的一部分，对开发人员来说是透明的。

## 程序类型 {#program-types}

用户可以创建一个&#x200B;**生产**&#x200B;程序或&#x200B;**沙盒**&#x200B;程序。

* 创建&#x200B;**生产程序**，以便为您的站点启用实时流量。
   * 请参阅[生产程序简介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)，了解更多详细信息。
* 通常，创建&#x200B;**沙盒程序**&#x200B;是为了提供培训、运行演示、支持、概念验证 (POC) 或归档等目的。
   * 沙盒环境并不意味着要承载实时流量，并且会有生产程序所没有的限制。
   * 它包括 Sites 和 Assets，交付时自动填充 Git 分支，其中包括示例代码、开发环境和非生产管道。
   * 请参阅[沙盒简介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)，了解更多详细信息。
