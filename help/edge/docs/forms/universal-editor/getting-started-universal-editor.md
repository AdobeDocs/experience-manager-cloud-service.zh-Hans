---
title: 使用通用编辑器完成 Edge Delivery Services for AEM Forms 快速入门
description: 了解如何使用 Edge Delivery Services 和通用编辑器的所见即所得创作功能来创建和发布高性能表单。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '2608'
ht-degree: 100%

---


# 使用通用编辑器完成 Edge Delivery Services for AEM Forms 快速入门

| 创作方法 | 指南 |
|---------------------------------|-----------------------------------------------------------------------|
| **通用编辑器（所见即所得）** | 本文 |
| **基于文档的创作** | [基于文档的教程](/help/edge/docs/forms/tutorial.md) |

适用于 AEM Forms 的 Edge Delivery Services 将高性能 Web 投放与通用编辑器中的所见即所得创作方法结合起来。本指南涵盖了表单的创建、自定义、发布和快速加载。

## 您将了解

在本教程结束时，您能够：

- 通过自适应表单块设置 GitHub 存储库
- 创建与 Edge Delivery Services 集成的 AEM 网站
- 使用通用编辑器构建和发布表单
- 配置本地开发环境

## 选择您的路径

选择符合您的场景的方法：

![选择您的路径决策指南](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*图：帮助您选择合适的实施路径的视觉指南*

| **路径 A：新项目** | **路径 B：现有的项目** |
|----------------------------------------|-------------------------------------------|
| 从已预先配置的模板开始 | 将表单添加到您当前的 AEM 项目 |
| **最适合：**&#x200B;新实施 | **最适合：**&#x200B;现有的 AEM Sites |
| **您将获得：**&#x200B;已预先配置的表单块 | **您将获得：**&#x200B;表单已添加到现有网站 |
| **步骤：**&#x200B;模板 → 设置 → 表单 | **步骤：**&#x200B;集成 → 配置 → 表单 |
| [从路径 A 开始](#path-a-create-new-project-with-forms) | [从路径 B 开始](#path-b-add-forms-to-existing-project) |

## 先决条件

为确保使用通用编辑器顺利而成功地使用适用于 AEM Forms 的 Edge Delivery Services，请在继续之前先检查并确认满足以下先决条件：

### 满足访问权限要求

- **GitHub 帐户**：您必须有一个有权创建新存储库的 GitHub 帐户。这对于管理您的项目源代码以及与您的团队协作至关重要。
- **AEM as a Cloud Service 创作访问权限**：确保您具有 AEM as a Cloud Service 环境的作者级别访问权限。创建、编辑和发布表单都需要这种访问权限。

### 技术要求

- **熟悉 Git**：您必须能够轻松执行基本的 Git 操作，例如克隆存储库、提交更改和推送更新。这些技能对于源代码控制和项目协作至关重要。
- **了解 Web 技术**：建议具备 HTML、CSS 和 JavaScript 的应用知识。这些技术是表单自定义和错误修复的基础。
- **Node.js（版本 16 或以上）**：本地开发和运行构建工具都需要 Node.js。确保您的系统上安装了 16 或更高版本。
- **包管理器（npm 或 yarn）**：您将需要 npm（节点包管理器）或 yarn 来管理项目依赖项和脚本。

### 建议背景

- **AEM Sites 概念**：对 AEM Sites 的基本了解，包括网站结构和内容创作，能帮助您有效地导航和集成表单。
- **表单设计原则**：熟悉表单设计的最佳实践，例如可用性、无障碍可访问性和数据验证，这将使您能够创建有效且用户友好的表单。
- **所见即所得编辑器的使用经验**：此前获得的所见即所得 (WYSIWYG) 编辑器的使用经验将帮助您更有效地利用通用编辑器的可视化创作功能。

>[!TIP]
>
> AEM 新手？从 [AEM Sites 快速入门指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=zh-Hans)开始。

## 路径 A：通过 Forms 创建新项目

**推荐用于：**&#x200B;新项目、试点项目或概念验证计划

使用 AEM Forms Boilerplate 来加速您的项目设置。此样板提供了一个可供立即使用的无缝集成了自适应表单块的模板，使您能够在 AEM 网站内快速构建和部署表单。

### 概述

要成功启动集成了表单的新项目，您需要：

1. 使用 AEM Forms Boilerplate 模板创建一个 GitHub 存储库。
2. 设置 AEM Code Sync 用于自动执行 AEM 与您的存储库之间的内容同步。
3. 配置您的 GitHub 项目与您的 AEM 环境之间的连接。
4. 建立并发布一个新的 AEM 网站。
5. 使用通用编辑器添加和管理表单。

以下几个部分将详细指导您完成每个步骤，确保您获得顺畅有效的项目设置体验。

+++步骤 1：从模板创建 GitHub 存储库

1. **访问 AEM Forms Boilerplate 模板**
   - 前往 [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)

   ![AEM Forms Boilerplate 模板](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *图：包含预配置自适应表单块的 AEM Forms Boilerplate 存储库*

2. **创建您的存储库**
   - 点击&#x200B;**使用此模板** > **创建新的存储库**

   ![从模板创建存储库](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *图：使用模板创建新的存储库*

3. **配置存储库设置**
   - **所有者**：选择您的 GitHub 帐户或组织
   - **存储库名称**：选择一个描述性名称（例如 `my-forms-project`）
   - **可见性**：选择&#x200B;**公开**（建议 Edge Delivery Services 使用）
   - 点击&#x200B;**创建存储库**

   ![存储库配置](/help/edge/docs/forms/assets/name-eds-repo.png)
   *图：将新存储库配置为公开可见*

**验证：**&#x200B;确认您有一个基于 AEM Forms Boilerplate 模板的新 GitHub 存储库。

+++

+++步骤 2：安装 AEM Code Sync

AEM Code Sync 会将您的 AEM 创作环境与您的 GitHub 存储库之间的内容更改自动同步。

1. **安装 GitHub 应用程序**
   - 前往 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)

2. **配置访问权限**
   - 选择&#x200B;**仅选择存储库**
   - 选择您新创建的存储库
   - 单击&#x200B;**保存**

   ![AEM Code Sync 安装](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *图：使用存储库专用的权限安装 AEM Code Sync*

**检查点：** AEM Code Sync 已安装完毕，并可以访问您的存储库。

+++

+++步骤 3：配置 AEM 集成

`fstab.yaml` 文件将您的 GitHub 存储库与 AEM 创作环境连接，以实现内容同步。

1. **导航到您的存储库**
   - 前往新创建的 GitHub 存储库
   - 您应该能看到 AEM Forms Boilerplate 文件

2. **创建 fstab.yaml 文件**
   - 在根目录中点击&#x200B;**添加文件** > **创建新文件**
   - 为文件命名 `fstab.yaml`

   ![创建 fstab.yaml 文件](/help/edge/docs/forms/assets/open-fstab.png)
   *图：创建 fstab.yaml 配置文件*

3. **添加您的 AEM 连接详细信息**

   复制粘贴以下配置，将替换占位符：

   ```yaml
   mountpoints:
     /: 
     url: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
     type: "markup" 
     suffix: ".html" 
   ```

   **替换：**
   - `<aem-author>`：您的 AEM as a Cloud Service 作者 URL（例如 `author-p12345-e67890.adobeaemcloud.com`）
   - `<owner>`：您的 GitHub 用户名或组织
   - `<repository>`：您的存储库名称

   **示例：**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![编辑 fstab.yaml 文件](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *图：配置 AEM 集成的挂载点*

4. **提交配置**
   - 添加提交消息：“添加 AEM 集成配置”
   - 点击&#x200B;**提交新文件**

   ![提交 fstab 更改内容](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *图：提交 fstab.yaml 配置*

**验证：**&#x200B;确认您的 GitHub 存储库与 AEM 连接。

>[!NOTE]
>
> 有构建问题吗？参见[解决 GitHub 构建问题](#troubleshooting-github-build-issues)。

+++

+++步骤 4：创建一个 AEM 网站并与您的 GitHub 存储库连接。

1. **访问 AEM Sites 控制台**
   - 登录您的 AEM as a Cloud Service 创作实例
   - 导航到 **Sites**

   ![AEM Sites 控制台](/help/edge/assets/select-sites.png)
   *图：访问 AEM Sites 控制台*

2. **开始创建网站**
   - 点击&#x200B;**创建** > **从模板创建网站**

   ![创建网站选项](/help/edge/docs/forms/assets/create-sites.png)
   *图：从模板创建一个新网站*

3. **选择 Edge Delivery Services 模板**
   - 选择 **Edge Delivery Services Site** 模板
   - 点击&#x200B;**下一个**

   ![选择网站模板](/help/edge/docs/forms/assets/select-site-template.png)
   *图：选择 Edge Delivery Services 网站模板*

   >[!NOTE]
   >
   >**模板不可用？**&#x200B;如果您看不到 Edge Delivery Services 模板：
   >
   >1. 点击&#x200B;**导入**，上传模板
   >2. 从 [GitHub 发行版本](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)下载模板

4. **配置您的网站**

   输入以下信息：

   | 字段 | 值 | 示例 |
   |-----------------|-----------------------------|-----------------------------------------|
   | **网站标题** | 网站的描述性名称 | “我的表单项目” |
   | **网站名称** | URL 友好的名称 | &quot;my-forms-project&quot; |
   | **GitHub URL** | 您的存储库 URL | `https://github.com/mycompany/my-forms-project` |

   ![网站配置](/help/edge/docs/forms/assets/create-aem-site.png)
   *图：配置集成了 GitHub 的新 AEM 网站*

5. **完成网站创建**
   - 检查您的设置
   - 单击&#x200B;**创建**

   ![确认网站创建](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *图：确认网站创建*

   **成功！**&#x200B;您的 AEM 网站创建完毕，并已与 GitHub 连接。

6. **在通用编辑器中打开**
   - 在 Sites 控制台中找到您的新网站
   - 选择 `index` 页面
   - 点击&#x200B;**编辑**

   ![在通用编辑器中编辑网站](/help/edge/docs/forms/assets/edit-site.png)
   *图：打开您的网站进行编辑*

   通用编辑器在一个新选项卡中打开，提供所见即所得的创作功能。

   ![通用编辑器用户界面](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *图：您的网站在通用编辑器中打开，可以所见即所得的方法进行编辑*

**验证：**&#x200B;确认您的 AEM 网站已准备好进行表单创作。

+++

+++步骤 5：发布您的网站

发布后，您的网站可以在 Edge Delivery Services 上供全球访问。

1. **从 Sites 控制台快速发布**
   - 返回到 AEM Sites 控制台
   - 选择您的网站页面（或通过 Ctrl+A 选择全部）
   - 点击&#x200B;**快速发布**

   ![发布 AEM 网站](/help/edge/docs/forms/assets/publish-sites.png)
   *图：选择要快速发布的页面*

2. **确认发布**
   - 在确认对话框中点击&#x200B;**发布**

   ![快速发布对话框](/help/edge/docs/forms/assets/quick-publish.png)
   *图：确认发布操作*

   **另一种方法：**&#x200B;您还可以使用发布按钮直接从通用编辑器发布。

   ![从通用编辑器发布](/help/edge/docs/forms/assets/qui.png)
   *图：直接从通用编辑器发布*

3. **访问您的上线网站**

   您的网站现已上线：

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **URL 结构说明：**
   - `<branch>`：GitHub 分支（通常为 `main`）
   - `<repo>`：您的存储库名称
   - `<owner>`：您的 GitHub 用户名或组织
   - `<site-name>`：您的 AEM 网站名称

   **示例：**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**验证：**&#x200B;确认您的网站在 Edge Delivery Services 上线。

>[!TIP]
>
> **URL 模式：**
>
> - **主页：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **其他页面：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**下一步：** [创建您的第一个表单](#create-your-first-form)

+++

## 路径 B：在现有的项目中添加表单

**最适合：** 使用 Edge Delivery Services 的现有 AEM Sites

如果您已经有一个使用 Edge Delivery Services 的 AEM 项目，就可以通过集成自适应表单块来添加表单功能。

### 路径 B 的先决条件

要继续将表单集成到您现有的 AEM 项目中，请确保满足以下先决条件：

- 您有一个使用 [AEM Boilerplate XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk) 创建的现有 AEM 项目。
- [本地开发环境已经设置](#set-up-local-development-environment)
- 您拥有对项目存储库的 Git 访问权限，因此您可以根据需要克隆、修改和推送更改。

>[!NOTE]
>
> 如果您的项目使用 [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms) 进行了初始设置，表单功能就已经包含在内。在这种情况下，您可以继续前往[创建您的第一个表单](#create-your-first-form)部分。

以下指南提供了一种在现有项目中添加表单功能的结构化方法。每个步骤都旨在确保通用编辑器环境中的无缝集成和最佳功能。

### 概述

您将完成以下高级概述步骤：

1. 将自适应表单块文件复制到您的项目中。
2. 更新项目的配置，以识别和支持表单组件。
3. 调整 ESLint 规则，以适应新文件和编码模式。
4. 构建您的项目，并将更改提交到您的存储库。

+++步骤 1：复制表单块文件

1. **导航到您的本地项目**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **从 AEM Forms Boilerplate 下载所需文件**

   从 [AEM Forms Boilerplate 存储库](https://github.com/adobe-rnd/aem-boilerplate-forms)复制这些文件：

   | 源 | 目标 | 用途 |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | 核心表单功能 |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | 通用编辑器集成 |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | 编辑器样式 |

3. **更新编辑器支持**
   - 将您的 `/scripts/editor-support.js` 文件替换为 [AEM Forms Boilerplate 中的 editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)

**验证：**&#x200B;确认表单块文件已在您的项目中。

+++

+++步骤 2：更新组件配置

1. **更新分区模型**

   打开 `/models/_section.json`，然后将表单组件添加到过滤器：

   ```json
   {
        "filters": [
        {
      "id": "section",
      "components": [
           "text",
           "image",
           "button",
        "form",
        "embed-adaptive-form"
      ]
       }
     ]
   }
   ```

   **作用：**&#x200B;在通用编辑器组件选取器中启用表单组件。

**验证：**&#x200B;确认表单组件显示在通用编辑器中。

+++

+++步骤 3：配置 ESLint（可选）

**为什么要执行此步骤：**&#x200B;防止表单专用文件中的代码错误，并配置适当的验证规则。

1. **更新 .eslintignore**

   将这些行添加到 `/.eslintignore`：

   ```bash
   # Form block rule engine files
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

2. **更新 .eslintrc.js**

   将这些规则添加到 `/.eslintrc.js` 中的 `rules` 对象中：

   ```javascript
   {
     "rules": {
       // Existing rules...
   
       // Form component cell limits
    'xwalk/max-cells': ['error', {
         '*': 4, // default limit
      form: 15,
      wizard: 12,
      'form-button': 7,
      'checkbox-group': 20,
      checkbox: 19,
      'date-input': 21,
      'drop-down': 19,
      email: 22,
      'file-input': 20,
      'form-fragment': 15,
      'form-image': 7,
      'multiline-input': 23,
      'number-input': 22,
      panel: 17,
      'radio-group': 20,
      'form-reset-button': 7,
      'form-submit-button': 7,
      'telephone-input': 20,
      'text-input': 23,
      accordion: 14,
      modal: 11,
      rating: 18,
      password: 20,
         tnc: 12
       }],
   
       // Disable this rule for forms
       'xwalk/no-orphan-collapsible-fields': 'off'
     }
   }
   ```

**验证：**&#x200B;确认 ESLint 可与表单组件共同使用。

+++

+++步骤 4：构建与部署

1. **安装依赖项并构建**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **作用：**
   - 通过表单组件更新 `component-definition.json`
   - 使用表单模型生成 `component-models.json`
   - 通过筛选规则创建 `component-filters.json`

2. **验证生成的文件**

   检查项目根目录中的这些文件是否包含与表单相关的对象：
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **提交并推送更改内容**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**验证：**&#x200B;确认您的项目包含表单功能。

+++

**下一步：** [创建您的第一个表单](#create-your-first-form)

## 创建您的第一个表单

**谁应该关注这一节：**\
这一节内容面向采用路径 A（新项目）或路径 B（现有项目）的用户。

现在您的项目已具备表单创建功能，因此您可以使用通用编辑器直观的所见即所得创作环境来构建您的第一个表单。以下步骤提供了一种在您的 AEM 网站内设计、配置和发布表单的结构化方法。

### 概述

在通用编辑器中创建表单的过程包括几个关键阶段：

1. **插入自适应表单块**\
   首先将自适应表单块添加到您选择的页面中。

2. **添加表单组件**\
   填充表单，插入文本字段、按钮和其他输入元素等组件。

3. **配置组件属性**\
   调整每个组件的设置和属性，以满足表单的要求。

4. **预览和测试您的表单**\
   使用预览功能在发布之前验证表单的外观和行为。

5. **发布更新后的页面**\
   感到满意后，发布您的页面，使表单可供最终用户使用。

接下来几节将详细指导您完成每个步骤，确保您获得顺畅有效的表单创建体验。

+++步骤 1：添加自适应表单块

1. **在通用编辑器中打开您的页面**
   - 导航至 AEM 中的 **Sites** 控制台。
   - 选择要添加表单（例如 `index`）的页面
   - 点击&#x200B;**编辑**

   您的页面将在通用编辑器中打开，可以所见即所得的方式进行编辑。


2. **添加自适应表单组件**
   - 打开&#x200B;**内容树**&#x200B;面板（左侧边栏）
   - 导航到您想要添加表单的那个分区
   - 点击&#x200B;**添加** (+) 图标
   - 从组件列表中选择&#x200B;**自适应表单**

   ![添加自适应表单块](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *图：将自适应表单块添加到您的页面*

**验证：**&#x200B;确认您有一个空的表单容器。

+++

+++步骤 2：添加表单组件

1. **导航到您的表单块**
   - 在内容树中，找到您新添加的自适应表单分区

   ![自适应表单块已添加](/help/edge/docs/forms/assets/adative-form-block.png)
   *图：内容树中的自适应表单块*

2. **添加表单组件**

   您可以通过两种方式添加组件：

   **方法 A：点击添加**
   - 点击表单分区中的&#x200B;**添加** (+) 图标
   - 从&#x200B;**自适应表单组件**&#x200B;列表中添加组件

   **方法 B：拖放**
   - 将组件直接从组件面板拖到您的表单中

   ![添加表单组件](/help/edge/docs/forms/assets/add-component.png)
   *图：将组件添加到表单中*

   **推荐的基本组件：**
   - 文本输入（用于姓名、电子邮件）
   - 文本区域（用于消息）
   - 提交按钮

3. **配置组件属性**
   - 选择任意一个表单组件
   - 使用&#x200B;**属性**&#x200B;面板（右侧边栏）配置：
      - 标签和占位符
      - 验证规则
      - 必填字段设置

   ![组件属性面板](/help/edge/docs/forms/assets/component-properties.png)
   *图：配置组件属性*

4. **预览您的表单**

   您的表单看起来类似这样：

   ![预览完成的表单](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *图：使用通用编辑器创建的表单示例*

**验证：**&#x200B;确认您的表单已准备好发布。

>[!IMPORTANT]
>
> 不要忘记在更改后发布您的页面，以便在浏览器中查看更新内容。

+++

+++步骤 3：发布表单

1. **从通用编辑器发布**
   - 点击通用编辑器中的&#x200B;**发布**&#x200B;按钮

   ![发布表单](/help/edge/docs/forms/assets/publish-form.png)
   *图：从通用编辑器发布您的表单*

2. **确认发布**
   - 在确认对话框中点击&#x200B;**发布**

   ![确认发布](/help/edge/docs/forms/assets/publish-form1.png)
   *图：确认发布操作*

   您将看到确认发布成功的消息。

   ![发布成功](/help/edge/docs/forms/assets/publish-form2.png)
   *图：确认发布成功*

3. **查看您的上线表单**

   您的表单现已上线：

   ```
   https://<branch>--<repo>--<owner>.aem.live/content/<site-name>/
   ```

   **URL 示例：**

   ```
   https://main--my-forms-project--mycompany.aem.live/content/my-forms-project/
   ```

   ![上线表单页面](/help/edge/docs/forms/assets/publish-index-page.png)
   *图：您在 Edge Delivery Services 上发布的表单页面*

**祝贺您！**&#x200B;您的表单现已上线，并已准备好收集提交内容。

+++

### 后续步骤

现在您有了一个工作表单，您可以：

- 通过编辑 CSS 和 JavaScript 文件&#x200B;**自定义样式**
- **添加高级表单功能**，例如验证规则和条件逻辑
- **设置本地开发**，以实现更快的迭代
- 为特定的用例&#x200B;**创建独立表单**

>[!TIP]
>
> **了解详情：**[在通用编辑器中创建独立表单](/help/edge/docs/forms/universal-editor/create-forms.md)

## 设置本地开发环境

**最适合：**&#x200B;想要自定义表单样式和行为的开发人员

本地开发环境允许您做出更改，且无需经过发布周期就能立即查看这些更改。

+++设置 AEM CLI 和本地环境

1. **安装 AEM CLI**

   AEM CLI 简化了本地开发任务：

   ```bash
       npm install -g @adobe/aem-cli
   ```

2. **克隆您的存储库**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   将 `<owner>` 和 `<repo>` 替换为您的实际 GitHub 详细信息。

3. **启动本地开发服务器**

   ```bash
   aem up
   ```

   这将启动一个具有热重载功能的本地服务器。

4. **进行自定义**

   - 编辑 `blocks/form/` 目录中的文件，定义表单的样式和行为
   - 更改 `form.css` 定义样式
   - 更新 `form.js` 定义行为

   在您位于 `http://localhost:3000` 的浏览器中&#x200B;**立即查看更改**

5. **部署您的更改**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   您的更改在以下环境中可用：
   - **预览：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **生产：** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## 疑难解答

### 常见问题和解决方案

+++GitHub 构建问题

**问题：**&#x200B;构建失败或代码错误

**解决办法 1：处理代码错误**

如果遇到代码错误：

1. 在您的项目根目录中打开 `package.json`
2. 找到 `lint` 脚本：

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. 暂时禁用代码检查：

   ```json
   "scripts": {
     "lint": "echo 'skipping linting for now'"
   }
   ```

4. 提交并推送更改

**解决办法 2：模块路径错误**

如果您看到“无法解析模块‘/scripts/lib-franklin.js’的路径”：

1. 导航至 `blocks/form/form.js`
2. 更新导入语句：

   ```javascript
   // Change this:
   import { ... } from '/scripts/lib-franklin.js';
   
   // To this:
   import { ... } from '/scripts/aem.js';
   ```

+++

+++表单功能问题

**问题：**&#x200B;表单提交功能不起作用

**解决办法：**

- 确保您有一个提交按钮组件
- 检查表单操作 URL 配置
- 验证表单验证规则
- 首先在预览模式中测试

**问题：**&#x200B;样式问题

**解决办法：**

- 检查 `blocks/form/` 中的 CSS 文件路径
- 清除浏览器缓存
- 验证 CSS 语法
- 在本地开发环境中测试

+++

+++通用编辑器问题

**问题：**&#x200B;通用编辑器中不显示表单组件

**解决办法：**

- 验证 AEM Code Sync 是否已安装且已运行
- 检查 `fstab.yaml` 是否具有正确的 AEM 作者 URL
- 确保您的 AEM 实例已启用早期访问
- 确认 `component-definition.json` 包含表单组件

**问题：**&#x200B;更改在发布后看不见

**解决办法：**

- 等待 CDN 缓存刷新
- 检查浏览器缓存（尝试隐身/私人模式）
- 验证是否使用了正确的 URL 格式

+++



