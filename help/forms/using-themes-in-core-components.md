---
title: 创建和使用主题
description: 您可以使用主题来使使用核心组件的自适应表单风格化并提供视觉标识。 您可以跨任意数量的自适应Forms共享主题。
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 5%

---

# 自适应Forms中的主题（核心组件） {#themes-for-af-using-core-components}

您可以创建和应用主题，以使用核心组件使自适应表单风格化。 主题包含组件和面板的样式详细信息。 样式包括诸如背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式反映在相应的组件上。 主题是独立管理的，无需引用自适应表单。

当您 [创建自适应表单](/help/forms/creating-adaptive-form.md) 使用核心组件，“现成”主题显示在 **样式** 选项卡。 默认情况下，仅 **画布** 提供了主题。

>[!NOTE]
>
>不应将自适应表单主题与 [自适应表单模板](/help/forms/template-editor.md). 自适应表单主题仅包含自适应表单的样式信息。 自适应表单模板定义表单结构和初始内容，并包含用于创建新内容的主题 [自适应表单](/help/forms/creating-adaptive-form.md).

## 使用核心组件在自适应Forms中使用画布主题 {#using-theme-in-adaptive-form}

将主题应用于自适应表单的步骤包括：

1. 登录到您的AEM Forms创作实例。

1. 点按 **Adobe Experience Manager** > **Forms** > **Forms和文档**.

1. 单击 **创建** > **自适应Forms**. 随即会打开创建自适应表单的向导。

1. 在中选择核心组件模板 **来源** 选项卡。

   >[!NOTE]
   >
   > 创建包含核心组件的自适应表单时，您会在“样式”选项卡下方看到画布主题。 这是目前唯一可用的开箱即用主题。 但您可以通过设置前端管道将主题更改为喜欢并保存以供将来使用。

1. 选择中的画布主题 **样式** 选项卡。
1. 单击&#x200B;**创建**。

创建自适应表单时，自适应表单主题用作自适应表单模板的一部分来定义样式。

## 自定义主题 {#customizing-theme}

要自定义主题，

* [在Cloud Manager中设置管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* 使用配置用户 [投稿人角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* 您应该有一个 [Git基础知识](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) 和Cloud ServiceGit存储库。

要自定义画布主题，请执行以下操作：

1. [克隆画布主题](#1-download-canvas-theme-download-canvas-theme)
1. [了解主题的结构](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [在package.json和package_lock.json中更改名称](#changename-packagelock-packagelockjson)
1. [创建 ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [启动本地代理服务器](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [自定义主题](#customize-the-theme-customizing-theme)
1. [提交更改](#6-committing-the-changes-committing-the-changes)
1. [部署管道](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1.克隆画布主题 {#download-canvas-theme}

打开命令提示符并运行以下命令以克隆画布主题：

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> 表单创建向导的“样式”选项卡显示的主题名称与package.json文件中的主题名称相同。

### 2.了解主题结构 {#structure-of-canvas-theme}

自适应表单主题是一个包，其中包含定义表单样式并符合自适应表单主题结构的CSS、JavaScript和静态资源。 自适应表单主题具有以下典型的前端项目结构：

* `src/components`：特定于AEM核心组件的JavaScript和CSS文件
* `src/resources`：图标、徽标和字体等静态文件
* `src/site`：应用于整个AEM Sites页面的JavaScript和CSS文件
* `src/theme.ts`：JavaScript &amp; CSS主题的主要入口点
* `src\theme.scss`：应用于整个主题的JavaScript和CSS文件

此 `src/components` 文件夹具有特定于所有AEM核心组件（如按钮、复选框、容器、页脚等）的JavaScript和CSS文件。 您可以通过编辑特定于AEM组件的CSS文件来设置按钮或复选框的样式。

![编辑主题](/help/forms/assets/theme_structure.png)

要自定义主题，您可以启动本地代理服务器，以根据实际AEM内容实时查看主题自定义。

### 3.更改画布主题的package.json和package_lock.json中的名称 {#changename-packagelock-packagelockjson}

在中更新画布主题的名称和版本 `package.json` 和 `package_lock.json` 文件。

>[!NOTE]
>
> 名称不应包含 `@aemforms` 标记之前。 它应该是用户提供的名称形式的简单文本。

![画布主题图片](/help/forms/assets/changename_canvastheme.png)

### 4.在主题文件夹中创建.env文件 {#creating-env-file-theme-folder}

创建 `.env` 文件，并添加以下参数：

* **AEM url**
AEM_URL=https://[author-instance]

* **AEM站点名称**
AEM_ADAPTIVE_FORM=Form_name

* **AEM代理端口**
AEM_PROXY_PORT=7000


![画布主题结构](/help/forms/assets/env-file-canvas-theme.png)

### 5.启动本地代理服务器 {#starting-a-local-proxy-server}

1. 从命令行中，导航到本地计算机上主题的根。
1. 执行 `npm install`，npm 将检索依赖项并安装项目。
1. 执行 `npm run live`，代理服务器将启动。

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. 点击或单击 **本地登录（仅限管理任务）** 并使用AEM管理员提供给您的代理用户凭据进行登录。

   ![本地登录](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * 创建本地用户以本地登录。 为主题设计者提供参与者角色。
   > * 如果将AEM URL指定为 `http://localhost:[port]/` 在 `.env` 画布主题文件，您将直接重定向到浏览器。

1. 登录后，将浏览器中的 URL 更改为指向 AEM 管理员提供给您的示例内容的路径。

   * 例如，如果提供的路径为 `/content/formname.html?wcmmode=disabled`，将URL更改为 `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![代理的示例内容](/help/forms/assets/sample_af.png)

导航到自适应表单，查看应用于自适应表单的画布主题。

### 6.自定义主题 {#customize-theme}

1. 在编辑器中，打开文件 `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > 您可以通过编辑 `site/_variables.scss` 文件。

1. 编辑变量 `font colour` 到 `red`.

   ![编辑主题](/help/forms/assets/edit_theme.png)

   **设置其他AEM组件的样式**

   您可以通过更改自适应表单在编辑器中的CSS文件来设置其不同组件的样式。 Canvas Theme文件夹中的每个Adaptive Form核心组件都有不同的CSS文件夹。

   ![核心组件](/help/forms/assets/theme-component.png)

   要在主题编辑器中指定特定组件的样式，可以在主题文件夹中编辑CSS。 例如，如果要更改文本框字段的边框颜色，请在编辑器中打开CSS文件并更改其边框颜色。

   ![编辑文本框CSS](/help/forms/assets/edit_color_textbox.png)

1. 保存文件时，代理服务器通过行来识别更改 `[Browsersync] File event [change]`.

   ![代理浏览器同步](/help/forms/assets/browser_sync.png)

1. 切换回本地代理服务器的浏览器后，更改将立即可见。

   ![更改AF主题](/help/forms/assets/edit_theme_af.png)

主题设计者预览本地代理服务器中的更改，并根据不同AEM组件的要求自定义主题。

在将更改提交到AEM Git存储库之前，您需要访问 [Git存储库信息](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 7.提交更改 {#committing-the-changes}

更改主题并使用本地代理服务器测试该主题后，将更改提交到AEM FormsCloud Service的Git存储库。 它使自定义主题可在FormsCloud Service环境中提供给Adaptive Forms作者使用。

在将更改提交到AEM FormsCloud Service的Git存储库之前，需要克隆本地计算机上的存储库。 要克隆存储库：

1. 通过单击 **[!UICONTROL 存储库]** 选项。

   ![创建新主题存储库](/help/forms/assets/createrepo_canvastheme.png)

1. 单击 **[!UICONTROL 添加存储库]** 并指定 **存储库名称** 在 **添加存储库** 对话框。 单击“**[!UICONTROL 保存]**”。

   ![添加画布主题存储库](/help/forms/assets/addcanvasthemerepo.png)

1. 单击 **[!UICONTROL 复制存储库URL]** 以复制已创建存储库的URL。

   ![画布主题URL](/help/forms/assets/copyurl_canvastheme.png)

1. 打开命令提示符并克隆上面创建的云存储库。

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. 使用类似于的命令将正在编辑的主题存储库的文件移动到云存储库中
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
例如，使用此命令 `cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. 在云存储库的目录中，使用以下命令提交您移入的主题文件。

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. 自定义项将被推送到Git存储库。

   ![已提交更改](/help/forms/assets/cmd_git_push.png)

您的自定义项现在安全地存储在Git存储库中。


### 8.运行前端管道 {#deploy-pipeline}

1. 创建前端管道以部署自定义主题。 了解 [如何设置一线管道以部署自定义主题](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).
1. 运行创建的前端管道以部署下的自定义主题文件夹 **[!UICONTROL 样式]** 自适应表单创建向导的选项卡。

>[!NOTE]
>
>将来，如果您在画布主题文件夹中进行任何修改，则需要重新运行上述管道。 因此，必须记住管道的名称。

## 自定义主题的示例 {#example-to-customize-a-theme}

1. 登录到您的AEM Forms创作实例。
1. 打开使用核心组件创建的自适应表单。
1. 使用命令提示符启动本地代理服务器，然后单击 **本地登录（仅限管理任务）**.
1. 登录后，您将被重定向到浏览器并查看应用的主题。
1. 下载 [画布主题](https://github.com/adobe/aem-forms-theme-canvas) 并解压缩下载的zip文件夹。
1. 在首选编辑器中打开解压缩的zip文件夹。
1. 创建 `.env` 文件，并添加参数： **AEM URL**， **AEM_ADAPTIVE_FORM** 和 **AEM_PROXY_PORT**.
1. 打开Canvas主题文件夹中文本框的CSS文件，并更改其边框颜色以显示 `red` 颜色并保存更改。
1. 再次重新打开浏览器，您将看到所做的更改立即反映在自适应表单中。
1. 将画布主题文件夹移动到克隆的存储库中。
1. 提交更改并运行前端管道。

执行管道后，该主题将在“样式”选项卡下可用。

## 最佳实践 {#best-practices}

* **避免使用其他主题中的资源**

  编辑主题时，您可以浏览和添加其他主题中的资产（如图像）。 例如，您正在编辑页面的背景。 例如，当您选择 **[!UICONTROL 页面]** ![编辑按钮](assets/edit-button.png)> **[!UICONTROL 背景]** > **[!UICONTROL 添加]** > **[!UICONTROL 图像]**，您将看到一个对话框，通过该对话框可以浏览并添加其他主题中的图像。

  如果从其他主题添加资产，并且移动或删除了其他主题，则您可能会遇到当前主题的问题。 建议您避免浏览和添加其他主题中的资产。

* **更改容器面板布局宽度**

  不建议更改容器面板布局宽度。 指定容器面板的宽度时，该宽度会变为静态并且不会适应不同的显示。

* **使用表单编辑器或主题编辑器处理页眉和页脚**

  如果要使用字体样式、背景和透明度等样式选项来设置页眉和页脚的样式，请使用主题编辑器。
如果要提供徽标图像、页眉中的公司名称和页脚中的版权信息等信息，请使用表单编辑器选项。
