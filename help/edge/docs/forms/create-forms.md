---
title: AEM Forms Edge Delivery Service快速入门
description: 制作完美的表单，快！ ⚡基于AEM Forms Edge Delivery文档的创作=速度飞快，采用SEO友好的表单，可让用户和搜索引擎更开心。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f37a99cd5cbfb745cb591e3be2a46a5f52139cb2
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---


# 在AEM Forms Edge Delivery Service上创建表单

在当今的数字时代，创建用户友好的表单对于任何组织都至关重要。 AEM Forms Edge交付允许您使用熟悉的工具(如Word或Google文档)创建表单。

这些表单将数据直接提交到Microsoft Excel或Google Sheets文件，使您能够使用动态的生态系统以及Google Sheets、Microsoft Excel和Microsoft Sharepoint的强大API，轻松处理提交的数据或启动现有的业务工作流。

## 先决条件

* 您拥有Github帐户。
* 您可以访问Google Sheets或Microsoft SharePoint。
* 您了解Git、HTML、CSS和JavaScript的基础知识。
* 您已安装Node和NPM以进行本地开发。

## 开始之前

* 设置和克隆边缘交付服务(EDS)项目。 请参阅 [开发人员教程](https://www.aem.live/developer/tutorial) 以了解详细信息。
* 克隆 [Forms阻止存储库](https://github.com/adobe/afb). 它包含呈现表单所需的表单块。

![Edge Delivery Forms快速入门](/help/edge/assets/getting-started-with-eds-forms.png)

## 将表单块添加到您的边缘交付服务(EDS)项目 {#add-forms-block-to-an-eds-project}

AEM Forms Edge Delivery包括表单块，可帮助您轻松创建表单以捕获和存储捕获的数据。 要将表单块包含到您的边缘交付服务项目中，请执行以下操作：

1. 导航到本地开发环境上的边缘交付服务(EDS)项目文件夹。


   ```Shell
   cd [EDS Project folder]
   ```

1. 创建名为的文件夹 `form` 在EDS项目目录下。 例如，在EDS项目的目录下，名为 `Portal`，创建一个名为的文件夹 `form`.

   ```Shell
   mkdir form
   ```


1. 添加 [Forms块](https://github.com/adobe/afb/tree/main/blocks/form) 文件移至“form”文件夹。

   ```shell
   cp -R <source:path of the form block> <destination: path of the form folder created in the previous step>
   
   For example
   
   cp -R Documents/afb/blocks/form Documents/portal/blocks/
   ```

1. 将“form”文件夹和基础文件签入GitHub上的边缘交付服务项目。

   ```Shell
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   您现在可以呈现EDS表单了。

   >[!NOTE]
   >
   > * 如果您的拉取请求/eds项目构建失败，并且您遇到与导入 `franklin-lib.js` 文件，更新import语句以引用 `aem.js` 文件，而不是 `franklin-lib.js` 文件。
   > * 如果您遇到任何绒毛错误，请随时将其忽略。 要绕过lint检查，请导航到package.json文件，然后从更新“lint”脚本 `"lint": "npm run lint:js && npm run lint:css"` 到 `"lint": "echo 'skipping linting for now'"`. 然后，将更改提交到package.json文件。

## 使用Microsoft Excel或Google工作表创建表单 {#create-a-form-for-an-eds-project}

允许网站开发人员创建表单并选择从网站访客那里收集哪些信息可能会有所帮助。 作者可以使用电子表格轻松设置表单，而不是复杂的流程。 他们需要添加正确的列标题，然后使用表单块在网站上轻松显示标题。 要创建表单，请执行以下操作：

1. 在Microsoft Excel或Google驱动器上AEM Edge Delivery项目目录下的任意位置创建Microsoft SharePoint工作簿或Google工作表。

1. 确保AEM用户(例如 `helix@adobe.com`)对工作表具有编辑权限。

1. 打开您创建的工作簿，并将默认工作表的名称更改为“shared-default”。

   ![将默认工作表重命名为“shared-default”](/help/edge/assets/rename-sheet-to-helix-default.png)

1. 复制 [联系我们电子表格](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) 到您自己的电子表格。

   ![联系我们电子表格](/help/edge/assets/contact-us-form-spreadsheet.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以预览和发布工作表。

   在预览和发布时，浏览器会打开以JSON格式显示工作表内容的新选项卡。 确保记下实时URL，因为这是以后呈现表单所必需的。

   URL 的格式为：

   ```shell
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

## 使用Edge Delivery Service (EDS)页面预览表单 {#add-a-form-to-your-eds-page}

到目前为止，您已为EDS项目启用表单块并准备了表单的结构。 现在，要将表单包含到EDS页面中并呈现它，请执行以下操作：

1. 转到Microsoft SharePoint或Google Drive上的AEM Edge Delivery项目目录。

1. 要将表单添加到页面，请打开相应的文档文件。 例如，打开索引文件。

1. 导航到文档中要添加表单的所需位置。

1. 将名为“Form”的块添加到该文件中，类似于下面显示的一个块。

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   在第二行中，以超链接的形式包含您在上一节中提到的URL。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以预览和发布页面。 将渲染表单。

   例如，以下是基于 [联系我们电子表格](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link)：


   ![联系我们（EDS表格）](/help/edge/assets/eds-form.png)

   表单块呈现表单，但尚未准备好接受数据。 单击提交按钮时，您会遇到与以下内容类似的错误：

   ![提交表单时出错](/help/edge/assets/form-error.png)

   [准备工作表以接受数据](/help/edge/docs/forms/submit-forms.md). 在准备接受数据之后，您可以将数据提交到工作表。


## 查看更多

* [创建和预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到站点页面](/help/edge/docs/forms/publish-eds-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [更改表单的主题和样式](/help/edge/docs/forms/style-theme-forms.md)