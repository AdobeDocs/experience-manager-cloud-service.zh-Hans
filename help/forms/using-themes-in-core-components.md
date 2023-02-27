---
title: 创建和使用主题
description: 您可以使用主题来使用核心组件对自适应表单进行风格化和提供可视化标识。 您可以在任意数量的自适应Forms中共享主题。
source-git-commit: 0205ffeabcb422ad70fd9439a1af246f438c52d5
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 5%

---


# 自适应Forms中的主题（核心组件） {#themes-for-af-using-core-components}

您可以使用核心组件创建并应用主题以风格化自适应表单。 主题包含组件和面板的样式详细信息。 样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式将反映在相应的组件上。 主题是独立管理的，不引用自适应表单。

当您 [创建自适应表单](/help/forms/creating-adaptive-form.md) 使用核心组件时，现成主题会显示在 **样式** 选项卡。 默认情况下，仅 **画布** 主题。

>[!NOTE]
>
>自适应表单主题不应与 [自适应表单模板。](/help/forms/template-editor.md) 自适应表单主题仅包含自适应表单的样式信息。 自适应表单模板可定义表单结构和初始内容，并包含一个主题以允许创建新表单 [自适应表单。](/help/forms/creating-adaptive-form.md)

## 在自适应Forms中使用画布主题（使用核心组件） {#using-theme-in-adaptive-form}

将主题应用于自适应表单的步骤如下：

1. 登录到您的AEM Forms创作实例。

1. 点按 **Adobe Experience Manager** > **Forms** > **Forms和文档**.

1. 单击 **创建** > **自适应Forms**. 此时将打开创建自适应表单的向导。

1. 在 **来源** 选项卡。

   >[!NOTE]
   >
   > 创建包含核心组件的自适应表单时，您会在样式选项卡下看到画布主题。 这是当前唯一可用的现成主题。 但您可以根据自己的喜好更改主题，并通过设置前端管道将其保存以供将来使用。

1. 在 **样式** 选项卡。
1. 单击&#x200B;**创建**。

自适应表单主题用作自适应表单模板的一部分，用于在创建自适应表单时定义样式。

## 自定义主题 {#customizing-theme}

要自定义主题，请

* [在Cloud Manager中设置管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* 使用 [参与者角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* 您应该拥有 [Git基本知识](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) 和Cloud ServiceGit存储库。

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
> 表单创建向导的“样式”选项卡显示与package.json文件中相同的主题名称。

### 2.了解主题的结构 {#structure-of-canvas-theme}

自适应表单主题是包含CSS、JavaScript和静态资源的包，这些资源定义表单的样式并符合自适应表单主题的结构。 自适应表单主题具有以下前端项目的典型结构：

* `src/components`:特定于AEM核心组件的JavaScript和CSS文件
* `src/resources`：图标、徽标和字体等静态文件
* `src/site`:应用于整个AEM Sites页面的JavaScript和CSS文件
* `src/theme.ts`:JavaScript和CSS主题的主要入口点
* `src\theme.scss`:适用于整个主题的JavaScript和CSS文件

的 `src/components` 文件夹具有特定于所有AEM核心组件的JavaScript和CSS文件，例如按钮、复选框、容器、页脚等。 您可以通过编辑特定于AEM组件的CSS文件来设置按钮或复选框的样式。

![编辑主题](/help/forms/assets/theme_structure.png)

要自定义主题，您可以启动本地代理服务器，以便根据实际的AEM内容实时查看主题自定义。

### 4.更改画布主题的package.json和package_lock.json中的名称 {#changename-packagelock-packagelockjson}

在 `package.json` 和 `package_lock.json` 文件。

>[!NOTE]
>
> 名称不应具有 `@aemforms` 标记。 它应该是简单的文本，作为用户提供的名称。

![画布主题图片](/help/forms/assets/changename_canvastheme.png)

### 3.在主题文件夹中创建.env文件 {#creating-env-file-theme-folder}

创建 `.env` 文件，并添加以下参数：

* **AEM url**
AEM_URL=https://[author-instance]

* **AEM网站名称**
AEM_ADAPTIVE_FORM=Form_name

* **AEM代理端口**
AEM_PROXY_PORT=7000


![画布主题结构](/help/forms/assets/env-file-canvas-theme.png)

### 4.启动本地代理服务器 {#starting-a-local-proxy-server}

1. 从命令行中，导航到本地计算机上主题的根。
1. 执行 `npm install`，npm 将检索依赖项并安装项目。
1. 执行 `npm run live`，代理服务器将启动。

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. 点按或单击 **在本地登录（仅限管理员任务）** 并使用AEM管理员为您提供的代理用户凭据登录。

   ![本地登录](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * 创建本地用户以在本地登录。 为主题设计器提供参与者角色。
   > * 如果您将AEM URL指定为 `http://localhost:[port]/` 在 `.env` 文件，您将被直接重定向到浏览器。


1. 登录后，将浏览器中的 URL 更改为指向 AEM 管理员提供给您的示例内容的路径。

   * 例如，如果提供的路径为 `/content/formname.html?wcmmode=disabled`，请将URL更改为 `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![代理的示例内容](/help/forms/assets/sample_af.png)

导航到自适应表单，以查看应用于自适应表单的画布主题。

### 5.自定义主题 {#customize-theme}

1. 在编辑器中，打开文件 `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > 您可以通过编辑 `site/_variables.scss` 文件。

1. 编辑 `font colour` to `red`.

   ![编辑主题](/help/forms/assets/edit_theme.png)

   **设置不同AEM组件的样式**

   您可以通过在编辑器中更改自适应表单的CSS文件来设置其不同组件的样式。 画布主题文件夹中每个自适应表单核心组件的CSS文件夹各不相同。

   ![核心组件](/help/forms/assets/theme-component.png)

   要在主题编辑器中指定特定组件的样式，可以在主题文件夹中编辑CSS。 例如，如果要更改文本框字段的边框颜色，请在编辑器中打开CSS文件并更改其边框颜色。

   ![编辑文本框CSS](/help/forms/assets/edit_color_textbox.png)

1. 保存文件时，代理服务器通过行识别更改 `[Browsersync] File event [change]`.

   ![代理浏览器同步](/help/forms/assets/browser_sync.png)

1. 切换回本地代理服务器的浏览器后，更改会立即显示。

   ![更改AF主题](/help/forms/assets/edit_theme_af.png)

主题设计器预览本地代理服务器中的更改，并根据不同AEM组件的要求自定义主题。

在将更改提交到AEM Git存储库之前，您需要访问 [Git存储库信息](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 6.提交更改 {#committing-the-changes}

在对主题进行更改并使用本地代理服务器对其进行测试后，将更改提交到AEM FormsCloud Service的Git存储库。 它让自定义主题在您的FormsCloud Service环境中可用，供自适应Forms作者使用。

在将更改提交到AEM FormsCloud Service的Git存储库之前，您需要在本地计算机上克隆该存储库。 要克隆存储库，请执行以下操作：

1. 通过单击 **[!UICONTROL 存储库]** 选项。

   ![创建新主题存储库](/help/forms/assets/createrepo_canvastheme.png)

1. 单击 **[!UICONTROL 添加存储库]** 并指定 **存储库名称** 在 **添加存储库** 对话框。 单击“**[!UICONTROL 保存]**”。

   ![添加画布主题存储库](/help/forms/assets/addcanvasthemerepo.png)

1. 单击 **[!UICONTROL 复制存储库URL]** 复制已创建存储库的URL。

   ![画布主题URL](/help/forms/assets/copyurl_canvastheme.png)

1. 打开命令提示符并克隆上面创建的云存储库。

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. 使用类似于
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
例如，使用此命令 
`cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. 在云存储库的目录中，使用以下命令提交您移入的主题文件。

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. 自定义项会推送到Git存储库。

   ![已提交更改](/help/forms/assets/cmd_git_push.png)

现在，您的自定义项可安全地存储在Git存储库中。


### 7.运行前端管道 {#deploy-pipeline}

1. 创建前端管道以部署自定义主题。 学习 [如何设置前沿管道以部署自定义主题](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).
1. 运行创建的前端管道以在 **[!UICONTROL 样式]** 自适应表单创建向导的选项卡。

>[!NOTE]
>
>将来，如果在画布主题文件夹中进行任何修改，则需要再次重新运行上述管道。 因此，必须记住管道的名称。

## 自定义主题的示例 {#example-to-customize-a-theme}

1. 登录到您的AEM Forms创作实例。
1. 打开使用核心组件创建的自适应表单。
1. 使用命令提示符启动本地代理服务器，然后单击 **在本地登录（仅限管理员任务）**.
1. 登录后，您将被重定向到浏览器并查看应用的主题。
1. 下载 [画布主题](https://github.com/adobe/aem-forms-theme-canvas) 并解压缩下载的zip文件夹。
1. 在首选编辑器中打开提取的zip文件夹。
1. 创建 `.env` 文件，并添加参数： **AEM URL**, **AEM_ADAPTIVE_FORM** 和 **AEM_PROXY_PORT**.
1. 在“画布”主题文件夹中打开文本框的CSS文件，并将其边框颜色更改为 `red` 颜色并保存更改。
1. 再次重新打开浏览器，您会看到所做的更改会立即反映在自适应表单中。
1. 在克隆的存储库中移动画布主题文件夹。
1. 提交更改并运行前端管道。

执行管道后，“样式”(Style)选项卡下将提供该主题。

## 最佳实践 {#best-practices}

* **避免使用其他主题的资产**

   编辑主题时，您可以浏览其他主题中的资产（如图像）并添加这些资产。 例如，您正在编辑页面的背景。 例如，当您选择 **[!UICONTROL 页面]** ![edit-button](assets/edit-button.png)> **[!UICONTROL 背景]** > **[!UICONTROL 添加]** > **[!UICONTROL 图像]**&#x200B;时，您会看到一个对话框，通过该对话框可以浏览并添加其他主题中的图像。

   如果从其他主题添加资产，而另一个主题被移动或删除，则您可能会遇到当前主题的问题。 建议您避免从其他主题浏览和添加资产。

* **更改容器面板布局宽度**

   不建议更改容器面板布局宽度。 指定容器面板的宽度时，该面板会变为静态，且不会适应不同的显示。

* **使用表单编辑器或主题编辑器处理页眉和页脚**

   如果要使用字体样式、背景和透明度等样式选项来设置页眉和页脚的样式，请使用主题编辑器。
如果要提供徽标图像、页眉中的公司名称以及页脚中的版权信息等信息，请使用表单编辑器选项。
