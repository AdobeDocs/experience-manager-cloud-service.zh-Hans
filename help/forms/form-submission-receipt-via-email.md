---
title: 如何在AEM Forms中通过电子邮件发送表单提交确认？
description: AEM Forms允许您配置电子邮件提交操作，以在提交表单时向用户发送确认。
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# 通过电子邮件发送表单提交确认 {#sending-a-form-submission-acknowledgement-via-email}

## 自适应表单数据提交 {#adaptive-form-data-submission}

自适应Forms提供了多个现成的[提交操作](configuring-submit-actions.md)工作流，用于将表单数据提交到不同的端点。

例如，**[!UICONTROL 发送电子邮件]**&#x200B;提交操作在成功提交自适应表单时发送电子邮件。 您还可以将其配置为通过电子邮件发送表单数据和PDF。

本文详细介绍在自适应表单及其提供的不同配置上启用电子邮件操作的步骤。

>[!NOTE]
>
>您还可以使用&#x200B;**[!UICONTROL 通过电子邮件发送PDF]**&#x200B;选项，通过电子邮件将填写好的表单作为PDF附件发送。 可用于此操作的配置选项与&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;操作的可用选项相同。 电子邮件PDF操作仅适用于基于XFA的自适应Forms

## 发送电子邮件操作 {#email-action}

利用“发送电子邮件”操作，作者可在自适应表单成功提交后自动向一个或多个收件人发送电子邮件。

<!-- >>[!NOTE]
>
>To use the Send email action, you need to configure the AEM mail service as described in [Configuring the mail service](/help/sites-administering/notification.md#configuring-the-mail-service).

### Enabling Send email action on an Adaptive Form {#enabling-email-action-on-an-adaptive-form}

1. Open an Adaptive Form in **[!UICONTROL edit]** mode.

1. In the **[!UICONTROL Content]** tab, select **[!UICONTROL Form Container]** and select ![configure](assets/configure-icon.svg) to view the Adaptive Form properties.  

1. In the **[!UICONTROL Submission]** section, select **[!UICONTROL Send email]** from the **[!UICONTROL Submit Action]** drop-down list.  

   ![Submit Actions](assets/submission-actions.png)

1. Specify valid email IDs in the **[!UICONTROL To]**, **[!UICONTROL CC]**, and **[!UICONTROL BCC]** fields.

   Specify the subject and the body of the email in the **[!UICONTROL Subject]** and **[!UICONTROL Email Template]** fields, respectively.

   You can also specify variable placeholders in the fields, in which case, the values of the fields are processed when the form is successfully submitted by an user. For more information, see [Using Adaptive Form field names to dynamically create email content](form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Include attachments]** if the form includes file attachments and you want to attach these files in the email.

   >[!NOTE]
   >
   >If you choose the **[!UICONTROL Send PDF via Email]** option, you must select the Include attachments option.

1. Click ![save](assets/save_icon.svg) to save the changes. -->

### 使用自适应表单字段名称动态创建电子邮件内容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

自适应表单中的字段名称称为占位符，在用户提交表单后，这些占位符将替换为该字段的值。

在&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;操作中，您可以使用执行该操作时处理的占位符。 这意味着在用户提交表单时生成电子邮件的标头（如&#x200B;**[!UICONTROL To]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL Subject]**）。

要定义占位符，请选择&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;作为提交操作后，在字段中指定`${<field name>}`。

例如，如果表单包含名为`email_addr`的&#x200B;**[!UICONTROL 电子邮件地址]**&#x200B;字段，用于捕获用户的电子邮件ID，则可以在&#x200B;**[!UICONTROL 收件人]**、**[!UICONTROL 抄送]**&#x200B;或&#x200B;**[!UICONTROL 密送]**&#x200B;字段中指定以下内容。

`${email_addr}`

当用户提交表单时，会向在表单的`email_addr`字段中输入的电子邮件ID发送电子邮件。

>[!NOTE]
>
>您可以在字段的&#x200B;**[!UICONTROL 编辑]**&#x200B;对话框中找到字段的名称。

变量占位符也可以在&#x200B;**[!UICONTROL 主题]**&#x200B;和&#x200B;**[!UICONTROL 电子邮件模板]**&#x200B;字段中使用。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重复面板中的字段不能用作变量占位符。

