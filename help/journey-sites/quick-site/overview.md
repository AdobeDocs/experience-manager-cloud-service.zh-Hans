---
title: AEM快速网站创建历程
description: 从此处开始，逐步了解易于使用的AEM快速网站创建工具的引导式旅程，以简化AEM网站的前端开发并快速自定义您的网站，而无需了解AEM后端知识。
source-git-commit: efeb97d4bd7e7c11ec2c0ba1244a32b8b9affdab
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 1%

---


# AEM快速网站创建历程 {#quick-site-creation-journey}

从此处开始，逐步了解易于使用的AEM快速网站创建工具的引导式旅程，以简化AEM网站的前端开发并快速自定义您的网站，而无需了解AEM后端知识。

>[!CAUTION]
>
>快速网站创建工具当前为技术预览。 它可用于测试和评估目的，并且除非与Adobe支持部门达成协议，否则不会用于生产。

## 简介 {#introduction}

AEM Sites是用于创建和管理数字体验的强大工具集。 内容作者可以使用站点编辑器轻松创建数字体验，并使用站点控制台组织内容，同时还能够实时查看由AEM跨渠道向受众交付的内容。

AEM快速站点创建工具允许非开发人员使用站点模板从头开始快速创建新站点。 创建网站后，快速创建工具还允许快速自定义AEM网站（JavaScript、CSS和静态资源）的主题和样式。 这允许需要零AEM知识的前端开发人员与内容创建者分开工作并与之并行工作。 AEM管理员只需下载网站主题并将其提供给前端开发人员，该开发人员使用自己喜爱的工具对其进行自定义，然后将更改提交到AEM代码存储库，然后将其部署。

通过消除网站创建方面的任何开发人员知识、消除前端开发的AEM知识要求，并允许主题开发与内容创建并行进行，AEM快速网站创建工具极大地加快了网站的价值实现时间，并提高了网站的自定义和部署敏捷性。

## AEM文档历程 {#documentation-journeys}

[文档历程](/help/journey-documentation/home.md) 将许多不同且可能复杂的主题和特性联系起来，提供一种说明，帮助读者从头到尾理解和解决业务问题(对AEM而言，读者可能是新手)，同时尽量少地了解以前的主题或AEM知识。

文档历程围绕最佳实践原则进行设计，根据Adobe的最新研究、Adobe顾问的成熟实施经验以及客户项目的反馈提供信息。

如果您想了解Adobe如何建议如何使用AEM解决网站业务案例，可从AEM Sites历程开始。

## 受众 {#audience}

此历程阐述了自定义AEM Sites主题的要求、步骤和方法。 其主要受众是前端开发人员，他们不需要任何AEM知识。 但是，为了说明整个过程，历程涉及管理员，他们假定具有基本的AEM Sites和Cloud Manager知识。 实际上，多个人员可以担任多个角色，此历程支持管理员和前端开发人员的观点。

| 角色 | 描述 | 角色在历程 |
|---|---|---|
| 前端开发人员 | 自定义网站主题 | 采用AEM管理员提供的主题并自定义它，以便能够部署到AEM站点。 |
| 内容作者 | 创建和管理作为站点交付的内容 | 内容作者在AEM上创建内容，该内容将使用前端开发人员自定义的主题进行渲染。 |
| AEM 管理员 | 创建新AEM网站 | AEM管理员根据模板创建新站点，然后为前端开发人员提供要自定义的主题。 |
| Cloud Manager管理员 | 创建管道并授予访问权限 | Cloud Manager管理员会创建前端管道并授予前端开发人员的访问权限，以便能够向AEM git存储库提交自定义设置。 |

## AEM快速网站创建历程 {#the-journey}

您将在此历程中探索许多主题。 以下文章为您提供有关使用快速网站创建工具创建和自定义AEM网站的基本知识，并链接到详细的技术文档。

|#|文章|描述|负责角色| |—|—|—|— |0|AEM快速网站创建历程|本文档|AEM和Cloud Manager管理员| |1|[了解Cloud Manager和快速网站创建工作流程](cloud-manager.md)|了解Cloud Manager以及它如何将新的快速网站创建过程联系起来。|AEM管理员| |2|[从模板创建网站](create-site.md)|了解如何使用网站模板快速创建新的AEM网站。|AEM管理员| |3|[设置管道](pipeline-setup.md)|创建前端管道以管理网站主题的自定义。|Cloud Manager管理员| |4|[授予对前端开发人员的访问权限](grant-access.md)|将前端开发人员载入Cloud Manager，以便他们能够访问您的AEM站点git存储库和管道。|Cloud Manager管理员| |5|[检索Git存储库访问信息](retrieve-access.md)|了解前端开发人员如何使用Cloud Manager访问git存储库信息。|前端开发人员| |6|[自定义网站主题](customize-theme.md)|了解如何构建网站主题、如何对其进行自定义，以及如何使用实时AEM内容对其进行测试。|前端开发人员| |7|[部署自定义主题](deploy-theme.md)|了解如何使用管道部署网站主题。|前端开发人员|

## 下一步 {#what-is-next}

现在，您便可以开始Adobe快速网站创建历程。

* 如果您是AEM或Cloud Manager管理员，或者同时担任前端开发人员和管理员角色，或者如果您只想了解AEM中的端到端流程，请从历程的开头开始 [了解Cloud Manager](cloud-manager.md) 如下所述。
* 如果您仅负责前端开发，并且将与AEM和Cloud Manager管理员进行交互，则可以直接跳转到 [检索Git存储库访问信息](retrieve-access.md) 以访问AEM git存储库并开始自定义。
* 如果您已经了解AEM Sites和Cloud Manager可以一起使用，并且希望直接开始配置，则可以 [直接跳转到从模板创建新站点。](create-site.md)

## 其他资源 {#additional-resources}

请查看这些其他资源，以了解有关AEM强大功能如何协同工作的更多信息。

* [AEMas a Cloud Service技术文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已经对AEM有了很深的了解，则可能需要直接查阅深入的技术文档。
* [站点管理文档](/help/sites-cloud/administering/site-creation/create-site.md)  — 有关快速网站创建工具功能的更多详细信息，请参阅网站创建技术文档。
