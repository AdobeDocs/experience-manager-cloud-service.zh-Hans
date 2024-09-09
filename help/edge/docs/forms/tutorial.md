---
title: AEM FormsEdge Delivery Services快速入门 — 开发人员教程
description: 本教程将帮助您启动并运行新的 Adobe Experience Manager Forms (AEM) 项目。在十到二十分钟内，您将创建自己的表格。
feature: Edge Delivery Services
exl-id: bb7e93ee-0575-44e1-9c5e-023284c19490
role: Admin, Architect, Developer
source-git-commit: 4a8153ffbdbc4da401089ca0a6ef608dc2c53b22
workflow-type: tm+mt
source-wordcount: '1850'
ht-degree: 98%

---

# 快速入门 - 开发人员教程

在当今的数字时代，创建用户友好的表单对于任何组织都至关重要。AEM Forms (EDS)Edge Delivery Services允许您使用熟悉的工具(如Google文档和Microsoft Office)创建表单。

这些表单可将数据直接提交到 Microsoft Excel 或 Google Sheets 文件，使您能够使用 Google Sheets、Microsoft Excel 和 Microsoft SharePoint 充满活力的生态系统和强大的 API 来轻松处理提交的数据或启动现有的业务工作流程。

AEM Forms 提供了一个称为 Adaptive Forms Block 的区块，可帮助您轻松创建表单来捕获和存储捕获的数据。您可以[创建一个预先配置了 Adaptive Forms Block 的新 AEM 项目](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)或[将 Adaptive Forms Block 添加到现有的 AEM 项目](#add-adaptive-forms-block-to-your-existing-aem-project)。

本 AEM Forms 教程将指导您使用新的 Adobe Experience Manager (AEM) Forms 项目创建、预览和发布您自己的自定义表单。

## 先决条件

* 您有 GitHub 帐户，并且了解 Git 基础知识。
* 您有一个 Google 或 Microsoft SharePoint 帐户。
* 您了解 HTML、CSS 和 JavaScript 的基础知识。
* 您已安装 Node/npm 以进行本地开发。

**小心！** 本教程使用 macOS、Chrome 和 Visual Studio Code。虽然这些步骤可以针对其他设置进行调整，但屏幕截图和特定 UI 元素可能会根据您选择的操作系统、浏览器和代码编辑器而有所不同。


## 创建一个预配置了 Adaptive Forms Block 的新 AEM 项目

AEM Forms Boilerplate 模板可帮助您快速开始使用预先配置了 Adaptive Forms Block 的 AEM 项目。这是遵循 AEM 最佳实践并直接开始构建表单的最快、最简单的方法。

### 开始使用 AEM Forms 样板存储库模板

1. 为您的 AEM 项目创建 GitHub 存储库。创建存储库：
   1. 转到[https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)。

      ![AEM Forms Boilerplate](/help/edge/assets/aem-forms-boilerplate.png)
   1. 单击&#x200B;**“使用此模板”**&#x200B;选项，然后选择&#x200B;**“创建新存储库”**&#x200B;选项。将打开创建新存储库屏幕。

      ![使用 AEM Forms Boilerplate 创建新存储库](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. 在创建新存储库屏幕上，选择“**所有者**”，并指定&#x200B;**存储库名称**。Adobe 建议将存储库设置为&#x200B;**公开**&#x200B;状态。因此，选择&#x200B;**“公开”**&#x200B;选项，然后单击&#x200B;**“创建存储库”**。

   ![将存储库设置为公开](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. 在您的存储库上安装 AEM Code Sync GitHub 应用程序。安装：
   1. 转到 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)。
   1. 在“安装 AEM Code Sync”屏幕上，选择“**仅选择存储库**”选项，然后选择新创建的存储库。单击“保存”。

   ![将存储库设置为公开](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > 如果您使用带有 IP 过滤功能的 GitHub Enterprise，则可以将以下 IP 添加到允许列表：3.227.118.73

   恭喜！您有一个在 `https://<branch>--<repo>--<owner>.hlx.page/` 上运行的新网站。

   * `<branch>` 指 GitHub 存储库的分支。
   * `<repository>` 表示您的 GitHub 存储库。
   * `<owner>` 指托管您 GitHub 存储库的 GitHub 帐户用户名。

   例如，如果分支名称为 `main`，存储库为 `wefinance`，所有者为 `wkndforms`，则网站将在 [https://main--wefinance--wkndforms.hlx.page/](https://main--wefinance--wkndforms.hlx.page/) 启动并运行。



### 链接您自己的内容源

您新创建的 GitHub 存储库指向[存储在 Google Drive 文件夹](https://drive.google.com/drive/folders/1bvjfi6TqpYA7DvbX6kKc-m7FgHuJ4RUQ)中的示例内容。此只读内容为您的表单提供了一个很好的起点。请随意将其复制到您自己的 Google Drive 中并对其进行自定义以满足您的需求。

![Google Drive 上的示例内容](/help/edge/assets/folder-with-sample-content.png)

要将示例内容复制到您自己的内容文件夹并将 GitHub 存储库指向您自己的内容文件夹：

1. 在 Google Drive 或 Microsoft SharePoint 中专门为您的 AEM 内容创建一个新文件夹。本文档使用在 Microsoft SharePoint 上创建的文件夹。

1. 与 Adobe Experience Manager 用户（helix@adobe.com）共享该文件夹。

   ![使用“管理访问权限”选项与 AEM 用户共享文件夹 - SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![使用“管理访问权限”选项与 AEM 用户共享文件夹 - Google Drive](/help/edge/assets/share-google-drive-folder.png)


   确保您已向 Adobe Experience Manager 用户提供对该文件夹的编辑权限。

   ![与 AEM 用户共享文件夹，提供编辑权限- SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png)

   ![与 AEM 用户共享文件夹，提供编辑权限 - Google Drive](/help/edge/assets/add-aem-user-google-folder.png)

1. 将 [Google Drive 文件夹中存储的示例内容复制到](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_)您的文件夹。复制：

   1. 一起下载文件或下载单个文件。

      ![下载示例内容](/help/edge/assets/download-sample-content.png)

      `nav` 和 `footer` 文件定义页面的基本版面，在整个项目中很少更改。它们还具有与大多数其他内容文件不同的特定结构。通过检查这些文件，您将了解 AEM 项目中内容的组织方式。


   1. 将这些文件上传到 Microsoft SharePoint 或 Google Drive 文件夹。

      ![Google Drive 上的示例内容](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      确保您`enquiry`将示例内容中的工作表复制到 Google Drive 或 Microsoft SharePoint 上的文件夹中。它包含样本表单的结构。

1. 现在您已经设置了内容文件夹，是时候将其链接到您之前使用 AEM Forms Boilerplate 创建的 GitHub 上的项目了。连接：

   1. 转到您之前使用 AEM Forms Boilerplate 创建的 GitHub 存储库。
   1. 打开 `fstab.yaml` 以供编辑。
   1. 将现有引用替换为您与 AEM 用户共享的文件夹的路径（helix@adobe.com）。

      ![Google Drive 上的示例内容](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      如果您使用 Microsoft SharePoint，则文件夹路径将使用以下格式：

      ```HTML
      https://<tenant>.SharePoint.com/sites/<sp-site>/Shared%20Documents/<folder-name>
      ```

      例如，

      ```HTML
      https://adobe.SharePoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      有关使用 Microsoft SharePoint 管理文件的更多信息，请参阅[如何使用 Adobe SharePoint](https://www.aem.live/docs/setup-customer-sharepoint)。


   1. 提交更新的`fsatb.yaml`文件，一旦您更新了参考并且一切看起来都很好。如果您遇到任何构建问题，请参阅 [解决 GitHub 构建问题](#troubleshooting-github-build-issues)。



      ![提交更新的 fsatab.yaml 文件](/help/edge/assets/commit-updated-fstab-yaml.png)

      这会将您的内容文件夹连接到您的网站。更新参考后，您最初可能会遇到“404 未找到”错误。这是因为您的内容尚未预览。下一部分将介绍如何开始创作和预览内容。



### 预览和发布内容

完成最后一步后，您的新内容源不为空，但在升级到预览或实时阶段之前，它不会在您的网站上可见。目前，这可能会导致 404 错误。

要预览未发布的内容：

1. 安装名为 [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo) 的 Chrome 扩展程序。

   ![安装 AEM SideKick](/help/edge/assets/install-aem-sidekick.png)

   将扩展程序安装到 Chrome 后，不要忘记固定它，这样可以更轻松地找到它。

   ![固定 AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. 要设置 Sidekick Chrome 扩展程序，请转到之前共享的 Google Drive 或 Microsoft SharePoint 文件夹，右键单击浏览器工具栏中的扩展程序图标，然后选择 `Add this project`。

   ![AEM Sidekick - 添加项目](/help/edge/assets/aem-sidekick-add-a-project.png)

   安装扩展程序并添加项目后，您就可以预览和发布 Google Drive 中的内容。

1. 选择 Microsoft SharePoint 或 Google Drive 文件夹中的所有文档。您可以通过在单击时按住 Ctrl 键 (Windows/Linux) 或 Cmd 键 (Mac) 选择多个文档。

   ![选择所有文件](/help/edge/assets/select-all-files.png)

1. 单击固定到 Chrome 扩展栏的 AEM Sidekick 图标。屏幕上会出现一个工具栏。您可以选择预览或发布您的内容。

   如果您复制 `index`、`nav`、`footer` 和 `enquiry` 文件，所有这些都是单独的文档，具有自己的预览和发布周期，因此请确保预览（和发布）所有这些文件。

   预览文件后，新的浏览器选项卡会显示文档。要预览示例表单，请访问以下 URL：


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.live
   ```

   * `<branch>` 指 GitHub 存储库的分支。
   * `<repository>` 表示您的 GitHub 存储库。
   * `<owner>` 指托管您 GitHub 存储库的 GitHub 帐户用户名。


   `https://<branch>--<repo>--<owner>.hlx.page/enquiry` URL.

   例如，如果您的项目存储库名为“wefinance”，位于帐户所有者“wkndforms”下，并且您使用的是“main”分支，则 URL 为：

   [https://main--wefinance--wkndforms.hlx.page](https://main--wefinance--wkndforms.hlx.page)

### 创建表单

示例内容包括一个“查询”表，用作“查询”表单的模板。工作表的每一行代表一个[表单字段](/help/edge/docs/forms/form-components.md#available-components)，并且列标题定义[字段属性](/help/edge/docs/forms/form-components.md#available-components)。此示例表单让您在构建表单方面取得了先机。

![查询表格](/help/edge/docs/forms/assets/enquiry-form-microsoft-sharepoint.png)

让我们从更新字段标签开始。打开“查询”表进行编辑，将提交按钮的标签更改为 `Let's Chat`，并使用 AEM Sidekick 预览和发布该文件。

![查询表格](/help/edge/assets/enquiry-form-preview-publish.png)

当您预览或发布文件时，该文件的 JSON 版本将显示在新选项卡中。复制文件的预览 (.hlx.page) 或发布 (.hlx.live) URL。

![表单电子表格的 JSON](/help/edge/assets//preview-and-publish-enquiry-form.png)

打开 `enquiry` 文件，并将表单区块中的 URL 替换为上一步中复制的文件的 URL。确保 URL 是超链接。

![带有电子表格 URL 的 .json URL 的查询文件](/help/edge/assets/enquiry-doc-to-embed-form.png)

使用 AEM Sidekick 预览和发布查询文件。

![带有电子表格 URL 的 .json URL 的查询文件](/help/edge/assets/preview-and-publish-enquiry-document.png)


要预览更新后的查询表单，请访问以下 URL：


```HTML
    https://<branch>--<repository>--<owner>.hlx.page/enquiry
       
```

提交按钮的标签更新为 `Let's Chat`。

![查询表格](/help/edge/assets/updated-form.png)

有关创建和发布新表单的详细信息，请参阅[创建表单](/help/edge/docs/forms/create-forms.md)指南。

### 开始开发样式和功能


立即启动并运行本地 AEM 开发环境：

1. 安装 AEM CLI：AEM CLI 简化了开发任务。让我们使用 npm 全局安装它：

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. 克隆您的 GitHub 项目：使用以下命令从 GitHub 克隆您的项目存储库，替换为 <owner> 存储库所有者和 <repo> 存储库名称：

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. 启动本地环境：导航到项目目录并使用单个命令启动本地 AEM 实例：

   ```
   cd <repo>
   aem up
   ```

Adaptive Forms Block `blocks/form` 文件夹是您表单样式和代码的游乐场！编辑此目录中的任何 `.css` 或 `.js` 文件，您将看到更改立即反映在浏览器中。

准备好展示您的创作了吗？使用 Git 提交并推送您的更改。这将更新可通过以下 URL 访问的预览和生产环境（将占位符替换为您的项目详细信息）：

预览：`https://<branch>--<repo>--<owner>.hlx.page/`
制作：`https://<branch>--<repo>--<owner>.hlx.live/`

恭喜！您已成功设置本地开发环境并部署了更改。



## 将 Adaptive Forms Block 添加到您现有的 AEM 项目


>[!VIDEO](https://video.tv.adobe.com/v/3427789)

如果您有现有的 AEM 项目，则可以将 Adaptive Forms Block 集成到当前项目中以开始表单创建。

>[!NOTE]
>
>
> 此步骤适用于使用 [AEM Boilerplate](https://github.com/adobe/aem-boilerplate) 构建的项目。如果您使用 [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms) 创建 AEM 项目，则可以跳过此步骤。

集成：

1. 将 Adaptive Forms Block 存储库 [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) 克隆到您的计算机。

1. 在下载的文件夹中，找到 `blocks/form` 文件夹。复制此文件夹。现在，导航到 AEM 项目的本地 `blocks` 文件夹并将复制的表单文件夹粘贴到此处。

1. 提交这些更改并将其推送到 GitHub 上的 AEM 项目。


就是这样！Adaptive Forms Block 现在是您的 AEM 项目的一部分。您可以开始创建表单并将其添加到 AEM 页面。


## 解决 GitHub 构建问题

通过解决潜在问题，确保 GitHub 构建过程顺利进行：

* **解决模块路径错误：**
如果遇到错误“无法解析模块 &quot;&#39;../../scripts/lib-franklin.js&#39; 的路径”，请导航至 [EDS 项目]/blocks/forms/form.js 文件。将 lib-franklin.js 文件替换为 aem.js 文件，可更新导入语句。

* **处理 Linting 错误：**
如果您遇到任何 Linting 错误，可以绕过它们。打开 [EDS Project]/package.json 文件并将“lint”脚本从 `"lint": "npm run lint:js && npm run lint:css"` 修改为 `"lint": "echo 'skipping linting for now'"`。保存文件并将更改提交到您的 GitHub 项目。


## 另请参阅

{{see-more-forms-eds}}
