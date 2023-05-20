---
title: 透過電子郵件傳送表單提交通知
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms可讓您設定電子郵件提交動作，在提交表單時傳送確認給使用者。
seo-description: AEM Forms allows you to configure the email Submit Action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# 透過電子郵件傳送表單提交通知 {#sending-a-form-submission-acknowledgement-via-email}

## 最適化表單資料提交 {#adaptive-form-data-submission}

最適化Forms提供數種現成可用的功能 [提交動作](configuring-submit-actions.md) 將表單資料提交至不同端點的工作流程。

例如， **[!UICONTROL 傳送電子郵件]** 提交動作會在成功提交最適化表單時傳送電子郵件。 您也可以將其設定為傳送電子郵件中的表單資料和PDF。

本文詳細說明在最適化表單及其提供的不同設定上啟用電子郵件動作的步驟。

>[!NOTE]
>
>您也可以使用 **[!UICONTROL 透過電子郵件傳送PDF]** 選項可透過電子郵件將完成的表單作為PDF附件傳送。 此動作可用的設定選項與以下動作可用的選項相同： **[!UICONTROL 傳送電子郵件]** 動作。 電子郵件PDF動作僅適用於XFA型最適化Forms

## 傳送電子郵件動作 {#email-action}

「傳送電子郵件」動作可讓作者在成功提交最適化表單時，自動傳送電子郵件給一或多個收件者。

<!-- >>[!NOTE]
>
>To use the Send email action, you need to configure the AEM mail service as described in [Configuring the mail service](/help/sites-administering/notification.md#configuring-the-mail-service).

### Enabling Send email action on an Adaptive Form {#enabling-email-action-on-an-adaptive-form}

1. Open an Adaptive Form in **[!UICONTROL edit]** mode.

1. In the **[!UICONTROL Content]** tab, tap **[!UICONTROL Form Container]** and tap ![configure](assets/configure-icon.svg) to view the Adaptive Form properties.  

1. In the **[!UICONTROL Submission]** section, select **[!UICONTROL Send email]** from the **[!UICONTROL Submit Action]** drop-down list.  

   ![Submit Actions](assets/submission-actions.png)

1. Specify valid email IDs in the **[!UICONTROL To]**, **[!UICONTROL CC]**, and **[!UICONTROL BCC]** fields.

   Specify the subject and the body of the email in the **[!UICONTROL Subject]** and **[!UICONTROL Email Template]** fields, respectively.

   You can also specify variable placeholders in the fields, in which case, the values of the fields are processed when the form is successfully submitted by an end user. For more information, see [Using Adaptive Form field names to dynamically create email content](form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Include attachments]** if the form includes file attachments and you want to attach these files in the email.

   >[!NOTE]
   >
   >If you choose the **[!UICONTROL Send PDF via Email]** option, you must select the Include attachments option.

1. Click ![save](assets/save_icon.svg) to save the changes. -->

### 使用最適化表單欄位名稱來動態建立電子郵件內容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

最適化表單中的欄位名稱稱為預留位置，可在使用者提交表單後，以該欄位的值取代。

在 **[!UICONTROL 傳送電子郵件]** 動作，則可以使用執行動作時所處理的預留位置。 這表示電子郵件的標題(例如 **[!UICONTROL 至]**， **[!UICONTROL CC]**， **[!UICONTROL 密件副本]**， **[!UICONTROL 主旨]**)會在使用者提交表單時產生。

若要定義預留位置，請指定 `${<field name>}` 在欄位中選取 **[!UICONTROL 傳送電子郵件]** 作為提交動作。

例如，如果表單包含 **[!UICONTROL 電子郵件地址]** 欄位，已命名 `email_addr`，若要擷取使用者的電子郵件ID，您可以在 **[!UICONTROL 至]**， **[!UICONTROL CC]**，或 **[!UICONTROL 密件副本]** 欄位。

`${email_addr}`

當使用者提交表單時，會傳送電子郵件至在中輸入的電子郵件ID `email_addr` 表單的欄位。

>[!NOTE]
>
>您可以在以下位置找到欄位名稱： **[!UICONTROL 編輯]** 欄位的對話方塊。

變數預留位置也可用在 **[!UICONTROL 主旨]** 和 **[!UICONTROL 電子郵件範本]** 欄位。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重複面板中的欄位無法當作變數預留位置使用。

