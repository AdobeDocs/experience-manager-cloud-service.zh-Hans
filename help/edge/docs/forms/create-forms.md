---
title: AEM Forms Edge Delivery Service快速入门
description: 制作完美的表单，快！ ⚡基于AEM Forms Edge Delivery文档的创作=速度飞快，采用SEO友好的表单，可让用户和搜索引擎更开心。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: b94bd6cd70af541444fda1d03f502b4588fd879b
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---


# 在AEM Forms Edge Delivery Service上创建表单

在当今的数字时代，创建用户友好的表单对于任何组织都至关重要。 AEM Forms Edge交付允许您使用熟悉的工具(如Word或Google文档)创建表单。

这些表单将数据直接提交到Microsoft Excel或Google Sheets文件，使您能够使用动态的生态系统以及Google Sheets、Microsoft Excel和Microsoft Sharepoint的强大API，轻松处理提交的数据或启动现有的业务工作流。

## 先决条件

* 您拥有GitHub帐户。
* 您可以访问Google Sheets或Microsoft SharePoint。
* 您了解Git、HTML、CSS和JavaScript的基础知识。
* 您已安装Node和NPM以进行本地开发。

## 开始之前

* 设置和克隆您的边缘交付服务(EDS)项目。 请参阅 [开发人员教程](https://www.aem.live/developer/tutorial) 以了解详细信息。
* 克隆 [Forms阻止存储库](https://github.com/adobe/afb). 它包含呈现表单所需的表单块。

![Edge Delivery Forms快速入门](/help/edge/assets/getting-started-with-eds-forms.png)

## 将表单块添加到您的边缘交付服务(EDS)项目 {#add-forms-block-to-an-eds-project}

AEM Forms Edge Delivery包括表单块，可帮助您轻松创建表单以捕获和存储捕获的数据。 要将表单块包含到您的边缘交付服务项目中，请执行以下操作：

1. 导航至 `blocks` 本地开发环境中Edge Delivery Service (EDS)项目文件夹中的文件夹。


   ```Shell
   cd [EDS Project folder]/blocks
   ```

1. 创建名为的文件夹 `form` 在 `blocks` 目录。 例如，在EDS项目的目录下，名为 `Portal`，创建一个名为的文件夹 `form`.

   ```Shell
   mkdir form
   ```


1. 添加 [Forms块](https://github.com/adobe/afb/tree/main/blocks/form) 文件移至“form”文件夹。

   ```shell
   cp -R <source:path of the form block> <destination: path of the form folder created in the previous step>
   ```

   **例如，**


   ```shell
   cp -R ../../afb/blocks/form ../../fantastic-computing-machine/blocks 
   ```



1. 将“form”文件夹和基础文件签入GitHub上的边缘交付服务项目。

   ```Shell
   cd ..
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   表单块将添加到您的EDS项目中。 您现在可以创建表单并将其添加到您的站点。

   >[!NOTE]
   >
   > * 如果遇到错误“无法解析模块“&#39;../../scripts/lib-franklin.js&#39;”的路径，请打开 `[EDS Project]/blocks/forms/form.js` 文件。 在import语句中，将 `franklin-lib.js` 文件包含 `aem.js` 文件。
   > * 如果您遇到任何绒毛错误，请随时将其忽略。 要绕过衬线检查，请打开 `[EDS Project]\package.json` 文件并更新“lint”脚本 `"lint": "npm run lint:js && npm run lint:css"` 到 `"lint": "echo 'skipping linting for now'"`. 保存文件并将其提交到GitHub项目。

## 使用Microsoft Excel或Google工作表创建表单 {#create-a-form-for-an-eds-project}

您可以使用电子表格轻松创建表单，而不是复杂的流程。 首先，将行和列标题添加到电子表格中，其中每一行定义一个表单字段，每一列标题定义相应表单字段的属性。

例如，在以下电子表格中，行定义 `contact us` 表单和列标题定义对应字段的属性。

![联系我们电子表格](/help/edge/assets/contact-us-form-spreadsheet.png)

要创建表单，请执行以下操作：

1. 在Microsoft SharePoint或Google驱动器上打开AEM Edge Delivery项目文件夹。

1. 在AEM Edge Delivery项目目录下的任意位置创建Microsoft Excel工作簿或Google工作表。 例如，创建一个名为 `contact-us` 在Google驱动器上的AEM Edge Delivery项目目录下。

1. 确保与AEM用户共享工作表(例如 `helix@adobe.com`) [为您的项目配置](https://www.aem.live/docs/setup-customer-sharepoint) 和用户具有工作表的编辑权限。

1. 打开您创建的电子表格，并将默认工作表的名称更改为“shared-default”。

   ![将默认工作表重命名为“shared-default”](/help/edge/assets/rename-sheet-to-shared-default.png)

1. 要添加表单的字段，请将行和列标题添加到 `shared-default` 工作表，其中每一行定义一个表单字段，每一列标题定义 [属性](/help/edge/docs/forms/eds-form-field-properties))。

   要快速启动，您可以复制 [联系我们电子表格](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) 到您的电子表格。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以预览和发布工作表。

   ![使用AEM Sidekick预览和发布工作表](/help/edge/assets/preview-form.png)

   在预览和发布时，浏览器会打开以JSON格式显示工作表内容的新选项卡。 确保记下实时URL，因为这是以后呈现表单所必需的。

   URL 的格式为：

   ```JSON
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```



## 使用Edge Delivery Service (EDS)页面预览表单 {#add-a-form-to-your-eds-page}

到目前为止，您已为EDS项目启用表单块并准备了表单的结构。 现在，要预览表单，请执行以下操作：

1. 转到Microsoft SharePoint或Google Drive上的AEM Edge Delivery项目目录。

1. 创建或打开doc文件以托管表单。 例如，打开索引文件。

1. 导航到文档中要添加表单的所需位置。

1. 将名为“Form”的块添加到该文件中，类似于下面显示的一个块。

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   在第二行中，以超链接的形式包含您在上一节中提到的URL。 您可以使用预览URL (.page URL)或发布URL (.live)。 为生产构建或测试表单和发布URL时，可以使用预览URL。

   >[!IMPORTANT]
   >
   >
   > 请确保未以纯文本形式提及URL。 它应作为超链接添加。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以预览页面。 页面现在会显示表单。 例如，以下是基于 [联系我们电子表格](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link)：


   ![EDS表单示例](/help/edge/assets/eds-form.png)

   现在，填写表单并单击“提交”按钮，您会遇到与以下内容类似的错误，因为电子表格尚未设置为接受数据。

   ![提交表单时出错](/help/edge/assets/form-error.png)


   下一步是 [准备电子表格以接受数据](/help/edge/docs/forms/submit-forms.md).



## 查看更多

* [表单字段属性](/help/edge/docs/forms/eds-form-field-properties)
* [创建和预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到站点页面](/help/edge/docs/forms/publish-eds-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [更改表单的主题和样式](/help/edge/docs/forms/style-theme-forms.md)
