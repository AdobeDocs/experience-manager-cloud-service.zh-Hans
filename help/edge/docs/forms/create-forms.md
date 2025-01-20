---
title: 适用于 AEM Forms 的 Edge Delivery Services 快速入门。创建表单。
description: 快速制作完美的表单！⚡ AEM Forms Edge Delivery 基于文档的创作 = 速度极快、SEO 友好的表单，让用户更加满意，搜索引擎更加优异。
feature: Edge Delivery Services
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
role: Admin, Architect, Developer
source-git-commit: 4dcc580a6e3b49b1839fbb0f101c172bddf5cfcc
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 88%

---

# 使用 Adaptive Forms Block 创建表单

>[!VIDEO](https://video.tv.adobe.com/v/3427881?quality=12&learn=on)

AEM Forms Edge Delivery 提供了一个称为 Adaptive Forms Block 的区块，可帮助您轻松创建表单，以捕获和存储捕获的数据。您可以[创建一个预先配置了 Adaptive Forms Block 的新 AEM 项目](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)或[将 Adaptive Forms Block 添加到现有的 AEM 项目](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)。

这些表单可将数据直接提交到 Microsoft Excel 或 Google Sheets 文件，使您能够使用 Google Sheets、Microsoft Excel 和 Microsoft SharePoint 充满活力的生态系统和强大的 API 来轻松处理提交的数据或启动现有的业务工作流程。

![基于文档的创作生态系统](/help/edge/assets/document-based-authoring-workflow-create-form.png)


## 先决条件

在开始之前，请确保您已完成以下步骤：

* 使用AEM Forms样板设置[AEM项目](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) [已将自适应Forms块添加到您现有的AEM项目](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)，并在本地计算机上克隆相应的GitHub存储库。
<!--In this document, the local folder of your Edge Delivery Services (EDS) project is referred as `[EDS Project repository]`.  -->
* 确保您有权访问 Google Sheets 或 Microsoft SharePoint。要将 Microsoft SharePoint 设置为您的内容源，请参阅[如何使用 SharePoint](https://www.aem.live/docs/setup-customer-sharepoint)



## 创建表单

<!--
+++ Step 1: Add the Adaptive Forms Block to your Edge Delivery Services (EDS) project.

The Adaptive  empowers users to create forms for an Edge Delivery Service Site. However, this block isn't included in the default AEM boilerplate (used to create an Edge Delivery Services project). To seamlessly integrate the Adaptive Forms Block into your Edge Delivery Services project:

1. **Clone the Adaptive Forms Block repository**: Clone the [Adaptive Forms Block repository](https://github.com/adobe-rnd/form-block) on your local machine. It contains the code to render the form on an EDS webpage. In this document, the local folder of your Forms Block repository is referred as `[Adaptive Forms Block repository]`.
2. **Locate the Adaptive Forms Block Repository:** Access the [Adaptive Forms Block repository]/blocks/src folder and copy its content. 

3. on your local machine and copy the `form` folder. 
4. **Paste the Adaptive Forms Block's code into your EDS Project:**
Navigate to the [EDS Project repository]/blocks/ folder on your local machine and create a 'form' folder. Paste the `[Adaptive Forms Block repository]/blocks/src content`, copied in perevious step to the `[EDS Project repository]/blocks/form` folder.
1. **Commit Changes to GitHub:** Check in the `[EDS Project repository]/blocks/form` folder and its underlying files to your Edge Delivery Services project on GitHub.

After completing these steps, the Adaptive Forms Block is successfully added to your Edge Delivery Services (EDS) project repository on GitHub. You can now create and add forms to a EDS Sites page.
 

**Troubleshooting GitHub build issues**

Ensure a smooth GitHub build process by addressing potential issues:

* **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file.

* **Handle Linting Errors:**
    Should you come across any linting errors, you can bypass them. Open the [EDS Project]/package.json file and modify the "lint" script from "lint": "npm run lint:js && npm run lint:css" to "lint": "echo 'skipping linting for now'". Save the file and commit the changes to your GitHub project. -->

+++

+++ 步骤 1：使用 Microsoft Excel 或 Google Sheet 创建表单。

使用电子表格可以轻松地制作表单，而无需执行复杂的流程。您可以定义构成表单结构的行和列。每行代表一个单独的[表单字段](/help/edge/docs/forms/form-components.md#available-components)，列标题定义相应的[字段属性](/help/edge/docs/forms/form-components.md#components-properties)。

例如，请考虑以下电子表格，其中行[查询](/help/edge/assets/enquiry.xlsx)的电子表格和列标题的轮廓字段定义了其属性：

![查询电子表格](/help/edge/assets/enquiry-form-spreadsheet.png)

要继续创建表单：

1. 访问 Microsoft SharePoint 或 Google Drive 上的 AEM Edge Delivery 项目文件夹。

1. 在 AEM Edge Delivery 项目目录中的任意位置创建一份 Microsoft Excel 工作簿或 Google 工作表。例如，在 Google Drive 上的 AEM Edge Delivery 项目目录中创建一个名为 `enquiry` 的电子表格。

   ![Google Drive 上的示例内容](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

1. 确保根据为项目指定的配置，与适当的 AEM 用户（例如 `forms@adobe.com`）[共享表](https://www.aem.live/docs/setup-customer-sharepoint)。授予用户编辑表的权限。

1. 打开创建的电子表格并将默认表重命名为“shared-default”。

   ![将默认工作表重命名为“shared-default”](/help/edge/assets/rename-sheet-to-shared-default.png)

1. 要添加表单字段，请将行和列标题插入“shared-default”表中。每行应该代表一个[表单字段](/help/edge/docs/forms/form-components.md#available-components)，列标题定义相应的字段[属性](/help/edge/docs/forms/form-components.md#components-properties)。


   为了快速开始，请考虑复制[查询电子表格](/help/edge/assets/enquiry.xlsx)中的内容到电子表格中。复制内容后，保存电子表格。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览表。

   ![使用 AEM Sidekick 预览表](/help/edge/assets/preview-form.png)

   预览时，新的浏览器选项卡会以 JSON 格式显示工作表的内容。确保捕获预览 URL，因为这是在下一节中渲染表单所必需的。URL 格式如下所示：


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form-path>/<form-file-name>.json
   ```

   * `<branch>` 指 GitHub 存储库的分支。
   * `<repository>` 表示您的 GitHub 存储库。
   * `<owner>` 指托管您 GitHub 存储库的 GitHub 帐户用户名。

   例如，如果项目的存储库名为“wefinance”，它位于帐户“wkndform”下，而您使用的是“main”分支，则URL如下所示：

   [https://main--wefinance--wkndform.aem.page/enquiry.json](https://main--wefinance--wkndform.aem.page/enquiry.json)


+++

+++ 步骤 2：使用 Edge Delivery Services (EDS) 页面预览表单。


到目前为止，您已经准备好了表单的结构。现在，要预览表单，请执行以下操作：

1. 打开您的 Microsoft SharePoint 或 Google Drive 帐户，并导航至 AEM Edge Delivery 项目目录。



1. 打开文档文件（例如索引文件）以嵌入表单。或者，您可以[创建新文档](/help/edge/assets/enquiry-form.docx)。

1. 移至文档中要添加表单的所需位置。

1. 创建表单区块来呈现表单。选择“插入”>“表格”，然后创建一个一列两行的表格。将表命名为“表单”并将预览 URL 粘贴到第二行中。确保 URL 的格式为超链接，而不是纯文本，如下所示：

   | 表单 |
   |---|
   | [https://main--wefinance--wkndform.aem.live/enquiry.json](https://main--wefinance--wkndform.aem.page/enquiry.json) |


   ![将 Adaptive Forms Block 添加到您的网页](/help/edge/assets/enquiry-doc-to-embed-form.png)

   该区块用作嵌入表单的占位符。在该区块的第二行中，添加 `<form>.json` 文件的预览 URL 作为超链接。

   >[!IMPORTANT]
   >
   >
   > 确保 URL 的格式为超链接，而不是显示为纯文本。


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览文档。页面现在显示表单。例如，以下是基于[查询电子表格](/help/edge/assets/enquiry-form.docx)的表单：


   [![EDS 表单样本](/help/edge/assets/updated-form.png)](https://main--wefinance--wkndform.aem.page/enquiry-form)

   现在，填写该表单并单击提交按钮，您会遇到类似于以下内容的错误，因为该电子表格尚未设置为接受数据。

   ![表单提交错误](/help/edge/assets/form-error.png)

+++


## 下一步

[准备您的电子表格](/help/edge/docs/forms/submit-forms.md)以在表单提交后开始接受数据。


## 另请参阅

{{see-more-forms-eds}}
