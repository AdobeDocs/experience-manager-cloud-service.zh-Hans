---
title: 在AEM自适应表单中使用Google reCAPTCHA
description: 使用Google reCAPTCHA服务可轻松增强表单安全性。 内部分步指南！
topic-tags: Adaptive Forms, author
hide: true
hidefromtoc: true
Keywords: Google reCAPTCHA service, Adaptive Forms, CAPTCHA challenge, Bot prevention, Core Components, Form submission security, Form spam prevention
source-git-commit: 496705937a01d99f988ba83f6d8984fc86dc8bfa
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 14%

---

# 在基于核心组件的AEM自适应表单中使用Google reCAPTCHA {#using-reCAPTCHA-in-adaptive-forms}

<span class="preview"> 这是预发行功能，可通过我们的 [预发行渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

| 应用到 | 文章链接 |
| -------- | ---------------------------- |
| 基于核心组件的自适应表单 | 本文 |
| 基于Foundation组件的自适应表单 | [单击此处](/help/forms/captcha-adaptive-forms.md) |

CAPTCHA（区分计算机和人类的完全自动化公共图灵测试）是一种在线交易中常用的程序，用于区分人类和自动化程序或机器人。它提出了一个挑战，并评估用户响应以确定是人还是机器人与网站交互。如果测试失败，它会阻止用户继续操作，并通过阻止机器人发布垃圾邮件或恶意目的来帮助确保在线交易的安全。

[!DNL AEM Forms] as a [!DNL Cloud Service] 在自适应Forms中支持Google reCAPTCHA v2。 您可以使用它在表单提交时提出验证码挑战. 要在自适应表单中使用reCAPTCHA，请执行以下操作：

1. [通过Google的reCAPTCHA服务连接您的AEM Forms环境](#connect-your-forms-environment-with-recaptcha-service-by-google)
1. [配置自适应表单以在提交表单时显示验证码质询](#using-reCAPTCHA)

## 通过Google的reCAPTCHA服务连接您的AEM Forms环境 {#connect-your-forms-environment-with-recaptcha-service-by-google}

通过Google的reCAPTCHA服务连接您的AEM Forms环境

1. 获取 [reCAPTCHA API密钥对](https://www.google.com/recaptcha/admin) 来自Google的。 它包括 **站点密钥** 和 **密钥**.

   ![创建Google网站的Google reCAPTCHA配置以获取reCAPTCHA密钥](/help/forms/assets/google-captcha.gif)
1. 在您的AEM Formsas a Cloud Service环境中创建配置容器。 配置容器包含用于将AEM连接到外部服务的云配置。 要创建并配置配置容器以将您的AEM Forms环境与Google的reCAPTCHA服务连接，请执行以下操作：
   1. 打开您的AEM Formsas a Cloud Service实例。
   1. 转到 **[!UICONTROL “工具”>“常规”>“配置浏览器”]**. 在配置浏览器中，您可以：
   1. 选择现有文件夹或创建文件夹。 您可以创建文件夹并为其启用云配置选项，也可以为现有文件夹启用云配置选项：

      * 要创建文件夹并为其启用云配置选项，请执行以下操作：
         1. 在配置浏览器中，单击 **[!UICONTROL 创建]**.
         1. 在创建配置对话框中，指定名称、标题，然后选择 **[!UICONTROL 云配置]** 选项。
         1. 单击 **[!UICONTROL 创建]**
      * 要为现有文件夹启用云配置选项，请执行以下操作：
         1. 在配置浏览器中，选择文件夹并点按 **[!UICONTROL 属性]**.
         1. 在配置属性对话框中，启用 **[!UICONTROL 云配置]**.
         1. 点按 **[!UICONTROL 保存并关闭]** 保存配置并退出对话框。

1. 配置Cloud Service：
   1. 在您的AEM创作实例上，转到 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** 并点击 **[!UICONTROL reCAPTCHA]**.
   1. 选择在上一部分中创建或更新的配置容器。 点按&#x200B;**[!UICONTROL 创建]**。
   1. 指定 **[!UICONTROL 标题]**， **[!UICONTROL 名称]**， **[!UICONTROL 站点密钥]**、和 **[!UICONTROL 密钥]** reCAPTCHA服务（在步骤1中获取）。 点按&#x200B;**[!UICONTROL 创建]**。


   ![配置该Cloud Service以通过Google将您的AEM Forms环境连接到reCAPTCHA服务](/help/forms/assets/captcha-configuration.gif)



   配置reCAPTCHA服务后，便可在自适应表单中使用。 有关更多信息，请参阅 [在自适应表单中使用Google reCAPTCHA](#using-reCAPTCHA).


## 以自适应表单的形式使用 Google reCAPTCHA {#using-reCAPTCHA}

要在自适应Forms中使用reCAPTCHA，请执行以下操作：

1. 打开您的AEM Formsas a Cloud Service实例。
1. 转到 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择自适应Forms并点按 **[!UICONTROL 属性]**. 对于 **[!UICONTROL 配置容器]** 选项，选择配置容器，该容器包含通过Google将AEM Forms与reCAPTCHA服务连接的云配置，然后点击 **[!UICONTROL 保存并关闭]**.

   如果您没有此类配置容器，请参阅部分 [通过Google的reCAPTCHA服务连接您的AEM Forms环境](#connect-your-forms-environment-with-recaptcha-service-by-google) 以了解如何创建此类配置容器。

   ![选择配置容器](/help/forms/assets/captcha-properties.png)

1. 选择自适应Forms并点按 **[!UICONTROL 编辑]**. 自适应表单在自适应Forms编辑器中打开。
1. 在组件浏览器中，拖放 **[!UICONTROL 自适应表单reCAPTCHA]** 自适应表单上的组件。

   Google reCAPTCHA验证对时间敏感，大约会在几分钟后过期。 因此，Adobe建议 **[!UICONTROL 自适应表单reCAPTCHA]** 之前安装的组件 **[!UICONTROL 提交]** 按钮。

1. 选择 **[!UICONTROL 自适应表单reCAPTCHA]** 组件并点按属性 ![“属性”图标](assets/configure-icon.svg) 图标。 此时将打开“属性”对话框。 指定以下必需属性：
   * **[!UICONTROL 名称]：** 在表单和规则编辑器中，您可以使用表单组件的唯一名称轻松标识该表单组件，但名称不得包含空格或特殊字符。
   * **[!UICONTROL 验证码配置]：** 选择配置为显示表单的Google reCAPTCHA对话框的云配置。 出于类似目的，您的环境中可以有多个云配置。 所以，请仔细选择服务。 如果未列出任何服务，请参阅 [通过Google的reCAPTCHA服务连接您的AEM Forms环境](#connect-your-forms-environment-with-recaptcha-service-by-google) 了解如何创建一个Cloud Service，将您的AEM Forms环境与Google的reCAPTCHA服务连接起来。
   * **验证码大小：** 您可以选择Google reCAPTCHA质询对话框的显示大小。 使用 **[!UICONTROL 紧凑]** 用于显示小尺寸和 **[!UICONTROL 普通]** 用于显示相对较大的Google reCAPTCHA挑战对话框的选项。

1. 点按 **[!UICONTROL 完成]**.

   现在， **受reCAPTCHA保护** 会显示在您的自适应表单上。 它显示在配置为使用Google reCAPTCHA服务的所有Adaptive Forms上。

   现在，只允许提交合法表单，在这些表单中，表单填充程序成功清除Google reCAPTCHA服务带来的挑战。
   ![Google受reCAPTCHA徽章保护](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Tap the component, select ![edit rules](assets/edit-rules-icon.svg), and tap **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Tap the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## 常见问题解答

**问：能否在自适应表单中使用多个Captcha组件？**
**Ans：** 不支持在自适应表单中使用多个验证码组件。 此外，不建议在标记为延迟加载的片段或面板中使用验证码组件。

## 另请参阅

* [创建自适应表单](/help/forms/creating-adaptive-form-core-components.md)
* [创建自适应表单片段](/help/forms/adaptive-form-fragments-core-components.md)
* [在 AEM Sites 页面或体验片段中添加自适应表单](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [以自适应表单的形式使用 Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
