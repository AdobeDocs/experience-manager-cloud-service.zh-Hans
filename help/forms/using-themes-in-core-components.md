---
title: 如何在自适应Forms中创建和使用主题？
description: 您可以使用主题来设置样式，并使用核心组件为自适应表单提供视觉标识。 您可以跨任意数量的自适应Forms共享主题。
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '2610'
ht-degree: 5%

---

# 自适应Forms中的主题 {#themes-for-af-using-core-components}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html) |
| AEM as a Cloud Service | 本文 |

您可以创建主题并应用它们来设置自适应表单的样式。 主题包含组件和面板的样式详细信息。 样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。在应用主题时，指定的样式会反映在相应的组件上。主题是独立管理的，无需引用自适应表单，并且可在多个自适应Forms中重复使用。

## 可用主题

Forms如Cloud Service所提供，下面列出了基于核心组件的自适应Forms的主题：

* [画布主题](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 主题](https://github.com/adobe/aem-forms-theme-wknd)
* [画架主题](https://github.com/adobe/aem-forms-theme-easel)

## 了解主题的结构

主题是一个包，其中包含定义自适应Forms样式的CSS文件、JavaScript文件和资源（如图标）。 自适应表单主题遵循特定的组织，由以下组件组成：

* `src/theme.scss`：此文件夹包括对整个主题产生广泛影响的CSS文件。 它用作定义和管理主题样式和行为的集中位置。 通过编辑此文件，您可以做出在整个主题中普遍应用的更改，从而影响自适应Forms和AEM Sites页面的外观和功能。

* `src/site`：此文件夹包含应用于整个AEM站点页面的CSS文件。 这些文件由代码和样式组成，这些代码和样式会影响AEM站点页面的整体功能和布局。 此处所做的任何修改都会反映在网站的所有页面中。 [何时使用它？]

* `src/components`：此文件夹中的CSS文件是为单个AEM核心组件设计的。 组件的每个专用文件夹包括 `.scss` 在自适应表单中为该特定组件设置样式的文件。 例如，/src/components/accordion/_accordion.scss文件包含自适应Forms折叠组件的样式信息。

  ![基于自适应表单的主题结构](/help/forms/assets/theme_structure.png)

* `src/resources`：此文件夹包含图标、徽标和字体等静态文件。 这些资源用于增强主题的可视化元素和总体设计。

## 创建主题

Forms如Cloud Service所提供，下面列出了基于核心组件的自适应Forms的主题。

* [画布主题](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 主题](https://github.com/adobe/aem-forms-theme-wknd)
* [画架主题](https://github.com/adobe/aem-forms-theme-easel)

您可以 [自定义这些主题中的任意主题以创建新主题](#customize-a-theme-core-components).

![主题自定义工作流](/help/forms/assets/workflow-of-customization-of-theme.png)

## 自定义主题 {#customize-a-theme-core-components}

自定义主题是指修改和个性化主题外观的过程。 自定义主题时，您可以更改其设计元素、布局、颜色、排版规则，有时还会更改底层代码。 它允许您为网站或应用程序创建独一无二的定制外观，同时保持主题提供的基本结构和功能。

### 前提条件 {#prerequisites-to-customize}

* 熟悉 [在Cloud Manager中设置管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline) 并且具备有关如何设置管道的基本知识可帮助您有效地管理和部署主题自定义项。
* 了解如何 [使用参与者角色配置用户](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html). 通过了解如何使用参与者角色配置用户，您可以授予进行主题自定义所需的权限。
* 安装最新版本的 [Apache Maven。](https://maven.apache.org/download.cgi) Apache Maven是一种常用于Java™项目的构建自动化工具。 安装最新版本可确保您具有主题自定义所需的依赖项。
* 安装纯文本编辑器。 例如，Microsoft® Visual Studio Code。 使用Microsoft等纯文本编辑器®Visual Studio Code为编辑和修改主题文件提供了用户友好的环境。

### 设置环境

* [启用自适应Forms核心组件](/help/forms/enable-adaptive-forms-core-components.md)  (对于您的本地开发和Cloud Service环境)。
* 配置 [前端部署管道](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html) 适合您的Cloud Service环境。 或者，您可以稍后配置管道，灵活地在设置部署管道之前排定测试和优化主题的优先级。

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

在了解先决条件并配置开发环境后，您已准备好开始根据特定要求自定义主题。

### 自定义主题 {#steps-to-customize-a-theme-core-components}

自定义主题是一个多步骤的过程。 要自定义主题，请按照列出的顺序执行步骤：

1. [克隆主题](#download-a-theme-core-components)
1. [设置主题的名称](#set-name-of-theme)
1. [自定义主题](#customize-the-theme)
1. [测试主题](#test-the-theme)
1. [部署主题](#deploy-the-theme)

文档中提供的示例基于 **画布** 主题，但请务必注意，您可以使用相同的说明克隆并自定义任何主题。 这些说明适用于任何主题，允许您根据特定需求修改主题。

#### 1.克隆主题 {#download-a-theme-core-components}

要克隆基于核心组件的自适应Forms的主题，请选择以下主题之一：

* [画布主题](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 主题](https://github.com/adobe/aem-forms-theme-wknd)
* [画架主题](https://github.com/adobe/aem-forms-theme-easel)

要克隆主题，请执行以下步骤：

1. 在本地开发环境中打开命令提示符或终端窗口。

1. 运行 `git clone` 命令以克隆主题。

   ```
      git clone [Path of Git Repository of the theme]
   ```

   替换 [主题的Git存储库路径] 以及主题的相应Git存储库的实际URL

   例如，要克隆画布主题，请执行以下命令：

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   成功执行命令后，您的计算机上将有一个主题的本地副本，位于  `aem-forms-theme-canvas` 文件夹。


#### 2.设置主题名称 {#set-name-of-theme}

1. 在纯文本编辑器中打开主题文件夹。 例如，要打开 `aem-forms-theme-canvas` Visual Studio代码编辑器中的文件夹。

1. 导航到 `aem-forms-theme-canvas` 文件夹。

1. 运行以下命令：

   ```
         code .
   ```

   ![在纯文本编辑器中打开主题文件夹](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   该文件夹将在Visual Studio Code中打开。

1. 打开 `package.json` 文件以供编辑。

1. 设置值 `name` 和 `description` 属性。

   name属性用于唯一标识主题，如“aem-forms-wknd-theme”，并显示在 **样式** 选项卡/ **表单创建向导**. description属性提供有关主题的其他详细信息，包括主题的用途和设计主题。 您还可以指定主题的版本、描述和许可证。

1. 保存并关闭该文件。

![画布主题名称更改图像](/help/forms/assets/changename_canvastheme.png)


#### 3.自定义主题 {#customize-the-theme}

您可以使用主题的全局变量自定义单个组件或进行主题级别更改。 对全局变量所做的任何更改都会影响所有单独的组件。 例如，您可以使用全局变量更改自适应表单所有组件的边框颜色，并使用明亮的填充颜色使用按钮组件设置CTA（行动号召）：

* [设置主题级别样式](#theme-customization-global-level)

* [设置组件级别样式](#component-based-customization)

##### 设置主题级别样式{#theme-customization-global-level}

此 `variable.scss` 文件包含主题的全局变量。 通过更新这些变量，您可以在主题级别进行与样式相关的更改。 要应用主题级别的样式，请执行以下步骤：

1. 打开 `<your-theme-sources>/src/site/_variables.scss` 文件以供编辑。
1. 更改任何属性的值。 例如，缺省错误颜色为 `red`. 要更改错误的颜色，请执行以下操作 `red` 到 `blue`，更改的颜色十六进制代码 `$errorvariable`. 例如：`$error: #196ee5`。
1. 保存并关闭该文件。

   ![编辑主题](/help/forms/assets/edit_theme.png)

同样，您可以使用 `variable.scss` 文件设置字体系列和类型、主题和字体颜色、字体大小、主题间距、错误图标、主题边框样式以及影响多个自适应表单组件的更多变量。

##### 设置组件级别样式 {#component-based-customization}

您还可以更改特定自适应表单核心组件的字体、颜色、大小和其他CSS属性。 例如，按钮、复选框、容器、页脚等。 您可以通过编辑特定组件的CSS文件来设置按钮或复选框的样式，以便与贵组织的样式保持一致。 要自定义组件的样式：

1. 打开文件 `<your-theme-sources>/src/components/<component>/<component.scss>` 进行编辑。 例如，要更改按钮组件的字体颜色，请打开 `<your-theme-sources>/src/components/button/button.scss`，文件。
1. 根据您的要求更改任意的值。 例如，将鼠标悬停时按钮组件的颜色更改为 `green`，更改的值 `color: $white` 中的属性 `cmp-adaptiveform-button__widget:hover` 类到十六进制代码 `#12B453` 或任何其他阴影的 `green`. 最终代码如下所示：

   ```
   .cmp-adaptiveform-button__widget:hover {
   background: $dark-gray;
   color: #12B453;
   }
   ```

1. 保存并关闭该文件。

   ![编辑文本框CSS](/help/forms/assets/edit_color_textbox.png)

   >
   >
   > 在主题和组件级别定义样式时，在组件级别定义的样式优先。

#### 4.测试自定义主题 {#test-the-theme}

要在本地环境中预览和测试更改，并根据不同AEM组件的要求自定义主题，请执行以下步骤：

* 4.1 [配置本地环境以进行测试](#rename-env-file-theme-folder)
* 4.2 [使用本地环境测试主题](#start-a-local-proxy-server)

##### 4.1.配置本地环境以进行测试 {#rename-env-file-theme-folder}

1. 在纯文本编辑器中打开主题文件夹。 例如，打开 `aem-forms-theme-canvas` Visual Studio代码编辑器中的文件夹。
1. 重命名 `env_template` 文件到 `.env` 文件，并添加以下参数：

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   例如，表单的URL为 `http://localhost:4502/editor.html/content/forms/af/contactusform.html`. 因此，的值：

   * AEM_URL = `http://localhost:4502/`
   * AEM_ADAPTIVE_FORM = `contactusform`

1. 保存文件。

   ![画布主题结构](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2使用本地环境测试主题 {#start-a-local-proxy-server}

1. 导航到主题文件夹的根。 在本例中，主题文件夹名称为 `aem-forms-theme-canvas`.
1. 打开命令提示符或终端。
1. 运行 `npm install` 以安装依赖项。
1. 运行 `npm run live` 以在本机浏览器中预览带有更新主题的表单。

   >[!NOTE]
   >
   > 如果在执行 `npm run live` 命令，在命令之前 `npm run live` 命令：
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

这是一个热门部署。 因此，无论您何时进行更改并保存 `_variables.scss` 和 `button.scss` 文件，服务器会自动选取更改并预览最新输出。 直线 `[Browsersync] File event [change]` 表示服务器已识别最新更改，并且正在本地环境中部署这些更改。

![代理浏览器同步](/help/forms/assets/browser_sync.png)

在遵循主题级别和组件级别提供的用于主题自定义的示例后，自适应表单的错误消息将更改为 `blue` 颜色，而按钮组件的标签颜色将更改为 `green` 在悬停时。

**预览主题级别样式**

![示例：错误颜色设置为蓝色](/help/forms/assets/theme-level-changes.png)

**预览组件级样式**

![示例：将悬停颜色设置为绿色](/help/forms/assets/button-customization.png)

###### 测试在Cloud Service环境中托管的表单的主题

您还可以测试AEM Formsas a Cloud Service实例上托管的自适应表单的主题。 要在云实例上托管的自适应Forms中为测试主题配置和设置本地环境，请执行以下步骤：

1. 在纯文本编辑器中打开主题文件夹。 例如，打开 `aem-forms-theme-canvas` Visual Studio代码编辑器中的文件夹。
1. 重命名 `env_template` 文件到 `.env` 文件并添加以下参数：

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   例如，云环境中表单的URL为 `https://author-XXXX.adobeaemcloud.com/editor.html/content/forms/af/contactusform.html`. 因此，的值：

   * AEM_URL = `https://author-XXXX-cmstg.adobeaemcloud.com/`
   * AEM_ADAPTIVE_FORM = `contactusform`
1. 保存文件。
1. 创建本地用户。

   >[!NOTE]
   >
   > 要创建本地用户，请执行以下操作：
   >
   > * 转到 **[!UICONTROL AEM主页]** > **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]** .
   > * 确保用户是 `forms-users` 组。

1. 导航到主题文件夹的根。 在本例中，主题文件夹名称为 `aem-forms-theme-canvas`.
1. 运行 `npm run live` 系统会将您重定向到本地浏览器。
1. 单击 `SIGN IN LOCALLY (ADMIN TASKS ONLY)` 并使用本地用户的凭据登录。

您可以预览包含最新更改的自适应表单。 对主题文件夹中所做的修改感到满意后，使用前端管道将主题部署到AEM Cloud Service环境。

#### 5.部署主题 {#deploy-the-theme}

要使用前端管道将主题部署到Cloud Service环境，请执行以下操作：

* 5.1 [创建主题存储库](#create-a-new-theme-repo)
* 5.2 [将更改推送到存储库](#committing-the-changes)
* 5.3 [运行前端管道](#run-a-frontend-pipeline)

##### 5.1创建主题存储库{#create-a-new-theme-repo}

您需要存储库来部署主题。 登录 [AEM Cloud Manager存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) 并为您的主题添加新存储库。

1. 通过单击 **[!UICONTROL 存储库]** > **[!UICONTROL 添加存储库]**.

   ![创建新主题存储库](/help/forms/assets/createrepo_canvastheme.png)


1. 指定 **存储库名称** 在 **添加存储库** 对话框。 例如，提供的名称是 `custom-canvas-theme-repo`.
1. 单击&#x200B;**[!UICONTROL 保存]**。

   ![添加画布主题存储库](/help/forms/assets/addcanvasthemerepo.png)

1. 单击 **[!UICONTROL 复制存储库URL]** 以复制存储库的URL。

   ![画布主题URL](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   > * 您可以将单个存储库用于多个主题。
   > * 要部署不同的主题，您必须创建单独的前端管道。
   >* 例如，您可以使用相同的存储库，如 `custom-canvas-theme-repo`，用于画布主题、WKND主题和画盘主题。 但是，要部署主题，您需要创建单独的前端管道。 使用相应的前端管道部署特定主题的未来自定义。

##### 5.2.将更改推送到存储库 {#committing-the-changes}

现在，将更改推送到AEM FormsCloud Service的主题存储库。

1. 导航到主题文件夹的根。  在本例中，主题文件夹名称为 `aem-forms-theme-canvas`.
1. 打开命令提示符或终端。
1. 按照列出的顺序运行以下命令：

   ```
   git remote add [alias-name-for-repository] [URL of repository]
   git add .
   git commit
   git push [name-for-createdrepository]
   ```

   例如：

   ```
   git remote add canvascloudthemerepo https://git.cloudmanager.adobe.com/stage-aemformsdev/customcanvastheme/
   git add .
   git commit
   git push canvascloudthemerepo 
   ```

   ![已提交更改](/help/forms/assets/cmd_git_push.png)



##### 5.3运行前端管道 {#run-a-frontend-pipeline}

使用部署主题 [前端管道。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html). 要部署主题，请执行以下步骤：

1. 登录到您的AEM Cloud Manager存储库。
1. 单击 **[!UICONTROL 添加]** 按钮来自 **[!UICONTROL 管道]** 部分。
1. 选择 **[!UICONTROL 添加非生产管道]** 或 **[!UICONTROL 添加生产管道]** 基于Cloud Service环境。 例如，下面的 **[!UICONTROL 添加生产管道]** 已选中选项。
1. 在 **[!UICONTROL 添加生产管道]** 对话框作为 **[!UICONTROL 配置]** 步骤，指定管道的名称。 例如，管道的名称为 `customcanvastheme`.
1. 单击&#x200B;**[!UICONTROL “继续”]**。
1. 选择 **[!UICONTROL 目标部署]** > **[!UICONTROL 前端代码]** 选项，在 **[!UICONTROL 源代码]** 步骤。
1. 选择 **[!UICONTROL 存储库]** 和 **[!UICONTROL Git分支]** 具有最新更改的值。 例如，此处选定的存储库名称为 `custom-canvas-theme-repo` 而Git分支是 `main`.
1. 选择 **[!UICONTROL 代码位置]** 作为 `/`，如果根文件夹中存在更改。
1. 单击&#x200B;**[!UICONTROL 保存]**。
   ![创建前端管道](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   管道设置完成后，会更新行动号召信息卡。

1. 右键单击创建的管道。
1. 单击 **[!UICONTROL 运行]** .

   ![流水线](/help/forms/assets/canvas-theme-run-pipeline.png)

构建完成后，主题即可在创作实例中供使用。 它显示在 **[!UICONTROL 样式]** 选项卡中，用于创建自适应表单时。

![样式选项卡下可用的自定义主题](/help/forms/assets/custom-theme-style-tab.png)

## 将主题应用于自适应表单 {#using-theme-in-adaptive-form}

将主题应用于自适应表单的步骤如下：

1. 登录到您的AEM Forms创作实例。

1. 选择 **Adobe Experience Manager** > **Forms** > **Forms和文档**.

1. 单击 **创建** > **自适应Forms**. 此时将打开创建自适应表单的向导。

1. 选择中的核心组件模板 **来源** 选项卡。
1. 选择中的主题 **样式** 选项卡。
1. 单击&#x200B;**创建**。

创建自适应表单时，自适应表单主题用作自适应表单模板的一部分来定义样式。

## 最佳实践 {#best-practices}

* **避免使用其他主题中的资源**

  编辑主题时，您可以浏览和添加其他主题中的资产（如图像）。 例如，您正在编辑页面的背景。 例如，当您选择 **[!UICONTROL 页面]** ![编辑按钮](assets/edit-button.png)> **[!UICONTROL 背景]** > **[!UICONTROL 添加]** > **[!UICONTROL 图像]**，您将看到一个对话框，它允许您浏览并在其他主题中添加图像。

  如果从其他主题添加资产，并且移动或删除了其他主题，则您可能会遇到当前主题的问题。 建议您避免浏览和添加其他主题中的资产。

* **更改容器面板布局宽度**

  不建议更改容器面板布局宽度。 指定容器面板的宽度时，其将变为静态并且不会适应不同的显示。

* **使用表单编辑器或主题编辑器处理页眉和页脚**

  如果要使用字体样式、背景和透明度等样式选项来设置页眉和页脚的样式，请使用主题编辑器。
如果要提供徽标图像、标题中的公司名称以及页脚中的版权信息等信息，请使用表单编辑器选项。

## 常见问题 {#faq}

**问：** 在全局级别和组件级别的主题文件夹中进行自定义时，哪种自定义设置优先？

**Ans：** 在全局级别和组件级别进行自定义时，组件级别的自定义设置优先。

<!--

## See next

* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/responsive-layout.md)
* [Generate Document of Record for Adaptive Forms (Core Components](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Create an Adaptive Forms with Repeatable sections](/help/forms/create-forms-repeatable-sections.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)


>[!MORELIKETHIS]
>
>* [Enable Adaptive Forms Core Components on AEM Forms as a Cloud Service and local development environment](/help/forms/enable-adaptive-forms-core-components.md)

-->


## 另请参阅 {#see-also}

{{see-also}}
* [为不同的屏幕大小和设备类型设置表单布局](/help/sites-cloud/authoring/features/responsive-layout.md)
* [生成自适应Forms记录文档（核心组件）](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [创建包含可重复部分的自适应Forms](/help/forms/create-forms-repeatable-sections.md)
* [主题模板和表单数据模型示例](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
* [在 AEM Forms as a Cloud Service 和本地开发环境上启用自适应表单核心组件](/help/forms/enable-adaptive-forms-core-components.md)
