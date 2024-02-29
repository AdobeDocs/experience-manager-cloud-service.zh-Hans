---
title: AEM Forms Edge Delivery Service快速入门。 创建表单。
description: 快速制作完美的表单！⚡ AEM Forms Edge Delivery 基于文档的创作 = 速度极快、SEO 友好的表单，让用户更加满意，搜索引擎更加优异。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 39bb45b285fcd938d44b9748aa8559b89a3636b2
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 17%

---


# 为Edge Delivery Service (EDS)站点创建表单

在当今的数字时代，创建用户友好的表单对于任何组织都至关重要。AEM Forms Edge Delivery 允许您使用 Word 或 Google Docs 等熟悉的工具创建表单。

这些表单可将数据直接提交到 Microsoft Excel 或 Google Sheets 文件，使您能够使用 Google Sheets、Microsoft Excel 和 Microsoft Sharepoint 充满活力的生态系统和强大的 API 来轻松处理提交的数据或启动现有的业务工作流程。

AEM Forms Edge Delivery提供了一个表单块，以帮助您轻松创建表单以捕获和存储捕获的数据。 您可以在AEM EDS项目中包含该表单块以开始创建表单。 我们开始吧：


## 先决条件

在开始之前，请确保您已完成以下步骤：

* 使用AEM样板设置边缘交付服务(EDS) GitHub项目，并在本地计算机上克隆相应的GitHub存储库。 请参阅 [开发人员教程](https://www.aem.live/developer/tutorial) 以了解详细信息。 在本文档中，将边缘交付服务(EDS)项目的本地文件夹称为 `[EDS Project repository]` .
* 克隆 [Forms阻止存储库](https://github.com/adobe/afb) 在本地计算机上。 它包含在EDS网页上呈现表单的代码。 在本文档中，将Forms Block存储库的本地文件夹称为 `[Forms Block repository]`.
* 确保您有权访问Google工作表或Microsoft SharePoint。 要将Microsoft SharePoint设置为您的内容源，请参阅 [如何使用Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint)



## 创建表单

+++ 步骤1：将表单块添加到您的边缘交付服务(EDS)项目。

使用“表单”块，用户可以为Edge Delivery Service站点创建表单。 但是，此块未包含在默认的AEM样板中（用于创建Edge Delivery Service项目）。 要将表单块无缝集成到您的边缘交付服务项目中，请执行以下操作：

1. **找到表单块存储库：** 访问 [Forms阻止存储库]/blocks文件夹并复制 `form` 文件夹。
1. **将表单块粘贴到EDS项目中：**
导航至 [EDS项目存储库]/blocks/文件夹并粘贴表单文件夹。
1. **将更改提交到GitHub：** 将表单文件夹及其基础文件签入到GitHub上的边缘交付服务项目。

完成这些步骤后，表单块已成功集成到GitHub上的边缘交付服务(EDS)项目存储库中。


**GitHub内部版本问题疑难解答**

通过解决以下潜在问题，确保顺利构建GitHub：

* **解决模块路径错误：**
如果您遇到错误“无法解析模块“&#39;../../scripts/lib-franklin.js&#39;”的路径，请导航至 [EDS项目]/blocks/forms/form.js文件。 将lib-franklin.js文件替换为aem.js文件以更新import语句。

* **处理Linting错误：**
如果您遇到任何绒毛错误，则可以绕过它们。 打开 [EDS项目]/package.json文件并将“lint”脚本从“lint”：“npm run lint：js &amp;&amp; npm run lint：css”修改为“lint”：“echo &#39;skipping linting for now&#39;”。 保存文件并将更改提交到GitHub项目。



+++

+++ 步骤2：使用Microsoft Excel或Google工作表创作表单。

使用电子表格可以轻松实现制作表单，而不是在复杂的流程中导航。 首先，您可以将行和列标题添加到电子表格中，其中每一行表示一个表单字段，而每个列标题定义对应字段的属性。

例如，请考虑以下电子表格，其中行概述了以下项的字段： `enquiry` 表单和列标题定义其属性：

![查询电子表格](/help/edge/assets/enquiry-form-spreadsheet.png)

要继续创建表单，请执行以下操作：

1. 访问Microsoft SharePoint或Google Drive上的AEM Edge Delivery项目文件夹。

1. 在AEM Edge Delivery项目目录中的任何位置创建Microsoft Excel工作簿或Google工作表。 例如，在 Google Drive 上的 AEM Edge Delivery 项目目录中创建一个名为 `enquiry` 的电子表格。

1. 确保与相应的AEM用户共享工作表(例如 `helix@adobe.com`) [根据为项目指定的配置](https://www.aem.live/docs/setup-customer-sharepoint). 授予用户对工作表的编辑权限。

1. 打开创建的电子表格，并将默认工作表重命名为“shared-default”。

   ![将默认工作表重命名为“共享默认”](/help/edge/assets/rename-sheet-to-shared-default.png)

1. 要添加表单字段，请将行和列标题插入“shared-default”工作表。 每一行应表示 [表单字段](/help/edge/docs/forms/form-components.md)，列标题定义相应的字段 [属性](/help/edge/docs/forms/eds-form-field-properties).

   为了SWIFT起步，请考虑复制 [查询电子表格](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0) 到电子表格中。 复制内容后，保存电子表格。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以预览工作表。

   ![使用AEM Sidekick预览工作表](/help/edge/assets/preview-form.png)

   预览和发布后，新的浏览器选项卡将以JSON格式显示工作表的内容。 确保捕获预览URL，因为这是在下一部分呈现表单所必需的。 URL格式如下所示：


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` 是指GitHub存储库的分支。
   * `<repository>` 表示您的GitHub存储库。
   * `<owner>` 指托管GitHub存储库的GitHub帐户的用户名。

   例如，如果项目的存储库名为“portal”，它位于帐户“wkandforms”下，而您使用的是“main”分支，则URL如下所示：

   `https://main--portal--wkndforms.hlx.page/enquiry.json`


+++

+++ 步骤3：使用边缘交付服务(EDS)页面预览表单。


到目前为止，您已经将表单块添加到EDS项目并准备了表单的结构。 现在，如果要预览表单：

1. **访问项目目录：** 打开您的Microsoft SharePoint或Google Drive帐户，然后导航到您的AEM Edge Delivery项目目录。

1. **将表单嵌入文档：** 打开文档文件（例如，索引文件）以嵌入表单。 或者，也可以创建新文档。

1. **导航到所需的位置：** 在文档中移动到要添加表单的所需位置。

1. **添加表单块：** 在文件中插入名为“Form”的块，如下所示：

   | 表单 |
   |---|
   | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   此块用作嵌入表单的占位符。 在块的第二行中，添加预览URL `<form>.json` 文件作为超链接。

   >[!IMPORTANT]
   >
   >
   > 确保URL的格式为超链接，而不是显示为纯文本。


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以预览文档。 页面现在显示表单。例如，以下是基于 [查询电子表格](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0)：


   [![EDS表单示例](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   现在，填写该表单并单击提交按钮，您会遇到类似于以下内容的错误，因为该电子表格尚未设置为接受数据。

   ![表单提交错误](/help/edge/assets/form-error.png)

+++


## 下一步

[准备电子表格](/help/edge/docs/forms/submit-forms.md) ，以便在提交表单后开始接受数据。



## 查看更多

* [表单组件](/help/edge/docs/forms/form-components.md)
* [表单字段属性](/help/edge/docs/forms/eds-form-field-properties)
* [创建并预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单，以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到 Sites 页面](/help/edge/docs/forms/publish-eds-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [改变表单主题和样式](/help/edge/docs/forms/style-theme-forms.md)
