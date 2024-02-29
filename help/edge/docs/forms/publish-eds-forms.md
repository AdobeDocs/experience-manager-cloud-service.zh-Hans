---
title: 发布 AEM Forms Edge Delivery Services 表单
description: 发布 AEM Forms Edge Delivery Services 表单
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 39bb45b285fcd938d44b9748aa8559b89a3636b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 19%

---


# 发布您的表单

准备好与客户共享表单以进行数据收集或提交后，您就可以发布该表单，使表单随时可供客户使用。

## 先决条件

* 此 [已在Github上为您的EDS项目启用表单块](/help/edge/docs/forms/create-forms.md).
* 您的表单已完全测试并可供使用。
* 您的 [电子表格已配置](/help/edge/docs/forms/submit-forms.md) 以接受数据。

## 发布您的表单

要发布表单，请执行以下操作：

1. 访问您的Microsoft SharePoint或Google Drive帐户，然后导航到 `[AEM Edge Delivery project directory]`.

1. 打开要嵌入表单的文档文件。 例如，您可以打开索引文件，或者创建新文档。

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

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览页面。页面现在显示表单。例如，以下是基于 [查询电子表格](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0)：


   [![EDS表单示例](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   现在，您的客户可以填写并提交表单。

## 疑难解答

+++ 无法将数据提交到表单

如果您遇到与以下消息类似的错误，则表示电子表格尚未配置为接受提交的数据。

![表单提交错误](/help/edge/assets/form-error.png)

+++


## 查看更多

* [创建并预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单，以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到 Sites 页面](/help/edge/docs/forms/publish-eds-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [改变表单主题和样式](/help/edge/docs/forms/style-theme-forms.md)
