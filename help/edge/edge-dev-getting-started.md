---
title: 使用Edge Delivery Services进行AEM创作的开发人员快速入门指南
description: 本指南将引导您启动并运行一个新的Adobe Experience Manager站点，该站点使用Edge Delivery Services和通用编辑器进行内容创作
feature: Edge Delivery Services
source-git-commit: 224cfe9853e8974c33b0e53e961a02d54f875a35
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---


# 通过Edge Delivery Services进行AEM创作 {#edge-dev-getting-started}

本指南将引导您启动并运行一个新的Adobe Experience Manager站点，该站点使用Edge Delivery Services和通用编辑器进行内容创作。

{{aem-authoring-edge-early-access}}

## 前提条件 {#prerequisites}

在开始阅读本指南之前，您应该已经熟悉的基础知识并有权访问Edge Delivery Services，包括：

* 您已完成 [Edge交付服务教程。](/help/edge/developer/tutorial.md)
* 您有权访问 [AEM Cloud Service沙盒。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
* 您有 [在同一沙盒环境中启用了通用编辑器。](/help/implementing/universal-editor/getting-started.md)

## 选择正确的编辑器 {#editor-choice}

AEM提供两种不同的内容编辑器，要使用的编辑器取决于您的情况。

* **通用编辑器**  — 这应该是新站点的默认选择。
* **AEM页面编辑器**  — 对于现有AEM Sites迁移到Edge Delivery Services，应选择此选项。

本指南重点介绍使用通用编辑器的Edge Delivery Services上的AEM项目。 查看文档 [针对Edge Delivery Services开发](/help/edge/developing.md) 有关选择正确的编辑器和将现有AEM站点迁移到Edge Delivery Services的更多详细信息。

## AEM创作和Edge Delivery Services快速入门 {#getting-started}

一旦你完成了 [先决条件](#prerequisites) 并且已经做了 [选择使用通用编辑器，](#editor-choice) 您可以开始自己的项目。

### 创建您的GitHub项目 {#create-github-project}

首先，您需要根据Adobe模板在GitHub上创建一个新项目。

1. 导航到 [`https://github.com/adobe-rnd/aem-boilerplate-xwalk`](https://github.com/adobe-rnd/aem-boilerplate-xwalk) 并单击 **使用此模板** 并选择 **创建新存储库**.

   * 您需要登录GitHub才能看到此选项。

   ![复制存储库项目](assets/edge-dev-getting-started/use-template-project.png)

1. 默认情况下，存储库将分配给您。 根据需要更改此设置，并提供存储库名称和描述，然后单击 **创建存储库**.

   ![创建存储库](assets/edge-dev-getting-started/create-repo.png)

1. 在同一浏览器的新选项卡中，导航到 [`https://github.com/apps/aem-code-sync`](https://github.com/apps/aem-code-sync) 并单击 **配置**.

   ![代码同步](assets/edge-dev-getting-started/configure-code-sync.png)

1. 单击 **配置** ，您在上一步中创建了新存储库的组织。

   ![选择用于代码同步的组织](assets/edge-dev-getting-started/code-sync-org.png)

1. 在“AEM代码同步GitHub”页面上，位于 **存储库访问权限**，选择 **仅选择存储库**，选择在上一步中创建的存储库，然后单击 **保存**.

   ![授予AEM代码同步访问权限](assets/edge-dev-getting-started/grant-code-sync-acces.png)

1. 安装AEM代码同步后，您将收到一个确认屏幕。 返回到新存储库的浏览器选项卡。

   ![代码同步安装确认](assets/edge-dev-getting-started/confirmation.png)

1. 单击 `fstab.yaml` 文件以打开它，然后 **编辑此文件** 图标进行编辑。

   ![fstab.yaml](assets/edge-dev-getting-started/fstab.png)

1. 编辑 `fstab.yaml` 文件来更新项目的挂载点。 将默认的Google文档URL替换为AEMas a Cloud Service创作实例的URL，然后单击 **提交更改……**.

   * `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`
   * 更改挂载点可告知Edge Delivery Services在何处查找站点的内容。

   ![更新fstab](assets/edge-dev-getting-started/fstab-update.png)

1. 根据需要添加提交消息，然后单击 **提交更改**，直接将其提交到 `main` 分支。

   ![正在提交更改](assets/edge-dev-getting-started/commit-fstab-changes.png)

1. 返回到存储库的根目录并单击 `paths.yaml` 然后 **编辑此文件** 图标。

   ![路径.yaml](assets/edge-dev-getting-started/paths.png)

1. 替换默认映射 `/content/<site-name>/:/` 并单击 **提交更改……**.

   * 提供您自己的 `<site-name>`. 您将在后续步骤中需要它。
   * 映射可告知Edge Delivery Services如何将AEM存储库中的内容映射到网站URL。

   ![正在更新路径.yaml](assets/edge-dev-getting-started/paths-update.png)

1. 根据需要添加提交消息，然后单击 **提交更改**，直接将其提交到 `main` 分支。

   ![正在提交更改](assets/edge-dev-getting-started/commit-fstab-changes.png)

### 创建和编辑新的AEM站点 {#create-aem-site}

现在您已经拥有GitHub项目，您必须创建一个项目可以使用的新AEM站点。

>[!NOTE]
>
>要使用通用编辑器编辑站点，必须使用基于Chromium的浏览器。

1. AEM Edge Delivery Services通过Adobe工程部门的 [项目Slack渠道。](/help/edge/docs/slack.md)

1. 登录到您的AEMas a Cloud Service创作实例，导航到站点控制台，然后点按或单击 **创建** -> **从模板创建站点**.

   ![从控制台创建新站点](assets/edge-dev-getting-started/create-site-console.png)

1. 在 **选择站点模板** 创建站点向导的选项卡，单击 **导入** 按钮以导入新模板。

   ![正在导入模板](assets/edge-dev-getting-started/site-templates.png)

1. 上载由Adobe工程团队为您提供的AEM创作和Edge Delivery Services站点模板。

1. 导入模板后，该模板将显示在向导中。 点按或单击以将其选定，然后点按或单击 **下一个**.

   ![选择模板](assets/edge-dev-getting-started/select-template.png)

1. 提供以下字段，然后点击或单击 **创建**.

   * **网站标题**  — 为站点添加描述性标题。
   * **网站标题**  — 使用 `<site-name>` 您在 [上一步。](#create-github-project)
   * **GitHub URL**  — 使用您在上一步中创建的GitHub项目的URL。

   ![站点详细信息](assets/edge-dev-getting-started/create-site-details.png)

1. AEM通过对话框确认站点创建。 点击或单击 **确定** 关闭。

   ![站点创建确认](assets/edge-dev-getting-started/site-creation-confirmation.png)

1. 在站点控制台上，导航到 `index.html` ，然后点按或单击 **编辑** 工具栏中。

   ![编辑新站点](assets/edge-dev-getting-started/new-site.png)

1. 将在新选项卡中打开通用编辑器。 您可能需要点按或单击 **使用Adobe登录** 验证以编辑您的页面。

   ![通用编辑器](assets/edge-dev-getting-started/universal-editor.png)

您现在可以使用通用编辑器编辑站点。 请参阅 [通用编辑器文档](/help/implementing/universal-editor/authoring.md) 以了解更多信息。

### 发布新站点 {#publishing}

使用通用编辑器编辑完新站点后，即可发布内容。

1. 在站点控制台上，选择您为新站点创建的所有页面，然后点按或单击 **快速发布** 工具栏中。

   ![选择要发布的页面](assets/edge-dev-getting-started/publishing.png)

1. 点击或单击 **Publish** 在确认对话框中启动流程。

   ![“发布”对话框](assets/edge-dev-getting-started/publish-confirmation.png)

1. 在同一浏览器中打开新选项卡，并导航到新站点的URL。

   * `https://main--<site-name>--<owner>.hlx.page`

1. 查看您的内容已发布。

   ![已发布内容](assets/edge-dev-getting-started/published-site.png)

## 后续步骤 {#next-steps}

现在，您已有一个用于Edge Delivery Services项目的AEM创作，您可以开始创建和设置自己的块。

请参阅指南 [创建指令用于通用编辑器的块](/help/edge/create-block.md) 以了解更多信息。
