---
title: 使用前端管道开发站点
description: 有了前端管道，前端开发人员可以获得更多的独立性，开发过程可以获得可观的速度。 本文档描述了应该给予的前端构建过程的一些特定注意事项。
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
source-git-commit: 74e4c4cc57dbdc78b6c93efe78c856bdafbae477
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 1%

---


# 使用前端管道开发站点 {#developing-site-with-front-end-pipeline}

[通过前端管道，](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 给前端开发人员更多的独立性，开发过程可以获得巨大的速度。 本文档介绍了此流程的工作方式以及一些需要注意的事项，以便您能够充分发挥此流程的潜力。

>[!TIP]
>
>如果您还不熟悉如何使用前端管道及其可能带来的好处，请查看 [快速站点创建历程](/help/journey-sites/quick-site/overview.md) 例如，如何快速部署新站点并完全独立于后端开发自定义其主题。

## 前端构建合同 {#front-end-build-contract}

类似于 [全栈构建环境，](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 前端管道有自己的环境。 开发人员可以灵活地使用此管道，但前提是遵守以下前端构建合同。

前端管道要求前端Node.js项目使用 `build` 脚本指令来生成它部署的版本。 这是因为Cloud Manager使用命令 `npm run build` 生成用于前端构建的可部署项目。

生成的内容 `dist` 文件夹是Cloud Manager最终部署的内容，充当静态文件。 这些文件托管在AEM外部，但可通过 `/content/...` 已部署环境上的URL。

## 节点版本 {#node-versions}

前端构建环境支持以下Node.js版本。

* 12
* 14（默认）
* 16
* 18

您可以使用 `NODE_VERSION` [环境变量](/help/implementing/cloud-manager/environment-variables.md) 以设置所需的版本。

## 单一事实来源 {#single-source-of-truth}

一般好的做法是维护部署到AEM的内容的单一真实来源。 Cloud Manager的目标是使这一单一的真实来源变得显而易见。 但是，由于前端管道允许将部分代码的位置解耦，因此前端管道的正确设置也存在一些额外的责任。 必须注意不要创建在同一环境中部署到同一站点的多个前端管道。

因此，尤其是在创建多个前端管道时，建议保持系统化的命名约定，例如：

* 前端模块的名称，由 `name` 的属性 `package.json` 文件，应包含其应用于的站点的名称。 例如，对于位于 `/content/wknd`，前端模块的名称类似于 `wknd-theme`.
* 当前端模块与其他模块共享相同的Git存储库时，其文件夹的名称应等于或包含前端模块的相同名称。 例如，如果前端模块名为 `wknd-theme`，则封入文件夹名称类似于 `wknd-theme-sources`.
* Cloud Manager前端管道的名称还应包含前端模块的名称，还应添加其部署到的环境（生产或开发）。 例如，对于名为的前端模块 `wknd-theme`，管道的名称可能如下 `wknd-theme-prod`.

此类公约应有效防止以下部署错误：

* 将前端模块应用到错误的站点
* 创建多个应用同一站点的前端模块，这些前端模块会相互覆盖
* 为相同源创建多个前端管道，这可能会导致争用情况，而不保证部署顺序

## 分离关注点 {#separation-of-concerns}

适用于任何分离关注点的另一种良好做法是，特别注意分离关注点的合同的设计和管理的方式。 对于前端管道，将该代码与其余代码分开的合同是站点渲染的HTML和JSON。 如果该HTML和JSON保持稳定，则前端管道通过使前端团队完全独立而实现其最大价值。

当前没有与前端管道同步运行全栈管道的特定功能。 因此，在将前端开发与全栈管道分离开时，必须格外注意将这两个关切领域隔开的合同。 该合同通常是Experience Manager呈现的HTML和/或JSON。 因此，该合同的更改必须在运行不同管道的团队之间经过周密规划，以便他们同意如何对相应的更改进行排序。

如果有必要对HTML和/或JSON输出执行会影响这两个关注领域的更改，通常建议执行以下步骤。

1. 后端团队首先使用新HTML和/或JSON输出设置开发环境。
   1. 通过全栈管道，他们部署渲染所需的新HTML和/或JSON输出所需的代码。
   1. 如果这是前端团队之前无权访问的环境，则必须执行以下步骤。
      1. URL：前端团队必须知道该开发环境的URL。
      1. ACL：必须为前端团队提供具有类似于“参与者”权限的本地AEM用户。
      1. Git：前端团队必须为专门针对该开发环境的前端模块设置单独的Git位置。
         * 通常的做法是创建 `dev` 分支，以便随后可以轻松将对开发环境所做的更改合并回 `main` 要部署到生产环境的分支。
      1. 管道：前端团队必须具有部署到开发环境的前端管道。 该管道将部署通常位于中的前端模块 `dev` 分支，如上一点所述。
1. 然后，前端团队使CSS和JS代码同时使用旧输出和新输出。
   1. 与往常一样，在本地开发：
      1. 此 `npx aem-site-theme-builder proxy` 在前端模块中执行的命令启动一个从AEM环境请求内容的代理服务器，同时将前端模块的CSS和JS文件替换为来自本地的文件 `dist` 文件夹。
      1. 配置 `AEM_URL` 变量 `.env` 文件允许控制本地代理服务器使用内容的AEM环境。
      1. 更改此值 `AEM_URL` 因此，您可以在生产环境和开发环境之间切换以调整CSS和JS，使其适合这两个环境。
      1. 它必须与呈现新输出的开发环境以及呈现旧输出的生产环境配合使用。
   1. 当更新的前端模块适用于这两个环境并将它们部署到两个环境中时，前端工作即告完成。
1. 然后，后端团队可以通过部署代码来更新生产环境，该代码通过全栈管道呈现新HTML和/或JSON输出。
1. 然后，前端团队可以清理其CSS和JS，并删除仅需要旧输出的内容，通过前端管道将最后一次更新部署到生产环境。

## 其他资源 {#additional-resources}

* [站点主题](/help/sites-cloud/administering/site-creation/site-themes.md)  — 了解如何使用AEM站点主题来自定义站点的样式和设计。
* [AEM站点主题生成器](https://github.com/adobe/aem-site-theme-builder) -Adobe提供AEM站点主题生成器作为一组用于创建新站点主题的脚本。
