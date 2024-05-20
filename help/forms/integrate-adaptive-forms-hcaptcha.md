---
title: 如何在AEM自适应表单中使用hCaptcha®？
description: 通过hCaptcha®服务轻松增强表单安全性。 内部分步指南！
topic-tags: Adaptive Forms, author
keywords: Captcha®服务，自适应Forms， CAPTCHA挑战，机器人防护，表单提交安全，表单垃圾邮件防护
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
source-git-commit: a8a31bae0f937aa8941d258af648d6be030a9fac
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 1%

---


# 使用hCaptcha连接AEM Forms环境® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"> 此功能属于早期采用者计划。 您可以从官方电子邮件ID写信到aem-forms-ea@adobe.com ，加入率先采用者计划并请求获取该功能的访问权限。 </span>

hCaptcha®服务可保护您的表单免遭机器人、垃圾邮件和自动滥用。 它会发起复选框构件质询并评估用户响应，以确定是人类还是机器人与表单交互。 它可防止用户在测试失败时继续操作，并通过阻止机器人发送垃圾邮件或恶意活动来帮助确保在线交易的安全。

<!-- ![hCaptcha®](assets/hCaptcha®-challenge.png)-->

AEM Formsas a Cloud Service支持自适应Forms中的hCaptcha®。 您可以用它来在提交表单时向用户显示复选框构件质询。

## 将AEM Forms环境与hCaptcha集成的先决条件® {#prerequisite}

要使用AEM Forms配置hCaptcha®，您需要获取 [验证码®站点密钥和密钥](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) 来自hCaptcha®网站。

## 配置hCaptcha的步骤® {#steps-to-configure-hcaptcha}

1. 在您的AEM Formsas a Cloud Service环境中创建配置容器。 配置容器包含用于将AEM连接到外部服务的云配置。 要创建并配置配置容器以使用hCaptcha连接AEM Forms环境，请执行以下操作®：
   1. 打开您的AEM Formsas a Cloud Service实例。
   1. 转到 **[!UICONTROL “工具”>“常规”>“配置浏览器”]**.
   1. 在配置浏览器中，您可以选择现有文件夹或创建文件夹。 您可以创建文件夹并为其启用云配置选项，也可以为现有文件夹启用云配置选项：

      * **创建文件夹并为其启用云配置选项**：
         1. 在配置浏览器中，单击 **[!UICONTROL 创建]**.
         1. 在创建配置对话框中，指定名称、标题，然后选择 **[!UICONTROL 云配置]** 选项。
         1. 单击&#x200B;**[!UICONTROL 创建]**。
      * 要为现有文件夹启用云配置选项，请执行以下操作：
         1. 在配置浏览器中，选择文件夹并选择 **[!UICONTROL 属性]**.
         1. 在配置属性对话框中，启用 **[!UICONTROL 云配置]**.
         1. 选择 **[!UICONTROL 保存并关闭]** 保存配置并退出对话框。

1. 配置Cloud Service：
   1. 在您的AEM创作实例上，转到 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** 并选择 **[!UICONTROL 验证码®]**.
      ![Ui中的hCaptcha®](assets/hcaptcha-in-ui.png)
   1. 选择已创建或已更新的配置容器，如上一节所述。 选择&#x200B;**[!UICONTROL 创建]**。
      ![配置验证码®](assets/config-hcaptcha.png)
   1. 指定 **[!UICONTROL 标题]**， **[!UICONTROL 名称]**， **[!UICONTROL 站点密钥]**、和 **[!UICONTROL 密钥]** 用于hCaptcha®服务 [在先决条件中获得](#prerequisite). 选择&#x200B;**[!UICONTROL 创建]**。

      ![配置Cloud Service以使用hCaptcha连接AEM Forms环境®](assets/create-hcaptcha-config.png)

>[!NOTE]
> 用户无需修改 [客户端JavaScript验证URL](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) 和 [服务器端验证URL](https://docs.hcaptcha.com/#verify-the-user-response-server-side) 因为它们已预先填充hCaptcha®验证。 对于某些国家/地区，端点可能会有所不同，请访问 [验证码®常见问题解答](https://docs.hcaptcha.com/faq#does-hcaptcha-support-access-by-users-in-china) 以了解更多信息。

配置hCAPTCHA服务后，便可在自适应表单中使用。

## 在自适应表单中使用hCaptcha®{#using-hCaptcha®-foundation-components}

1. 打开您的AEM Formsas a Cloud Service实例。
1. 转到 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择自适应表单并选择 **[!UICONTROL 属性]**. 对于 **[!UICONTROL 配置容器]** 选项，选择配置容器，其中包含使用hCaptcha®连接AEM Forms的云配置，然后选择 **[!UICONTROL 保存并关闭]**.

   如果您没有此类配置容器，请参阅部分 [使用hCaptcha连接AEM Forms环境®](#connect-your-forms-environment-with-hcaptcha-service) 以了解如何创建配置容器。

   ![选择配置容器](/help/forms/assets/captcha-properties.png)

1. 选择自适应表单并选择 **[!UICONTROL 编辑]**. 自适应表单在自适应Forms编辑器中打开。
1. 在组件浏览器中，拖放 **[!UICONTROL 验证码]** 自适应表单上的组件。
1. 选择 **[!UICONTROL 验证码]** 组件并单击属性 ![“属性”图标](assets/configure-icon.svg) 图标。 此时将打开“属性”对话框。

   ![替换文本](assets/hcaptcha-properties.png)

   指定以下属性：

   * **[!UICONTROL 标题]：** 指定验证码组件的标题，您可以在表单和规则编辑器中通过表单组件的唯一名称轻松识别表单组件。
   * **[!UICONTROL 验证消息]：** 在提交表单时提供验证码验证消息。
   * **[!UICONTROL 验证验证码]：** 您可以选择以下任一选项来验证验证码：
      * 在提交表单时
      * 在用户操作时。
   * **[!UICONTROL 验证码服务]：** 选择您的Captcha服务，在此选择hCaptcha®服务。
   * **[!UICONTROL 验证码配置]：** 选择为Captcha®配置的云配置。
     >[!NOTE]
     >出于类似目的，您的环境中可以有多个云配置。 所以，请仔细选择服务。 如果未列出任何服务，请参阅 [使用hCaptcha连接AEM Forms环境®](#connect-your-forms-environment-with-hcaptcha-service) 了解如何创建将AEM FormsCloud Service与hCaptcha®服务相连的环境。

   * **错误消息：** 提供在验证码提交失败时向用户显示的错误消息。
   * **验证码大小：** 选择hCaptcha®质询对话框的显示大小。 使用 **[!UICONTROL 紧凑]** 用于显示小尺寸和 **[!UICONTROL 普通]** 用于显示相对较大的hCaptcha®挑战对话框或 **[!UICONTROL 不可见]** 验证hCaptcha®，而无需在用户界面上显式呈现复选框小组件。

1. 选择&#x200B;**[!UICONTROL 完成]**。

现在，只有合法表单(表单填充程序成功清除hCaptcha®服务带来的挑战)才允许表单提交。

**hCaptcha®是Intuition Machines， Inc.的注册商标。**

## 常见问题解答

* **问：能否在自适应表单中使用多个Captcha组件？**
* **Ans：** 不支持在自适应表单中使用多个验证码组件。 此外，不建议在标记为延迟加载的片段或面板中使用验证码组件。

## 另请参阅 {#see-also}

{{see-also}}
