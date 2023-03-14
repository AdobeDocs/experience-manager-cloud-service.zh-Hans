---
title: 使用核心组件和Headless构建引人入胜的Forms
seo-title: Build Engaging Forms Using Core Components and Headless
description: 使用核心组件和Headless构建引人入胜的Forms
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
source-git-commit: 8f3ffc72507be1d28bc437041579578d6a479e23
workflow-type: tm+mt
source-wordcount: '2453'
ht-degree: 1%

---


# 使用核心组件和Headless构建引人入胜的Forms

## 实验室概述

在这个动手实验中，您将学习：

如何使用AEM Forms轻松创建自适应表单(使用与AEM Sites一致的最新核心组件)，通过将自适应表单作为Headless表单提供给Web、移动和聊天，实现全渠道数据捕获体验。 您还可以了解有关样式、自定义和前端开发的最佳实践。

## 主要要点

* **业务灵活性**：作为商业用户，我可以轻松为多个渠道创作表单体验。

* **能够成为前端开发人员**：作为前端开发人员，我可以使用Headless表单控制最终用户体验。

* **Developer Velocity**：作为开发人员，我可以轻松且一致地自定义Sites和Forms组件。

## 前提条件

AEM Forms作为Cloud Service沙盒

## 第1课

### 目标

熟悉AEM Formsas a Cloud Service环境。

### 课程上下文

在本课程中，您可以通过导航用户界面来熟悉AEM Formsas a Cloud Service环境。

### 练习

1. 打开浏览器，并输入Cloud Service创作环境的URL。 例如：
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. 根据共享的凭据登录到Cloud Service创作环境。 例如：用户名： [L716+001@summitlab.us](mailto:L716%2B001@summitlab.us)
密码： 
**Adobe123！**

1. 登录后，导航到AEM Forms UI。 单击 **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. 单击 **Forms和文档**. 关闭任何与首选项或信息相关的弹出窗口。

   ![](/help/forms/assets/screenshot2028113929.png)

   将显示所有可用表单。

   ![](/help/forms/assets/screenshot2028114029.png)

## 第2课

### 目标

使用最新的核心组件创作自适应表单、配置并提交表单。

## 课程上下文

在本课程中，作为企业用户，您将使用自适应表单创作功能为多个渠道（如Web、移动和聊天）创作自适应表单，并使用标准化的OOTB核心组件进行数据捕获。

## 练习

1. 为表单创建提交端点：

   1. 打开 <https://requestbin.com/> 在新的浏览器选项卡中。
      ![](/help/forms/assets/screenshot2028114329.png)

   1. 单击 **创建公共bin** 和复制端点URL。
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. 使用向导界面创作自适应表单：

   1. 在第1课中使用的“浏览器”选项卡中，导航到AEM Forms作为Cloud ServiceWeb界面，然后导航到Forms和“文档”。
      ![](/help/forms/assets/screenshot2028114029.png)

   1. 单击 **创建** 并选择自适应表单。
      ![](/help/forms/assets/screenshot2028114629.png)

   1. 选择 **带核心组件的空白** 模板选择屏幕中的模板，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. 单击 **样式** 选项卡，然后选择 **wknd — 主题** 主题，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. 单击 **提交** 选项卡，然后选择 **提交到REST端点** 卡并在中指定公共bin
      **POST请求的URL** 字段，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. 单击&#x200B;**创建**。指定表单的名称和标题。 例如， **contactact**. 单击&#x200B;**创建**。
      ![](/help/forms/assets/screenshot2028123329.png)

   1. 自适应表单编辑器将打开。 关闭任何弹出窗口或对话框以获取首选项或信息。 单击左边栏上的组件浏览器并添加 **页脚** 组件到空白表单的底部。
      ![](/help/forms/assets/screenshot2028121929.png)

   1. 添加 **页眉** 组件到表单顶部。
      ![](/help/forms/assets/screenshot2028122029.png)

   1. 添加 **标题** 组件到窗体中间。
      ![](/help/forms/assets/screenshot2028122129.png)

   1. 添加 **文本输入** 标题组件之后的组件。
      ![](/help/forms/assets/screenshot2028122329.png)

   1. 添加 **数字输入** 组件。
      ![](/help/forms/assets/screenshot2028122429.png)

   1. 添加 **提交按钮** 组件添加到表单。
      ![](/help/forms/assets/screenshot2028122529.png)

   1. 单击 **标题** 组件，以便 **弹出菜单** 将显示。 单击 **“编辑”图标** 在菜单中编辑标签。
      ![](/help/forms/assets/screenshot2028122629.png)

   1. 输入 `Contact Us` 作为标题文本。
      ![](/help/forms/assets/screenshot2028122829.png)

   1. 单击 **文本输入** 组件，以显示弹出菜单。 单击 **“编辑”图标** 在菜单中编辑标签。
      ![](/help/forms/assets/screenshot2028122929.png)

   1. 输入 **全名** 作为字段标签。
      ![](/help/forms/assets/screenshot2028123029.png)

   1. 单击 **数字输入** 组件，以显示弹出菜单。 单击 **“编辑”图标** 在菜单中编辑标签。
      ![](/help/forms/assets/screenshot2028123129.png)

   1. 输入 **电话号码** 作为字段标签。
      ![](/help/forms/assets/screenshot2028123829.png)


1. 将验证添加到表单：

   1. 单击 **电话号码** 组件，以显示弹出菜单。 单击 **“扳手”图标** 以配置字段。
      ![](/help/forms/assets/screenshot2028123429.png)

   1. 打开 **“验证”选项卡**，标记字段 **必需**，然后单击 **完成**. 将显示成功消息。
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. 单击 **预览** 以从最终用户的角度预览表单。
      ![](/help/forms/assets/screenshot2028125529.png)

   1. 用虚拟数据填写表单
      ![](/help/forms/assets/screenshot2028125629.png)

   1. 提交表单
      ![](/help/forms/assets/screenshot2028125729.png)

   1. 在请求箱选项卡中，检查已提交的数据。
      ![](/help/forms/assets/screenshot2028125829.png)

现在，为了进行剩余的练习，请使用预创建的注册表单。

1. 打开AEM Forms管理界面，例如， `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`，然后选择注册表单。

   ![](/help/forms/assets/screenshot2028115529.png)

1. 单击&#x200B;**发布**。

   ![](/help/forms/assets/screenshot2028115629.png)

   将显示成功消息。

   ![](/help/forms/assets/screenshot2028115729.png)

   表单的发布URL将类似于 `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. 要查看已发布的表单，请将上述URL中的项目ID (pXXXXXX)和环境ID (eXXXXXX)替换为您环境的ID。

## 第3课

### 目标

使用前端开发最佳实践更新样式。

### 课程上下文

在本课程中，作为前端开发人员，您将学习如何轻松更新之前创建的自适应表单的样式。

### 练习

设置主题的本地存储库：

1. 打开命令提示符或具有管理员权限的shell：

   ![](/help/forms/assets/screenshot2028115829.png)

1. 在命令提示符下，使用以下命令导航到 **c：\git** 文件夹

   ```Shell
   cd c:\git
   ```

1. 使用以下命令克隆主题前端代码：

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. 按照列出的顺序使用以下命令导航到 **aem-forms-theme-canvas** 目录并打开Visual Studio Code。

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. 选择 **信任父文件夹中所有文件的作者** 并单击 **是的，我相信作者**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. 要渲染托管在云服务发布环境中的表单，请重命名 `env_template` 文件。  要重命名文件，请右键单击 **env_template** 文件并选择 **重命名** 选项。

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. 为.env文件中的变量设置以下值并保存文件：

   * **AEM_URL**：指定您的Cloud Service发布环境。 例如，`https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**：指定表单的路径。 例如，如果表单路径为 `/content/forms/af/registration`，则此变量的值将为 `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)

   ![](/help/forms/assets/screenshot20228116569.png)


1. 在“Command Prompt（命令提示）”窗口中，运行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * 如果您收到一条消息，要求通过 `npm notice Run npm nstall -g npm@9.6.0`命令，忽略消息。
   > * 除非工作簿中有指示，否则不要运行其他npm命令。


1. 现在，运行以下命令来预览表单。

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   执行上述命令后，等待 `webpack compiled` 消息。 表单显示在浏览器选项卡中。

   >[!NOTE]
   >
   >如果您在执行之后在浏览器中遇到空白屏幕 `npm run live` 命令，更改 `localhost` 在浏览器URL中转到127.0.0.1并点击 **输入**.



   ![](/help/forms/assets/screenshot2028115129.png)


1. 在Visual Studio Code中，打开 `PROJECT\src\site\_variables.scss` 文件。 请注意 `$error` 颜色是红色的阴影。

   ![](/help/forms/assets/screenshot2028120729.png)

1. 在浏览器中，提交表单以查看 **名字** 字段。

   ![](/help/forms/assets/screenshot2028120829.png)

1. 设置 **$error** 颜色至 **#5736eb** 并保存文件。

   ![](/help/forms/assets/screenshot2028120729.png)

1. 刷新浏览器并提交表单。 请注意名字字段上的错误颜色已相应更改。

   ![](/help/forms/assets/screenshot2028121129.png)

1. 在命令提示符下，按 **CTRL+C**，输入 **Y**，并按 **输入** 键终止npm进程。 务必停止npm服务器，以免与下一组练习冲突。
1. 关闭Visual Studio代码和命令提示符窗口。

## 第4课

### 目标

将表单渲染为Headless表单，并将其渲染到Web/移动和其他界面。

### 课程上下文

在本课程中，作为前端开发人员，您将学习如何使用反应光谱设计框架将之前创建的自适应表单渲染为Headless表单。

### 练习

使用react starter项目设置本地存储库：

1. 使用管理员权限打开命令提示符。

   ![](/help/forms/assets/screenshot2028115829.png)

1. 在命令提示符下，使用以下命令导航到 **c：\git** 文件夹

   ```Shell
   cd c:\git
   ```

1. 使用以下命令克隆自适应表单react启动程序项目：

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. 按照列出的顺序使用以下命令导航到 **react-starter-kit-aem-headless-forms** 目录并打开Visual Studio Code。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   将打开Visual Studio Code窗口。

   ![](/help/forms/assets/screenshot2028117429.png)

要渲染托管在您的云服务发布环境中的表单，请执行以下操作：

1. 将env_template文件重命名为.env文件。 要重命名，请右键单击 **env_template** 文件并选择 **重命名** 选项。

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. 为.env文件中的变量设置以下值。 更新变量后，保存文件。

   * **AEM_URL**：指定云服务发布环境的URL。 例如，`https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**：指定在上一课程中创建的自适应表单的路径。 例如，`/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. 打开命令窗口，确保位于react-starter-kit-aem-headless-forms目录，然后运行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. 在“Command Prompt（命令提示）”窗口中，运行以下命令：

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   上述命令启动本地开发服务器，该服务器将使用反应光谱前端库以Headless方式呈现从AEM获取的表单定义。

   >[!NOTE]
   >
   >如果您在执行之后在浏览器中遇到空白屏幕 `npm start` 命令，更改 `localhost` 在浏览器URL中转到127.0.0.1并点击 **输入**.

   ![](/help/forms/assets/screenshot2028118229.png)

让我们检查此Headless表单中规则的执行：

1. 选择 **选中可享受5%折扣的复选框** 选项。 用于应用信用卡的后续选项已禁用。

   ![](/help/forms/assets/screenshot2028126229.png)

1. 取消选中 **选中可享受5%折扣的复选框** 以启用信用卡选项。

   ![](/help/forms/assets/screenshot2028126329.png)

让我们以业务用户身份对服务器上的表单进行更改，并自动查看反映在Headless表单中的更改。

1. 在浏览器中打开AEM Forms管理界面。 例如， [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. 选择 **注册** 表单并单击 **编辑。** 它会在自适应表单编辑器中打开表单。

   ![](/help/forms/assets/screenshot2028118529.png)

1. 选择 **电话号码** 字段，然后单击 **“编辑”图标（铅笔图标）** 工具栏中。 如果看不到弹出式工具栏，请单击以切换到编辑模式 **编辑** 按钮在右上方，从左到 **预览** 按钮。

   ![](/help/forms/assets/screenshot2028119629.png)

1. 将标签更改为手机号码。 单击表单中的任何空格，并保存对表单所做的更改。

   ![](/help/forms/assets/screenshot2028119729.png)

让我们发布更新的表单以将更改传播到发布环境。

1. 在AEM Forms管理界面选项卡中，选择注册表单，然后单击 **取消发布**. 如果您没有看到 **取消发布** 按钮，跳至步骤3以直接发布更改。

   ![](/help/forms/assets/screenshot2028119829.png)

1. 单击 **取消发布**. 单击 **关闭** 在各自的对话框中。

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. 浏览器刷新后，选择注册表单并单击 **Publish**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. 单击&#x200B;**发布**。单击 **关闭** 在相应的对话框中。

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. 在显示Headless表单的情况下刷新浏览器选项卡。 请注意，“电话号码”标签已更改为“手机号码”。

   ![](/help/forms/assets/screenshot2028120529.png)

1. 打开用于启动 **react-starter-kit-aem-headless-forms** 项目，按 **CTRL+C**，然后输入 **Y** 并按Enter键终止npm进程。 务必停止npm服务器，以免与下一组练习冲突。

1. 关闭Visual Studio代码和命令提示符窗口。


## 第5课

### 目标

使用Google材料UI将表单渲染为Headless表单

### 课程上下文

在本课程中，作为前端开发人员，您将了解如何使用Google材料UI将之前创建的自适应表单渲染为Headless表单。

### 练习

使用材料UI入门项目设置本地存储库：

1. 使用管理员权限打开命令提示符。

   ![](/help/forms/assets/screenshot2028115829.png)


1. 在命令提示符下，使用以下命令导航到 **c：\git** 文件夹：

   ```Shell
   cd c:\git
   ```

1. 按列出的顺序运行以下命令以创建名为mui的文件夹，并使用以下命令导航到mui文件夹：

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. 使用以下命令克隆自适应表单react启动程序项目：

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. 按照列出的顺序使用以下命令导航到 **react-starter-kit-aem-headless-forms** 文件夹并在Visual Studio Code中打开代码：

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

要渲染托管在您的云服务发布环境中的表单，请执行以下操作：

1. 重命名 **env_template** 文件到 **.env** 文件。 要重命名，请右键单击 **env_template** 文件并选择 **重命名**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. 为.env文件中的变量设置以下值。 更新变量后，保存文件。 使用 **CTRL + S** 切换组合以保存文件。

   * **AEM_URL**：指定云服务发布环境的URL。 例如， [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**：指定在上一课程中创建的自适应表单的路径。 例如，/content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. 打开命令窗口，确保您位于 **react-starter-kit-aem-headless-forms** 目录，并运行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. 在“Command Prompt（命令提示）”窗口中，运行以下命令：

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   该命令将启动本地开发服务器，并使用Google材料UI前端库以无头方式呈现从AEM获取的表单定义。

   >[!NOTE]
   >
   >如果您在执行之后在浏览器中遇到空白屏幕 `npm start` 命令，更改 `localhost` 在浏览器URL中转到127.0.0.1并点击 **输入**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. 要评估此表单演绎版中相同业务逻辑的执行，请执行以下操作：

   选择 **选中可享受5%折扣的复选框**. 后续选项 **您要申请We.Finance公司信用卡表格吗？** 被禁用。

   ![](/help/forms/assets/screenshot2028127329.png)

## 第6课

### 目标

使用材质UI组件变体创建Headless表单的替代外观

### 课程上下文

在本课程中，作为前端开发人员，您将了解如何使用材料UI为业务用户之前创建的自适应表单创建不同组件的替代表示形式。

### 练习

更新Headless项目中组件的变体。 要将材质UI文本输入组件的变体更改为 `OutlinedInput`：

1. 在可视代码中，通过打开 `index.tsx` 文件位置 `src/components/textinput/index.tsx`.

1. 添加 `//` 在代码行103的开头。 它将线条转换为注释。

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. 在第104行添加以下内容以使用不同的组件变体并保存文件。 使用 **CTRL + S** 切换组合以保存文件。

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   必须对“OverridedInput”变量使用正确的大小写，否则编译将失败。 本地开发环境编译在命令提示符下自动开始。 等待您看到以下消息

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. 如果浏览器未自动刷新，请刷新浏览器以查看文本输入组件使用不同的变体。

   ![](/help/forms/assets/screenshot2028127729.png)


   此更改适用于最终用户，不会对AEM Forms Server中的表单定义进行任何更改，并且此更改特定于正在考虑的Headless渠道。 例如，本实验中的Web渠道。

   ![](/help/forms/assets/screenshot2028127529.png)


1. 关闭Visual Studio代码和命令提示符窗口。

## 常见问题解答(FAQ)

+++ 自适应表单向导是否可公开使用？

是，它可作为Cloud Service在AEM Forms中使用。

+++


+++ 核心组件是否可公开发布？

是，自适应Forms核心组件随AEM FormsCloud Service提供。

+++

+++ Headless表单是否可公开使用？

是，Headless表单可作为Cloud Service随AEM Forms提供。

+++

+++ Headless表单是否需要单独的许可证？

否，Headless表单使用相同的许可值量度、表单提交次数。

+++

+++ AEM 6.5 Forms是否提供核心组件和Headless表单？

是，自适应表单核心组件和Headless表单都随AEM Forms 6.5 Service Pack 16及更高版本提供。

+++


## 下面的步骤

现在您已了解如何构建自适应表单并使用Headless表单将其交付到多个渠道，您应该尝试将新技能付诸实践。 通过为最终用户大规模创建并提供卓越的数据捕获体验，尽情体验吧！

## 资源

* [自适应表单核心组件简介](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [使用核心组件创建自适应表单](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [更新基于核心组件的AF的样式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Headless自适应表单](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [使用Headless React入门工具包](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


