---
title: 向表单添加可重复的部分
description: 在 EDS Form 中添加可重复部分
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d63d0f1152d0a23623c197924a44bc6b1e69fb42
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 8%

---


# 向表单添加可重复部分

自适应表单块提供添加表单或表单的部分或组件或使其可重复的功能。 这允许用户为同一类型的数据多次输入信息，使得收集工作经验或教育背景等信息更加容易。

例如，考虑用于收集有关人员工作体验信息的表单。 您可以有一个可重复的部分，用于捕获每个先前作业的详细信息。 可重复部分通常包含公司名称、职称、雇佣日期和工作责任等字段。 用户可以添加可重复部分的多个实例，以输入有关他们已执行的每个作业的信息。



在本文结束时，您将学习：

* [在表单中创建可重复的部分](#add-repeatable-sections-to-a-form)
* [设置表单中的最小或最大重复次数](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## 创建可重复部分

通过在表单中创建可重复的部分，用户能够输入同一数据集的多个实例，从而高效收集重复信息。 要在表单中创建可重复部分，请执行以下操作：

1. 转到Microsoft SharePoint或Google Workspace上的Edge Delivery项目文件夹，然后打开您的电子表格。

1. 使用添加表单字段 `type` 属性设置为 `fieldset`
1. 指定 `Name` 字段的。 name属性用于创建可重复部分。
1. 通过设置启用重复性 `repeatable` 到 `true`.
1. 指定描述性 `label` 用于字段。 它用作可重复部分的标题。

   请参阅下图，了解职位申请表中雇用历史记录部分的说明。

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. 对于要包含在部分中的每个字段，设置其 `Fieldset` 属性的名称与您在步骤3中选择的名称相同。

   例如，指定 `experience` 字段集的属性中列出的所有字段，这些字段将 `employment history` 部分。

   ![可重复部分字段及其属性的示例](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以预览和发布工作表。 可重复部分将添加到表单中。

   在“可重复”部分下方，用户会发现 **添加** 按钮，便于添加多个部分。

   ![可重复部分，添加按钮，可添加多个部分 ](/help/edge/assets/repeatable-section-example.png)


## 设置最小和最大重复

在窗体设计中，为可重复部分设置最小和最大重复次数是有利的。 这样，您就可以建立控制和一致性，同时有效地指导用户。 要设置最小或最大重复次数，请执行以下操作：

1. 转到Microsoft SharePoint或Google Workspace上的Edge Delivery项目文件夹，然后打开您的电子表格。

1. 对于 `type` `fieldset` 和 `repeatable` 属性设置为 `true`：

   * 设置 `min` 属性，指定可重复部分的最小次数。

   * 设置 `max` 属性，指定可重复部分的最大次数。

   ![设置min和max属性以指定可重复分段的次数](/help/edge/assets/repeatable-section-set-min-max.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览和发布工作表。

   添加可重复部分时，用户会发现 **删除** 图标，可更轻松地删除重复部分。 添加后，这些部分将无法减少到比指定的更少的实例。 `min` 属性。 这可确保遵守为表单完成设置的最低要求。

<!--

For example, consider a form used to collect information from users applying for a loan. . You may have a repeatable section for capturing details of each co-applicant. The repeatable section would typically contain fields such as co-co-applicant

The form allows users to provide personal information, including details of the co-applicants. Users can enter details for co-applicants, with this section being repeatable.

![Repeatable sections in forms](/help/forms/assets/eds-repeatable.png)

## Prerequisites

The [Adaptive Form block is enabled](/help/edge/docs/forms/create-forms.md) for your Edge Delivery Service project. 

## Add a repeatable section to a form 

Let's take an example of a loan application form. The form enables users to submit personal information. You can include co-applicant details using repeatable sections, with the option to add a minimum and maximum of three co-applicant sections.

"_You can use a Microsoft Excel file on your SharePoint Site or Google Sheet file on Google Drive to develop a form. Examples in this document are based on a [Microsoft Excel file on your SharePoint Site](https://www.aem.live/docs/setup-customer-sharepoint)._" 


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


## 查看更多

* [创建并预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单，以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到 Sites 页面](/help/edge/docs/forms/publish-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [改变表单主题和样式](/help/edge/docs/forms/style-theme-forms.md)
* [表单组件及其属性](/help/edge/docs/forms/form-components.md)