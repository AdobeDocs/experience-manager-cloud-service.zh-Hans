---
title: 将 reCAPTCHA 与 AEM Forms as a Cloud Service 的 Edge Delivery Services 结合使用
description: 在 EDS Form 中使用 Google reCAPTCHA
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
role: Admin, Architect, Developer
source-git-commit: fe45123b3aefddaf02bc8584283941db168ba174
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 24%

---


# 将 reCAPTCHA 与 AEM Forms as a Cloud Service 的 Edge Delivery Services 结合使用

<span> **reCAPTCHA**&#x200B;功能在预发行计划下。 要请求访问AEM FormsEdge Delivery Services的&#x200B;**reCAPTCHA**&#x200B;功能，请从您的工作地址发送电子邮件至mailto:aem-forms-ea@adobe.com。</span>

reCAPTCHA 是一种流行的工具，用于保护网站免受欺诈活动、垃圾邮件和滥用。在 Edge Delivery Services 中，自适应表单块提供了添加 Google reCAPTCHA 的功能，以区分人类和机器人。此功能允许用户保护他们的网站免受垃圾邮件和滥用。
例如，考虑一个收集旅行开始和结束日期、房间预算、预计旅行费用和旅行者信息等数据的查询表。在这种情况下，存在恶意用户利用该表单发送网络钓鱼电子邮件或使用垃圾邮件机器人向其中发送不相关或有害内容的风险。集成 reCAPTCHA 可验证提交内容是否来自真实用户，从而提供额外的安全性，有效减少垃圾邮件条目。

<!-- ![Recaptcha Image](/help/edge/docs/forms/assets/recaptcha-image.png){width="300" align="center"} -->

对于自适应表单块，Edge Delivery Services仅支持&#x200B;**基于得分的(v3)-reCAPTCHA**。

![Recaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png){width="300" align="center"}


读完本文后，您将学会：
* [为单个表单启用Google reCAPTCHA](#enable-google-recaptchas-for-a-single-form)
* [为网站上的所有表单启用reCAPTCHA](#enable-recaptcha-for-all-the-forms)

## 先决条件

* 按照[使用自适应Forms块创建表单](/help/edge/docs/forms/create-forms.md)中所述的步骤开始开发Edge Delivery ServicesForms。
* 使用[Google reCAPTCHA注册域并获取凭据](https://www.google.com/recaptcha/admin/create)。

## 为单个表单启用Google reCAPTCHA {#enable-google-recaptchas-for-a-single-form}

为单个表单启用Google reCAPTCHA涉及将Google的reCAPTCHA服务集成到特定的Web表单中，以防止自动滥用或垃圾邮件提交。

要为单个表单启用Google reCAPTCHA，请执行以下操作：
1. [在项目配置文件中配置reCAPTCHA密钥](#configure-secret-key)
1. [将reCAPTCHA站点密钥添加到表单](#add-site-key)

要在FormsEdge Delivery Services中开始配置reCaptcha，请参阅以下[电子表格](/help/edge/docs/forms/assets/recaptcha.xlsx)，其中包含表单的表单定义。

### 在项目配置文件中配置reCAPTCHA密钥 {#configure-secret-key}

在Google reCAPTCHA中注册的域的站点密钥已添加到位于Microsoft SharePoint或Google驱动器的AEM项目文件夹中的项目配置文件(`.helix/config`)。 要将站点密钥添加到配置文件，请执行以下操作：

1. 转到Microsoft®SharePoint或Google Drive上的“AEM项目”文件夹。
1. 在Microsoft SharePoint Site的AEM项目文件夹中创建`.helix/config.xlsx`文件，或在Google驱动器的AEM项目文件夹中创建`.helix/config`文件。

   >[!NOTE]
   >
   > [项目配置文件](https://www.aem.live/docs/configuration)是位于`/.helix/config`的电子表格。 如果文件不存在，请创建该文件。

1. 打开`config`文件并添加以下键值对：

   * **captcha.secret**： Google reCAPTCHA密钥值
   * **captcha.type**： reCAPTCHA v2

   >[!NOTE]
   >
   >  * 您可以从[Google reCAPTCHAAdmin Console](https://www.google.com/recaptcha/admin)检索reCAPTCHA密钥。
   >  * 您必须在`config`文件中将&#x200B;**captcha.type**&#x200B;的值指定为&#x200B;**reCAPTCHA v2**。

   请参阅下面的项目配置文件屏幕截图：

   ![项目配置文件](/help/forms/assets/recaptcha-config-file.png)

1. 保存 `config` 文件。

1. 使用[AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布`config`文件。

### 将reCAPTCHA站点密钥添加到表单 {#add-site-key}

在Google reCAPTCHA中注册的域的站点密钥会添加到要保护的表单的电子表格中。 要将Site键添加到表单：

1. 转到 Microsoft® SharePoint 或 Google Drive 上的 AEM Project 文件夹并打开电子表格。您还可以为表单创建新的电子表格。
1. 在电子表格中插入一行以添加新字段作为验证码，包括以下详细信息：
   * **类型**： captcha
   * **value**： Google reCAPTCHA站点密钥值

   请参阅下面的屏幕截图，其中显示了新行类型为CAPTCHA的电子表格：

   ![Recaptcha电子表格](/help/edge/docs/forms/assets/recaptcha-spreadsheet.png)

   >[!NOTE]
   >
   >  您可以从[Google reCAPTCHAAdmin Console](https://www.google.com/recaptcha/admin)检索reCAPTCHA密钥。

1. 保存电子表格。
1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览和发布工作表。

在表单定义中添加新行后，表单右下角会显示一个reCAPTCHA徽章。 这样可以确保表单现在不受欺诈活动、垃圾邮件和滥用的影响。

![recaptcha-form](/help/edge/docs/forms/assets/recaptcha-form.png)

## 为网站上的所有表单启用reCAPTCHA{#enable-recaptcha-for-all-the-forms}

要将Google reCAPTCHA应用于网站上使用Adaptive Forms Block的所有表单，请跳过之前的步骤，直接将`sitekey`值嵌入到`recaptcha.js`文件中。 要在`recaptcha.js`文件中包含站点键值，请执行以下操作：

1. [更新recaptcha.js文件中的Google reCAPTCHA站点密钥](#1-update-google-recaptcha-site-key-in-recaptchajs-file)
1. [部署文件并生成项目](#2-deploy-the-file-and-build-the-project)
1. [使用AEM Sidekick预览站点](#3-preview-the-site-using-the-aem-sidekick)

### 更新recaptcha.js文件中的Google reCAPTCHA站点密钥

1. 在本地计算机上打开相应的GitHub存储库。
1. 导航到`[../Form Block/integrations]`文件夹并打开`recaptcha.js`文件。
1. 将`siteKey`替换为Google reCAPTCHA站点密钥值。

   ![Recaptcha应用于所有表单](/help/forms/assets/recaptcha-apply-to-all-forms.png)

   >[!NOTE]
   >
   >  您可以从[Google reCAPTCHAAdmin Console](https://www.google.com/recaptcha/admin)检索reCAPTCHA密钥。

1. 保存 `recaptcha.js` 文件。

### 部署文件并生成项目

将更新的`recaptcha.js`文件部署到GitHub项目并验证生成是否成功。

### 使用AEM Sidekick预览站点

使用[AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布网站。

reCAPTCHA徽章开始显示在您网站上的所有表单中。

## 另请参阅

{{see-more-forms-eds}}

