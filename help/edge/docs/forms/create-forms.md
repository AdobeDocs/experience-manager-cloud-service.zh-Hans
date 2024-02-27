---
title: AEM Forms Edge Delivery Service 快速入门
description: 快速制作完美的表单！⚡ AEM Forms Edge Delivery 基于文档的创作 = 速度极快、SEO 友好的表单，让用户更加满意，搜索引擎更加优异。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 78d40574e6fea8dde22414e43fd77215b9e7d2a1
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 60%

---


# 在 AEM Forms Edge Delivery Service 上创建表单

在当今的数字时代，创建用户友好的表单对于任何组织都至关重要。AEM Forms Edge Delivery 允许您使用 Word 或 Google Docs 等熟悉的工具创建表单。

这些表单可将数据直接提交到 Microsoft Excel 或 Google Sheets 文件，使您能够使用 Google Sheets、Microsoft Excel 和 Microsoft Sharepoint 充满活力的生态系统和强大的 API 来轻松处理提交的数据或启动现有的业务工作流程。

AEM Forms Edge Delivery提供了一个表单块，以帮助您轻松创建表单以捕获和存储捕获的数据。 您可以在AEM EDS项目中包含该表单块以开始创建表单。 我们开始吧：


## 先决条件

在开始之前，请确保您已完成以下步骤：

* 使用AEM样板设置边缘交付服务(EDS) Github项目，并在本地计算机上克隆相应的Github存储库。 请参阅 [开发人员教程](https://www.aem.live/developer/tutorial) 以了解详细信息。 在本文档中，将边缘交付服务(EDS)项目的本地文件夹称为 `[EDS Project repository]` .
* 克隆 [Forms阻止存储库](https://github.com/adobe/afb) 在本地计算机上。 它包含在EDS网页上呈现表单的代码。 在本文档中，将Forms Block存储库的本地文件夹称为 `[Forms Block repository]`.
* 确保您有权访问Google工作表或Microsoft SharePoint。 要将Microsoft SharePoint设置为您的内容源，请参阅 [如何使用Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint)



## 创建表单

+++ 步骤1：将表单块添加到您的边缘交付服务(EDS)项目。

此 `Form block` 包括向EDS站点添加表单的功能。 该块未包含在使用AEM样板创建的项目中。 要在 Edge Delivery Service 中包含表单区块：

1. 导航至 `[Forms Block repository]/blocks` 文件夹并复制 `form` 文件夹。

1. 导航至 `[EDS Project repository]/blocks/` 文件夹并粘贴 `form` 文件夹。

1. 签入 `form` 文件夹和底层文件到GitHub上的边缘交付服务项目。

   该表单块将添加到GitHub上的EDS项目存储库中。 确保GitHub构建不会失败：

   * 如果遇到错误“无法解析模块&#39;../../scripts/lib-franklin.js&#39;的路径”，请打开 `[EDS Project]/blocks/forms/form.js` 文件。在导入语句中，将 `lib-franklin.js` 文件替换为 `aem.js` 文件。

   * 如果您遇到任何 linting 错误，可以忽略它们。要绕过 linting 检查，请打开 `[EDS Project]\package.json` 文件并将“lint”脚本从 `"lint": "npm run lint:js && npm run lint:css"` 更新为 `"lint": "echo 'skipping linting for now'"`。保存文件并将其提交到您的 GitHub 项目。

您现在可以创建一个表单并将其添加到您的网站。

+++

+++ 步骤2：使用Microsoft Excel或Google工作表创作表单。

您可以使用电子表格轻松创建表单，而不需要复杂的流程。您可以首先在电子表格中添加行标题和列标题，其中每行定义一个表单字段，每个列标题定义相应表单字段的属性。

例如，在以下电子表格中，行定义 `contact us` 表单的字段，而列标题则定义相应字段的属性。

![联系我们电子表格](/help/edge/assets/contact-us-form-spreadsheet.png)

要创建表单，请执行以下操作：

1. 打开 Microsoft SharePoint 或 Google Drive 上的 AEM Edge Delivery 项目文件夹。

1. 在 AEM Edge Delivery 项目目录下的任意位置创建一份 Microsoft Excel 工作簿或 Google 工作表。例如，在 Google Drive 上的 AEM Edge Delivery 项目目录中创建一个名为 `contact-us` 的电子表格。

1. 确保该表与[为您的项目配置](https://www.aem.live/docs/setup-customer-sharepoint)的 AEM 用户（例如 `helix@adobe.com`）共享，并且该用户具有该表的编辑权限。

1. 打开您创建的电子表格，并将默认工作表的名称更改为“共享默认”。

   ![将默认工作表重命名为“共享默认”](/help/edge/assets/rename-sheet-to-shared-default.png)

1. 要添加表单字段，请将行标题和列标题添加到 `shared-default` 工作表，其中每行定义一个表单字段，每个列标题定义相应表单字段的[属性](/help/edge/docs/forms/eds-form-field-properties)。

   要快速开始，您可以将[联系我们电子表格](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link)的内容复制到您的电子表格中。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览和发布工作表。

   ![使用 AEM Sidekick 预览和发布工作表](/help/edge/assets/preview-form.png)

   预览和发布时，浏览器会打开新选项卡，以 JSON 格式显示工作表的内容。请务必记下实时 URL，因为稍后渲染表单时需要它。

   URL 的格式为：

   ```JSON
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

+++

+++ 步骤3：使用边缘交付服务(EDS)页面预览表单。


到目前为止，您已经将表单块添加到EDS项目并准备了表单的结构。 现在，如果要预览表单：

1. 转到您的Microsoft SharePoint或Google Drive帐户，然后打开AEM Edge Delivery项目目录。

1. 打开doc文件以将表单嵌入其中。 例如，打开索引文件。 您还可以创建一个新的doc文件。

1. 导航到文档中要添加表单的所需位置。

1. 将名为“表单”的区块添加到文件中，类似于下面显示的区块。

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   在第二行中，包括您在前一节中记录的URL作为超链接。 将预览URL (.page URL)用于开发或测试目的，或将发布URL (.live)用于生产。

   >[!IMPORTANT]
   >
   >
   > 确保URL为超链接而不是以纯文本显示。


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览页面。页面现在会显示表单。

   例如，以下是基于[联系我们电子表格](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link)的表单：


   ![EDS Form 样本](/help/edge/assets/eds-form.png)

   现在，填写该表单并单击提交按钮，您会遇到类似于以下内容的错误，因为该电子表格尚未设置为接受数据。

   ![表单提交错误](/help/edge/assets/form-error.png)

+++


## 下一步

[准备电子表格](/help/edge/docs/forms/submit-forms.md) ，以便在提交表单后开始接受数据。



## 查看更多

* [表单字段属性](/help/edge/docs/forms/eds-form-field-properties)
* [创建并预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单，以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到 Sites 页面](/help/edge/docs/forms/publish-eds-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [改变表单主题和样式](/help/edge/docs/forms/style-theme-forms.md)
