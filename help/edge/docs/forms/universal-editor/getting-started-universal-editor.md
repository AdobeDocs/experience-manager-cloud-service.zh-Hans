---
title: 通用编辑器中 Edge Delivery Services for AEM Forms 快速入门——开发人员教程
description: 本教程将帮助您启动并运行新的 Adobe Experience Manager Forms (AEM) 项目。十到二十分钟后，您就可以在通用编辑器中创建自己的 Edge Delivery Services Forms。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 2b936b2495eb63defdb184320ae866bbecbe7546
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 100%

---


# 使用通用编辑器完成 Edge Delivery Services for AEM Forms 快速入门（所见即所得）

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| 基于通用编辑器的创作 | 本文 |
| 基于文档的创作 | [单击此处](/help/edge/docs/forms/tutorial.md) |


<span class="preview"> 此功能通过早期访问计划提供。要请求获得访问权限，请通过您的官方地址向 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> 发送电子邮件，并附上您的 GitHub 组织名称和存储库名称。例如，如果存储库 URL 为 https://github.com/adobe/abc，则组织名称为 adobe，存储库名称为 abc。</span>

在当今的数字时代，用户友好的表单对于所有组织都至关重要。Edge Delivery Services Forms 是使用通用编辑器创建的，提供了所见即所得（WYSIWYG）功能。它为高效的表单制作提供了一个现代化的直观界面。

AEM Forms 提供 Adaptive Forms Block，可帮助您轻松创建 Edge Delivery Services Forms，以捕获和存储数据。您可以[创建预先配置了 Adaptive Forms Block 的新 AEM 项目](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)或[将 Adaptive Forms Block 添加到现有的 AEM 项目](#add-adaptive-forms-block-to-your-existing-aem-project)。

![Github 存储库工作流](/help/edge/assets/repo-workflow.png){width=auto}

本教程将指导您使用通用编辑器的所见即所得创作功能，在新的或现有的 Adobe Experience Manager Site 项目中创建、预览和发布自己的表单。


## 先决条件

* 您有 GitHub 帐户，并且了解 Git 基础知识。
* 您了解 HTML、CSS 和 JavaScript 的基础知识。
* 您已安装 Node/npm 以进行本地开发。

## 创建预先配置了 Adaptive Forms Block 的新 AEM 项目

AEM Forms Boilerplate 模板可帮助您快速开始使用预先配置了 Adaptive Forms Block 的 AEM 项目。这是遵循 AEM 最佳实践并直接开始构建表单的最快、最简单的方法。

### 开始使用 AEM Forms 样板存储库模板

1. 为您的 AEM 项目创建 GitHub 存储库。创建存储库：
   1. 转到[https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)。

      ![AEM Forms Boilerplate](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. 单击&#x200B;**使用此模板**&#x200B;选项，然后选择&#x200B;**创建新存储库**&#x200B;选项。

      ![使用 AEM Forms Boilerplate 创建新存储库](/help/edge/docs/forms/assets/use-eds-form-template.png)

      将打开&#x200B;**创建新存储库**&#x200B;屏幕。

   1. 在&#x200B;**创建新存储库**&#x200B;屏幕上，选择&#x200B;**所有者**，并指定&#x200B;**存储库名称**。Adobe 建议将存储库设置为&#x200B;**公开**&#x200B;状态。因此，选择&#x200B;**公开**&#x200B;选项，然后单击&#x200B;**创建存储库**。

      ![将存储库设置为公开](/help/edge/docs/forms/assets/name-eds-repo.png)

1. 在您的存储库上安装 AEM Code Sync GitHub 应用程序。安装：
   1. 转到 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)。
   1. 在&#x200B;**安装 AEM Code Sync** 屏幕上，选择&#x200B;**仅选择存储库**&#x200B;选项，然后选择新创建的存储库。单击&#x200B;**保存**。

   ![将存储库设置为公开](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. 现在，将您使用 AEM Forms Boilerplate 创建的 GitHub 存储库链接到您的 AEM 项目创作环境。连接：

   1. 转到您之前使用 AEM Forms Boilerplate 创建的 GitHub 存储库。
   1. 打开 **fstab.yaml** 文件进行编辑。

      ![打开 fstab.yaml 文件](/help/edge/docs/forms/assets/open-fstab.png)

   1. 编辑 **fstab.yaml** 文件，更新您项目的挂载点。将 URL 替换为 AEM as a Cloud Service 创作实例的 URL。
      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![编辑 fstab.yaml 文件](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. 一旦更新了参考，并且一切看起来都很好，就提交更新后的 **fstab.yaml** 文件。

      ![提交更改](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      如果您遇到任何构建问题，请参阅[解决 GitHub 构建问题](#troubleshooting-github-build-issues)。

### 创建新的 AEM 项目

现在，您有了 GitHub 项目，可以继续在 AEM as a Cloud Service 创作实例中创建并发布新的 AEM 项目。
1. 要创建新的 AEM 项目，请执行以下操作：

   1. 登录 AEM as a Cloud Service 创作实例并选择 **Sites**。

      ![选择 Sites](/help/edge/assets/select-sites.png)

   1. 单击&#x200B;**创建** > **从模板创建 Site**。

      ![创建-Sites](/help/edge/docs/forms/assets/create-sites.png)

   1. 选择 Edge Delivery Services Site 模板并单击&#x200B;**下一步**。

      ![选择-Site-模板](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * 如果您的创作实例中没有 Edge Delivery Services Site 模板，请单击导入按钮上传模板。
      > * 您可以从 [GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases) 下载 Edge Delivery Services Site 模板 。

   1. 输入以下详细信息以创建新的 AEM 项目：
      * **Site 标题**——添加该 Site 的描述性标题。
      * **Site 标题**——使用在上一步定义的 `site-name`。
      * **GitHub URL**——使用在上一步创建的 GitHub 项目的 URL。

      ![创建 AEM Site](/help/edge/docs/forms/assets/create-aem-site.png)

   1. 出现&#x200B;**创建 Site** 对话框，单击&#x200B;**好的**。

      ![单击确定](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      只需几分钟，您的新 AEM 项目就创建完成了。

   1. 在 Sites 控制台中导航到新创建的 AEM 项目，然后单击&#x200B;**编辑**。
在此示例中，`index.html` 页面用于说明。

      ![编辑 AEM Site](/help/edge/docs/forms/assets/edit-site.png)

      AEM 项目会在新选项卡的通用编辑器中打开，实现所见即所得的创作。您现在可以编辑 AEM 项目。

      ![Site 在通用编辑器中打开](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. 发布您创建的 AEM 项目

   完成 AEM 项目编辑后，发布该项目。要发布：

   1. 在 Sites 控制台上，选择所有 AEM 项目页面，然后单击&#x200B;**快速发布**。

      ![发布 AEM Sites 项目](/help/edge/docs/forms/assets/publish-sites.png)

   1. 出现&#x200B;**快速发布**&#x200B;确认对话框，单击&#x200B;**发布**&#x200B;开始发布过程。

      ![快速发布确认对话框](/help/edge/docs/forms/assets/quick-publish.png)

      或者，您可以直接从通用编辑器用户界面发布 AEM 项目页面。

      ![快速发布确认对话框](/help/edge/docs/forms/assets/qui.png)

   恭喜！您有一个在 `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/` 上运行的新网站。

   * `<branch>` 指 GitHub 存储库的分支。
   * `<repository>` 表示您的 GitHub 存储库。
   * `<owner>` 指托管您 GitHub 存储库的 GitHub 帐户用户名。
   * `<site-name>` 指的是您创建的 Site 名称。

   例如，如果分支名称为 `main`，存储库为 `edsforms`，所有者为 `wkndforms` 且 `site-name` 为 `eds-forms`，则网站将在 `https://main--edsforms--wkndforms.aem.page/content/eds-forms/` 启动并运行

   >[!NOTE]
   >
   > * 要查看 AEM 项目的 `index.html` 页面，请使用以下 URL：`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * 要查看 AEM 项目以外的 `index page` 页面，请使用以下 URL：`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

现在，您可以开始[创建表单并将其添加到 AEM 项目](#add-edge-delivery-services-forms-to-aem-project)。

## 将 Adaptive Forms Block 添加到您现有的 AEM 项目

如果您有现有的 AEM 项目，则可以将 Adaptive Forms Block 集成到当前项目中以开始表单创建。

>[!NOTE]
>
>
> 此步骤适用于使用 [AEM Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-xwalk) 构建的项目。如果您使用 [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms) 创建 AEM 项目，则可以跳过此步骤。

进行集成：
1. **添加所需文件和文件夹**
   1. 将下列文件夹和文件从 [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms) 复制并粘贴到 AEM 项目中：

      * [Form Block](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) 文件夹
      * [form-common](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-common) 文件夹
      * [form-components](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-components) 文件夹
      * [form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) 文件
      * [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) 文件

1. **更新组件定义和模型文件**
   1. 导航到 AEM 项目中的 `../models/_component-definition.json` 文件，并根据 AEM Forms Boilerplate 中 [_component-definition.json 文件](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-definition.json#L39-L48)的更改进行更新。

   1. 导航到 AEM 项目中的 `../models/_component-models.json` 文件，并根据 AEM Forms Boilerplate 中 [_component-models.json 文件](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-models.json#L24-L26)的更改进行更新

1. **在编辑器脚本中添加表单编辑器**
   1. 导航到 AEM 项目中的 `../scripts/editor-support.js` 文件，并根据 AEM Forms Boilerplate 中 [editor-support.js 文件](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js#L105-L106)的更改进行更新
1. **更新 ESLint 配置文件**
   1. 导航到 AEM 项目中的 `../.eslintignore` 文件，并添加以下代码行，以防止出现与 Form Block 规则引擎相关的错误：

      ```
          blocks/form/rules/formula/*
          blocks/form/rules/model/*
      ```

1. 提交这些更改并将其推送到 GitHub 上的 AEM 项目存储库。

就是这样！Adaptive Forms Block 现在是您 AEM 项目的一部分。您可以[开始创建表单并将其添加到 AEM 项目](#add-edge-delivery-services-forms-to-aem-site-project)。

## 使用所见即所得方法创作表单

您可以在通用编辑器中打开 AEM 项目，进行所见即所得的创作，在这里您可以编辑项目并添加自适应表单分区，以便在 AEM 项目页面上包含 Edge Delivery Services Forms。

1. 将自适应表单分区添加到您的 AEM 项目页面。要添加：
   1. 在 Sites 控制台中导航到 AEM 项目，选择要编辑的 Site 页面，然后单击&#x200B;**编辑**。AEM 项目页面将在通用编辑器中打开以供编辑。
在此示例中，`index.html` 页面用于说明。
   1. 打开内容树，导航到要添加自适应表单分区的区域。
   1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标，然后从组件列表中选择&#x200B;**[!UICONTROL 自适应表单]**&#x200B;组件。

   ![内容树](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   添加了自适应表单分区。您现在可以开始将表单组件添加到 AEM 项目页面。

1. 将表单组件添加到已添加的自适应表单分区。要添加表单组件：
   1. 导航到内容树中已添加的自适应表单分区。

      ![Adaptive Forms Block 已添加](/help/edge/docs/forms/assets/adative-form-block.png)


   1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标，然后从&#x200B;**自适应表单组件**&#x200B;列表中添加所需的组件。

      ![添加组件](/help/edge/docs/forms/assets/add-component.png)

      您还可以拖放所需的自适应表单组件，因为通用编辑器提供了直观的拖放功能。

   1. 选择已添加的自适应表单组件，使用&#x200B;**[!UICONTROL 属性]**&#x200B;更新其属性。

      ![打开属性](/help/edge/docs/forms/assets/component-properties.png)

   1. 预览表单。
下面的屏幕快照显示了使用所见即所得创作在 AEM 项目中创作的表单：

      ![已添加的表单](/help/edge/docs/forms/assets/added-form-aem-sites.png)

      预览满意后，用户可以继续发布页面。

      >[!NOTE]
      >
      > 重要的是，更改后要再次发布 AEM 项目页面。否则，浏览器中将无法看到更新。

1. 重新发布 AEM 项目页面。

   1. 单击&#x200B;**发布**，添加表单后再次发布 AEM 项目页面。

      ![发布表单](/help/edge/docs/forms/assets/publish-form.png)

   1. 屏幕上出现&#x200B;**发布**&#x200B;确认对话框，单击&#x200B;**发布**&#x200B;开始发布。

      ![发布表单1](/help/edge/docs/forms/assets/publish-form1.png)

      单击&#x200B;**发布**&#x200B;按钮后，出现 `Publish started successfully` 消息。

      ![发布表单2](/help/edge/docs/forms/assets/publish-form2.png)

   您现在可以通过以下 URL 查看添加了 Edge Delivery Services Form 的 AEM 项目页面：
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`。

   例如，如果分支名称为 `main`，存储库为 `edsforms`，所有者为 `wkndforms` 且 Site 名称为 `eds-forms`，URL 应为：
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![索引页面](/help/edge/docs/forms/assets/publish-index-page.png)

您可以通过编辑 Adaptive Forms Block 中的 `.css` 和 `.js` 文件并[设置本地 AEM 开发环境](#set-up-local-aem-development-environment)在浏览器中立即查看更改。

>[!NOTE]
>
> 您还可以[在通用编辑器中创作独立的表单，并将其发布到 Edge Delivery Services。](/help/edge/docs/forms/universal-editor/create-forms.md)

## 设置本地 AEM 开发环境

您可以设置本地 AEM 开发环境，以便在本地开发自定义样式和组件。要启动并运行本地 AEM 开发环境：

1. **安装 AEM CLI**：AEM CLI 简化了开发任务。让我们使用 npm 全局安装它：

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **克隆您的 GitHub 项目**：使用以下命令从 GitHub 克隆您的 AEM 项目存储库，替换为 <owner> 存储库所有者和 <repo> 存储库名称：

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **启动本地环境**：导航到项目目录并使用单个命令开始本地 AEM 实例：

   ```
   cd <repo>
   aem up
   ```

您可以在 Adaptive Forms Block `blocks/form` 文件夹中进行本地更改，以便为您的表单设计样式和编码！编辑此目录中的 `.css` 或 `.js` 文件，您可以看到这些更改会立即反映在您的浏览器中。

完成更改后，使用 Git 命令提交并推送。这将更新可通过以下 URL 访问的预览和生产环境（将占位符替换为您的项目详细信息）：

预览：`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`

正式版：`https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## 解决 GitHub 构建问题

通过解决潜在问题，确保 GitHub 构建过程顺利进行：

* **处理 Linting 错误：**
如果您遇到任何 Linting 错误，可以绕过它们。打开 [EDS Project]/package.json 文件并将 “lint” 脚本从 `"lint": "npm run lint:js && npm run lint:css"` 修改为 `"lint": "echo 'skipping linting for now'"`。保存文件并将更改提交到您的 GitHub 项目。

* **解决模块路径错误：**
如果遇到错误“无法解析模块 &quot;&#39;../../scripts/lib-franklin.js&#39; 的路径”，请导航至 [EDS 项目]/blocks/forms/form.js 文件。将 lib-franklin.js 文件替换为 aem.js 文件，可更新导入语句。

## 另请参阅

{{universal-editor-see-also}}
