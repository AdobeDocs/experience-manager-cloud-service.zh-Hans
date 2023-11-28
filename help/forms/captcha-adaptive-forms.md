---
title: 如何在自适应Forms中使用CAPTCHA？
description: 了解如何为自适应表单配置或Google reCAPTCHA服务。
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: 9e06c115af2a262859d39bcd5ee0016df2475591
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 10%

---


# 在自适应Forms中使用reCAPTCHA {#using-reCAPTCHA-in-adaptive-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/creating-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html) |
| AEM as a Cloud Service | 本文 |
| 应用到 | 基于基础组件的自适应表单。 <br> 对于基于核心组件的自适应表单， [单击此处](/help/forms/captcha-adaptive-forms-core-components.md). |


CAPTCHA（区分计算机和人类的完全自动化公共图灵测试）是一种在线交易中常用的程序，用于区分人类和自动化程序或机器人。它提出了一个挑战，并评估用户响应以确定是人还是机器人与网站交互。如果测试失败，它会阻止用户继续操作，并通过阻止机器人发布垃圾邮件或恶意目的来帮助确保在线交易的安全。

[!DNL AEM Forms] 在自适应Forms中支持reCAPTCHA 。 您可以使用Google的reCAPTCHA服务来实施CAPTCHA。

>[!NOTE]
>
>* [!DNL AEM Forms] 支持reCaptcha v2和reCaptcha Enterprise。 不支持任何其他版本。
>* 上的离线模式不支持自适应Forms中的reCAPTCHA [!DNL AEM Forms] 应用程序。
>

## 通过Google配置reCAPTCHA服务 {#google-reCAPTCHA}

表单作者可以使用Google的reCAPTCHA服务在自适应Forms中实施reCAPTCHA。 它提供高级验证码功能以保护您的站点。 有关reCAPTCHA工作方式的更多信息，请参阅 [Google reCAPTCHA](https://developers.google.com/recaptcha/). reCAPTCHA服务包括 [!DNL reCAPTCHA v2] 和 [!DNL reCAPTCHA Enterprise] 您可以将集成到 [!DNL AEM Forms]. 根据要求，您可以配置reCAPTCHA服务以启用：

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [AEM Forms中的reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [AEM Forms中的reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)


### 配置reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. 创建或选择 [Google云项目](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) 并启用 [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. 获取 [项目编号](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) 并创建 [API密钥](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) 和 [网站的站点密钥](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. 为云服务创建配置容器。

   1. 转到 **[!UICONTROL “工具”>“常规”>“配置浏览器”]**.
   1. 选择文件夹或创建文件夹，然后使用以下步骤启用云配置的文件夹：
      1. 在配置浏览器中，选择文件夹并点按 **[!UICONTROL 属性]**.
      1. 在配置属性对话框中，启用 **[!UICONTROL 云配置]**.
      1. 点按 **[!UICONTROL 保存并关闭]** 保存配置并退出对话框。

1. 配置云服务 [!DNL reCAPTCHA Enterprise].

   1. 在您的Experience Manager创作实例上，转到 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**.
   1. 点按 **[!UICONTROL reCAPTCHA]**. 此时将打开“配置”页面。 选择您创建的配置容器并点击 **[!UICONTROL 创建]**.
   1. 选择版本为 [!DNL reCAPTCHA Enterprise] 并指定reCAPTCHA Enterprise服务的名称、项目ID、站点密钥和API密钥（在步骤2中获取）。
   1. 选择密钥类型，密钥类型应与您在中配置的站点密钥相同 [Google云项目](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin)例如， **复选框站点键** 或 **基于得分的网站密钥**.
   1. 指定 [阈值分数在0到1之间](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores). 分数大于或等于阈值分数标识人交互，否则被视为机器人交互。
   1. 点按 **[!UICONTROL 创建]** 以创建云服务配置。

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Tap **[!UICONTROL Save Settings]** and then tap **[!UICONTROL OK]** to complete the configuration.
-->

reCAPTCHA Enterprise服务一旦启用，就可用于自适应表单。 请参阅 [在自适应表单中使用CAPTCHA](#using-reCAPTCHA).

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->

### 配置Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. 获取 [reCAPTCHA API密钥对](https://www.google.com/recaptcha/admin) 来自Google的。 它包括 **站点密钥** 和 **密钥**.
1. 为云服务创建配置容器。
   1. 转到 **[!UICONTROL “工具”>“常规”>“配置浏览器”]**.
   1. 选择文件夹或创建文件夹，然后使用以下步骤启用云配置的文件夹：
      1. 在配置浏览器中，选择文件夹并点按 **[!UICONTROL 属性]**.
      1. 在配置属性对话框中，启用 **[!UICONTROL 云配置]**.
      1. 点按 **[!UICONTROL 保存并关闭]** 保存配置并退出对话框。

1. 为reCAPTCHA v2配置云服务。

   1. 在您的AEM创作实例上，转到 ![tools-1](assets/tools-1.png) > **Cloud Service**.
   1. 点按 **[!UICONTROL reCAPTCHA]**. 此时将打开“配置”页面。 选择您创建的配置容器并点击 **[!UICONTROL 创建]**.
   1. 选择版本为 [!DNL reCAPTCHA v2] ，指定reCAPTCHA服务（在步骤1中获取）的名称、站点密钥和密钥，然后点击 **[!UICONTROL 创建]** 以创建云服务配置。
   1. 在“编辑组件”对话框中，指定在步骤1中获取的站点密钥和密钥。 点按 **[!UICONTROL 保存设置]** 然后点击 **确定** 以完成配置。

   配置reCAPTCHA服务后，便可在自适应表单中使用。 有关更多信息，请参阅 [在自适应表单中使用CAPTCHA](#using-reCAPTCHA).

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## 在自适应表单中使用reCAPTCHA {#using-reCAPTCHA}

要在自适应表单中使用reCAPTCHA，请执行以下操作：

1. 在编辑模式下打开自适应表单。

   >[!NOTE]
   >
   >确保在创建自适应表单时选择的配置容器包含reCAPTCHA云服务。 您还可以编辑自适应表单属性，以更改与表单关联的配置容器。

1. 在组件浏览器中，拖放 **验证码** 组件到自适应表单上。

   >[!NOTE]
   >
   >* 不支持在自适应表单中使用多个验证码组件。 此外，不建议在标记为延迟加载的面板或片段中使用验证码。
   >* reCaptcha对时间敏感，大约会在几分钟后过期。 因此，建议在自适应表单中将Captcha组件放在提交按钮之前。

1. 选择您添加并点按的Captcha组件 ![cmppr](assets/cmppr.png) 以编辑其属性。
1. 指定验证码小部件的标题。 默认值为 **验证码**. 选择 **隐藏标题** 如果您不希望显示标题。
1. 从 **验证码服务** 下拉列表，选择 **reCAPTCHA** 以启用reCAPTCHA服务（如果已按照中的说明进行了配置） [Google提供的reCAPTCHA服务](#google-reCAPTCHA).
1. 从设置下拉列表中选择配置 **reCAPTCHA Enterprise** 或 **reCAPTCHA v2**
   1. 如果您选择 **reCAPTCHA Enterprise** 版本，键类型可以是 **复选框** 或 **基于得分**，它基于您在配置时的选择 [网站的站点密钥](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key)：

   >[!NOTE]
   >
   >* 在云配置中，使用 **键类型** 作为 **复选框**，则在验证码验证失败时，自定义错误消息将作为内联消息显示。
   >* 在云配置中，使用 **键类型** 作为 **基于得分**，则在验证码验证失败时，自定义的错误消息将作为弹出消息显示。

   1. 您可以选择大小为 **[!UICONTROL 普通]** 和 **[!UICONTROL 紧凑]**.
   1. 您可以选择 **[!UICONTROL 绑定引用]**，位于 **[!UICONTROL 绑定引用]** 提交的数据是绑定的数据，否则它是未绑定的数据。 以下是提交表单时未绑定数据和绑定数据（以SSN形式使用绑定引用）的XML示例。

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

   如果您选择 **reCAPTCHA v2** 版本：
   1. 您可以选择大小为 **[!UICONTROL 普通]** 或 **[!UICONTROL 紧凑]** 用于reCAPTCHA构件。
   1. 您可以选择 **[!UICONTROL 不可见]** 选项，用于仅在可疑活动的情况下显示CAPTCHA挑战。

   已在自适应表单上启用reCAPTCHA服务。 您可以预览表单并查看验证码是否正常工作。 此 **受reCAPTCHA保护** 徽章（如下所示）显示在受保护的表单上。
   ![Google受reCAPTCHA徽章保护](/help/forms/assets/google-recaptcha-v2.png)

1. 保存属性。

>[!NOTE]
> 
> 不选择 **[!UICONTROL 默认]** 从“验证码服务”下拉列表中，默认的AEM CAPTCHA服务已弃用。

>[!VIDEO](https://video.tv.adobe.com/v/3422641/recaptcha-google-adaptive-forms/?quality=12&learn=on)

### 根据规则显示或隐藏验证码组件 {#show-hide-captcha}

您可以选择根据您在自适应表单中组件上应用的规则来显示或隐藏CAPTCHA组件。 点按组件，选择 ![编辑规则](assets/edit-rules-icon.svg)，然后点击 **[!UICONTROL 创建]** 以创建规则。 有关创建规则的更多信息，请参阅 [规则编辑器](rule-editor.md).

例如，仅当表单中的“货币值”字段的值超过25000时，CAPTCHA组件才必须在自适应表单中显示。

点按 **[!UICONTROL 货币值]** 字段，并创建以下规则：

![显示或隐藏规则](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> 当您选择reCAPTCHA v2配置并且大小被设置为 [!UICONTROL 不可见]，显示/隐藏选项仍保持禁用状态。

### 验证验证码 {#validate-captcha}

您可以在提交表单时验证自适应表单中的验证码，也可以根据用户操作和条件进行验证码验证。

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

[!DNL Experience Manager Forms] 提供 `ValidateCAPTCHA` 用于使用预定义条件验证验证码的API。 您可以使用自定义提交操作或通过定义自适应表单中组件的规则来调用API。

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

此示例表示 `ValidateCAPTCHA` 仅当用户在填写表单时指定的数字框中的数字位数大于5时，API才会验证表单中的验证码。

**选项1：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API使用自定义提交操作验证CAPTCHA**

执行以下步骤以使用 `ValidateCAPTCHA` 使用自定义提交操作验证验证码的API：

1. 添加脚本以包含 `ValidateCAPTCHA` 用于自定义提交操作的API。 有关自定义提交操作的更多信息，请参阅 [创建自适应Forms的自定义提交操作](custom-submit-action-form.md).
1. 从中选择自定义提交操作的名称 **[!UICONTROL 提交操作]** 中的下拉列表 **[!UICONTROL 提交]** 自适应表单的属性。
1. 点按 **[!UICONTROL 提交]**. 系统会根据中定义的条件验证验证码 `ValidateCAPTCHA` 自定义提交操作的API。

**选项2：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API用于在提交表单之前在用户操作中验证CAPTCHA**

您还可以调用 `ValidateCAPTCHA` API，方法是对自适应表单中的组件应用规则。

例如，您添加 **[!UICONTROL 验证验证码]** 按钮，并创建规则以在单击按钮时调用服务。

下图说明了在单击服务时调用服务的方式 **[!UICONTROL 验证验证码]** 按钮：

![验证验证码](assets/captcha-validation1.gif)

您可以调用自定义servlet，其中包含 `ValidateCAPTCHA` 使用规则编辑器的API，并根据验证结果启用或禁用自适应表单的提交按钮。

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

reCAPTCHA服务使用 `https://www.recaptcha.net/` 作为默认域。 您可以修改要设置的设置 `https://www.google.com/` 或任何用于加载、渲染和验证reCAPTCHA服务的自定义域名。

设置 **[!UICONTROL af.cloudservices.recaptcha.domain]** 的属性 **[!UICONTROL 自适应表单和交互式通信Web渠道配置]** 要指定的配置 `https://www.google.com/` 或任何其他自定义域名。 以下JSON文件显示了一个示例：

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
