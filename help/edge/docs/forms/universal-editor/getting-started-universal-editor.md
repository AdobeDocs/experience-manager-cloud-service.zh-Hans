---
title: 通用编辑器中的AEM FormsEdge Delivery Services快速入门 — 开发人员教程
description: 本教程将帮助您启动并运行新的 Adobe Experience Manager Forms (AEM) 项目。10到20分钟后，您将在通用编辑器中创建自己的Edge Delivery ServicesForms 。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: c27b8e413c060de601a72a669d86c4add2a4167d
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 23%

---


# 使用通用编辑器(WYSIWYG)的AEM FormsEdge Delivery Services快速入门

在当今的数字时代，用户友好的表单对于所有组织都至关重要。 Edge Delivery ServicesForms使用通用编辑器创建，该编辑器提供了WYSIWYG（所见即所得）功能。 它提供了一个现代、直观的界面，以实现高效的表单创作。

AEM Forms提供了一个称为自适应Forms块的块，以帮助您轻松创建Edge Delivery ServicesForms以捕获和存储数据。 您可以[创建预配置了自适应Forms块的新AEM项目](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)或[将自适应Forms块添加到现有AEM项目](#add-adaptive-forms-block-to-your-existing-aem-project)。

本教程将指导您使用通用编辑器的WYSIWYG创作，通过新的或现有的Adobe Experience Manager站点项目创建、预览和发布您自己的表单。


## 先决条件

* 您有 GitHub 帐户，并且了解 Git 基础知识。
* 您有一个 Google 或 Microsoft SharePoint 帐户。
* 您了解 HTML、CSS 和 JavaScript 的基础知识。
* 您已安装 Node/npm 以进行本地开发。

## 创建一个预配置了 Adaptive Forms Block 的新 AEM 项目

AEM Forms Boilerplate 模板可帮助您快速开始使用预先配置了 Adaptive Forms Block 的 AEM 项目。这是遵循AEM最佳实践并快速开始构建表单的最快、最简单的方法。

### 开始使用 AEM Forms 样板存储库模板

1. 为您的 AEM 项目创建 GitHub 存储库。创建存储库：
   1. 转到[https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)。

      ![AEM Forms Boilerplate](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. 单击&#x200B;**使用此模板**&#x200B;选项并选择&#x200B;**新建存储库**&#x200B;选项。

      ![使用 AEM Forms Boilerplate 创建新存储库](/help/edge/docs/forms/assets/use-eds-form-template.png)

      将打开&#x200B;**新建存储库**&#x200B;屏幕。

   1. 在&#x200B;**创建新存储库**&#x200B;屏幕上，选择&#x200B;**所有者**，并指定&#x200B;**存储库名称** 。 Adobe建议将存储库设置为&#x200B;**Public**。 因此，选择&#x200B;**“公开”**&#x200B;选项，然后单击&#x200B;**“创建存储库”**。

      ![将存储库设置为公开](/help/edge/docs/forms/assets/name-eds-repo.png)

1. 在您的存储库上安装 AEM Code Sync GitHub 应用程序。安装：
   1. 转到 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)。
   1. 在&#x200B;**安装AEM代码同步**&#x200B;屏幕上，选择&#x200B;**仅选择存储库**&#x200B;选项并选择新创建的存储库。 单击&#x200B;**保存**。

   ![将存储库设置为公开](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. 现在，将使用AEM Forms样板创建的GitHub存储库链接到您的AEM项目创作环境。 连接：

   1. 转到您之前使用 AEM Forms Boilerplate 创建的 GitHub 存储库。
   1. 打开&#x200B;**fstab.yaml**&#x200B;文件进行编辑。

      ![打开fstab.yaml文件](/help/edge/docs/forms/assets/open-fstab.png)

   1. 编辑&#x200B;**fstab.yaml**文件以更新项目的挂载点。 将URL替换为AEM as a Cloud Service创作实例的URL。
      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![编辑fstab.yaml文件](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. 提交更新的&#x200B;**fstab.yaml**&#x200B;文件，一旦更新了引用并且一切正常。

      ![提交更改](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      如果您遇到任何构建问题，请参阅 [解决 GitHub 构建问题](#troubleshooting-github-build-issues)。

### 创建新的AEM项目

现在您已经拥有GitHub项目，您可以继续在AEM as a Cloud Service创作实例中创建和发布新的AEM项目。
1. 要创建新的AEM项目，请执行以下操作：

   1. 登录到AEM as a Cloud Service创作实例并选择&#x200B;**站点**。

      ![选择站点](/help/edge/assets/select-sites.png)

   1. 单击&#x200B;**从模板创建** > **站点**。

      ![创建站点](/help/edge/docs/forms/assets/create-sites.png)

   1. 选择Edge Delivery Services站点模板，然后单击&#x200B;**下一步**。

      ![select-site-template](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * 如果Edge Delivery Services站点模板在创作实例中不可用，请单击“导入”按钮上传模板。
      > * 您可以从[GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)下载Edge Delivery Services站点模板。

   1. 输入以下详细信息以创建新的AEM项目：
      * **站点标题** - 添加该站点的描述性标题。
      * **网站标题** — 使用您在上一步中定义的`site-name`。
      * **GitHub URL** - 使用在上一步创建的 GitHub 项目的 URL。

      ![创建AEM站点](/help/edge/docs/forms/assets/create-aem-site.png)

   1. 出现&#x200B;**创建站点**&#x200B;对话框，请单击&#x200B;**确定**。

      ![单击“确定”](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      在几分钟内，您的新AEM项目即创建完毕。

   1. 导航到站点控制台中新创建的AEM项目，然后单击&#x200B;**编辑**。
在本例中，`index.html`页面用于进行说明。

      ![编辑AEM站点](/help/edge/docs/forms/assets/edit-site.png)

      AEM项目将在通用编辑器的新选项卡中打开，从而启用WYSIWYG创作功能。 您现在可以编辑您的AEM项目。

      在通用编辑器中打开![站点](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. Publish您创建的AEM项目

   完成编辑AEM项目后，请发布该项目。 要发布：

   1. 在站点控制台上，选择所有AEM项目页面，然后单击&#x200B;**快速Publish**。

      ![发布AEM Sites项目](/help/edge/docs/forms/assets/publish-sites.png)

   1. 出现&#x200B;**快速Publish**&#x200B;确认对话框，单击&#x200B;**Publish**&#x200B;开始发布过程。

      ![快速Publish确认对话框](/help/edge/docs/forms/assets/quick-publish.png)

      或者，您也可以直接从通用编辑器用户界面发布AEM项目页面。

      ![快速Publish确认对话框](/help/edge/docs/forms/assets/qui.png)

   恭喜！您有一个在 `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/` 上运行的新网站。

   * `<branch>` 指 GitHub 存储库的分支。
   * `<repository>` 表示您的 GitHub 存储库。
   * `<owner>` 指托管您 GitHub 存储库的 GitHub 帐户用户名。
   * `<site-name>`引用您创建的站点名称的名称。

   例如，如果分支名称为`main`，存储库为`edsforms`，所有者为`wkndforms`且`site-name`为`eds-forms`，则网站将在`https://main--edsforms--wkndforms.aem.page/content/eds-forms/`启动并运行

   >[!NOTE]
   >
   > * 要查看AEM项目的`index.html`页面，请使用URL： `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * 若要查看AEM项目的`index page`以外的页面，请使用URL： `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

现在，您可以开始[创建表单并将其添加到您的AEM项目](#add-edge-delivery-services-forms-to-aem-project)。

## 将自适应Forms块添加到您现有的AEM项目

如果您有现有的 AEM 项目，则可以将 Adaptive Forms Block 集成到当前项目中以开始表单创建。

>[!NOTE]
>
>
> 此步骤适用于使用 [AEM Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-xwalk) 构建的项目。如果您使用 [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms) 创建 AEM 项目，则可以跳过此步骤。

集成：

1. 将自适应Forms块GitHub存储库[https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)克隆到您的计算机。
1. 在下载的文件夹中，找到`blocks/form`文件夹并复制此文件夹。
1. 将AEM项目GitHub存储库克隆到计算机。
1. 现在，导航到本地AEM项目存储库中的`blocks`文件夹，并将复制的表单文件夹粘贴到该文件夹中。
1. 提交这些更改并将其推送到GitHub上的AEM项目存储库。

就是这样！自适应Forms块现在包含在您的AEM项目中。 您可以[开始创建表单并将其添加到您的AEM项目](#add-edge-delivery-services-forms-to-aem-site-project)。

## 使用WYSIWYG创作AEM Forms

您可以在通用编辑器中打开AEM项目以进行WYSIWYG创作，您可以在该编辑器中编辑项目并添加自适应表单部分，以在AEM项目页面上包含Edge Delivery Services表单。

1. 将“自适应表单”部分添加到您的AEM项目页面。 要添加：
   1. 导航到站点控制台中的AEM项目，然后单击&#x200B;**编辑**。 “AEM项目”页面将在通用编辑器中打开以进行编辑。
在本例中，`index.html`页面用于进行说明。
   1. 打开内容树并导航到要添加自适应表单部分的位置。
   1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标并从组件列表中选择&#x200B;**[!UICONTROL 自适应表单]**&#x200B;组件。

   ![内容树](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   自适应表单部分会添加到指定位置。 您现在可以开始将表单组件添加到“AEM项目”页面。

1. 将表单组件添加到添加的自适应表单部分。 要添加表单组件：
   1. 导航到内容树中添加的自适应表单部分。

      已添加![自适应表单块](/help/edge/docs/forms/assets/adative-form-block.png)


   1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标，然后从&#x200B;**自适应表单组件**&#x200B;列表中添加所需的组件。

      ![添加组件](/help/edge/docs/forms/assets/add-component.png)

      您还可以拖放所需的自适应Forms组件，因为通用编辑器提供了直观的拖放功能。

   1. 选择添加的自适应表单组件以使用&#x200B;**[!UICONTROL 属性]**&#x200B;更新其属性。

      ![打开属性](/help/edge/docs/forms/assets/component-properties.png)

      以下屏幕截图显示了使用WYSIWYG创作在AEM项目中创作的表单：

      ![已添加表单](/help/edge/docs/forms/assets/added-form-aem-sites.png)

   >[!NOTE]
   >
   > 进行更改后再次发布AEM项目页面很重要；否则，更新在浏览器中不可见。

1. 重新发布AEM项目页面。

   1. 单击&#x200B;**Publish**&#x200B;可在添加表单后再次发布AEM项目页面。

      ![发布表单](/help/edge/docs/forms/assets/publish-form.png)

   1. 屏幕上将显示&#x200B;**Publish**&#x200B;确认对话框，请单击&#x200B;**Publish**&#x200B;开始发布。

      ![发布表单1](/help/edge/docs/forms/assets/publish-form1.png)

      单击&#x200B;**Publish**&#x200B;按钮后，将显示`Publish started successfully`消息。

      ![发布表单2](/help/edge/docs/forms/assets/publish-form2.png)

   现在，您可以在以下URL查看添加了的“Edge Delivery Services表单”的“AEM项目”页面：
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`。

   例如，如果分支名称为`main`，存储库为`edsforms`，所有者为`wkndforms`，站点名称为`eds-forms`，则URL将为：
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![索引页](/help/edge/docs/forms/assets/publish-index-page.png)

您可以通过编辑Adaptive Forms块中的`.css`和`.js`文件以及[设置本地AEM开发环境](#set-up-local-aem-development-environment)来设置FormsEdge Delivery Services的样式，以便在浏览器中立即查看更改。

## 设置本地AEM开发环境

您可以设置本地AEM开发环境，以便在本地开发自定义样式和组件。 使用本地AEM开发环境启动并运行：

1. **安装AEM CLI**： AEM CLI简化了开发任务。 让我们使用 npm 全局安装它：

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **克隆GitHub项目**：使用以下命令从GitHub克隆AEM项目存储库，替换 <owner> 存储库所有者和 <repo> 存储库名称：

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **启动本地环境**：导航到项目目录，然后使用一条命令启动本地AEM实例：

   ```
   cd <repo>
   aem up
   ```

您可以在Adaptive Forms Block `blocks/form`文件夹中进行本地更改，以便为表单设置样式和编码！ 编辑此目录中的`.css`或`.js`文件，您会看到所做的更改会立即反映在浏览器中。

完成更改后，使用Git命令提交和推送更改。 这将更新您的预览和生产环境，可通过以下URL访问（将占位符替换为项目详细信息）：

预览：`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
制作：`https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## 解决 GitHub 构建问题

通过解决潜在问题，确保 GitHub 构建过程顺利进行：

* **处理 Linting 错误：**
如果您遇到任何 Linting 错误，可以绕过它们。打开 [EDS Project]/package.json 文件并将 “lint” 脚本从 `"lint": "npm run lint:js && npm run lint:css"` 修改为 `"lint": "echo 'skipping linting for now'"`。保存文件并将更改提交到您的 GitHub 项目。

<!-- * **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file. -->
