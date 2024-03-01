---
title: 发布 AEM Forms Edge Delivery Services 表单
description: 发布 AEM Forms Edge Delivery Services 表单
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 10%

---


# 发布您的表单

准备好与客户共享表单以进行数据收集或提交后，您就可以发布该表单，使表单随时可供客户使用。

## 先决条件

* 此 [已在GitHub上为您的EDS项目启用自适应表单块](/help/edge/docs/forms/create-forms.md).
* 您的表单已完全测试并可供使用。
* 您的 [电子表格已配置](/help/edge/docs/forms/submit-forms.md) 以接受数据。

## 发布您的表单

+++ 1.发布电子表格

1. 打开您的Microsoft SharePoint或Google Drive帐户，然后导航到您的AEM Edge Delivery项目目录。

1. 打开具有您的表单的电子表格。 例如， `enquiry` 表单Microsoft Excel工作簿。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以预览工作表。

   ![使用AEM Sidekick预览工作表](/help/edge/assets/preview-form.png)

   成功完成预览操作后，电子表格内容将转换为JSON格式。 然后，预览页面会以结构化表格式显示此内容。 例如，随附的图像说明了“查询”表单的内容。

   ![Forms预览JSON格式](/help/edge/assets/forms-preview-json-format.png)

1. 使用AEM Sidekick发布工作表。 确保捕获发布URL，因为这是在下一部分呈现表单所必需的。 URL格式如下所示：


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` 是指GitHub存储库的分支。
   * `<repository>` 表示您的GitHub存储库。
   * `<owner>` 指托管GitHub存储库的GitHub帐户的用户名。

   例如，如果项目的存储库名为“portal”，它位于帐户“wkandforms”下，而您使用的是“main”分支，则URL如下所示：

   `https://main--portal--wkndforms.hlx.page/enquiry.json`

+++

+++ 2.将表单添加到您的网页

添加 `<form>.json` 以方便客户交互，使表单填写者能够轻松填写和提交表单。


要将表单添加到网页，请执行以下操作：

1. 访问您的Microsoft SharePoint或Google Drive帐户，然后导航到 `[AEM Edge Delivery project directory]`.

1. 打开要嵌入表单的文档文件。 例如，您可以打开 `index.docx` 文件，或者创建新文档。

1. 确定文档中要插入表单的所需部分，并相应地导航到该部分。

1. 将名为“Form”的块添加到该文件中，类似于以下提供的示例：

   | 表单 |
   |---|
   | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   此块用作嵌入表单的占位符。 在块的第二行中，添加的URL `<form>.json` 文件作为超链接。

   >[!IMPORTANT]
   >
   >
   > 确保URL的格式为超链接，而不是显示为纯文本。

   将预览URL (.page URL)用于开发或测试目的，或将发布URL (.live)用于生产。 以下是预览和发布URL的示例：

   **预览URL**
| 表单 | |—| | [https://main--portal--wkndforms.hlx.page/enquiry.json](https://main--portal--wkndforms.hlx.page/enquiry.json)  |


   **发布URL**
| 表单 | |—| | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json)  |

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以预览网页。 页面现在显示表单。例如，以下是基于 [查询电子表格](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0)：


   [![EDS表单示例](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

1. 使用AEM Sidekick发布表单。 现在，您的客户可以填写并提交表单。

+++

## 疑难解答

+++ 无法将数据提交到表单

如果遇到与以下消息类似的错误，则表示电子表格未配置为 [接受提交的](/help/edge/docs/forms/submit-forms.md) 尚未生成数据。

![表单提交错误](/help/edge/assets/form-error.png)

+++


## 查看更多

* [创建并预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单，以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到 Sites 页面](/help/edge/docs/forms/publish-eds-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [改变表单主题和样式](/help/edge/docs/forms/style-theme-forms.md)
