---
title: 发布适用于 AEM Forms 的 Edge Delivery Services
description: 发布适用于 AEM Forms 的 Edge Delivery Services
feature: Edge Delivery Services
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '585'
ht-degree: 100%

---

# 发布您的表单并开始收集数据

您准备好与客户共享表单以进行数据收集或提交后，您只需将其发布，表单即可供客户随时使用。

![基于文档的创作生态系统](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## 先决条件

- 您有一个基于 [AEM Forms 模板的 AEM 项目](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)或[在现有的 AEM 项目中添加了 Adaptive Forms Block](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)
- 您的表单已经过全面测试，随时可以使用。
- 您的[电子表格已配置](/help/edge/docs/forms/submit-forms.md)，可接受数据。


## 发布表单

+++ &#x200B;1. 发布电子表格

1. 打开您的 Microsoft SharePoint 或 Google Drive 帐户，并导航至 AEM Edge Delivery 项目目录。

1. 打开包含您表单的电子表格。例如，[“enquiry”](/help/edge/assets/enquiry.xlsx) 表单 Microsoft Excel 工作簿。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览表。

   ![使用 AEM Sidekick 预览表](/help/edge/assets/preview-form.png)

   成功完成预览操作后，电子表格内容将转换为 JSON 格式。然后，预览页面以结构化表格格式呈现该内容。例如，附图说明了 “enquiry” 表单的内容。

   ![表单预览 JSON 格式](/help/edge/assets/forms-preview-json-format.png)

1. 使用 AEM Sidekick 发布表。确保捕获发布 URL，因为这是在下一节中渲染表单所必需的。URL 格式如下所示：


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form>.json
   ```

   - `<branch>` 指 GitHub 存储库的分支。
   - `<repository>` 表示您的 GitHub 存储库。
   - `<owner>` 指托管您 GitHub 存储库的 GitHub 帐户用户名。

   例如，如果您的项目存储库名为 “wefinance” 且位于帐户 “wkndform” 下，并且您使用的是 “main” 分支和 “enquiry” 表单，则 URL 如下所示：

   `https://main--wefinance--wkndform.aem.live/enquiry.json`
&lt;!--(https://main--wefinance--wkndform.aem.live/enquiry.json)-->

+++

+++ &#x200B;2. 将表单添加到您的网页

将 `<form>.json` 添加到网页方便客户互动，让表单填写者能够轻松填写并提交表单。


要将表单添加到您的网页：

1. 访问您的 Microsoft SharePoint 或 Google Drive 帐户并导航至您的`[AEM Edge Delivery project directory]`。

1. 打开要嵌入表单的文档文件。例如，您可以打开 [enquiry-form.docx](/help/edge/assets/enquiry-form.docx) 文件，或者创建一个新文档。

1. 在文档中确定要插入表单的部分，并相应地导航到该部分。

1. 将名为“表单”的区块添加到文件中。例如，如果您的项目存储库名为 “wefinance” 且位于帐户所有者 “wkndform” 下，并且您使用的是 “main” 分支。

   | 表单 |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |

   ![将名为“表单”的区块添加到文件中](/help/edge/assets/enquiry-doc-to-embed-form.png)

   该区块用作嵌入表单的占位符。在该区块的第二行中，添加 `<form>.json` 文件的 URL 作为超链接。

   >[!IMPORTANT]
   >
   >
   > 确保 URL 的格式为超链接，而不是显示为纯文本。

   使用预览 URL (.page URL) 进行开发或测试，或使用发布 URL (.live) 进行生产。

   例如，如果您的项目存储库名为 “wefinance” 且位于帐户所有者 “wkndform” 下，并且您使用的是 “main” 分支。

   以下是带有预览和发布 URL 的示例：

   **预览 URL**

   | 表单 |
   |---|
   | `https://main--wefinance--wkndform.aem.page/enquiry.json` |


   **发布 URL**

   | 表单 |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览网页。页面现在显示表单。例如，以下是基于 [“enquiry” 电子表格](/help/edge/assets/enquiry-form.docx)的表单：


   ![EDS 表单样本](/help/edge/assets/updated-form.png)

1. 使用 AEM Sidekick 发布表单。现在，您的客户可以填写表单并提交。

+++

## 疑难解答

+++ 无法向表单提交数据

如果您遇到类似于以下错误消息，则表明电子表格尚未配置为[接受提交的](/help/edge/docs/forms/submit-forms.md)数据。

![表单提交错误](/help/edge/assets/form-error.png)

+++



