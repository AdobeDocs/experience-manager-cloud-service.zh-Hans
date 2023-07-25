---
title: 在自适应Forms中使用CAPTCHA
seo-title: Using CAPTCHA in Adaptive Forms
description: 了解如何在自适应Forms中配置AEM CAPTCHA或Google reCAPTCHA服务。
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in Adaptive Forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: 115f8dfc8d3ba025f1e815bb8ae87cfb8a513e65
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 3%

---

# 在自适应Forms中使用CAPTCHA{#using-captcha-in-adaptive-forms}

|版本 |文章链接 | |青瓦-------- |青瓦---------------------------- | | AEM 6.5 |    [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html)                  | | AEMAS A CLOUD SERVICE |本文 |
=======

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/creating-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>


CAPTCHA（完全自动化公共图灵测试，用于区分计算机和人类）是一种在线交易中常用的程序，用于区分人类和自动化程序或机器人。 它会提出挑战，并评估用户响应以确定是人类还是机器人与网站交互。 它可以在测试失败时阻止用户继续操作，并通过阻止机器人发送垃圾邮件或恶意目的，帮助确保在线交易的安全。

[!DNL AEM Forms] 支持自适应Forms中的验证码。 您可以使用Google的reCAPTCHA服务来实施CAPTCHA。

>[!NOTE]
>
>* [!DNL AEM Forms] 仅支持reCaptcha v2。 不支持任何其他版本。
>* 上的离线模式下不支持自适应Forms中的验证码 [!DNL AEM Forms] 应用程序。
>

## 通过Google配置reCAPTCHA服务 {#google-reCAPTCHA}

表单作者可以使用Google的reCAPTCHA服务在自适应Forms中实施CAPTCHA。 它提供高级验证码功能以保护您的站点。 有关reCAPTCHA工作方式的更多信息，请参阅 [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![reCAPTCHA](assets/recaptcha_new.png)

在中实施reCAPTCHA服务 [!DNL AEM Forms]：

1. 获取 [reCAPTCHA API密钥对](https://www.google.com/recaptcha/admin) 来自Google的。 它包括站点密钥和密钥。
1. 为云服务创建配置容器。

   1. 转到 **[!UICONTROL “工具”>“常规”>“配置浏览器”]**.
      * 请参阅 [配置浏览器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=en#introduction) 文档，以了解更多信息。
   1. 执行以下操作可为云配置启用全局文件夹，或跳过此步骤为云服务配置创建和配置其他文件夹。

      1. 在配置浏览器中，选择 **[!UICONTROL 全局]** 文件夹并点按 **[!UICONTROL 属性]**.

      1. 在配置属性对话框中，启用 **[!UICONTROL 云配置]**.
      1. 点按 **[!UICONTROL 保存并关闭]** 保存配置并退出对话框。

   1. 在配置浏览器中，点按 **[!UICONTROL 创建]**.
   1. 在创建配置对话框中，指定文件夹的标题并启用 **[!UICONTROL 云配置]**.
   1. 点按 **[!UICONTROL 创建]** 以创建为云服务配置启用的文件夹。

1. 为reCAPTCHA配置云服务。

   1. 在您的Experience Manager创作实例上，转到 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. 点按 **[!UICONTROL reCAPTCHA]**. 此时将打开“配置”页。 选择在上一步中创建的配置容器并点按 **[!UICONTROL 创建]**.
   1. 指定reCAPTCHA服务的名称、站点密钥和密钥，然后点按 **[!UICONTROL 创建]** 以创建云服务配置。
   1. 在“编辑组件”对话框中，指定在步骤1中获取的站点密钥和密钥。 点按 **[!UICONTROL 保存设置]** 然后点按 **[!UICONTROL 确定]** 以完成配置。

   配置reCAPTCHA服务后，即可在自适应Forms中使用。 有关更多信息，请参阅 [在自适应Forms中使用CAPTCHA](#using-captcha).

## 在自适应Forms中使用CAPTCHA {#using-captcha}

要在自适应Forms中使用验证码，请执行以下操作：

1. 在编辑模式下打开自适应表单。

   >[!NOTE]
   >
   > 确保在创建自适应表单时选择的配置容器包含reCAPTCHA云服务。 您还可以编辑自适应表单属性以更改与表单关联的配置容器。

1. 在组件浏览器中，拖放 **[!UICONTROL 验证码]** 自适应表单上的组件。

   >[!NOTE]
   >
   > * 不支持在自适应表单中使用多个验证码组件。 此外，不建议在标记为延迟加载的面板或片段中使用验证码。
   > * 验证码对时间敏感，大约一分钟后过期。 因此，建议将Captcha组件放在自适应表单中的“提交”按钮之前。

1. 选择您添加的Captcha组件并点按 ![cmppr](assets/configure-icon.svg) 以编辑其属性。
1. 指定CAPTCHA小部件的标题。 默认值为 **[!UICONTROL 验证码]**. 选择 **[!UICONTROL 隐藏标题]** 如果您不想显示标题。
1. 从 **[!UICONTROL 验证码服务]** 下拉列表，选择 **[!UICONTROL reCAPTCHA]** 启用reCAPTCHA服务（如果已按中的说明进行配置） [Google提供的reCAPTCHA服务](#google-reCAPTCHA). 从“设置”下拉列表中选择一个配置。
1. 选择类型 **[!UICONTROL 普通]** 或 **[!UICONTROL 紧凑]** 用于reCAPTCHA构件。 您也可以选择 **[!UICONTROL 不可见]** 选项仅在可疑活动的情况下显示CAPTCHA质询。 受保护的表单上会显示下面显示的reCAPTCHA保护徽章。

   ![受reCAPTCHA徽章保护的Google](assets/google-recaptcha-v2.png)

   >[!NOTE]
   >
   > 不选择 **[!UICONTROL 默认]** 从Captcha服务下拉列表中，默认的Experience ManagerCAPTCHA服务已弃用。

1. 保存属性。

已在自适应表单上启用reCAPTCHA服务。 您可以预览表单并查看验证码是否正常工作。

### 根据规则显示或隐藏验证码组件 {#show-hide-captcha}

您可以选择根据应用于自适应表单中组件的规则显示或隐藏CAPTCHA组件。 点按组件，选择 ![编辑规则](assets/edit-rules-icon.svg)，然后点按 **[!UICONTROL 创建]** 创建规则。 有关创建规则的更多信息，请参阅 [规则编辑器](rule-editor.md).

例如，仅当表单中的货币值字段的值超过25000时，CAPTCHA组件才必须在自适应表单中显示。

点按 **[!UICONTROL 货币值]** 字段，并创建以下规则：

![显示或隐藏规则](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> 当您选择reCAPTCHA v2配置并且大小设置为 [!UICONTROL 不可见]，则显示/隐藏选项保持禁用状态。

### 验证验证码 {#validate-captcha}

您可以在提交表单时验证自适应表单中的CAPTCHA，也可以根据用户操作和条件进行CAPTCHA验证。

#### 在提交表单时验证验证码 {#validation-form-submission}

要在提交自适应表单时自动验证验证码，请执行以下操作：

1. 点按CAPTCHA组件并选择 ![cmppr](assets/configure-icon.svg) 查看组件属性。
1. 在 **[!UICONTROL 验证验证码]** 部分，选择 **[!UICONTROL 在提交表单时验证验证码]**.
1. 点按 ![完成](assets/save_icon.svg) 以保存组件属性。

#### 在用户操作和条件上验证验证码 {#validate-captcha-user-action}

要根据条件和用户操作验证验证码，请执行以下操作：

1. 点按CAPTCHA组件并选择 ![cmppr](assets/configure-icon.svg) 查看组件属性。
1. 在 **[!UICONTROL 验证验证码]** 部分，选择 **[!UICONTROL 在用户操作时验证验证码]**.
1. 点按 ![完成](assets/save_icon.svg) 以保存组件属性。

[!DNL Experience Manager Forms] 提供 `ValidateCAPTCHA` 用于使用预定义条件验证CAPTCHA的API。 您可以使用自定义提交操作或通过定义自适应表单中组件的规则来调用API。

以下示例为 `ValidateCAPTCHA` 用于使用预定义条件验证CAPTCHA的API：

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
     GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

此示例表明 `ValidateCAPTCHA` 仅当用户在填写表单时指定的数字框中的数字位数大于5时，API才会验证表单中的验证码。

**选项1：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API使用自定义提交操作验证验证码**

执行以下步骤以使用 `ValidateCAPTCHA` 使用自定义提交操作验证CAPTCHA的API：

1. 添加脚本以包含 `ValidateCAPTCHA` 用于自定义提交操作的API。 有关自定义提交操作的更多信息，请参阅 [为自适应Forms创建自定义提交操作](custom-submit-action-form.md).
1. 从中选择自定义提交操作的名称 **[!UICONTROL 提交操作]** 中的下拉列表 **[!UICONTROL 提交]** 自适应表单的属性。
1. 点按 **[!UICONTROL 提交]**. 验证码将根据 `ValidateCAPTCHA` 自定义提交操作的API。

**选项2：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API用于在提交表单之前对用户操作验证验证码**

您还可以调用 `ValidateCAPTCHA` API，方法是对自适应表单中的组件应用规则。

例如，您添加 **[!UICONTROL 验证验证码]** 按钮，并创建规则以在单击按钮时调用服务。

下图说明了在单击服务时如何调用服务 **[!UICONTROL 验证验证码]** 按钮：

![验证验证码](assets/captcha-validation1.gif)

您可以调用包含以下内容的自定义servlet `ValidateCAPTCHA` 使用规则编辑器的API，并根据验证结果启用或禁用自适应表单的提交按钮。

同样，您可以使用规则编辑器在自适应表单中包含用于验证验证码的自定义方法。

### 添加自定义验证码服务 {#add-custom-captcha-service}

[!DNL Experience Manager Forms] 提供reCAPTCHA作为CAPTCHA服务。 但是，您可以添加自定义服务以在 **[!UICONTROL CAPTCHA服务]** 下拉列表。

以下是向自适应表单添加其他CAPTCHA服务的界面的实现示例：

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` 指Sling存储库中CAPTCHA组件的资源路径。 此属性用于包含特定于CAPTCHA组件的详细信息。 例如， `captchaPropertyNodePath` 包含有关在CAPTCHA组件上配置的reCAPTCHA云配置的信息。 云配置信息提供 **[!UICONTROL 站点密钥]** 和 **[!UICONTROL 密钥]** 用于实施reCAPTCHA服务的设置。

`userResponseToken` 是指 `g_recaptcha_response` 在表单中求解验证码后生成的验证码。

### 编辑reCAPTCHA服务域 {#reCAPTCHA-service-domain}

reCAPTCHA服务使用 `https://www.recaptcha.net/` 作为默认域。 您可以修改要设置的设置 `https://www.google.com/` 或任何用于加载、渲染和验证reCAPTCHA服务的自定义域名。

设置 **[!UICONTROL af.cloudservices.recaptcha.domain]** 的属性 **[!UICONTROL 自适应表单和交互式通信Web渠道配置]** 要指定的配置 `https://www.google.com/` 或任何其他自定义域名。 以下JSON文件显示了一个示例：

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)。
