---
title: 使用前端管道开发站点
description: 前端管道增强了开发人员的独立性，并加快了开发过程。 本文概述了前端构建过程的主要注意事项，以确保最佳性能和效率。
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 3%

---


# 使用前端管道开发站点 {#developing-site-with-front-end-pipeline}

{{traditional-aem}}

[前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)为前端开发人员提供了更大的独立性，并显着加快了开发。 本文介绍了该过程的工作方式，并重点介绍了可帮助您充分利用该过程的关键注意事项。

>[!TIP]
>
>如果您还不熟悉如何使用前端管道及其好处，请参阅[快速站点创建历程](/help/journey-sites/quick-site/overview.md)指南。 它提供了一个示例，说明如何快速部署新站点并自定义其主题，而不依赖于后端开发。

## 了解AEM Cloud Manager中的前端管道设置和构建过程 {#front-end-build-contract}

与[全栈构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)类似，前端管道有自己的环境。 开发人员可以灵活地使用此管道，前提是遵循前端构建合同。

前端管道要求前端`Node.js`项目使用`build`脚本指令生成它部署的生成。 存在此要求是因为Cloud Manager使用命令`npm run build`生成前端生成的可部署项目。

`dist`文件夹的结果内容是Cloud Manager最终部署的内容，将它们作为静态文件提供。 这些文件托管在AEM外部，但通过已部署环境上的`/content/...` URL提供。

## 支持的Node.js版本 {#node-versions}

前端构建环境支持以下`Node.js`版本：

* 23
* 22
* 20
* 18
* 16
* 14（默认）
* 12

您可以使用`NODE_VERSION` [环境变量](/help/implementing/cloud-manager/environment-variables.md)来设置所需的版本。

## 在AEM中命名和管理前端管道的最佳实践 {#single-source-of-truth}

AEM部署的最佳实践是维护单一、明确的事实来源。 Cloud Manager旨在强化这一原则。 但是，由于前端管道允许部分代码解耦，因此正确的设置至关重要。 为避免冲突，请确保多个前端管道不会部署到同一环境中的同一站点。

因此，尤其是创建多个前端管道时，Adobe建议您维护系统化的命名约定。 您可以使用以下推荐：

* 由`package.json`文件的`name`属性定义的前端模块的名称应包含其适用的站点的名称。 例如，对于位于`/content/wknd`的站点，前端模块的名称类似于`wknd-theme`。
* 当前端模块与其他模块共享相同的Git存储库时，其文件夹的名称应等于或包含前端模块的相同名称。 例如，如果前端模块名为`wknd-theme`，则封入文件夹名称类似于`wknd-theme-sources`。
* Cloud Manager前端管道的名称还应包含前端模块的名称，还应添加其部署到的环境（生产或开发）。 例如，对于名为`wknd-theme`的前端模块，管道的名称可能类似于`wknd-theme-prod`。

此类约定可以防止以下部署错误：

* 将前端模块应用到错误的站点。
* 创建多个应用同一站点的前端模块，这些前端模块会相互覆盖。
* 为相同源创建多个前端管道，这可能会导致争用情况，无法保证部署顺序。

## 协调前端和后端开发，以提高AEM中的稳定性 {#separation-of-concerns}

任何分离关注的关键最佳实践都是仔细设计和管理定义它们之间边界的合同。 在前端管道中，此合同是站点渲染的HTML和JSON输出。 保持此输出的稳定性可确保前端管道提供最大价值，使前端团队能够独立工作。

目前没有内置功能可与前端管道同步运行全栈管道。 因此，在将前端开发与全栈管道分离开时，关键是要仔细管理合同以界定其界限。 此合同通常包含Experience Manager渲染的HTML和/或JSON。 对此合同的任何更改应在管理不同管道的团队之间仔细协调，以确保顺利过渡和更新顺序的正确。

通常建议在更改HTML或JSON输出时执行以下步骤，尤其是当两个区域都受到影响时。

1. 后端团队首先会使用新的HTML或JSON输出设置开发环境。
   1. 通过全栈管道，他们部署了渲染新HTML或JSON输出（或同时渲染两者）所需的代码。
   1. 如果这是前端团队之前无权访问的环境，则必须执行以下步骤。
      1. URL：前端团队必须知道该开发环境的URL。
      1. ACL：必须为前端团队提供具有类似于“参与者”权限的本地AEM用户。
      1. Git：前端团队必须为专门针对该开发环境的前端模块设置单独的Git位置。

         常见的做法是创建`dev`分支以管理在开发环境中所做的更改。 通过此做法，可以更轻松地合并回`main`分支，该分支用于部署到生产环境。

      1. 管道：前端团队必须具有部署到开发环境的前端管道。 该管道将部署通常位于`dev`分支中的前端模块，如前一点所述。
1. 然后，前端团队使CSS和JS代码同时使用旧输出和新输出。
   1. 与往常一样，要在本地进行开发，请执行以下操作：
      1. `npx aem-site-theme-builder proxy`命令启动从AEM环境中检索内容的代理服务器。 它使用本地`dist`文件夹中的这些文件替换前端模块的CSS和JS文件。
      1. 通过配置隐藏`.env`文件中的`AEM_URL`变量，您可以控制本地代理服务器使用内容的AEM环境。
      1. 因此，通过更改`AEM_URL`的值，您可以在生产环境和开发环境之间切换以调整CSS和JS，使其同时适用于这两个环境。
      1. 它必须与呈现新输出的开发环境以及呈现旧输出的生产环境配合使用。
   1. 当更新的前端模块适用于这两个环境并将它们部署到两个环境中时，前端工作即告完成。
1. 然后，后端团队可以通过全栈管道部署用于呈现新HTML或JSON输出（或同时呈现两者）的代码来更新生产环境。
1. 前端团队可以清理其CSS和JS，删除仅旧输出所需的元素，并使用前端管道将最终更新部署到生产环境。

## 其他资源 {#additional-resources}

* 了解如何使用 AEM 站点主题来自定义站点的样式和设计。

  查看[站点主题](/help/sites-cloud/administering/site-creation/site-themes.md)。

* Adobe 提供 AEM 站点主题生成器作为一组用于创建新站点主题的脚本。

  查看[AEM站点主题生成器](https://github.com/adobe/aem-site-theme-builder)



