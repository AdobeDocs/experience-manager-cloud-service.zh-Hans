---
title: 在AEM FormsEdge Delivery Services中使用reCAPTCHA
description: 在EDS表单中使用Google reCAPTCHA
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---


# 在AEM FormsEdge Delivery Services中使用reCAPTCHA

reCAPTCHA是一种常用的工具，用于保护网站免受欺诈活动、垃圾邮件和滥用的影响。 在Edge Delivery Services中，自适应Forms块提供添加Google reCAPTCHA的功能，以区分人类和机器人。 此功能允许用户保护其网站免受垃圾邮件和滥用。
例如，考虑一个查询表单，该表单收集诸如开始和结束行程日期、房间预算、预计行程成本和旅客信息等数据。 在这种情况下，恶意用户可能会利用表单进行攻击，例如发送网络钓鱼电子邮件，或使用垃圾邮件程序向其发送不相关或有害的内容。 集成reCAPTCHA后，可验证所提交的内容是否来自正版用户，从而增强安全性，并有效地将垃圾邮件条目减至最少。

Edge Delivery Services仅支持 **基于得分(v3)-reCAPTCHA** 用于自适应表单块。

![Recaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png)

此 **reCAPTCHA** 功能在预发行计划下。 要请求访问 **reCAPTCHA** AEM FormsEdge Delivery Services的功能，请用您的工作地址向mailto:aem-forms-ea@adobe.com发送电子邮件。

<!--
By the end of this article, you learn to:
  * [Enable Google reCAPTCHA's for a single form](#enable-google-recaptchas-for-a-single-form)
  * [Enable reCAPTCHA for all the forms on your Site](#enable-recaptcha-for-all-the-forms)

## Pre-requisite

Register your domain with [Google reCAPTCHA and obtain credentials](https://www.google.com/recaptcha/admin/create).

## Enable Google reCAPTCHA's for a single form {#enable-google-recaptchas-for-a-single-form}

Enabling Google reCAPTCHA for a single form involves integrating Google's reCAPTCHA service into a specific web form to prevent automated abuse or spam submissions.

To enable Google reCAPTCHA's for a single form:
1. [Configure the reCAPTCHA secret key in project configuration file](#configure-secret-key)
1. [Add reCAPTCHA site key to your form](#add-site-key)


### Configure the reCAPTCHA secret key in project configuration file {#configure-secret-key}

The Site Secret for domain registered with Google reCAPTCHA is added to project the configuration file (`.helix/config`) in your AEM Project folder at Microsoft SharePoint or Google Drive. To add the Site Secret to the config file:

1. Go to your AEM Project folder on Microsoft® SharePoint or Google Drive. 
1. Create the `.helix/config.xlsx` file in your AEM Project folder in Microsoft SharePoint Site or the `.helix/config` file in AEM Project folder within your Google Drive. 

    >[!NOTE]
    >
    > The [project configuration file](https://www.aem.live/docs/configuration) is a spreadsheet located at `/.helix/config`. If the file does not exist, create it.

1. Open the `config` file and add the following key and value pairs:

    * **captcha.secret**: Google reCAPTCHA secret key value
    * **captcha.type**: reCAPTCHA v2
  
   Refer to the image for an illustration of a project configuration file:

    ![Project configuration file](/help/forms/assets/recaptcha-config-file.png)

    >[!NOTE]
    >
    >  You can retrieve the reCAPTCHA keys from the [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1.  Preview and publish the `config` file using [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content). 

### Add reCAPTCHA site key to your form {#add-site-key}

The Site Key for domain registered with Google reCAPTCHA is added to the spreadsheet of the form that is to be protected. To add the Site key to a form:

1. Go to your AEM Project folder on Microsoft® SharePoint or Google Drive and open your spreadsheet. You can also create new spreadsheet for a form.
1. Insert a row into the spreadsheet to add new field as CAPTCHA, including the following details:
    * **type**: captcha
    * **value**: Google reCAPTCHA site key value
  
    Refer to the illustration below, depicting the spreadsheet with the new row type as CAPTCHA:
  
   ![Recaptcha spreadsheet](/help/forms/assets/recaptcha-spreadsheet.png)

    >[!NOTE]
    >
    >  You can retrieve the reCAPTCHA keys from the [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) to preview and publish the sheet. 
You can refer to the [spreadsheet](/help/forms/assets/recaptcha-enquiry.xlsx) that includes the form definition for an enquiry form.

After adding new row in the form definition, a reCAPTCHA badge appears at the bottom-right corner of the form. This ensures that the form is now protected from fraudulent activities, spam, and misuse.

![recaptcha-form](/help/forms/assets/recaptcha-form.png)

Refer to the URL below, which showcases the live form with the reCAPTCHA badge:
https://main--wefinance--wkndforms.hlx.live/enquiry

## Enable reCAPTCHA for all the forms on your Site{#enable-recaptcha-for-all-the-forms}

To apply Google reCAPTCHA to all the forms on your Site that use Adaptive Forms Block, skip the previous steps and directly embed the `sitekey` value into the `recaptcha.js` file. To include site key value in the `recaptcha.js` file:

1. Open the corresponding GitHub repository on your local machine. 
1. Navigate to `../blocks/form/integrations/recaptcha.js` file.
1. Replace the `siteKey` with Google reCAPTCHA site key value.

    ![Recaptcha apply to all forms](/help/forms/assets/recaptcha-apply-to-all-forms.png)

    >[!NOTE]
    >
    >  You can retrieve the reCAPTCHA keys from the [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) to preview and publish the site. 

The reCAPTCHA badge starts appearing for all the forms on your Site. 
-->

## 另请参阅

{{see-more-forms-eds}}

