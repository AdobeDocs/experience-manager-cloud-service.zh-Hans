---
title: Experience Modernization Agent入门
description: 了解使用Experience Modernization Console通过Experience Modernization Agent快速提高工作效率的第一步。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: c80ce5a9fc5f208fd910d5cef72225085248fb4d
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# Experience Modernization Agent入门 {#getting-started}

了解使用Experience Modernization Console通过Experience Modernization Agent快速提高工作效率的第一步。

>[!NOTE]
>
>如果您有兴趣使用Experience Modernization Console，可以请求访问权限以确保顺利入门体验。

## 准备Edge Delivery GitHub存储库 {#prepare-repo}

1. 选择要与Experience Modernization Console一起使用的[Edge Delivery Services](/help/edge/overview.md)存储库。
   * 这个项目可以是现有的Edge Delivery Services项目，也可以在[开发人员教程](https://www.aem.live/developer/tutorial)之后使用[样板存储库](https://github.com/adobe/aem-boilerplate)创建新的项目。
1. 确保存储库中安装了[AEMY GitHub应用程序](https://github.com/apps/aem-aemy)。
   * 这将允许控制台检查您的代码。
1. 确保存储库中安装了[AEM代码同步GitHub应用程序](https://github.com/apps/aem-code-sync)。
   * 这允许Edge Delivery Services同步您的代码。
   * 如果您的存储库基于教程，则此步骤已完成。

## 打开“体验现代化”控制台 {#open-console}

1. 导航到[`aemcoder.adobe.io`.](https://aemcoder.adobe.io)
1. 使用您的Adobe ID登录。

## 连接您的GitHub存储库 {#connect-repo}

当您首次登录时，控制台会提示您输入存储库。

![首次登录控制台屏幕](assets/first-sign-on.png)

1. 单击&#x200B;**连接存储库**。
1. 这将在新的浏览器选项卡上打开AEMY应用程序。 单击&#x200B;**授权AEM AEMY**。
1. 返回控制台，选择&#x200B;**所有者**、**存储库**&#x200B;和&#x200B;**分支选择**，然后单击&#x200B;**签出到工作区**。
   ![正在连接到GitHub项目](assets/connect-to-github-project.png)
1. 当提示&#x200B;**替换现有工作区**&#x200B;时，单击&#x200B;**替换工作区**。
   ![替换现有工作区](assets/replace-existing-workspace.png)

您的GitHub项目现在已连接到控制台，并且您现在位于主屏幕上。

![控制台主页](assets/console-home.png)

## 开始提示 {#start-prompting}

现在，您的控制台可以访问您的代码，您可以开始提示了。

1. 要开始导入，您可以导入网站的内容：
   * “迁移页面`https://wknd-trendsetters.site`。”
1. 这会导入网站的内容。
   * 控制台观察关注点的分离并单独处理内容和演示。
   * 网站内容的初始导入可能需要几分钟的时间。
   * 控制台在开始工作时会向您提供持续的反馈，包括计划步骤的概述。
     ![内容导入](assets/content-import.png)
1. 导入网站后，**Workspace**&#x200B;面板会显示页面。 选择要在右侧面板中预览的页面。
   ![内容已导入](assets/content-imported.png)
1. 现在您有了内容，可以提示从同一源导入样式。
   * “从`https://wknd-trendsetters.site`导入常规样式。”
1. 与初始内容导入一样，导入过程可能需要几分钟时间，并且控制台在处理您的请求并导入样式时会提供反馈。 任务完成后，单击右侧面板中的&#x200B;**刷新预览**&#x200B;以查看样式化的内容。
   ![样式已导入](assets/styles-imported.png)

现在，您已将内容和样式导入到控制台中。

## 上传内容 {#upload-content}

要将您的内容上传到[文档创作](https://da.live)，请执行以下操作：

1. 确保您处于&#x200B;**Content**&#x200B;视图中，然后单击右上方的&#x200B;**Upload content**&#x200B;按钮。
   * 默认情况下，您进入控制台时处于&#x200B;**Content**&#x200B;视图中。
   * 在控制台左侧的侧栏中，高亮显示的图标表示您的视图。
1. 将打开&#x200B;**上传内容**&#x200B;对话框，目标组织和存储库已预填充您的`fstab.yaml`。
   * 如果连接的存储库中不存在`fstab.yaml`，则需要手动输入您的&#x200B;**组织**&#x200B;和&#x200B;**存储库**。
   * 如果您使用了样板，则会提供`fstab.yaml`。
1. 选择要上载的文件，然后单击&#x200B;**上载**。
   ![上载内容对话框](assets/upload-content.png)
1. 控制台通过将&#x200B;**上传**&#x200B;按钮灰显来指示上传过程。
   ![正在上传](assets/uploading.png)
1. 完成后，控制台底部会显示通知。
   在AEM中查看![](assets/view-in-aem.png)

若要在“文档创作”中访问上传的内容，可以选择在上传完成时单击通知中的&#x200B;**在AEM中查看**，或导航到`https://da.live/#/{organization}/{repository}`。

![文档创作中的内容](assets/content-in-document-authoring.png)

您导入的内容现在处于“文档创作”状态。

## 推送代码更改 {#push-code-changes}

在对代码所做的更改感到满意后，可以将它们推送到GitHub存储库。

1. 切换到&#x200B;**代码**&#x200B;视图（左侧边栏中为`</>`图标），然后切换到&#x200B;**Git更改**&#x200B;选项卡（右上角的分支图标）。
   ![代码视图](assets/code-view-git-changes.png)
1. 在更改的文件列表中，如果某些文件显示为未跟踪，请单击其`+`按钮以暂存它们。
1. 单击右上方的&#x200B;**GitHub操作**&#x200B;按钮，然后从下拉列表中选择&#x200B;**推送**。
1. 在&#x200B;**推送更改**&#x200B;对话框中，选择将更改推送至新PR（默认）或当前分支，然后单击&#x200B;**确认**&#x200B;以进行推送。
   * 如有疑问，您可以推送到当前分支以保持事情简单。
1. 完成后，控制台底部会显示通知。
   ![查看PR](assets/view-pr.png)

如果要直接访问GitHub中的推送更改，请在推送完成时单击通知中的&#x200B;**查看PR**。

GitHub中的![代码](assets/code-in-github.png)

您的代码现在位于GitHub中。

## 预览站点 {#preview-site}

要查看预览环境中的更改，请执行以下操作：

1. 返回到文档创作。
   * 上传内容后，在AEM **中单击**&#x200B;查看后，该内容可能仍在您打开的浏览器选项卡中打开。
   * 或导航到`https://da.live/#/{organization}/{repository}`
1. 打开您之前上传到AEM的其中一个页面。
1. 单击纸飞机图标（右上方）并选择&#x200B;**预览**。
   ![发布到预览](assets/publish-to-preview.png)

恭喜！现在，您已迁移的内容和样式在AEM预览环境中处于实时状态。

![已发布的预览内容](assets/published-preview.png)

如果将代码推送到`main`以外的分支，则从“文档创作”中打开的预览将不会显示样式。 通过更新预览的URL更改为分支，此时您可以看到自己的样式。

## 其他资源 {#additional-resources}

当您继续探索Experience现代化代理及其控制台时，以下文档可能会很有用。

* [体验现代化控制台](/help/ai-in-aem/agents/modernization/console.md) — 有关该控制台、其视图、选项和功能的详细信息
* [Edge Delivery Services开发人员教程](https://www.aem.live/developer/tutorial) — 如果您不熟悉AEM和Edge Delivery Services项目，则很有用
* [文档创作](https://da.live) — 如果您不熟悉用于内容管理的文档创作，则很有用
