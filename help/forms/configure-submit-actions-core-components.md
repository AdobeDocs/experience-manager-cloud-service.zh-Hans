---
title: 如何为自适应表单配置提交操作？
description: 自适应表单提供了多个提交操作。提交操作定义了提交后处理自适应表单的方式。您可以使用内置的提交操作或创建自己的提交操作
keywords: 如何为自适应表单选择提交操作、将自适应表单连接到sharepoint列表、将自适应表单连接到sharepoint文档库、将自适应表单连接到表单数据模型(FDM)
feature: Adaptive Forms, Core Components
exl-id: 495948e8-30a7-4e7c-952f-c71de15520f0
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 41%

---


# 基于核心组件的自适应Forms中支持的提交操作

<span class="preview"> Adobe 建议使用核心组件[将自适应表单添加到 AEM Sites 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)或[创建独立的自适应表单](/help/forms/creating-adaptive-form-core-components.md)。</span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html?lang=zh-Hans) |
| AEM as a Cloud Service（基础组件） | [单击此处](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service（核心组件） | 本文 |
| AEM as a Cloud Service (Edge Delivery Services) | [单击此处](/help/forms/configure-submit-action-eds-forms.md) |

提交操作让您选择通过自适应表单捕获的数据的目标。当用户单击自适应表单上的&#x200B;**[!UICONTROL 提交]**&#x200B;按钮时，将触发此操作。基于核心组件的自适应Forms支持各种[现成的提交操作](#submit-actions-supported-by-adaptive-forms-based-on-core-components)。

<!--You can also configure different actions for an Adaptive Form submissions.

* **Redirect URL/Path** - This option allows user to configure a page for each form, to which the form users are redirected after submitting an Adaptive Form. 
* **Show Message** - This option allows users to add a message that is displayed when the Adaptive Form is successfully submitted. The predefined text is included in the dialog box and it can be modified by the user. -->

## 提交基于核心组件的Forms操作

基于核心组件的自适应Forms支持以下提交操作：

* [发送电子邮件](/help/forms/configure-submit-action-send-email.md)
* [调用 Power Automate 流](/help/forms/forms-microsoft-power-automate-integration.md)
* [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [调用Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [使用表单数据模型（FDM）提交](/help/forms/using-form-data-model.md)
* [提交到 Azure Blob 存储](/help/forms/configure-submit-action-azure-blob-storage.md)
* [提交到 REST 端点](/help/forms/configure-submit-action-restpoint.md)
* [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [调用 AEM 工作流](/help/forms/configure-submit-action-workflow.md)
* [提交到Marketo启用](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [提交到Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)

您还可以将基于核心组件的自适应表单提交到其他存储配置：

* [将自适应表单连接到 Salesforce 应用程序](/help/forms/aem-forms-salesforce-integration.md)
* [将自适应表单连接到 Microsoft](/help/forms/ms-dynamics-odata-configuration.md)

此外，您可以[自定义默认的提交操作](/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md)以符合特定的组织要求。


### 根据核心组件配置自适应表单的提交操作

<!--To define a Submit action for an Adaptive Form, use the Configure Dialog of an **Adaptive Form Container** component. The configure dialog of a **Adaptive Form Container** component includes:

* Basic Tab
* Form Data Model Tab
* Submission Tab
  ![AEM Forms Submit action](/help/forms/assets/aem-forms-submit-action.png)
  -->

您可以使用“配置”对话框的“提交”选项卡定义表单容器属性。 若要了解有关表单容器组件的“配置”对话框的详细信息，请[单击此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html?lang=zh-Hans)。

![单击扳手图标以打开“自适应表单容器”对话框来配置提交操作](/help/forms/assets/adaptive-forms-submit-message.png)

<!--To select and configure a Submit Action for your form:

1. Open the Content browser, and select the **[!UICONTROL Guide Container]** component of your Adaptive Form. 
1. Click the Guide Container properties ![Guide properties](/help/forms/assets/configure-icon.svg) icon. The Adaptive Form Container dialog box opens. 

1. Click the  **[!UICONTROL Submission]** tab. 

    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure a submit action](/help/forms/assets/adaptive-forms-submit-message.png)

1. Select and configure a **[!UICONTROL Submit action]**, based on your requirements. -->

<!--
## Send Email {#send-email}

To send an email to one or more recipients upon successful submission of the form, you can use the **[!UICONTROL Send Email]** Submit Action. 

Refer to [configure the send email submit action for an Adaptive Form](/help/forms/configure-submit-action-send-email.md) to learn how to set up an Adaptive Form to send an email upon successful submission.
>[!NOTE]
>
>Send PDF via Email Submit Action is applicable only to Adaptive Forms that use XFA template as form model. 

>[!NOTE]
>
>Ensure that the [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>exists. The directory is required to temporarily store attachments. If the directory does not exist, create it.


>[!CAUTION]
>
>If you  [prefill](prepopulate-adaptive-form-fields.md) a form template,  a Form Data Model (FDM) or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema , form template, or form data model (FDM)) that is data does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost. 

>[!CAUTION]
>
>If you [prefill](prepopulate-adaptive-form-fields.md) a form template, a Form Data Model (FDM) or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema, or form data model(FDM)) that does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost.

## Submit to Microsoft&reg; SharePoint {#submit-to-sharedrive}

The **[!UICONTROL Submit to SharePoint]** Submit Action connects an Adaptive Form with a Microsoft&reg; SharePoint Storage. You can submit the form data files, attachments, or Document of Record to the connected Microsoft&reg; Sharepoint Storage. 

Integration of AEM Adaptive Form with Microsoft&reg; SharePoint enables the submission, retrieval, or storage of data, files, and other relevant information within the SharePoint storage. To learn how to configure submit to SharePoint submit action for an Adaptive Form, [click here](/help/forms/configure-submit-action-sharepoint.md). 

## Submit using Form Data Model (FDM) {#submit-using-form-data-model}

The **[!UICONTROL Submit using Form Data Model (FDM)]** Submit Action writes submitted Adaptive Form data for the specified data model object in a Form Data Model (FDM) to its data source. When configuring the Submit Action, you can choose a data model object whose submitted data you want to write back to its data source.

When a user submits a form based on a form data model (FDM), you can [configure the form to write the submitted data to the data sources associated with the data model object](/help/forms/using-form-data-model.md#write-submitted-adaptive-form-data-into-data-sources-write-af).

## Submit to REST endpoint {#submit-to-rest-endpoint}

The **[!UICONTROL Submit to REST Endpoint]** submit action sends the submitted data to a REST URL. This URL can be either an internal server (the server where the form is displayed) or an external server. The data of an Adaptive Form is submitted to a REST URL using the **[!UICONTROL Submit to REST endpoint]** Submit Action.

For a comprehensive guide on the detailed steps to post or submit data to a REST URL, refer to [configure submit to REST Endpoint submit action for Adaptive Forms](/help/forms/configure-submit-action-restpoint.md).

## Invoke an AEM Workflow {#invoke-an-aem-workflow}

The **[!UICONTROL Invoke an AEM Workflow]** Submit Action integrates an Adaptive Form with an [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hans#extending-aem). When a form is submitted, the selected workflow starts automatically. 

 [Integrate AEM Adaptive Form with AEM Workflow: Streamlining Business Processes](/help/forms/configure-submit-action-workflow.md) provides step-by-step instructions to seamlessly integrate AEM Workflow with Adaptive Forms, optimizing business processes and enhancing workflow automation.

## Submit to OneDrive {#submit-to-onedrive}

The **[!UICONTROL Submit to OneDrive]** Submit Action connects an Adaptive Form with a Microsoft&reg; OneDrive. You can submit the form data, files, attachments, or Document of Record to the connected Microsoft&reg; OneDrive Storage. 

AEM Forms Cloud Service with Microsoft&reg; OneDrive helps in optimize data submission. Explore the steps of [integrating OneDrive with AEM Forms](/help/forms/configure-submit-action-onedrive.md) for streamlined and secure storage.

## Submit to Azure Blob Storage {#submit-to-azure-blob-storage}

The **[!UICONTROL Submit to Azure Blob Storage]** Submit Action connects an Adaptive Form with a Microsoft&reg; Azure portal and allows you to submit various elements such as form data, files, attachments, or Document of Record to the associated Azure Storage containers.

AEM as a Cloud Service allows submitting data to Azure Storage from AEM Adaptive Forms. Learn how to [create and use Azure Blob Storage configuration in AEM Forms](/help/forms/configure-submit-action-azure-blob-storage.md) for efficient data storage. 

To set values of a configuration, [Generate OSGi Configurations using the AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hans#generating-osgi-configurations-using-the-aem-sdk-quickstart), and [deploy the configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hans#deployment-process) to your Cloud Service instance.

## Submit to Power Automate {#microsoft-power-automate}

You can configure an Adaptive Form to run a Microsoft&reg; Power Automate Cloud Flow on submission. The configured Adaptive Form sends captured data, attachments, and Document Of Record to Power Automate Cloud Flow for processing. It helps you build custom data capture experience while harnessing the power of Microsoft&reg; Power Automate to build business logics around captured data and automate customer workflows. 
Adaptive Forms editor provides the **Invoke a Microsoft&reg; Power Automate flow** submit action to send adaptive forms data, attachments, and Document Of Record to Power Automate Cloud Flow. To use the Submit action to send captured data to Microsoft&reg; Power Automate, [Connect your Forms as a Cloud Service instance with Microsoft&reg; Power Automate](forms-microsoft-power-automate-integration.md)  

After a successful configuration, use the [Invoke a Microsoft&reg; Power Automate flow](forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) submit action to send data to a Power Automate Flow.  

## Submit to Workfront Fusion {#workfront-fusion}

You can configure an Adaptive Form to submit data to Workfront Fusion on submission. Workfront Fusion allows automation of processes so that user can concentrate on new tasks rather than repeating the same tasks again and again. It automates both simple and complex tasks, saving time and ensuring consistent process execution.

The Adaptive Forms editor provides the **Invoke a WorkFront Fusion Scenario** submit action to send Adaptive Forms data or attachments to a Workfront Fusion scenario. To use the submit action for sending captured data to a Workfront Fusion scenario, refer to [Submit an Adaptive Form to Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md).

## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. 
## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). 
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). 

## Use synchronous or asynchronous submission {#use-synchronous-or-asynchronous-submission}

A Submit Action can use synchronous or asynchronous submission.

**Synchronous submission**: Traditionally, web forms are configured to submit synchronously. In a synchronous submission, when users submit a form, they are redirected to an acknowledgment page, a thank you page, or if there is submission failure, an error page. You can select the **[!UICONTROL Use asynchronous submission]** option to redirect the users to a webpage or show a message on submission.  

![Configure Submit Action](assets/thank-you-setting.png)

**Asynchronous submission**: Modern web experiences like single page applications are gaining popularity where the web page remains static while client-server interaction happens in the background. You can now provide this experience with Adaptive Forms by [configuring asynchronous submission](asynchronous-submissions-adaptive-forms.md).

## Server-Side Revalidation in Adaptive Form {#server-side-revalidation-in-adaptive-form}

Typically, in any online data capture system, developers place someJavaScript validations on client side to enforce a few business rules. But in modern browsers, end users have way to bypass those validations and manually do submissions using various techniques, Such as Web Browser DevTools Console. Such techniques are also valid for Adaptive Forms. A forms developer can create various validation logics, but technically, end users can bypass those validation logics and submit invalid data to the server. Invalid data would break the business rules that a form author has enforced.

The server-side revalidation feature provides the ability to run the validations that an Adaptive Forms author has provided while designing an Adaptive Form on the server. It prevents any possible compromise of data submissions and business rules violations represented in terms of form validations.

### What to validate on Server? {#what-to-validate-on-server-br}

All out of the box (OOTB) field validations of an Adaptive Form that are rerun at the server are:

* Required
* Validation Picture Clause
* Validation Expression

### Enabling Server-side Validation {#enabling-server-side-validation-br}

Use the **[!UICONTROL Revalidate on server]** under Adaptive Form Container in the sidebar to enable or disable server-side validation for the current form.

![Enabling Server-Side Validation](assets/revalidate-on-server.png)

Enabling Server-Side Validation

If end-user bypass those validations and submit the forms, the server again performs the validation. If the validation fails at server end, then the submit transaction is stopped. The user is presented with the original form again. The captured data and submitted data are presented to the user as an error.

>[!NOTE]
>
>Server-side validation validates the form model. You are recommended to create a separate client library for validations and not mix it with other things like HTML styling and DOM manipulation in the same client library.

## Error handling on Submit Action {#error-handling-on-submit-action}

As a part of AEM security and hardening guidelines, configure custom error pages such as 400.jsp, 404.jsp, and 500.jsp. These handlers are called, when on submitting a form 400, 404, or 500 errors appear. The handlers are also called when these error codes are triggered on the Publish node. You can also create JSP pages for other HTTP error codes.

When you prefill a form data model (FDM), or schema based Adaptive Form with XML or JSON data complaint to a schema that is data does not contain `<afData>`, `<afBoundData>`, and `</afUnboundData>` tags, then the data of unbounded fields of the Adaptive Form is lost. The schema can be an XML schema, JSON schema, or a Form Data Model (FDM). Unbounded fields are Adaptive Form fields without the `bindref` property.

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). 
## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Create an Adaptive Form (core components)](/help/forms/creating-adaptive-form-core-components.md)
* [Create a custom Submit Action for Adaptive Forms](/help/forms/custom-submit-action-form.md)

-->

## 另请参阅 {#see-also}

{{af-submit-action}}

