---
title: 自定义站点主题
description: 了解如何使用实时 AEM 内容构建、自定义和测试站点主题。
exl-id: b561bee0-3a64-4dd3-acb8-996f0ca5bfab
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 100%

---

# 自定义站点主题 {#customize-the-site-theme}

了解如何使用实时 AEM 内容构建、自定义和测试站点主题。

## 迄今为止的故事 {#story-so-far}

在 AEM 快速站点创建历程的上一个文档[检索 Git 存储库访问信息](retrieve-access.md)中，您已了解前端开发人员如何使用 Cloud Manager 访问 Git 存储库信息，您现在应：

* 从较高层面了解什么是 Cloud Manager。
* 已检索您的凭据来访问 AEM Git，以便您能提交自定义项。

此历程的这一部分将执行下一步并深入探究站点主题，为您展示如何自定义站点主题，然后使用您检索到的访问凭据来提交这些自定义项。

## 目标 {#objective}

本文档说明如何使用实时 AEM 内容构建、自定义和测试 AEM 站点主题。阅读本文档后，您应：

* 了解站点主题的基本结构以及如何对其进行编辑。
* 了解如何通过本地代理使用实际 AEM 内容测试您的主题自定义。
* 了解如何将更改提交到 AEM Git 存储库。

## 负责角色 {#responsible-role}

此历程的这一部分适用于前端开发人员。

## 理解主题结构 {#understand-theme}

将 AEM 管理员提供的主题提取到要编辑该主题的位置，然后在首选编辑器中将其打开。

![编辑主题](assets/edit-theme.png)

您会看到该主题是一个典型的前端项目。该结构最重要的部分包括：

* `src/main.ts`：JS &amp; CSS 主题的主要入口点
* `src/site`：应用于整个站点的 JS &amp; CSS 文件
* `src/components`：特定于 AEM 组件的 JS &amp; CSS 文件
* `src/resources`：图标、徽标和字体等静态文件

>[!TIP]
>
>如果您想了解有关标准 AEM 站点主题的更多信息，请参阅本文档末尾的[其他资源](#additional-resources)部分中的 GitHub 链接。

在对主题项目的结构感到满意后，启动本地代理，以便根据实际 AEM 内容实时查看任何主题自定义。

## 启动本地代理 {#starting-proxy}

1. 从命令行中，导航到本地计算机上主题的根。
1. 执行 `npm install`，npm 将检索依赖项并安装项目。

   ![npm install](assets/npm-install.png)

1. 执行 `npm run live`，代理服务器将启动。

   ![npm run live](assets/npm-run-live.png)

1. 代理服务器在启动时将自动打开浏览器并转到 `http://localhost:7001/`。点按或单击&#x200B;**本地登录(仅管理任务)**，并使用 AEM 管理员提供给您的代理用户凭据进行登录。

   ![本地登录](assets/sign-in-locally.png)

1. 登录后，将浏览器中的 URL 更改为指向 AEM 管理员提供给您的示例内容的路径。

   * 例如，如果提供的路径为 `/content/<your-site>/en/home.html?wcmmode=disabled`
   * 将 URL 更改为 `http://localhost:7001/content/<your-site>/en/home.html?wcmmode=disabled`

   ![代理的示例内容](assets/proxied-sample-content.png)

您可以浏览站点以探究内容。由于站点是从实时 AEM 实例中实时提取的，因此，可以根据实际内容来自定义主题。

## 自定义主题 {#customize-theme}

现在您可以开始自定义主题了。下面是一个简单示例，说明如何通过代理实时查看更改。

1. 在编辑器中，打开文件 `<your-theme-sources>/src/site/_variables.scss`

   ![编辑主题](assets/edit-theme.png)

1. 编辑变量 `$color-background`，并将它设置为白色以外的值。在此示例中，使用 `orange`。

   ![编辑的主题](assets/edited-theme.png)

1. 在保存文件时，您会看到代理服务器通过 `[Browsersync] File event [change]` 行来识别更改。

   ![代理浏览器同步](assets/proxy-browsersync.png)

1. 切换回代理服务器的浏览器后，更改将立即可见。

   ![橙色主题](assets/orange-theme.png)

您可以根据 AEM 管理员提供给您的要求继续自定义主题。

## 提交更改 {#committing-changes}

自定义完成后，可以将其提交到 AEM Git 存储库。首先，您必须将存储库克隆到本地计算机。

1. 从命令行中，导航到要克隆存储库的位置。
1. 执行[之前从 Cloud Manager 中检索到的命令。](retrieve-access.md)它应类似于 `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`。使用[在此历程的上一部分中检索到的](retrieve-access.md) Git 用户名和密码。

   ![克隆存储库](assets/clone-repo.png)

1. 使用类似于 `mv <site-theme-sources> <cloned-repo>` 的命令将正在编辑的主题项目移动到克隆的存储库中
1. 在克隆的存储库的目录中，使用以下命令提交您刚刚移入的主题文件。

   ```text
   git add .
   git commit -m "Adding theme sources"
   git push
   ```

1. 自定义项将推送到 AEM Git 存储库。

   ![已提交更改](assets/changes-committed.png)

自定义项现在将安全地存储在 AEM Git 存储库中。

## 下一步 {#what-is-next}

现在您已完成 AEM 快速站点创建历程的这一部分，您应：

* 了解站点主题的基本结构以及如何对其进行编辑。
* 了解如何通过本地代理使用实际 AEM 内容测试您的主题自定义。
* 了解如何将更改提交到 AEM Git 存储库。

在此知识的基础上继续您的 AEM 快速站点创建历程，接下来查看文档[部署自定义主题](deploy-theme.md)，其中您将了解如何使用前端管道来部署主题。

## 其他资源 {#additional-resources}

我们建议您查看文档[部署自定义主题](deploy-theme.md)来继续快速站点创建历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续此历程所必需的。

* [AEM 站点主题](https://github.com/adobe/aem-site-template-standard-theme-e2e) – 这是 AEM 站点主题的 GitHub 存储库。
* [npm](https://www.npmjs.com) – 用于快速构建站点的 AEM 主题基于 npm。
* [webpack](https://webpack.js.org) – 用于快速构建站点的 AEM 主题依赖 webpack。
