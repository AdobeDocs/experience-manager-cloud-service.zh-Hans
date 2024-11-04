---
title: 如何在AEM自适应表单中使用Google reCAPTCHA？
description: 使用Google reCAPTCHA服务可轻松增强表单安全性。 里面有分步指南！
topic-tags: Adaptive Forms, author
keywords: Google reCAPTCHA服务，自适应Forms， CAPTCHA挑战，机器人预防，核心组件，表单提交安全性，表单垃圾邮件预防
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: ec2f2a2951689ef20434ea6f531089502299bcb5
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 7%

---

# 在基于核心组件的AEM自适应表单中使用Google reCAPTCHA {#using-reCAPTCHA-in-adaptive-forms}

| 应用到 | 文章链接 |
| -------- | ---------------------------- |
| 基于核心组件的自适应表单 | 本文 |
| 基于Foundation组件的自适应表单 | [单击此处](/help/forms/captcha-adaptive-forms.md) |

CAPTCHA（区分计算机和人类的完全自动化公共图灵测试）是一种在线交易中常用的程序，用于区分人类和自动化程序或机器人。它提出了一个挑战，并评估用户响应以确定是人还是机器人与网站交互。如果测试失败，它会阻止用户继续操作，并通过阻止机器人发布垃圾邮件或恶意目的来帮助确保在线交易的安全。

AEM Formsas a Cloud Service支持以下CAPTCHA解决方案：

* [Google reCAPTCHA](#connect-your-aem-forms-environment-with-recaptcha-service-by-google)
* [验证码](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)


## 通过Google将AEM Forms核心组件与reCAPTCHA服务连接起来 {#connect-your-forms-environment-with-recaptcha-service-by-google}

表单作者可以使用Google的reCAPTCHA服务在自适应Forms中实施reCAPTCHA。 它提供高级验证码功能以保护您的站点。 有关reCAPTCHA工作方式的更多信息，请参阅[Google reCAPTCHA](https://developers.google.com/recaptcha/)。 您使用它在表单提交时提出验证码质询。[!DNL AEM Forms] as a [!DNL Cloud Service]支持Google reCAPTCHA v2和reCAPTCHA Enterprise。 不支持任何其他版本。 另请注意，自适应Forms中的reCAPTCHA在AEM Forms应用程序的离线模式下不受支持。

根据要求，您可以配置reCAPTCHA服务以启用：

* [reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms-core-components)
* [reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)

### 配置reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms-core-components}

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

   ![创建Google网站的Google reCAPTCHA配置以获取reCAPTCHA密钥](/help/forms/assets/google-captcha.gif)
1. 在AEM Formsas a Cloud Service环境中创建配置容器。 配置容器包含用于将AEM连接到外部服务的云配置。 要创建并配置配置容器以将您的AEM Forms环境与Google的reCAPTCHA服务连接，请执行以下操作：
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
         1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置并退出对话框。

1. 配置Cloud Service：
   1. 在您的AEM创作实例上，转到![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**&#x200B;并选择&#x200B;**[!UICONTROL reCAPTCHA]**。
   1. 选择在上一部分中创建或更新的配置容器。 选择&#x200B;**[!UICONTROL 创建]**。
   1. 指定reCAPTCHA服务的&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 名称]**、**[!UICONTROL 站点密钥]**&#x200B;和&#x200B;**[!UICONTROL 密钥]**（在步骤1中获取）。 选择&#x200B;**[!UICONTROL 创建]**。

   ![配置该Cloud Service以通过Google将您的AEM Forms环境连接到reCAPTCHA服务](/help/forms/assets/captcha-configuration.gif)

   配置reCAPTCHA服务后，便可在自适应表单中使用。 有关详细信息，请参阅[在自适应表单中使用Google reCAPTCHA](#using-reCAPTCHA)。


在自适应表单中使用Google reCAPTCHA

## 以自适应表单的形式使用 Google reCAPTCHA {#using-reCAPTCHA}

要在自适应Forms中使用reCAPTCHA，请执行以下操作：

1. 打开您的AEM Formsas a Cloud Service实例。
1. 转到&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择自适应Forms并选择&#x200B;**[!UICONTROL 属性]**。 对于&#x200B;**[!UICONTROL 配置容器]**&#x200B;选项，请选择包含通过Google将AEM Forms与reCAPTCHA服务连接的云配置的配置容器，然后选择&#x200B;**[!UICONTROL 保存并关闭]**。

   如果您没有此类配置容器，请参阅[通过Google的reCAPTCHA服务连接您的AEM Forms环境](#connect-your-forms-environment-with-recaptcha-service-by-google)部分，以了解如何创建此类配置容器。

   ![选择配置容器](/help/forms/assets/captcha-properties.png)

1. 选择自适应Forms并选择&#x200B;**[!UICONTROL 编辑]**。 自适应表单在自适应Forms编辑器中打开。
1. 从组件浏览器中，将&#x200B;**[!UICONTROL 自适应表单reCAPTCHA]**&#x200B;组件拖放到自适应表单上。

   >[!NOTE]
   > * Google reCAPTCHA验证对时间敏感，大约会在几分钟后过期。 因此，Adobe建议将&#x200B;**[!UICONTROL 自适应表单reCAPTCHA]**&#x200B;组件放在&#x200B;**[!UICONTROL Submit]**&#x200B;按钮之前。

1. 选择&#x200B;**[!UICONTROL 自适应表单reCAPTCHA]**&#x200B;组件并选择属性![属性图标](assets/configure-icon.svg)图标。 此时将打开“属性”对话框。 指定以下必需属性：
   * **[!UICONTROL 名称]：**&#x200B;您可以轻松地在表单和规则编辑器中使用表单组件的唯一名称来标识该表单组件，但名称不得包含空格或特殊字符。
   * **[!UICONTROL 标题]：**&#x200B;指定验证码小部件的标题。 默认值为&#x200B;**验证码**。 如果不想显示标题，请选择&#x200B;**隐藏标题**。 选择&#x200B;**允许标题**&#x200B;的富文本，以富文本格式编辑您的标题。 您还可以将标题标记为&#x200B;**未绑定的表单元素**。
   * **[!UICONTROL CAPTCHA配置]：**&#x200B;从&#x200B;**reCAPTCHA Enterprise**&#x200B;或&#x200B;**reCAPTCHA v2**&#x200B;的“设置”下拉列表中选择一个配置，以便显示表单的Google reCAPTCHA对话框：
      1. 如果您选择&#x200B;**reCAPTCHA Enterprise**&#x200B;版本，则密钥类型可以是&#x200B;**复选框**&#x200B;或基于&#x200B;**分数**，它基于您在为网站配置[站点密钥](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key)时的选择：
         >[!NOTE]
         >
         >* 在将&#x200B;**键类型**&#x200B;作为&#x200B;**复选框**&#x200B;的云配置中，如果验证码验证失败，自定义错误消息将显示为内联消息。
         >* 在&#x200B;**键类型**&#x200B;为&#x200B;**基于**&#x200B;分数的云配置中，如果验证码验证失败，自定义错误消息将显示为弹出消息。
      1. 你可以选择大小为&#x200B;**[!UICONTROL 普通]**&#x200B;和&#x200B;**[!UICONTROL 紧凑]**。

     >[!NOTE]
     >* 出于类似目的，您的环境中可以有多个云配置。 所以，请仔细选择服务。 如果未列出任何服务，请参阅[将您的AEM Forms环境与Google的reCAPTCHA服务连接](#connect-your-forms-environment-with-recaptcha-service-by-google)，了解如何创建将AEM Forms环境与Google的reCAPTCHA服务连接的Cloud Service。

   * **验证码大小：**&#x200B;您可以选择Google reCAPTCHA质询对话框的显示大小。 使用&#x200B;**[!UICONTROL 紧凑]**&#x200B;选项可显示小尺寸，使用&#x200B;**[!UICONTROL 普通]**选项可显示相对大尺寸的Google reCAPTCHA质询对话框。
如果您选择**reCAPTCHA v2**&#x200B;版本：
      1. 您可以为reCAPTCHA构件选择大小为&#x200B;**[!UICONTROL Normal]**&#x200B;或&#x200B;**[!UICONTROL Compact]**。
      1. 您可以选择&#x200B;**[!UICONTROL 不可见]**&#x200B;选项，以便仅在可疑活动的情况下显示验证码质询。

   已在自适应表单上启用reCAPTCHA服务。 您可以预览表单并查看验证码是否正常工作。 受reCAPTCHA保护的&#x200B;**徽章**&#x200B;将显示在受保护的表单上，如下所示。

   ![受reCAPTCHA徽章保护的Google](/help/forms/assets/google-recaptcha-v2.png)

1. 选择&#x200B;**[!UICONTROL 完成]**。

   现在，受reCAPTCHA保护的&#x200B;****&#x200B;显示在您的自适应表单上。 它显示在配置为使用Google reCAPTCHA服务的所有Adaptive Forms上。

   现在，只允许提交合法表单，在这些表单中，表单填充程序成功清除Google reCAPTCHA服务带来的挑战。

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