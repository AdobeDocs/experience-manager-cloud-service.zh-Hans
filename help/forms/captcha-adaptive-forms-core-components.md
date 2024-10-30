---
title: How to use Google reCAPTCHA in an AEM Adaptive Form?
description: Enhance form security with Google reCAPTCHA service effortlessly. 里面有分步指南！
topic-tags: Adaptive Forms, author
keywords: Google reCAPTCHA服务，自适应Forms， CAPTCHA挑战，机器人预防，核心组件，表单提交安全性，表单垃圾邮件预防
feature: Adaptive Forms, Core Components
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
role: User, Developer
source-git-commit: bba5e5d283da616baa57b788181af73d59d86ee3
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 11%

---

# 在基于核心组件的AEM自适应表单中使用Google reCAPTCHA {#using-reCAPTCHA-in-adaptive-forms}

| 应用到 | 文章链接 |
| -------- | ---------------------------- |
| 基于核心组件的自适应表单 | 本文 |
| 基于Foundation组件的自适应表单 | [单击此处](/help/forms/captcha-adaptive-forms.md) |

CAPTCHA（区分计算机和人类的完全自动化公共图灵测试）是一种在线交易中常用的程序，用于区分人类和自动化程序或机器人。它提出了一个挑战，并评估用户响应以确定是人还是机器人与网站交互。如果测试失败，它会阻止用户继续操作，并通过阻止机器人发布垃圾邮件或恶意目的来帮助确保在线交易的安全。

AEM Formsas a Cloud Service支持以下CAPTCHA解决方案：

* [Google reCAPTCHA](#connect-your-aem-forms-environment-with-recaptcha-service-by-google)
* [](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)


## Connect your AEM Forms environment with reCAPTCHA service by Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Form authors can use the reCAPTCHA service by Google to implement reCAPTCHA in Adaptive Forms. 它提供高级验证码功能以保护您的站点。 有关reCAPTCHA工作方式的更多信息，请参阅[Google reCAPTCHA](https://developers.google.com/recaptcha/)。 [!DNL AEM Forms] as a [!DNL Cloud Service]支持自适应Forms中的Google reCAPTCHA v2。 您可以用它来提交表单时提出验证码质询。 通过Google的reCAPTCHA服务连接您的AEM Forms环境

1. 从Google获取[reCAPTCHA API密钥对](https://www.google.com/recaptcha/admin)。 它包含&#x200B;**站点密钥**&#x200B;和&#x200B;**密钥**。

   ![创建Google网站的Google reCAPTCHA配置以获取reCAPTCHA密钥](/help/forms/assets/google-captcha.gif)
1. Create Configuration Container on your AEM Forms as a Cloud Service environment. A Configuration Container holds Cloud Configurations used to connect AEM to external services. To create and configure a Configuration Container to connect your AEM Forms environment with reCAPTCHA service by Google:
   1. 打开您的AEM Formsas a Cloud Service实例。
   1. 转到&#x200B;**[!UICONTROL 工具>常规>配置浏览器]**。 在配置浏览器中，您可以：
   1. 选择现有文件夹或创建文件夹。 您可以创建文件夹并为其启用云配置选项，也可以为现有文件夹启用云配置选项：

      * 要创建文件夹并为其启用云配置选项，请执行以下操作：
         1. 在配置浏览器中，单击&#x200B;**[!UICONTROL 创建]**。
         1. 在创建配置对话框中，指定名称、标题，然后选择&#x200B;**[!UICONTROL 云配置]**&#x200B;选项。
         1. 单击&#x200B;**[!UICONTROL 创建]**
      * 要为现有文件夹启用云配置选项，请执行以下操作：
         1. 在配置浏览器中，选择文件夹，然后选择&#x200B;**[!UICONTROL 属性]**。
         1. 在配置属性对话框中，启用&#x200B;**[!UICONTROL 云配置]**。
         1. ****

1. Configure the Cloud Service:
   1. ![](assets/tools-1.png)********
   1. 选择在上一部分中创建或更新的配置容器。 选择&#x200B;**[!UICONTROL 创建]**。
   1. 指定reCAPTCHA服务的&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 名称]**、**[!UICONTROL 站点密钥]**&#x200B;和&#x200B;**[!UICONTROL 密钥]**（在步骤1中获取）。 选择&#x200B;**[!UICONTROL 创建]**。

   ![配置该Cloud Service以通过Google将您的AEM Forms环境连接到reCAPTCHA服务](/help/forms/assets/captcha-configuration.gif)

   Once the reCAPTCHA service is configured, it is available for use in an Adaptive Form. [](#using-reCAPTCHA)

## 以自适应表单的形式使用 Google reCAPTCHA {#using-reCAPTCHA}

To use reCAPTCHA in Adaptive Forms:

1. Open your AEM Forms as a Cloud Service instance.
1. 转到&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择自适应Forms并选择&#x200B;**[!UICONTROL 属性]**。 对于&#x200B;**[!UICONTROL 配置容器]**&#x200B;选项，请选择包含通过Google将AEM Forms与reCAPTCHA服务连接的云配置的配置容器，然后选择&#x200B;**[!UICONTROL 保存并关闭]**。

   如果您没有此类配置容器，请参阅[通过Google的reCAPTCHA服务连接您的AEM Forms环境](#connect-your-forms-environment-with-recaptcha-service-by-google)部分，以了解如何创建此类配置容器。

   ![选择配置容器](/help/forms/assets/captcha-properties.png)

1. 选择自适应Forms并选择&#x200B;**[!UICONTROL 编辑]**。 The Adaptive Form opens in Adaptive Forms Editor.
1. ****

   Google reCAPTCHA validation is time-sensitive and expires in about a couple of minutes. ********

1. ****![](assets/configure-icon.svg)It opens the properties dialog. Specify the following mandatory properties:
   * **[!UICONTROL 名称]：**&#x200B;您可以轻松地在表单和规则编辑器中使用表单组件的唯一名称来标识该表单组件，但名称不得包含空格或特殊字符。
   * **[!UICONTROL CAPTCHA配置]：**&#x200B;选择配置为显示表单的Google reCAPTCHA对话框的云配置。 出于类似目的，您的环境中可以有多个云配置。 所以，请仔细选择服务。 如果未列出任何服务，请参阅[将您的AEM Forms环境与Google的reCAPTCHA服务连接](#connect-your-forms-environment-with-recaptcha-service-by-google)，了解如何创建将AEM Forms环境与Google的reCAPTCHA服务连接的Cloud Service。
   * ************

1. 选择&#x200B;**[!UICONTROL 完成]**。

   现在，受reCAPTCHA保护的&#x200B;****&#x200B;显示在您的自适应表单上。 它显示在配置为使用Google reCAPTCHA服务的所有Adaptive Forms上。

   现在，只允许提交合法表单，在这些表单中，表单填充程序成功清除Google reCAPTCHA服务带来的挑战。
   ![受reCAPTCHA徽章保护的Google](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Select the component, select ![edit rules](assets/edit-rules-icon.svg), and select **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Select the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## 常见问题解答

**问：能否在自适应表单中使用多个Captcha组件？**
不支持在自适应表单中使用多个Captcha组件的**Ans：**。 此外，不建议在标记为延迟加载的片段或面板中使用验证码组件。

## 另请参阅 {#see-also}

{{see-also}}