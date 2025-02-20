---
title: 将 reCAPTCHA 与 AEM Forms as a Cloud Service 的 Edge Delivery Services 结合使用
description: 在适用于 AEM Forms 的 Edge Delivery Services 的表单中使用 Google reCAPTCHA
feature: Edge Delivery Services
keywords: 在表单中使用reCAPTCHA，在通用编辑器中使用reCAPTCHA，在表单中添加reCAPTCHA
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: ba42a99e6138616ab6a7564c4bf58400844bdcc4
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 6%

---


# 在WYSIWYG创作中使用reCAPTCHA

CAPTCHA（用于区分计算机和人的完全自动化公共图灵测试）是一种常用的工具，用于保护网站免受欺诈活动、垃圾邮件和滥用。

例如，考虑根据附加扣减额和税率计算税额的表单。 在这种情况下，存在恶意用户利用该表单发送网络钓鱼电子邮件或使用垃圾邮件机器人向其中发送不相关或有害内容的风险。集成CAPTCHA后，通过验证来自真实用户的提交内容来提高安全性，从而有效地将垃圾邮件条目减至最少。

![Google recaptcha](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

在Edge Delivery Services Forms中，表单块允许您使用&#x200B;**Captcha（不可见）**&#x200B;组件[将Google reCAPTCHA与表单](#connect-forms-with-recaptcha-service-by-google)连接以区分人类和机器人。 此功能可帮助作者保护表单免受垃圾邮件和滥用。

## 将Forms与Google提供的reCAPTCHA服务连接起来

您可以创作Edge Delivery Services Forms以实施Google提供的reCAPTCHA服务。 根据您的需求，您可以为Edge Delivery Services Forms配置以下reCAPTCHA服务之一：

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> 有关reCAPTCHA工作方式的更多信息，请参阅[Google reCAPTCHA](https://developers.google.com/recaptcha/)。

### 配置reCAPTCHA Enterprise

reCAPTCHA Enterprise是Google提供的一项高级、企业级欺诈检测和预防服务。 它以reCAPTCHA（基于得分）为基础，但提供了额外的功能、可扩展性和定制性，以满足复杂的业务需求。

#### 开始之前

在为Edge Delivery Services Forms配置Google reCAPTCHA Enterprise之前，请确保您已完成以下步骤：

1. 创建或选择[Google Cloud项目](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin)并检索[项目ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed)。

1. [为您的Google Cloud项目启用reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api)并[创建API密钥](https://console.cloud.google.com/apis/credentials)。

1. 为您的Google Cloud项目](https://console.cloud.google.com/security/recaptcha)创建一个[站点密钥，并复制该站点密钥。

获得这些凭据后，您可以继续为表单配置reCAPTCHA Enterprise：

1. [创建云配置容器](#1-create-cloud-configuration-container)
1. [为reCAPTCHA Enterprise创建云服务配置](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1.创建云配置容器

要创建云配置容器，请执行以下步骤：

1. 登录您的创作实例。
1. 转到&#x200B;**[!UICONTROL 工具]** ![工具–1](/help/forms/assets/tools-1.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**。

   ![云配置容器](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中，导航到您的表单并选择&#x200B;**[!UICONTROL 属性]**。

   ![云配置属性](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. 在&#x200B;**[!UICONTROL 配置属性]**&#x200B;对话框中，启用&#x200B;**[!UICONTROL 云配置]**。

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置并退出对话框。

   ![启用云配置属性](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
’
创建云配置容器后，将其发布。

   ![发布云配置](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2.为reCAPTCHA Enterprise创建云服务配置

要为reCAPTCHA Enterprise创建云服务配置，请执行以下步骤：

1. 登录您的创作实例。
1. 导航到&#x200B;**[!UICONTROL 工具]** ![工具–1](/help/forms/assets/tools-1.png) > **[!UICONTROL 云服务]** > **[!UICONTROL reCAPTCHA]**。

   ![Recaptcha云配置](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   将打开&#x200B;**配置**&#x200B;对话框。

1. 导航到您的表单并选择&#x200B;**[!UICONTROL 创建]**。

   ![验证码配置](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   将打开&#x200B;**[!UICONTROL 创建reCAPTCHA配置]**&#x200B;对话框。

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. 选择版本为[!DNL ReCAPTCHA Enterprise]并指定标题、名称、项目ID、站点密钥和API密钥。

   >[!NOTE]
   >
   > 您可从reCAPTCHA Enterprise的[开始之前](#before-you-start)部分获取项目ID、站点密钥和API密钥。

1. 选择&#x200B;**[!UICONTROL 密钥类型]**&#x200B;作为&#x200B;**基于得分的站点密钥**。
1. 指定0到1](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores)范围内的[阈值分数。 分数大于或等于阈值分数会标识人类交互，否则被视为机器人交互。
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建云服务配置。

   创建reCAPTCHA云配置后，将其发布。

   ![发布Recaptcha配置](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

您现在可以创建或编辑表单，并使用基于WYSIWYG的创作添加reCAPTCHA组件。 有关将Google reCAPTCHA集成到表单中的详细说明，请参阅[在表单中使用reCAPTCHA](#use-recaptcha-in-your-form)。

## 配置reCAPTCHA

reCAPTCHA是Google提供的免费服务，可帮助网站检测和阻止滥用的流量，包括机器人和垃圾邮件。 它支持在后台运行的基于得分的版本，并为每个用户交互分配风险得分（从0.0到1.0不等）。 分数大于或等于阈值分数会标识人类交互，否则被视为机器人交互。

#### 开始之前

在为Google Forms配置Edge Delivery Services reCAPTCHA之前，请从Google控制台](https://www.google.com/recaptcha/admin)检索[reCAPTCHA API密钥对。 该对包括站点密钥和密钥。

>[!NOTE]
>
> * Edge Delivery Services Forms仅支持基于&#x200B;**reCAPTCHA得分的**&#x200B;版本。

获得API密钥对后，您可以继续为表单配置reCAPTCHA：

1. [创建云配置容器](#1-create-cloud-configuration-container-1)
1. [创建reCAPTCHA的云服务配置](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1.创建云配置容器

要创建云配置容器，请执行以下步骤：

1. 登录您的创作实例。
1. 转到&#x200B;**[!UICONTROL 工具]** ![工具–1](/help/forms/assets/tools-1.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**。

   ![云配置容器](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中，导航到您的表单并选择&#x200B;**[!UICONTROL 属性]**。

   ![云配置属性](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. 在&#x200B;**[!UICONTROL 配置属性]**&#x200B;对话框中，启用&#x200B;**[!UICONTROL 云配置]**。

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置并退出对话框。

   ![启用云配置属性](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   创建云配置容器后，将其发布。

   ![发布云配置](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2.为reCAPTCHA创建云服务配置

要为reCAPTCHA创建云服务配置，请执行以下步骤：

1. 登录您的创作实例。
1. 导航到&#x200B;**[!UICONTROL 工具]** ![工具–1](/help/forms/assets/tools-1.png) > **[!UICONTROL 云服务]** > **[!UICONTROL reCAPTCHA]**。

   ![Recaptcha云配置](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   将打开&#x200B;**配置**&#x200B;对话框。

1. 导航到您的表单并选择&#x200B;**[!UICONTROL 创建]**。

   ![验证码配置](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   将打开&#x200B;**[!UICONTROL 创建reCAPTCHA配置]**&#x200B;对话框。

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. 选择版本为[!DNL ReCAPTCHA v2]并指定标题和名称。
1. 指定站点密钥和密钥。

   >[!NOTE]
   >
   > 您可以从[开始之前](#before-you-begin)部分获取reCAPTCHA的站点密钥和密钥。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建云服务配置。

   创建reCAPTCHA云配置后，将其发布。

   ![发布Recaptcha配置](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

您现在可以创建并编辑表单，并使用基于WYSIWYG的创作添加reCAPTCHA组件。 有关将Google reCAPTCHA集成到表单中的详细说明，请参阅[在表单中使用reCAPTCHA](#use-recaptcha-in-your-form)。

### 在表单中使用reCAPTCHA

要创作表单并添加reCAPTCHA（不可见）组件，请执行以下步骤：

1. 在通用编辑器中打开表单进行编辑。
1. 导航到内容树中已添加的自适应表单分区。
1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标并从&#x200B;**自适应表单组件**&#x200B;列表中添加&#x200B;**[!UICONTROL Captcha (Invisible)]**&#x200B;组件。

   ![添加reCaptcha组件](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   您还可以拖放所需的自适应Forms组件，因为通用编辑器提供了直观的拖放功能。

1. 在添加&#x200B;**[!UICONTROL Captcha (Invisible)]**&#x200B;组件后，单击&#x200B;**发布**&#x200B;以再次发布表单。

   ![重新发布表单](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

现在，您可以在以下URL查看带有reCAPTCHA服务的表单：
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`。

![带有reCAPTCHA的表单](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## 常见问题解答

* **如果用户未创建reCAPTCHA云配置，会发生什么情况？**

  **A**：如果用户没有创建reCAPTCHA云配置，AEM服务器将在全局配置容器中搜索reCAPTCHA云配置。 如果全局配置容器中不存在配置，则AEM服务器会引发错误。

* **如果用户创建多个reCAPTCHA云配置，会发生什么情况？**
  **A**：如果用户创建多个reCAPTCHA云配置，系统将自动选择第一个创建的reCAPTCHA配置。

* **为什么修改或更改在已发布的URL上不可见？**
如果修改或更改在已发布的URL中不可见，请确保重新发布表单以应用更新。

* **Edge Delivery Services Forms支持哪种reCAPTCHA服务？**
  **A**： Edge Delivery Services Forms仅支持Google提供的基于得分的reCAPTCHA服务。


## 另请参阅

{{universal-editor-see-also}}

