---
title: 如何在自适应Forms中使用CAPTCHA？
description: 了解如何为自适应表单配置或Google reCAPTCHA服务。
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
feature: Adaptive Forms, Foundation Components
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 9%

---


# 在自适应Forms中使用reCAPTCHA {#using-reCAPTCHA-in-adaptive-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/creating-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html) |
| AEM as a Cloud Service | 本文 |
| 应用到 | 基于基础组件的自适应表单。 对于基于核心组件的自适应表单，<br>，请[单击此处](/help/forms/captcha-adaptive-forms-core-components.md)。 |


CAPTCHA（区分计算机和人类的完全自动化公共图灵测试）是一种在线交易中常用的程序，用于区分人类和自动化程序或机器人。它提出了一个挑战，并评估用户响应以确定是人还是机器人与网站交互。如果测试失败，它会阻止用户继续操作，并通过阻止机器人发布垃圾邮件或恶意目的来帮助确保在线交易的安全。

AEM Formsas a Cloud Service支持以下CAPTCHA解决方案：

* [Google reCAPTCHA](#configure-recaptcha-service-by-google)
* [Cloudflare Turnstile](/help/forms/integrate-adaptive-forms-turnstile.md)
* [验证码](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## 通过Google配置reCAPTCHA服务 {#google-reCAPTCHA}

表单作者可以使用Google的reCAPTCHA服务在自适应Forms中实施reCAPTCHA。 它提供高级验证码功能以保护您的站点。 有关reCAPTCHA工作方式的更多信息，请参阅[Google reCAPTCHA](https://developers.google.com/recaptcha/)。 AEM Forms支持[!DNL reCAPTCHA v2]和[!DNL reCAPTCHA Enterprise]。 不支持任何其他版本。 另请注意，[!DNL AEM Forms]应用程序在离线模式下不支持自适应Forms中的reCAPTCHA。 根据要求，您可以配置reCAPTCHA服务以启用：

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [AEM Forms中的reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [AEM Forms中的reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)


### 配置reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. 创建或选择[Google Cloud项目](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin)并启用[reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api)。
1. 获取[项目ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed)并为网站创建[API密钥](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key)和[站点密钥](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key)。
1. 为云服务创建配置容器。

   1. 转到&#x200B;**[!UICONTROL 工具>常规>配置浏览器]**。
   1. 选择文件夹或创建文件夹，然后使用以下步骤启用云配置的文件夹：
      1. 在配置浏览器中，选择文件夹，然后选择&#x200B;**[!UICONTROL 属性]**。
      1. 在配置属性对话框中，启用&#x200B;**[!UICONTROL 云配置]**。
      1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置并退出对话框。

1. 为[!DNL reCAPTCHA Enterprise]配置云服务。

   1. 在您的Experience Manager创作实例上，转到![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**。
   1. 选择&#x200B;**[!UICONTROL reCAPTCHA]**。 此时将打开“配置”页面。 选择您创建的配置容器，然后选择&#x200B;**[!UICONTROL 创建]**。
   1. 选择版本为[!DNL reCAPTCHA Enterprise]，并为reCAPTCHA Enterprise服务指定名称、项目ID、站点密钥和API密钥（在步骤2中获取）。
   1. 选择密钥类型，密钥类型应与您在[Google Cloud项目](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin)中配置的站点密钥相同，例如，**复选框站点密钥**&#x200B;或&#x200B;**基于得分的站点密钥**。
   1. 指定0到1](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores)范围内的[阈值分数。 分数大于或等于阈值分数标识人交互，否则被视为机器人交互。
   1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建云服务配置。

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Select **[!UICONTROL Save Settings]** and then select **[!UICONTROL OK]** to complete the configuration.
-->

reCAPTCHA Enterprise服务一旦启用，就可用于自适应表单。 请参阅在自适应表单](#using-reCAPTCHA)中使用CAPTCHA [。

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->

### 配置Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. 从Google获取[reCAPTCHA API密钥对](https://www.google.com/recaptcha/admin)。 它包含&#x200B;**站点密钥**&#x200B;和&#x200B;**密钥**。
1. 为云服务创建配置容器。
   1. 转到&#x200B;**[!UICONTROL 工具>常规>配置浏览器]**。
   1. 选择文件夹或创建文件夹，然后使用以下步骤启用云配置的文件夹：
      1. 在配置浏览器中，选择文件夹，然后选择&#x200B;**[!UICONTROL 属性]**。
      1. 在配置属性对话框中，启用&#x200B;**[!UICONTROL 云配置]**。
      1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置并退出对话框。

1. 为reCAPTCHA v2配置云服务。

   1. 在您的AEM创作实例上，转到![tools-1](assets/tools-1.png) > **Cloud Service**。
   1. 选择&#x200B;**[!UICONTROL reCAPTCHA]**。 此时将打开“配置”页面。 选择您创建的配置容器，然后选择&#x200B;**[!UICONTROL 创建]**。
   1. 将版本选择为[!DNL reCAPTCHA v2]，为reCAPTCHA服务（在步骤1中获取）指定名称、站点密钥和密钥，然后选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建云服务配置。
   1. 在“编辑组件”对话框中，指定在步骤1中获取的站点密钥和密钥。 选择&#x200B;**[!UICONTROL 保存设置]**，然后选择&#x200B;**确定**&#x200B;以完成配置。

   配置reCAPTCHA服务后，便可在自适应表单中使用。 有关详细信息，请参阅[在自适应表单中使用CAPTCHA](#using-reCAPTCHA)。

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## 在自适应表单中使用Google reCAPTCHA {#using-reCAPTCHA}

要在自适应表单中使用Google reCAPTCHA，请执行以下操作：

1. 在编辑模式下打开自适应表单。

   >[!NOTE]
   >
   >确保在创建自适应表单时选择的配置容器包含reCAPTCHA云服务。 您还可以编辑自适应表单属性，以更改与表单关联的配置容器。

1. 从组件浏览器中，将&#x200B;**Captcha**&#x200B;组件拖放到自适应表单上。

   >[!NOTE]
   >
   >* 不支持在自适应表单中使用多个验证码组件。 此外，不建议在标记为延迟加载的面板或片段中使用验证码。
   >* reCaptcha对时间敏感，大约会在几分钟后过期。 因此，建议在自适应表单中将Captcha组件放在提交按钮之前。

1. 选择您添加的Captcha组件，然后选择![cmppr](assets/cmppr.png)以编辑其属性。
1. 指定验证码小部件的标题。 默认值为&#x200B;**验证码**。 如果不想显示标题，请选择&#x200B;**隐藏标题**。
1. 从&#x200B;**Captcha服务**&#x200B;下拉列表中，选择&#x200B;**reCAPTCHA**&#x200B;以启用reCAPTCHA服务(如果您已按照Google的[reCAPTCHA服务](#google-reCAPTCHA)中的说明进行配置)。
1. 从&#x200B;**reCAPTCHA Enterprise**&#x200B;或&#x200B;**reCAPTCHA v2**&#x200B;的“设置”下拉列表中选择配置
   1. 如果您选择&#x200B;**reCAPTCHA Enterprise**&#x200B;版本，则密钥类型可以是&#x200B;**复选框**&#x200B;或基于&#x200B;**分数**，它基于您在为网站配置[站点密钥](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key)时的选择：

   >[!NOTE]
   >
   >* 在将&#x200B;**键类型**&#x200B;作为&#x200B;**复选框**&#x200B;的云配置中，如果验证码验证失败，自定义错误消息将显示为内联消息。
   >* 在&#x200B;**键类型**&#x200B;为&#x200B;**基于**&#x200B;分数的云配置中，如果验证码验证失败，自定义错误消息将显示为弹出消息。

   1. 你可以选择大小为&#x200B;**[!UICONTROL 普通]**&#x200B;和&#x200B;**[!UICONTROL 紧凑]**。
   1. 您可以选择&#x200B;**[!UICONTROL 绑定引用]**，在&#x200B;**[!UICONTROL 绑定引用]**&#x200B;中，提交的数据是绑定数据，否则是未绑定的数据。 以下是提交表单时未绑定数据和绑定数据（以SSN形式使用绑定引用）的XML示例。

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data>
                   <captcha16820607953761>
                       <captchaType>reCaptchaEnterprise</captchaType>
                       <captchaScore>0.9</captchaScore>
                   </captcha16820607953761>
               </data>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>371237912</SSN>
                       <FirstName>Sarah </FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608034928</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data/>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>
                           <captchaType>reCaptchaEnterprise</captchaType>
                           <captchaScore>0.9</captchaScore>
                       </SSN>
                       <FirstName>Sarah</FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608035111</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   如果您选择&#x200B;**reCAPTCHA v2**&#x200B;版本：
   1. 您可以为reCAPTCHA构件选择大小为&#x200B;**[!UICONTROL Normal]**&#x200B;或&#x200B;**[!UICONTROL Compact]**。
   1. 您可以选择&#x200B;**[!UICONTROL 不可见]**&#x200B;选项，以便仅在可疑活动的情况下显示验证码质询。

   已在自适应表单上启用reCAPTCHA服务。 您可以预览表单并查看验证码是否正常工作。 受reCAPTCHA保护的&#x200B;**徽章**将显示在受保护的表单上，如下所示。
   ![受reCAPTCHA徽章保护的Google](/help/forms/assets/google-recaptcha-v2.png)

1. 保存属性。

>[!NOTE]
> 
> 请勿从Captcha服务下拉列表中选择&#x200B;**[!UICONTROL Default]**，因为默认的AEM CAPTCHA服务已弃用。

>[!VIDEO](https://video.tv.adobe.com/v/3422641/recaptcha-google-adaptive-forms/?quality=12&learn=on)

### 根据规则显示或隐藏验证码组件 {#show-hide-captcha}

您可以选择根据您在自适应表单中组件上应用的规则来显示或隐藏CAPTCHA组件。 选择组件，选择![编辑规则](assets/edit-rules-icon.svg)，然后选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建规则。 有关创建规则的更多信息，请参阅[规则编辑器](rule-editor.md)。

例如，仅当表单中的“货币值”字段的值超过25000时，CAPTCHA组件才必须在自适应表单中显示。

选择表单中的&#x200B;**[!UICONTROL 货币值]**&#x200B;字段并创建以下规则：

![显示或隐藏规则](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> 当您选择reCAPTCHA v2配置并且大小设置为[!UICONTROL 不可见]时，显示/隐藏选项保持禁用状态。

### 验证验证码 {#validate-captcha}

您可以在提交表单时验证自适应表单中的验证码，也可以根据用户操作和条件进行验证码验证。

#### 在提交表单时验证验证码 {#validation-form-submission}

要在提交自适应表单时自动验证验证码，请执行以下操作：

1. 选择CAPTCHA组件并选择![cmppr](assets/configure-icon.svg)以查看组件属性。
1. 在&#x200B;**[!UICONTROL 验证验证码]**&#x200B;部分中，选择&#x200B;**[!UICONTROL 在提交表单时验证验证码]**。
1. 选择![完成](assets/save_icon.svg)以保存组件属性。

#### 在用户操作和条件上验证验证码 {#validate-captcha-user-action}

要根据条件和用户操作验证验证码，请执行以下操作：

1. 选择CAPTCHA组件并选择![cmppr](assets/configure-icon.svg)以查看组件属性。
1. 在&#x200B;**[!UICONTROL 验证CAPTCHA]**&#x200B;部分中，针对用户操作&#x200B;]**选择**[!UICONTROL &#x200B;验证CAPTCHA。
1. 选择![完成](assets/save_icon.svg)以保存组件属性。

[!DNL Experience Manager Forms]提供了`ValidateCAPTCHA` API以使用预定义条件验证验证码。 您可以使用自定义提交操作或通过定义自适应表单中组件的规则来调用API。

以下是使用预定义条件验证CAPTCHA的`ValidateCAPTCHA` API示例：

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

该示例表示`ValidateCAPTCHA` API仅在填写表单时用户指定的数字框中的数字位数大于5时才验证表单中的验证码。

**选项1：使用[!DNL Experience Manager Forms] ValidateCAPTCHA API通过自定义提交操作来验证CAPTCHA**

执行以下步骤，使用`ValidateCAPTCHA` API通过自定义提交操作验证验证码：

1. 将包含`ValidateCAPTCHA` API的脚本添加到自定义提交操作。 有关自定义提交操作的详细信息，请参阅[为自适应Forms创建自定义提交操作](custom-submit-action-form.md)。
1. 从自适应表单的&#x200B;**[!UICONTROL 提交]**&#x200B;属性中的&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择自定义提交操作的名称。
1. 选择&#x200B;**[!UICONTROL 提交]**。 根据自定义提交操作的`ValidateCAPTCHA` API中定义的条件验证验证码。

**选项2：在提交表单**&#x200B;之前，使用[!DNL Experience Manager Forms] ValidateCAPTCHA API在用户操作中验证验证码

您还可以通过对自适应表单中的组件应用规则来调用`ValidateCAPTCHA` API。

例如，您在自适应表单中添加了&#x200B;**[!UICONTROL 验证CAPTCHA]**&#x200B;按钮，并创建了一个规则以在单击按钮时调用服务。

下图说明了如何通过单击&#x200B;**[!UICONTROL 验证CAPTCHA]**&#x200B;按钮调用服务：

![验证验证码](assets/captcha-validation1.gif)

您可以使用规则编辑器调用包含`ValidateCAPTCHA` API的自定义servlet，并根据验证结果启用或禁用自适应表单的提交按钮。

同样，您可以使用规则编辑器在自适应表单中包含用于验证验证码的自定义方法。

<!--

### Add custom CAPTCHA services {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. However, you can add a custom service to display in the **[!UICONTROL CAPTCHA Service]** drop-down list.  

The following is a sample implementation of the interface to add additional CAPTCHA service to your Adaptive Form:

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

`captchaPropertyNodePath` refers to the resource path of the CAPTCHA component in the Sling repository. Use this property to include details specific to the CAPTCHA component. For example, `captchaPropertyNodePath` includes information for the reCAPTCHA cloud configuration configured on the CAPTCHA component. The cloud configuration information provides **[!UICONTROL Site Key]** and **[!UICONTROL Secret Key]** settings for implementing the reCAPTCHA service.

`userResponseToken` refers to the `g_recaptcha_response` that gets generated after solving a CAPTCHA in a form. -->

### 编辑reCAPTCHA服务域 {#reCAPTCHA-service-domain}

reCAPTCHA服务使用`https://www.recaptcha.net/`作为默认域。 您可以修改设置以设置`https://www.google.com/`或任何自定义域名，以便加载、渲染和验证reCAPTCHA服务。

设置&#x200B;**[!UICONTROL 自适应表单和交互式通信Web渠道配置]**&#x200B;的&#x200B;**[!UICONTROL af.cloudservices.recaptcha.domain]**&#x200B;属性以指定`https://www.google.com/`或任何其他自定义域名。 以下JSON文件显示了一个示例：

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hans#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hans#deployment-process)。

## 另请参阅 {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Reference Themes, Templates, and Form Data models for Adaptive Forms](/help/forms/reference-themes-templates-data-models.md)

-->
