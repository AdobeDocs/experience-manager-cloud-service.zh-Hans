---
title: AEM 快速站点创建历程
description: 从这里开始引导式历程，通过易用的 AEM 快速站点创建工具来简化 AEM 站点的前端开发并在不具备 AEM 后端知识的情况下快速自定义您的站点。
exl-id: b8218232-0298-4b16-9dab-fa59be592a24
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '1030'
ht-degree: 100%

---

# AEM 快速站点创建历程 {#quick-site-creation-journey}

从这里开始引导式历程，通过易用的 AEM 快速站点创建工具来简化 AEM 站点的前端开发并在不具备 AEM 后端知识的情况下快速自定义您的站点。

## 简介 {#introduction}

AEM Sites 是用于创建和管理数字体验的强大工具集。内容作者可以使用站点编辑器轻松创建数字体验，并使用站点控制台组织内容，同时能够实时查看 AEM 将通过不同的渠道交付给受众的内容。

借助 AEM 快速站点创建工具，非开发人员可以使用站点模板从头开始快速创建新站点。创建后，还可利用快速站点创建工具快速自定义 AEM 站点的主题和样式（JavaScript、CSS 和静态资源）。这样一来，无需了解 AEM 的前端开发人员既可独立于内容创建者工作，又可与内容创建者并行工作。AEM 管理员只需下载站点主题并将它提供给前端开发人员，后者会使用他们喜欢的工具来自定义站点主题，再将更改提交到 AEM 代码存储库，随后进行部署。

利用 AEM 快速站点创建工具，无需了解有关站点创建的任何开发人员知识，也无需达到前端开发的 AEM 知识要求，并且可以同时进行主题开发和内容创建，从而大大加快了站点的价值实现速度，改善了站点自定义并提高了部署敏捷性。

## 视频概述 {#video-overview}

要快速了解此功能的实际应用况，[您可以观看此时长 5 分钟的介绍视频](https://www.youtube.com/watch?v=NQeQ1jZ7ZBw)。

此文档历程将带您逐步详细地了解视频中的所有功能，以便您了解工作流并能够在自己的环境中重新创建流程。

## AEM 文档历程 {#documentation-journeys}

[文档历程](/help/journey-documentation/documentation-journeys.md)通过提供叙述来帮助可能是 AEM 新手的读者彻底理解和解决业务问题，同时假定读者拥有最少的主题或 AEM 知识，从而将许多不同且可能复杂的主题和功能联系起来。

文档历程是围绕最佳实践准则而设计的，其中包含了 Adobe 的最新研究、Adobe 顾问提供的成熟实施经验以及来自客户项目的反馈。

如果您想了解 Adobe 就如何使用 AEM 解决站点业务案例提出的建议，则可以从 AEM Sites 历程开始。

## 受众 {#audience}

此历程列出了自定义 AEM Sites 主题的要求、步骤和方法。其主要受众是前端开发人员，他们无需了解 AEM。但是，为了说明整个流程，在此历程中，已假定管理员基本了解 AEM Sites 和 Cloud Manager。在实践中，多个人员可以充当多个角色，此历程支持来自管理员和前端开发人员的观点。

| 角色 | 描述 | 历程中的角色 |
|---|---|---|
| 前端开发人员 | 自定义站点主题 | 采用 AEM 管理员提供的主题并对其进行自定义，以便将其部署到 AEM 站点。 |
| 内容作者 | 创建和管理作为站点交付的内容 | 内容作者在 AEM 上创建使用前端开发人员自定义的主题呈现的内容。 |
| AEM 管理员 | 创建新的 AEM 站点 | AEM 管理员基于模板创建新站点，然后为前端开发人员提供要自定义的主题。 |
| Cloud Manager 管理员 | 创建管道并授予访问权限 | Cloud Manager 管理员创建前端管道并向前端开发人员授予访问权限，以便他们能够将自定义项提交到 AEM Git 存储库。 |

## AEM 快速站点创建历程 {#the-journey}

您将在此历程中探究多个主题。以下文章为您提供了使用快速站点创建工具来创建和自定义 AEM 站点的基础知识以及指向详细技术文档的链接。

|#|文章|描述|负责角色|
|---|---|---|--|
|0|AEM 快速站点创建历程|本文档|AEM 和 Cloud Manager 管理员|
|1|[了解 Cloud Manager 和快速站点创建工作流](cloud-manager.md)|了解 Cloud Manager 以及它如何将新的快速站点创建流程联系起来。|AEM 管理员|
|2|[从模板创建站点](create-site.md)|了解如何使用站点模板快速创建新的 AEM 站点。|AEM 管理员|
|3|[设置您的管道](pipeline-setup.md)|创建前端管道来管理站点主题的自定义。|Cloud Manager 管理员|
|4|[向前端开发人员授予访问权限](grant-access.md)|将前端开发人员载入 Cloud Manager，以便他们能够访问您的 AEM 站点 Git 存储库和管道。|Cloud Manager 管理员|
|5|[检索 Git 存储库访问信息](retrieve-access.md)|了解前端开发人员如何使用 Cloud Manager 访问 Git 存储库信息。|前端开发人员|
|6|[自定义站点主题](customize-theme.md)|了解如何使用实时 AEM 内容构建、自定义和测试站点主题。|前端开发人员|
|7|[部署自定义主题](deploy-theme.md)|了解如何使用管道部署站点主题。|前端开发人员|

## 下一步 {#what-is-next}

您现在已准备好开始您的 Adobe 快速站点创建历程。

* 如果您是 AEM 或 Cloud Manager 管理员、同时担任前端开发人员和管理员角色或只想了解 AEM 中的端到端流程，请在开始历程时，首先参阅[了解 Cloud Manager](cloud-manager.md)，如下所述。
* 如果您只负责前端开发，并且会与 AEM 和 Cloud Manager 管理员进行交互，则可以直接跳转至[检索 Git 存储库访问信息](retrieve-access.md)以获取对 AEM Git 存储库的访问权限并开始进行自定义。
* 如果您已了解 AEM Sites 和 Cloud Manager 的协作方式，并且希望直接从配置开始操作，则可以[直接跳至“从模板创建新站点”](create-site.md)。

## 其他资源 {#additional-resources}

查看这些附加资源，详细了解 AEM 的强大功能如何协作。

* [AEM as a Cloud Service 技术文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) – 如果您已对 AEM 有一定的了解，则可能需要直接参阅深入的技术文档。
* [站点管理文档](/help/sites-cloud/administering/site-creation/create-site.md) – 查看有关站点创建的技术文档，了解有关快速站点创建工具的功能的更多详细信息。
