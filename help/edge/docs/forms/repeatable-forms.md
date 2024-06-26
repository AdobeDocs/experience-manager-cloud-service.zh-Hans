---
title: 将可重复部分添加到表单
description: 在 EDS Form 中添加可重复部分
feature: Edge Delivery Services
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: ht
source-wordcount: '533'
ht-degree: 100%

---

# 将可重复部分添加到表单

Adaptive Forms Block 提供了添加或使表单的部分或组件可重复的功能。该功能允许用户针对同一类型的数据多次输入信息，从而更方便地收集工作经验或教育背景等信息。

例如，请看一个用于收集个人工作经验信息的表单。您可以设置一个可重复的分区，用于记录以前每份工作的详细信息。可重复分区通常包含公司名称、职位、就业日期和工作职责等字段。用户可以在可重复分区中添加多个实例，以输入有关他们所做过的每项工作的信息。

读完本文后，您将学会：

* [在表单中创建可重复分区](#add-repeatable-sections-to-a-form)
* [设置表单中的最小或最大重复次数](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## 创建可重复分区

在表单中创建可重复分区，使用户能够输入同一组数据的多个实例，从而有效收集重复信息。要在表单中创建可重复分区：

1. 转到 Microsoft SharePoint 或 Google Workspace 上的 Edge Deliver 项目文件夹并打开电子表格。

1. 添加一个表单字段，并将 `type` 属性设置为 `fieldset`
1. 指定字段的 `Name`。名称属性用于创建可重复分区。
1. 通过将 `repeatable` 设置为 `true`，启用可重复性。
1. 为字段指定描述性 `label`，用作可重复分区的标题。

   请参阅下图，了解工作申请表单中工作经历部分的说明。

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. 对于要包含在该分区中的每个字段，将其 `Fieldset` 属性设置为您在步骤 3 中选择的相同名称。

   例如，在要包含在 `employment history` 分区中的所有相关字段的“字段集”属性中指定 `experience`。

   ![可重复分区字段及其属性的示例](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览和发布工作表。将可重复分区添加到表单中。

   在可重复分区下方，用户可以找到直观的“**添加**”按钮，方便轻松添加多个分区。

   ![可重复分区，“添加”按钮，用于添加多个部分 ](/help/edge/assets/repeatable-section-example.png)


## 设置最小和最大重复次数

在表单设计中，为可重复分区设置最小和最大重复次数很有益处。这样，您就可以在有效指导用户的同时建立控制和一致性。要设置最小或最大重复次数：

1. 转到 Microsoft SharePoint 或 Google Workspace 上的 Edge Deliver 项目文件夹并打开电子表格。

1. 对于具有 `type` `fieldset` 和 `repeatable` 属性的字段设置为 `true`：

   * 设置 `min` 属性来指定该部分可以重复的最小次数。

   * 设置 `max` 属性来指定该部分可以重复的最大次数。

   ![设置 min 和 max 属性来指定该部分可以重复的次数](/help/edge/assets/repeatable-section-set-min-max.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览和发布工作表。

   添加可重复分区时，用户会看到直观的“**删除**”图标，可以更轻松地删除可重复分区。添加后，这些分区的实例数就不得少于 `min` 属性指定的实例数。这样可以确保遵守表单填写的最低要求。

<!--

For example, consider a form used to collect information from users applying for a loan. . You may have a repeatable section for capturing details of each co-applicant. The repeatable section would typically contain fields such as co-co-applicant

The form allows users to provide personal information, including details of the co-applicants. Users can enter details for co-applicants, with this section being repeatable.

![Repeatable sections in forms](/help/forms/assets/eds-repeatable.png)

## Prerequisites

The [Adaptive Forms Block is enabled](/help/edge/docs/forms/create-forms.md) for your Edge Delivery Services project. 

## Add a repeatable section to a form 

Let's take an example of a loan application form. The form enables users to submit personal information. You can include co-applicant details using repeatable sections, with the option to add a minimum and maximum of three co-applicant sections.

"_You can use a Microsoft Excel file on your SharePoint Site or Google Sheet file on Google Drive to develop a form. Examples in this document are based on a [Microsoft Excel file on your SharePoint Site](https://www.aem.live/docs/setup-customer-SharePoint)._" 


To add repeatable sections in Edge Delivery:

1. [Author a form using Microsoft Excel](#author-form)
2. [Preview and publish the form](#preview-form)

### Author a form using Microsoft Excel {#author-form}

1. Go to your Edge Deliver project folder on Microsoft SharePoint or Google Workspace and open your spreadsheet. For example, open an a spreadsheet named `loan-application.xlsx`.

1. Add a new columns labeled `Repeatable` to the sheet contaning your form fields. By default, the `shared-default` sheet contains the form fields.  

1. Add new columns labeled as `Repeatable`, `Min`, and `Max` in your Microsoft Excel file.
1. Specify the value for the `Repeatable` column as `True` for the fieldset that you want to make repeatable.
1. Specify the values for the `Min` and `Max` columns. The `Min` value represents the minimum number of occurrences for which the panel repeats, while the `Max` value represents the maximum number of occurrences for which the panel repeats.
1. Save your Microsoft Excel file.
     
>[!NOTE]
>
> Here is the [Loan application](/help/forms/assets/loan-application.xlsx) excel sheet for your reference. 

### Preview/Publish the form using your Edge Delivery Service

1. Open or create new document file in a Microsft SharePoint Site to embed the Excel sheet  in it using a `Form Block`. For example, open the `index` file and add a `Form Block`.
2. Open the command prompt, navigate to your AEM Edge Delivery project directory on your local machine, and execute the command as `aem up`.

The form is accessible at `https://localhost:3000`, where clicking the `Add` button adds new repeatable section for entering co-applicant details. You can also delete the the repeatable section by clicking the `Delete` button. 

>[!NOTE]
>
> If you encounter a "Page Not Found" error while accessing your form at localhost, add the directory name of the Microsoft SharePoint Site in front of the URL where your form is located. For example, `http://localhost:3000/<dir-name>/`

-->


## 另请参阅

{{see-more-forms-eds}}
