---
title: 将 reCAPTCHA 与 AEM Forms as a Cloud Service 的 Edge Delivery Services 结合使用
description: 在用于AEM FormsEdge Delivery Services的表单中使用Google reCAPTCHA
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
role: Admin, Architect, Developer
source-git-commit: 4a8153ffbdbc4da401089ca0a6ef608dc2c53b22
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 95%

---


# 将 reCAPTCHA 与 AEM Forms as a Cloud Service 的 Edge Delivery Services 结合使用

<span>**reCAPTCHA** 功能目前处于预发布计划之中。要请求访问AEM FormsEdge Delivery Services的&#x200B;**reCAPTCHA**&#x200B;功能，请从您的工作地址发送电子邮件至mailto:aem-forms-ea@adobe.com。</span>

reCAPTCHA 是一种流行的工具，用于保护网站免受欺诈活动、垃圾邮件和滥用。在 Edge Delivery Services 中，自适应表单块提供了添加 Google reCAPTCHA 的功能，以区分人类和机器人。此功能允许用户保护他们的网站免受垃圾邮件和滥用。
例如，考虑一个收集旅行开始和结束日期、房间预算、预计旅行费用和旅行者信息等数据的查询表。在这种情况下，存在恶意用户利用该表单发送网络钓鱼电子邮件或使用垃圾邮件机器人向其中发送不相关或有害内容的风险。集成 reCAPTCHA 可验证提交内容是否来自真实用户，从而提供额外的安全性，有效减少垃圾邮件条目。

<!-- ![Recaptcha Image](/help/edge/docs/forms/assets/recaptcha-image.png){width="300" align="center"} -->

Edge Delivery Services 仅支持 **基于分数的（v3）-reCAPTCHA** 用于自适应表单块。Edge Delivery Services 仅支持自适应表单块的基于分数的 (v3) reCAPTCHA。

![Recaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png){width="300" align="center"}


读完本文后，您将学会：
* [为单个表单启用 Google reCAPTCHA](#enable-google-recaptchas-for-a-single-form)
* [为您网站上的所有表单启用 reCAPTCHA](#enable-recaptcha-for-all-the-forms)

## 先决条件

* 按照 [使用自适应表单块创建表单](/help/edge/docs/forms/create-forms.md)中所述的步骤开始开发 Edge Delivery Services 表单。
* 使用 [Google reCAPTCHA 注册您的域名并获取凭证](https://www.google.com/recaptcha/admin/create)。

## 为单个表单启用 Google reCAPTCHA {#enable-google-recaptchas-for-a-single-form}

为单个表单启用 Google reCAPTCHA 涉及将 Google 的 reCAPTCHA 服务集成到特定的 Web 表单中，以防止自动滥用或垃圾邮件提交。

为单个表单启用 Google reCAPTCHA：
1. [在项目配置文件中配置reCAPTCHA密钥](#configure-secret-key)
1. [将 reCAPTCHA 站点密钥添加到您的表单中](#add-site-key)

要开始在 Edge Delivery Services Forms 中配置 reCaptcha，请参阅以下包含表单的表单定义的[电子表格](/help/edge/docs/forms/assets/recaptcha.xlsx)。

### 在项目配置文件中配置reCAPTCHA密钥 {#configure-secret-key}

使用 Google reCAPTCHA 注册的域的站点机密被添加到 Microsoft Sharepoint 或 Google Drive 上的（`.helix/config`）AEM 项目文件夹中的项目配置文件。要将站点机密添加到配置文件：

1. 转到 Microsoft® SharePoint 或 Google Drive 上的 AEM 项目文件夹。
1. 创建 `.helix/config.xlsx` Microsoft SharePoint 站点中的 AEM 项目文件夹中的文件或 `.helix/config` Google 驱动器内的 AEM 项目文件夹中的文件。

   >[!NOTE]
   >
   > 这 [项目配置文件](https://www.aem.live/docs/configuration) 电子表格位于 `/.helix/config`。如果该文件不存在，则创建它。

1. 打开 `config` 文件并添加以下键和值对：

   * **验证码密码**：Google reCAPTCHA 密钥值
   * **验证码类型**: reCAPTCHA v2

   >[!NOTE]
   >
   >  * 您可以从 [Google reCAPTCHA 管理控制台](https://www.google.com/recaptcha/admin)检索 reCAPTCHA 密钥。
   >  * 您必须将 **文件中的** captcha.type值 `config` 指定为 **reCAPTCHA v2**。

   请参阅下面的项目配置文件截图：

   ![项目配置文件](/help/forms/assets/recaptcha-config-file.png)

1. 保存 `config` 文件。

1. 使用 [AEM Sidekick ](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布文件`config`。

### 将 reCAPTCHA 站点密钥添加到您的表单中 {#add-site-key}

使用 Google reCAPTCHA 注册的域名的站点密钥被添加到要保护的表单的电子表格中。要将站点键添加到表单：

1. 转到 Microsoft® SharePoint 或 Google Drive 上的 AEM Project 文件夹并打开电子表格。您还可以为表单创建新的电子表格。
1. 在电子表格中插入一行以添加新字段作为 CAPTCHA，包括以下详细信息：
   * **类型**：验证码
   * **价值**：Google reCAPTCHA 站点密钥值

   请参阅下面的屏幕截图，其中描绘了新行类型为 CAPTCHA 的电子表格：

   ![Recaptcha 电子表格](/help/edge/docs/forms/assets/recaptcha-spreadsheet.png)

   >[!NOTE]
   >
   >  您可以从 [Google reCAPTCHA 管理控制台](https://www.google.com/recaptcha/admin)检索 reCAPTCHA 密钥。

1. 保存电子表格。
1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览和发布工作表。

在表单定义中添加新行后，表单的右下角会出现一个 reCAPTCHA 徽章。这确保了表单现在受到保护，免受欺诈活动、垃圾邮件和滥用。

![recaptcha 表单](/help/edge/docs/forms/assets/recaptcha-form.png)

## 为您网站上的所有表单启用 reCAPTCHA{#enable-recaptcha-for-all-the-forms}

要将 Google reCAPTCHA 应用于您网站上使用自适应表单块的所有表单，请跳过前面的步骤并直接将 `sitekey` 值嵌入到 `recaptcha.js` 文件中。在 `recaptcha.js` 文件中包含站点密钥值：

1. [在 recaptcha.js 文件中更新 Google reCAPTCHA 站点密钥](#1-update-google-recaptcha-site-key-in-recaptchajs-file)
1. [部署文件并构建项目](#2-deploy-the-file-and-build-the-project)
1. [使用 AEM Sidekick 预览站点](#3-preview-the-site-using-the-aem-sidekick)

### 在 recaptcha.js 文件中更新 Google reCAPTCHA 站点密钥

1. 在本地机器上打开相应的 GitHub 存储库。
1. 导航 `[../Form Block/integrations]` 文件夹并打开 `recaptcha.js` 文件。
1. 更换 `siteKey` 带有Google reCAPTCHA 站点密钥值。

   ![Recaptcha 适用于所有表格](/help/forms/assets/recaptcha-apply-to-all-forms.png)

   >[!NOTE]
   >
   >  您可以从 [Google reCAPTCHA 管理控制台](https://www.google.com/recaptcha/admin)检索 reCAPTCHA 密钥。

1. 保存 `recaptcha.js` 文件。

### 部署文件并构建项目

将更新后的`recaptcha.js`文件部署到您的 GitHub 项目并验证是否成功构建。

### 使用 AEM Sidekick 预览站点

使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 预览和发布网站。

reCAPTCHA 徽章开始出现在您网站上的所有表格上。

## 另请参阅

{{see-more-forms-eds}}

