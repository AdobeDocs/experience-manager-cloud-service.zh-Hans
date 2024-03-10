---
title: AEM FormsEdge Delivery Services快速入门 — 开发人员教程
description: 本教程可帮助您启动并运行新的Adobe Experience Manager Forms (AEM)项目。 10到20分钟后，您将创建自己的表单。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 30dfe0cfd7f845ba7a27699db22f8c4e61a0f7ed
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 12%

---


# 快速入门 - 开发人员教程

在当今的数字时代，创建用户友好的表单对于任何组织都至关重要。AEM FormsEdge Delivery Services(EDS)允许您使用熟悉的工具(如Google文档和Microsoft Office)创建表单。

这些表单可将数据直接提交到 Microsoft Excel 或 Google Sheets 文件，使您能够使用 Google Sheets、Microsoft Excel 和 Microsoft Sharepoint 充满活力的生态系统和强大的 API 来轻松处理提交的数据或启动现有的业务工作流程。

AEM Forms提供了一个称为自适应Forms块的块，以帮助您轻松创建表单以捕获和存储捕获的数据。 您可以创建一个预配了自适应Forms块的新AEM项目，或将该自适应Forms块添加到现有AEM项目中。

此AEM Forms教程将指导您使用新的Adobe Experience Manager (AEM) Forms项目创建、预览和发布自己的自定义表单。 您还将学习将自适应Forms块添加到现有AEM项目。

* **[创建预配了自适应Forms块的新AEM项目](#create-a-new-eds-project-pre-equipped-with-adaptive-forms-block)**
* **[将自适应Forms块添加到现有AEM项目](#add-adaptive-forms-block-to-an-existing-eds-project)**



## 先决条件

* 您拥有GitHub帐户，并了解Git基础知识。
* 您拥有Google或Microsoft SharePoint帐户。
* 您了解HTML、CSS和JavaScript的基础知识。
* 您已安装Node/npm以进行本地开发。

**抬头！** 本教程使用macOS、Chrome和Visual Studio Code。 虽然这些步骤可以适应其他设置，但屏幕截图和特定UI元素可能会因您选择的操作系统、浏览器和代码编辑器而异。


## 创建预配了自适应Forms块的新AEM项目

AEM Forms样板模板可帮助您快速开始使用预配置了Adaptive Forms Block的AEM项目。 这是遵循AEM最佳实践并快速开始构建表单的最快速、最简单的方法。

### AEM Forms样板存储库模板快速入门

1. 为您的AEM项目创建Github存储库。 要创建存储库，请执行以下操作：
   1. 转到 [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms样板](/help/edge/assets/aem-forms-boilerplate.png)
   1. 单击 **使用此模板** 选项，然后选择 **创建新存储库** 选项。 此时将打开“创建新存储库”屏幕。

      ![使用AEM Forms样板创建新存储库](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. 在“创建新存储库”屏幕上，选择 **所有者**，并指定 **存储库名称** . Adobe建议将存储库设置为 **公共**. 因此，请选择 **公共** 选项，然后单击 **创建存储库**.

   ![将存储库设置为公共](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. 在存储库中安装AEM代码同步GitHub应用程序。 要安装，请执行以下操作：
   1. 转到 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. 在“安装AEM代码同步”屏幕上，选择 **仅选择存储库** 选项，然后选择新创建的存储库。 单击“保存”。

   ![将存储库设置为公共](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > 如果您使用的是带有IP过滤功能的Github Enterprise，则可以将以下IP添加到允许列表： 3.227.118.73

   恭喜！您有一个新网站正在运行 `https://<branch>--<repo>--<owner>.hlx.page/`.

   * `<branch>` 指 GitHub 存储库的分支。
   * `<repository>` 表示您的 GitHub 存储库。
   * `<owner>` 指托管您 GitHub 存储库的 GitHub 帐户用户名。

   例如，如果分支名称为 `main`，存储库为 `wefinance`，所有者为 `wkndforms`，则网站将在 [https://main--wefinance--wkndforms.hlx.page/](https://main--wefinance--wkndforms.hlx.page/).



### 链接您自己的内容源

您新创建的Github存储库指向 [存储在Google Drive文件夹中的示例内容](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_). 此只读内容为您的表单提供了一个良好的起点。 您可以随意将其复制到自己的Google驱动器中，并根据自己的需要进行自定义。

![Google Drive上的示例内容](/help/edge/assets/folder-with-sample-content.png)

要将示例内容复制到您自己的内容文件夹，请将Github存储库指向您自己的内容文件夹：

1. 在Google Drive或Microsoft SharePoint中专门为您的AEM内容创建新文件夹。 本文档使用在Microsoft SharePoint上创建的文件夹。

1. 与Adobe Experience Manager用户共享文件夹(helix@adobe.com)。

   ![使用“管理访问权限”选项可与AEM用户共享文件夹 — SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![使用“管理访问权限”选项可与AEM用户 — Google驱动器共享文件夹](/help/edge/assets/share-google-drive-folder.png)


   确保您已向Adobe Experience Manager用户提供对该文件夹的编辑权限。

   ![与AEM用户共享文件夹，提供编辑权限 — SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png)

   ![与AEM用户共享文件夹，提供编辑权限 — Google驱动器](/help/edge/assets/add-aem-user-google-folder.png)

1. 复制 [存储在Google Drive文件夹中的示例内容](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_) 到您的文件夹。 要复制，请执行以下操作：

   1. 一起下载文件或下载单个文件。

      ![下载示例内容](/help/edge/assets/download-sample-content.png)

      此 `index`， `nav`、和 `footer` 文件定义了页面的基本布局，并且在整个项目中很少会发生更改。 它们还具有与大多数其他内容文件不同的特定结构。 通过检查这些文件，您可以了解如何在AEM项目中组织内容。


   1. 将这些文件上传到Microsoft SharePoint或Google Drive文件夹。

      ![Google Drive上的示例内容](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      确保复制  `enquiry` 将示例内容中的工作表移至Google Drive或Microsoft SharePoint上的文件夹。 它包含用于示例表单的结构。

1. 现在，您已设置内容文件夹，接下来该将其链接到您之前使用AEM Forms样板创建的GitHub项目。 要连接：

   1. 转到您使用AEM Forms样板早期创建的GitHub存储库。
   1. 打开 `fstab.yaml` 进行编辑。
   1. 将现有引用替换为您与AEM用户共享的文件夹的路径(helix@adobe.com)。

      ![Google Drive上的示例内容](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      如果您使用Microsoft SharePoint，则文件夹路径会使用以下格式：

      ```HTML
      https://<tenant>.sharepoint.com/sites/  <sp-site>/Shared%20Documents/<folder-name>
      ```

      例如，

      ```HTML
      https://adobe.sharepoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      有关在Microsoft SharePoint中使用管理文件的更多信息，请参阅 [如何使用AdobeSharepoint](https://www.aem.live/docs/setup-customer-sharepoint).



   1. 提交更新的 `fsatb.yaml` 文件，一旦您更新了引用，一切看起来都不错。 如果您遇到任何生成问题，请参阅 [GitHub内部版本问题疑难解答](#troubleshooting-github-build-issues).



      ![提交更新的fsatab.yaml文件](/help/edge/assets/commit-updated-fstab-yaml.png)

      这会将您的内容文件夹连接到您的网站。 更新引用后，您最初可能会遇到“404 Not Found”错误。 这是因为您的内容尚未预览。 下一节将介绍如何开始创作和预览内容。

      ![提交更新的fsatab.yaml文件](/help/edge/assets/aem-forms-project-folder-error.png)

### 预览和发布您的内容

完成最后一个步骤后，您的新内容源不为空，但在它升级到预览或实时阶段之前，您将无法在网站上看到它。 目前，这可能会导致404错误。

要预览未发布的内容，请执行以下操作：

1. 安装名为的Chrome扩展 [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo).

   ![安装AEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

   将扩展安装到Chrome后，请别忘了将其固定，这样可以更轻松地找到它。

   ![固定AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. 要设置SidekickChrome扩展，请转到您之前共享的Google Drive或Microsoft SharePoint文件夹，然后右键单击浏览器工具栏中的扩展图标并选择 `Add this project`.

   ![AEM Sidekick — 添加项目](/help/edge/assets/aem-sidekick-add-a-project.png)

   安装扩展并添加项目后，您便可以从Google Drive预览和发布内容。

1. 选择Microsoft SharePoint或Google Drive文件夹中的所有文档。 您可以通过按住Ctrl键(Windows/Linux)或Cmd键(Mac)并单击来选择多个文档。

   ![选择所有文件](/help/edge/assets/select-all-files.png)

1. 单击固定到Chrome扩展栏的AEM Sidekick图标。 屏幕上将显示一个工具栏。 您可以选择预览或发布内容。

   如果您复制了 `index`， `nav`， `footer` 和 `enquiry` 文件，所有这些文件都是单独的文档，都有自己的预览和发布周期，因此请确保预览（和发布）所有这些文件。

   预览文件时，新的浏览器选项卡会显示文档。 要预览示例表单，请转到以下URL：


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.live
   ```

   * `<branch>` 指 GitHub 存储库的分支。
   * `<repository>` 表示您的 GitHub 存储库。
   * `<owner>` 指托管您 GitHub 存储库的 GitHub 帐户用户名。


   `https://<branch>--<repo>--<owner>.hlx.page/enquiry` URL。

   例如，如果项目的存储库名为“wefinance”，它位于帐户所有者“wkndforms”下，而您使用的是“main”分支，则URL为：



   [https://main--wefinance--wkndforms.hlx.page](https://main--wefinance--wkndforms.hlx.page).

### 创建表单

示例内容包括一个“inquiry”表，它用作“inquiry”表单的模板。 工作表的每一行代表 [表单字段](/help/edge/docs/forms/form-components.md#available-components)，列标题定义 [字段属性](/help/edge/docs/forms/form-components.md#available-components). 此示例表单为您提供了构建表单的良好开端。

![查询表](/help/edge/assets/enquiry-form-microsoft-sharepoint.png)

让我们从更新字段表开始。 打开“查询”工作表进行编辑，将提交按钮的标签更改为 `Let's Chat`，并使用sidekick发布它。

![查询表](/help/edge/assets/enquiry-form-preview-publish.png)

要预览更新的查询表单，请转到以下URL：


```HTML
    https://<branch>--<repository>--<owner>.hlx.page/enquiry
       
```

提交按钮的标签将更新为 `Let's Chat`.

![查询表](/help/edge/assets/updated-form.png)

有关创建和发布新表单的详细信息，请转到 [创建表单](/help/edge/docs/forms/create-forms.md) 指南。

### 开始开发样式和功能


立即使用本地AEM开发环境启动并运行：

1. 安装AEM CLI：AEM CLI简化了开发任务。 让我们使用npm全局安装它：

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. 克隆Github项目：使用以下命令从GitHub克隆项目存储库，并替换 <owner> 与存储库所有者和 <repo> 使用存储库名称：

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. 启动本地环境：导航到项目目录，然后使用一条命令触发本地AEM实例：

   ```
   cd <repo>
   aem up
   ```

自适应Forms块 `blocks/form` 文件夹是您用于表单样式和代码的游乐场！ 编辑任意 `.css` 或 `.js` 文件在此目录中，您会看到所做的更改会立即反映在浏览器中。

准备好展示您的创建吗？ 使用Git提交并推送更改。 这将更新可在这些URL访问的预览和生产环境（将占位符替换为项目详细信息）：

预览： `https://<branch>--<repo>--<owner>.hlx.page/`
生产： `https://<branch>--<repo>--<owner>.hlx.live/`
恭喜！ 您已成功设置本地开发环境并部署了更改。



## 将自适应Forms块添加到您现有的AEM项目


>[!VIDEO](https://video.tv.adobe.com/v/3427789)

如果您现有AEM项目，则可以将Adaptive Forms块集成到当前项目中以开始创建表单。 要集成，请执行以下操作：

1. 将自适应Forms块存储库https://github.com/adobe-rnd/aem-boilerplate-forms克隆到您的计算机。

1. 在下载的文件夹内，找到 `blocks/form` 文件夹。 复制此文件夹。 现在，导航到您的AEM项目的本地 `blocks` 文件夹并将复制的表单文件夹粘贴到此处。

1. 在GitHub上提交这些更改并将其推送到AEM项目。


就是这样！自适应Forms块现在包含在您的AEM项目中。 您可以开始创建表单，并将表单添加到AEM页面。


## GitHub内部版本问题疑难解答

通过解决潜在问题，确保 GitHub 构建过程顺利进行：

* **解决模块路径错误：**
如果遇到错误“无法解析模块 &quot;&#39;../../scripts/lib-franklin.js&#39; 的路径”，请导航至 [EDS 项目]/blocks/forms/form.js 文件。将 lib-franklin.js 文件替换为 aem.js 文件，可更新导入语句。

* **处理 Linting 错误：**
如果您遇到任何 Linting 错误，可以绕过它们。打开 [EDS 项目]/package.json 文件并将 lint 脚本从 &quot;lint&quot;: &quot;npm run lint:js &amp;&amp; npm run lint:css&quot; 修改为 &quot;lint&quot;: &quot;echo &#39;skipping linting for now&#39;&quot;。保存文件并将更改提交到您的 GitHub 项目。


## 另请参阅

* [使用Google Sheets或Microsoft Excel创建表单](/help/edge/docs/forms/create-forms.md)
* [将表单直接提交到Microsoft Excel或Google工作表](/help/edge/docs/forms/submit-forms.md)
* [更改表单的外观](/help/edge/docs/forms/style-theme-forms.md)






