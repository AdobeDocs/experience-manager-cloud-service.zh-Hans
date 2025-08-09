---
title: 使用通用编辑器的AEM Forms Edge Delivery Services快速入门
description: 了解如何使用Edge Delivery Services以及通用编辑器的WYSIWYG创作创建和发布高性能表单。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: tm+mt
source-wordcount: '2609'
ht-degree: 1%

---


# 使用通用编辑器的AEM Forms Edge Delivery Services快速入门

| 创作方法 | 指南 |
|---------------------------------|-----------------------------------------------------------------------|
| **Universal Editor （所见即所得）** | 本文 |
| **文档式创作** | [基于文档的教程](/help/edge/docs/forms/tutorial.md) |

Edge Delivery Services for AEM Forms将高性能Web交付与Universal Editor中的WYSIWYG创作功能整合在一起。 本指南介绍创建、自定义和发布快速加载表单。

## 您将完成的任务

在本教程结束时，您将执行以下操作：

- 使用自适应Forms块设置GitHub存储库
- 创建与Edge Delivery Services集成的AEM站点
- 使用通用编辑器生成和发布表单
- 配置本地开发环境

## 选择您的路径

选择与您的方案匹配的方法：

![选择您的路径决策指南](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*图：帮助您选择正确实施路径的可视指南*

| **路径A：新项目** | **路径B：现有项目** |
|----------------------------------------|-------------------------------------------|
| 从预配置的模板开始 | 将表单添加到当前的AEM项目 |
| **最适合：**&#x200B;新实施 | **最适合：**&#x200B;现有AEM Sites |
| **您获得的内容：**&#x200B;预配置的Forms块 | **您获得的内容：** Forms已添加到现有站点 |
| **步骤：**&#x200B;模板→设置→Forms | **步骤：**→配置→Forms集成 |
| [以路径A](#path-a-create-new-project-with-forms)开始 | [以路径B](#path-b-add-forms-to-existing-project)开始 |

## 先决条件

要确保在使用通用编辑器的AEM Forms中顺利、成功地使用Edge Delivery Services，请在继续之前查看并确认以下先决条件：

### 访问要求

- **GitHub帐户**：您必须拥有有权创建新存储库的GitHub帐户。 这对于管理项目源代码并与团队协作至关重要。
- **AEM as a Cloud Service创作访问权限**：确保您拥有AEM as a Cloud Service环境的创作级别访问权限。 创建、编辑和发布表单需要此访问权限。

### 技术要求

- **熟悉Git**：您应该能够熟练执行基本的Git操作，如克隆存储库、提交更改和推送更新。 这些技能是源代码控制和项目协作的基础。
- **了解Web技术**：建议具备有关HTML、CSS和JavaScript的工作知识。 这些技术构成了表单自定义和故障排除的基础。
- **Node.js（版本16或更高版本）**：本地开发和运行生成工具需要Node.js。 确保系统上安装了版本16或更高版本。
- **包管理器（npm或yarn）**：您需要npm（节点包管理器）或yarn来管理项目依赖项和脚本。

### 建议的背景

- **AEM Sites概念**：对AEM Sites的基本了解（包括网站结构和内容创作）将帮助您有效地导航和集成表单。
- **表单设计原则**：熟悉表单设计的最佳实践（例如可用性、可访问性和数据验证）将使您能够创建有效且用户友好的表单。
- **WYSIWYG编辑器的使用体验**：以前使用What You See Is What You Get (WYSIWYG)编辑器的体验将帮助您更有效地利用通用编辑器的可视化创作功能。

>[!TIP]
>
> 初次使用AEM？ 从[AEM Sites快速入门指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html)开始。

## 路径A：使用Forms创建新项目

**推荐用于：**&#x200B;新项目、试验或概念验证计划

利用AEM Forms样板加快项目设置。 此样板提供了可无缝集成自适应Forms块的现成模板，使您能够在AEM站点中快速构建和部署表单。

### 概述

要成功启动具有集成表单的新项目，您将：

1. 使用AEM Forms样板模板创建GitHub存储库。
2. 设置AEM代码同步以自动执行AEM与您的存储库之间的内容同步。
3. 配置GitHub项目与AEM环境之间的连接。
4. 建立和发布新的AEM站点。
5. 使用通用编辑器添加和管理表单。

以下部分将详细指导您完成每个步骤，确保顺利、高效地进行项目设置。

+++步骤1：从模板创建GitHub存储库

1. **访问AEM Forms样板模板**
   - 转到[https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)

   ![AEM Forms样板模板](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *图：具有预配置的自适应Forms块的AEM Forms样板存储库*

2. **创建存储库**
   - 单击&#x200B;**使用此模板** > **创建新存储库**

   ![从模板创建存储库](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *图：使用模板创建新存储库*

3. **配置存储库设置**
   - **所有者**：选择您的GitHub帐户或组织
   - **存储库名称**：请选择一个描述性名称（如`my-forms-project`）
   - **可见性**：选择&#x200B;**公共**(建议用于Edge Delivery Services)
   - 单击&#x200B;**创建存储库**

   ![存储库配置](/help/edge/docs/forms/assets/name-eds-repo.png)
   *图：配置您的新存储库使其具有公共可见性*

**验证：**&#x200B;确认您具有基于AEM Forms样板模板的新GitHub存储库。

+++

+++步骤2：安装AEM代码同步

AEM代码同步会在AEM创作环境和GitHub存储库之间自动同步内容更改。

1. **安装GitHub应用程序**
   - 转到[https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)

2. **配置访问权限**
   - 选择&#x200B;**仅选择存储库**
   - 选择您新创建的存储库
   - 单击&#x200B;**保存**

   ![AEM代码同步安装](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *图：正在安装具有特定于存储库的权限的AEM代码同步*

**检查点：** AEM代码同步现已安装，并且有权访问您的存储库。

+++

+++步骤3：配置AEM集成

`fstab.yaml`文件将您的GitHub存储库连接到AEM创作环境，以进行内容同步。

1. **导航到您的存储库**
   - 转到新创建的GitHub存储库
   - 您应该会看到AEM Forms样板文件

2. **创建fstab.yaml文件**
   - 单击根目录中的&#x200B;**添加文件** > **创建新文件**
   - 命名文件`fstab.yaml`

   ![正在创建fstab.yaml文件](/help/edge/docs/forms/assets/open-fstab.png)
   *图：正在创建fstab.yaml配置文件*

3. **添加您的AEM连接详细信息**

   复制并粘贴以下配置，替换占位符：

   ```yaml
   mountpoints:
     /: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
   ```

   **替换：**
   - `<aem-author>`：您的AEM as a Cloud Service作者URL（例如，`author-p12345-e67890.adobeaemcloud.com`）
   - `<owner>`：您的GitHub用户名或组织
   - `<repository>`：您的存储库名称

   **示例：**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![正在编辑fstab.yaml文件](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *图：为AEM集成配置装入点*

4. **提交配置**
   - 添加提交消息：“添加AEM集成配置”
   - 单击&#x200B;**提交新文件**

   ![正在提交fstab更改](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *图：正在提交fstab.yaml配置*

**验证：**&#x200B;确认您的GitHub存储库与AEM的连接。

    >[！NOTE]
    >
>存在生成问题？ 请参阅[GitHub生成问题疑难解答](#troubleshooting-github-build-issues)。

+++

+++步骤4：创建连接到GitHub存储库的AEM站点。

1. **访问AEM Sites控制台**
   - 登录AEM as a Cloud Service创作实例
   - 导航到&#x200B;**站点**

   ![AEM Sites控制台](/help/edge/assets/select-sites.png)
   *图：访问AEM Sites控制台*

2. **开始创建站点**
   - 单击&#x200B;**从模板创建** > **站点**

   ![创建站点选项](/help/edge/docs/forms/assets/create-sites.png)
   *图：从模板*&#x200B;创建新站点

3. **选择Edge Delivery Services模板**
   - 选择&#x200B;**Edge Delivery Services站点**&#x200B;模板
   - 单击&#x200B;**下一步**

   ![站点模板选择](/help/edge/docs/forms/assets/select-site-template.png)
   *图：选择Edge Delivery Services站点模板*

   >[!NOTE]
   >
   >**模板不可用？**&#x200B;如果您没有看到Edge Delivery Services模板：
   >
   >1. 单击&#x200B;**导入**&#x200B;以上载模板
   >2. 从[GitHub版本](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)下载模板

4. **配置您的站点**

   输入以下信息：

   | 字段 | 值 | 示例 |
   |-----------------|-----------------------------|-----------------------------------------|
   | **网站标题** | 站点的描述性名称 | “我的Forms项目” |
   | **站点名称** | URL友好名称 | &quot;my-forms-project&quot; |
   | **GitHub URL** | 您的存储库URL | `https://github.com/mycompany/my-forms-project` |

   ![站点配置](/help/edge/docs/forms/assets/create-aem-site.png)
   *图：使用GitHub集成配置新的AEM站点*

5. **完成站点创建**
   - 查看设置
   - 单击&#x200B;**创建**

   ![确认站点创建](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *图：确认站点创建*

   **成功！**&#x200B;您的AEM站点现已创建并连接到GitHub。

6. 在通用编辑器中打开&#x200B;****
   - 在站点控制台中，找到新站点
   - 选择`index`页面
   - 单击&#x200B;**编辑**

   ![在通用编辑器中编辑站点](/help/edge/docs/forms/assets/edit-site.png)
   *图：正在打开您的站点进行编辑*

   通用编辑器将在新选项卡中打开，并提供WYSIWYG创作功能。

   ![通用编辑器界面](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *图：您的站点在通用编辑器中打开以进行WYSIWYG编辑*

**验证：**&#x200B;确认您的AEM站点已准备好进行表单创作。

+++

+++步骤5：发布您的站点

发布功能使您的网站可在Edge Delivery Services上全局访问。

1. **从站点控制台快速发布**
   - 返回到AEM Sites控制台
   - 选择您的网站页面（或使用Ctrl+A选择所有）
   - 单击&#x200B;**快速发布**

   ![正在发布AEM网站](/help/edge/docs/forms/assets/publish-sites.png)
   *图：为快速发布选择页面*

2. **确认发布**
   - 在确认对话框中，单击&#x200B;**发布**

   ![快速发布对话框](/help/edge/docs/forms/assets/quick-publish.png)
   *图：确认发布操作*

   **替代项：**&#x200B;您还可以使用“发布”按钮直接从Universal Editor中发布。

   从通用编辑器![发布](/help/edge/docs/forms/assets/qui.png)
   *图：直接从通用编辑器发布*

3. **访问您的实时网站**

   您的网站现在位于：

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **URL结构说明：**
   - `<branch>`： GitHub分支（通常为`main`）
   - `<repo>`：您的存储库名称
   - `<owner>`：您的GitHub用户名或组织
   - `<site-name>`：您的AEM站点名称

   **示例：**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**验证：**&#x200B;确认您的网站在Edge Delivery Services上处于活动状态。

>[!TIP]
>
> **URL模式：**
>
> - **主页：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **其他页面：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**下一步：**[创建您的第一个表单](#create-your-first-form)

+++

## 路径B：将Forms添加到现有项目

**最适合：**&#x200B;具有Edge Delivery Services的现有AEM Sites

如果您已有一个使用Edge Delivery Services的AEM项目，则可以通过集成自适应Forms块来添加表单功能。

### 路径B的先决条件

要继续将表单集成到您现有的AEM项目中，请确保满足以下先决条件：

- 您有一个使用[AEM样板XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk)创建的现有AEM项目。
- 您已设置[本地开发环境](#set-up-local-development-environment)
- 您拥有对项目存储库的Git访问权限，允许您根据需要克隆、修改和推送更改。

>[!NOTE]
>
> 如果您的项目最初是使用[AEM Forms样板](https://github.com/adobe-rnd/aem-boilerplate-forms)设置的，则已包含表单功能。 在这种情况下，您可以转到[创建您的第一个表单](#create-your-first-form)部分。

以下指南提供了一种将表单功能添加到现有项目的结构化方法。 每个步骤都旨在确保在Universal Editor环境中实现无缝集成和最佳功能。

### 概述

您将完成以下高级步骤：

1. 将自适应Forms块文件复制到项目中。
2. 更新项目配置以识别和支持表单组件。
3. 调整ESLint规则以适应新文件和编码模式。
4. 构建项目并将更改提交到存储库。

+++步骤1：复制Forms块文件

1. **导航到您的本地项目**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **从AEM Forms样板下载所需文件**

   从[AEM Forms样板存储库](https://github.com/adobe-rnd/aem-boilerplate-forms)复制这些文件：

   | 源 | 目标 | 用途 |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | 核心表单功能 |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | 通用编辑器集成 |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | 编辑器样式 |

3. **更新编辑器支持**
   - 将您的`/scripts/editor-support.js`文件替换为AEM Forms样板[中的](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)editor-support.js

**验证：**&#x200B;确认表单块文件在您的项目中。

+++

+++步骤2：更新组件配置

1. **更新节模型**

   打开`/models/_section.json`并将表单组件添加到筛选器：

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

   **此操作的内容：**&#x200B;在通用编辑器组件选取器中启用表单组件。

**验证：**&#x200B;确认表单组件显示在通用编辑器中。

+++

+++步骤3：配置ESLint（可选）

**为什么执行此步骤：**&#x200B;防止表单特定文件出现Linting错误，并配置正确的验证规则。

1. **更新.eslingnore**

   将这些行添加到`/.eslintignore`：

   ```bash
   # Form block rule engine files
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

2. **更新.eslintrc.js**

   将这些规则添加到`rules`中的`/.eslintrc.js`对象：

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

**验证：**&#x200B;确认ESLint可与表单组件配合使用。

+++

+++步骤4：生成和部署

1. **安装依赖项并生成**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **此操作的内容：**
   - 使用表单组件更新`component-definition.json`
   - 使用表单模型生成`component-models.json`
   - 使用筛选规则创建`component-filters.json`

2. **验证生成的文件**

   检查项目根目录中的这些文件是否包含与表单相关的对象：
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **提交和推送更改**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**验证：**&#x200B;确认您的项目包含表单功能。

+++

**下一步：**[创建您的第一个表单](#create-your-first-form)

## 创建您的第一个表单

**谁应关注此部分：**\
本节与路径A（新项目）或路径B（现有项目）之后的用户相关。

利用现在可用于创建表单的项目，您可以使用通用编辑器中直观的WYSIWYG创作环境构建第一个表单。 以下步骤提供了一种结构化方法，用于在AEM站点中设计、配置和发布表单。

### 概述

在通用编辑器中创建表单的过程包括几个关键阶段：

1. **插入自适应表单块**\
   首先，将自适应表单块添加到您选择的页面。

2. **添加表单组件**\
   通过插入文本字段、按钮和其他输入元素等组件填充表单。

3. **配置组件属性**\
   根据表单要求，调整每个组件的设置和属性。

4. **预览和测试您的表单**\
   使用预览功能在发布之前验证表单的外观和行为。

5. **发布更新的页面**\
   满意后，发布您的页面以使表单可供最终用户使用。

以下部分将详细指导您完成其中的每个步骤，确保获得流畅有效的表单创建体验。

+++步骤1：添加自适应表单块

1. **在通用编辑器中打开您的页面**
   - 导航到AEM中的&#x200B;**站点**&#x200B;控制台
   - 选择要添加表单的页面（例如，`index`）
   - 单击&#x200B;**编辑**

   您的页面将在通用编辑器中打开，以便对WYSIWYG进行编辑。

2. **添加自适应表单组件**
   - 打开&#x200B;**内容树**&#x200B;面板（左侧边栏）
   - 导航到要添加表单的部分
   - 单击&#x200B;**添加** (+)图标
   - 从组件列表中选择&#x200B;**自适应表单**

   ![添加自适应表单块](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *图：将自适应表单块添加到页面*

**验证：**&#x200B;确认您的表单容器为空。

+++

+++第2步：添加表单组件

1. **导航到您的表单块**
   - 在内容树中，找到新添加的自适应表单部分

   已添加![自适应表单块](/help/edge/docs/forms/assets/adative-form-block.png)
   *图：内容树中的自适应表单块*

2. **添加表单组件**

   您可以通过两种方式添加组件：

   **方法A：单击以添加**
   - 单击表单部分中的&#x200B;**添加** (+)图标
   - 从&#x200B;**自适应表单组件**&#x200B;列表中选择组件

   **方法B：拖放**
   - 将组件面板中的组件直接拖到表单中

   ![正在添加表单组件](/help/edge/docs/forms/assets/add-component.png)
   *图：正在将组件添加到表单*

   **推荐的入门级组件：**
   - 文本输入（用于姓名、电子邮件）
   - 文本区域（用于消息）
   - 提交按钮

3. **配置组件属性**
   - 选择任意表单组件
   - 使用&#x200B;**属性**&#x200B;面板（右侧边栏）配置：
      - 标签和占位符
      - 验证规则
      - 必填字段设置

   ![组件属性面板](/help/edge/docs/forms/assets/component-properties.png)
   *图：正在配置组件属性*

4. **预览您的表单**

   您的表单将如下所示：

   ![已完成的表单预览](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *图：使用通用编辑器创建的示例表单*

**验证：**&#x200B;确认您的表单已准备好发布。

>[!IMPORTANT]
>
> 进行更改后请记得发布页面，以便在浏览器中查看更新。

+++

+++第3步：发布表单

1. 从通用编辑器&#x200B;**发布**
   - 单击通用编辑器中的&#x200B;**发布**&#x200B;按钮

   ![正在发布表单](/help/edge/docs/forms/assets/publish-form.png)
   *图：正在从通用编辑器发布表单*

2. **确认发布**
   - 在确认对话框中，单击&#x200B;**发布**

   ![发布确认](/help/edge/docs/forms/assets/publish-form1.png)
   *图：确认发布操作*

   您将看到一条确认发布的成功消息。

   ![发布成功](/help/edge/docs/forms/assets/publish-form2.png)
   *图：发布确认成功*

3. **查看您的实时表单**

   您的表单现在位于：

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **示例URL：**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

   ![实时表单页面](/help/edge/docs/forms/assets/publish-index-page.png)
   *图：您在Edge Delivery Services上发布的表单页面*

**恭喜！**&#x200B;您的表单现已上线并准备好收集提交内容。

+++

### 后续步骤

现在您有了工作表单，您可以：

- **通过编辑CSS和JavaScript文件自定义样式**
- **添加高级表单功能**，如验证规则和条件逻辑
- **设置本地开发**&#x200B;以获得更快的迭代
- **为特定用例创建独立表单**

>[!TIP]
>
> **了解更多：** [在通用编辑器中创建独立表单](/help/edge/docs/forms/universal-editor/create-forms.md)

## 设置本地开发环境

**最适合：**&#x200B;要自定义表单样式和行为的开发人员

本地开发环境允许您进行更改并立即查看它们，而无需经过发布周期。

+++设置AEM CLI和本地开发

1. **安装AEM CLI**

   AEM CLI简化了本地开发任务：

   ```bash
       npm install -g @adobe/aem-cli
   ```

2. **克隆存储库**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   将`<owner>`和`<repo>`替换为您实际的GitHub详细信息。

3. **启动本地开发服务器**

   ```bash
   aem up
   ```

   这将启动具有热重载功能的本地服务器。

4. **进行自定义**

   - 编辑`blocks/form/`目录中的文件以了解表单样式和行为
   - 修改`form.css`以设置样式
   - 更新`form.js`的行为

   **立即查看浏览器中的更改**，位于`http://localhost:3000`

5. **部署您的更改**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   您所做的更改将在以下位置提供：
   - **预览：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **生产：** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## 疑难解答

### 常见问题和解决方案

+++GitHub版本问题

**问题：**&#x200B;生成失败或Linting错误

**解决方案1：处理Linting错误**

如果遇到线形错误：

1. 在项目根目录中打开`package.json`
2. 查找`lint`脚本：

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. 暂时禁用筛选：

   ```json
   "scripts": {
     "lint": "echo 'skipping linting for now'"
   }
   ```

4. 提交并推送更改

**解决方案2：模块路径错误**

如果您看到“无法解析模块‘/scripts/lib-franklin.js’的路径”：

1. 导航到`blocks/form/form.js`
2. 更新import语句：

   ```javascript
   // Change this:
   import { ... } from '/scripts/lib-franklin.js';
   
   // To this:
   import { ... } from '/scripts/aem.js';
   ```

+++

+++通用编辑器问题

**问题：**&#x200B;表单组件未出现在通用编辑器中

**解决方案：**

- 验证是否已安装并运行AEM代码同步
- 检查`fstab.yaml`是否具有正确的AEM作者URL
- 确保您的AEM实例已启用提前访问
- 确认`component-definition.json`包含表单组件

**问题：**&#x200B;发布后更改不可见

**解决方案：**

- 等待CDN缓存刷新
- 检查浏览器缓存（尝试无痕模式/私有模式）
- 验证是否使用了正确的URL格式

+++

+++表单功能问题

**问题：**&#x200B;表单提交不起作用

**解决方案：**

- 确保您具有提交按钮组件
- 检查表单操作URL配置
- 验证表单验证规则
- 首先在预览模式下测试

**问题：**&#x200B;样式问题

**解决方案：**

- 检查`blocks/form/`中的CSS文件路径
- 清除浏览器缓存
- 验证CSS语法
- 在本地开发环境中测试

+++

