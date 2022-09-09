---
title: 了解 Cloud Manager 和快速站点创建工作流
description: 了解 Cloud Manager 以及它如何将新的快速站点创建流程联系起来。
exl-id: 5d264078-e552-48ca-8d82-294a646e6b1f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 100%

---

# 了解 Cloud Manager 和快速站点创建工作流 {#understand-cloud-manager}

了解 Cloud Manager 以及它如何将新的快速站点创建流程联系起来。

>[!TIP]
>
>如果您专门负责前端开发，则可以在此历程中跳过[检索 Git 存储库访问信息](retrieve-access.md)一文。
>
>如果您既是 AEM 管理员，又是 Cloud Manager 管理员，并且负责前端开发和管理员任务，或者只是想了解 AEM 中用于前端开发的端到端流程，请继续阅读当前文档并继续此历程。

## 目标 {#objective}

本文档可帮助您了解 AEM 快速站点创建工具的工作原理，并让您大致了解端到端流程。阅读本文档后，您应：

* 了解 AEM Sites 和 Cloud Manager 如何协作来推动前端开发
* 了解如何在不具有 AEM 知识的情况下将前端自定义步骤与 AEM 完全分离开来。

在继续此历程的下一步来开始配置之前，可通过本文档了解快速站点创建解决方案的这些基本部分。

虽然我们建议您逐步完成此历程，但如果您已了解 AEM Sites 和 Cloud Manager 的协作方式，并且希望直接从配置开始操作，则可以[跳至此历程的下一步](create-site.md)。

## 负责角色 {#responsible-role}

此历程的这一部分适用于 AEM 管理员和 Cloud Manager 管理员。

## 要求和先决条件 {#requirements-prerequisites}

在开始使用快速站点创建工具来创建和自定义站点之前，需要达到几个要求。

由于此历程适用于前端开发人员、管理员和所有角色的组合，因此，此处列出了针对两者的所有要求。

请务必了解一点，对于前端开发人员而言，AEM 访问权限或知识不是必需的。

### 知识 {#knowledge}

| 知识 | 角色 |
|---|---|
| 了解前端开发的标准工具和流程 | 前端开发人员 |
| 有关如何在 AEM 中创建和管理站点的基本知识 | AEM 管理员 |
| Cloud Manager 的基本知识 | Cloud Manager 管理员 |

对于前端开发人员来说，AEM 知识不是必需的。

### 工具 {#tools}

| 工具 | 角色 |
|---|---|
| 首选前端开发环境 | 前端开发人员 |
| npm | 前端开发人员 |
| webpack | 前端开发人员 |
| 对 Cloud Manager 的访问权限 | Cloud Manager 管理员 |
| 成为 Cloud Manager 中的&#x200B;**业务负责人**&#x200B;角色的成员 | Cloud Manager 管理员 |
| 成为 Cloud Manager 中的系统管理员 | Cloud Manager 管理员 |
| 对 Admin Console 的访问权限 | Cloud Manager 管理员 |
| 成为 Cloud Manager 中的&#x200B;**部署管理器**&#x200B;角色的成员 | Cloud Manager 管理员 |
| 成为 Cloud Manager 中的&#x200B;**部署管理器**&#x200B;角色的成员 | 前端开发人员 |

对于前端开发人员来说，无需使用 AEM。

>[!TIP]
>
>如果您不熟悉 Cloud Manager 角色和角色管理，请参阅[其他资源](#additional-resources)部分中的“基于角色的权限”文档。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的必要组件，并且充当平台的单一入口点。

为了支持客户进行企业开发设置，AEM as a Cloud Service 与 Cloud Manager 及其专用 CI/CD 管道完全集成。快速站点创建工具扩展了这些功能以支持专用的前端开发管道。

在此历程中，无需全面了解 Cloud Manager。从较高的层面来看，Cloud Manager 的结构包含几个级别。

![Cloud Manager 结构](assets/cloud-manager-structure.png)

* **租户** – 每个客户均配有一个租户。
* **项目** – 每个租户都有一个或多个项目，这些项目通常反映了客户的许可解决方案。
* **环境** – 每个项目都有多个环境，例如用于实时内容的生产环境、一个用于暂存的环境，一个用于开发的环境。
* **存储库** – 这些环境具有 Git 存储库，可在其中维护应用程序和前端代码。
* **工具和工作流** – 管道管理从存储库到环境的代码部署。

示例通常有助于将此层级置于上下文中。

* WKND 旅游和冒险企业可能是专注于旅游相关媒体的&#x200B;**租户**。
* WKND 旅游和冒险企业租户可能具有两个&#x200B;**项目**：一个针对 WKND 杂志的 Sites 项目和一个针对 WKND 媒体的 Assets 项目。
* WKND 杂志和 WKND 媒体项目都具有开发、暂存和生产&#x200B;**环境**。

## 快速站点创建前端开发流程 {#flow}

整个流程简单直观，即使您尚不具有丰富的 Cloud Manager 经验也是如此。

1. AEM 管理员登录到 AEM 环境，并使用站点模板创建新站点。
1. Cloud Manager 管理员在 Cloud Manager 中创建前端管道。此管道可协调从 Git 存储库到 AEM 环境的代码部署。
1. AEM 管理员从项目的 AEM 实例中导出站点主题，并将它提供给前端开发人员。
1. Cloud Manager 管理员向前端开发人员授予对可在其中提交自定义项的 AEM Git 存储库的访问权限。
1. 前端开发人员检索访问凭据以访问 Git 和管道。
1. 前端开发人员自定义主题，通过代理用站点中的实际内容对主题进行测试，然后将更改提交到 Git 存储库。
1. 前端开发人员执行管道以将主题自定义项部署到项目的生产环境。

![快速站点创建流程](assets/qsc-flow.png)

使用快速站点创建工具的主要好处在于，纯前端开发人员只负责实际自定义。 前端开发人员不与 AEM 交互或无需任何 AEM 知识。

## 下一步 {#what-is-next}

现在您已完成 AEM 快速站点创建历程的这一部分，您应：

* 了解 AEM Sites 和 Cloud Manager 如何协作来推动前端开发
* 了解如何在不具有 AEM 知识的情况下将前端自定义步骤与 AEM 完全分离开来。

在此知识的基础上继续您的 AEM 快速站点创建历程，接下来查看文档[从模板创建站点](create-site.md)，了解如何使用模板快速创建新的 AEM 站点。

## 其他资源 {#additional-resources}

我们建议您查看文档[从模板创建站点](create-site.md)来继续快速站点创建历程的下一部分，以下是一些其他可选资源，这些资源对文档中提到的一些概念进行了更深入的探究，但并非继续此历程所必需的。

* [Cloud Manager 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) – 如果您想了解有关 Cloud Manager 功能的更多详细信息，您可能需要直接参阅深入的技术文档。
* [基于角色的权限](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) – Cloud Manager 预配置了一些具有适当权限的角色。有关这些角色及其管理方式的详细信息，请参阅本文档。
* [npm](https://www.npmjs.com) – 用于快速构建站点的 AEM 主题基于 npm。
* [webpack](https://webpack.js.org) – 用于快速构建站点的 AEM 主题依赖 webpack。
