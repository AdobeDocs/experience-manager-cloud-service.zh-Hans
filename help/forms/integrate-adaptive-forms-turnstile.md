---
title: 如何在AEM自适应表单中使用Turnstile？
description: 使用Turnstile服务轻松增强表单安全性。 里面有分步指南！
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
exl-id: 644c351b-a167-4d18-8b99-b7cae6be48d5
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 12%

---

<span class="preview"> 此功能属于早期采用者计划。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

CAPTCHA（区分计算机和人类的完全自动化公共图灵测试）是一种在线交易中常用的程序，用于区分人类和自动化程序或机器人。它提出了一个挑战，并评估用户响应以确定是人还是机器人与网站交互。如果测试失败，它会阻止用户继续操作，并通过阻止机器人发布垃圾邮件或恶意目的来帮助确保在线交易的安全。

AEM Formsas a Cloud Service支持以下CAPTCHA解决方案：

* [Cloudflare Turnstile](#integrate-aem-forms-environment-with-turnstile-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms.md)
* [验证码](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## 将AEM Forms环境与Turnstile验证码集成

Cloudflare的Turnstile Captcha是一项安全措施，旨在保护表单和站点免受自动机器人、恶意攻击、垃圾邮件和不需要的自动流量的侵害。 在允许提交表单之前，它会在表单提交时显示一个复选框，以验证他们是人类。 AEM Formsas a Cloud Service支持自适应Forms核心组件中的Turnstile Captcha。

<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

### 将AEM Forms环境与Turnstile验证码集成的先决条件 {#prerequisite}

要为AEM Forms核心组件配置Turnstile，您需要获取 [转门锁站点密钥和密钥](https://developers.cloudflare.com/turnstile/get-started/) 从Turnstile的网站。

### 为AEM Forms配置Turnstile的步骤{#steps-to-configure-turnstile}

1. 在AEM Formsas a Cloud Service环境中创建配置容器。 配置容器包含用于将AEM连接到外部服务的云配置。 要创建并配置配置容器以将您的AEM Forms环境与Turnstile连接，请执行以下操作：
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
   1. 在您的AEM创作实例上，转到 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** 并选择 **[!UICONTROL Turnstile]**.
      ![Turnstile in ui](assets/turnstile-in-ui.png)
   1. 选择已创建或已更新的配置容器，如上一节所述。 选择&#x200B;**[!UICONTROL 创建]**。
      ![配置旋转门](assets/config-hcaptcha.png)
   1. 指定 **[!UICONTROL 构件类型]** 作为托管，构件类型可能会发生更改，具体取决于在先决条件中获得的键， **[!UICONTROL 标题]**， **[!UICONTROL 名称]**， **[!UICONTROL 站点密钥]**、和 **[!UICONTROL 密钥]** 用于Turnstile服务 [在先决条件中获得](#prerequisite). 选择&#x200B;**[!UICONTROL 创建]**。

      ![配置Cloud Service以将AEM Forms环境与Turnstile连接](assets/config-turntstile.png)

>[!NOTE]
> 用户无需修改客户端JavaScript验证URL和服务器端验证URL，因为它们已为Turnstile验证预先填充。

配置Turnstile Captcha服务后，便可在自适应表单中使用。

## 在自适应表单中使用 Turnstile{#using-turnstile-foundation-components}

1. 打开您的AEM Formsas a Cloud Service实例。
1. 转到 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择自适应表单并选择 **[!UICONTROL 属性]**. 对于 **[!UICONTROL 配置容器]** 选项，选择包含将AEM Forms与Turnstile连接的云配置的配置容器，然后选择 **[!UICONTROL 保存并关闭]**.

   如果您没有此类配置容器，请参阅部分 [将AEM Forms环境与Turnstile连接](#connect-your-forms-environment-with-turnstile-service) 以了解如何创建配置容器。

   ![选择配置容器](/help/forms/assets/captcha-properties.png)

1. 选择自适应表单并选择 **[!UICONTROL 编辑]**. 自适应表单在自适应Forms编辑器中打开。
1. 在组件浏览器中，拖放 **[!UICONTROL 验证码]** 自适应表单上的组件。
1. 选择 **[!UICONTROL 验证码]** 组件并单击属性 ![“属性”图标](assets/configure-icon.svg) 图标。 此时将打开“属性”对话框。

   ![设置](assets/turnstile-setting-v1.png)

   指定以下属性：

   * **[!UICONTROL 标题]：** 指定验证码组件的标题，您可以在表单和规则编辑器中通过表单组件的唯一名称轻松识别表单组件。
   * **[!UICONTROL 验证消息]：** 提供验证消息，用于验证表单提交中的验证码。
   * **[!UICONTROL 验证验证码]：** 您可以选择其中一个选项来验证验证码：
      * 在提交表单时
      * 在用户操作时。
   * **[!UICONTROL 验证码服务]：** 选择您的Captcha服务，在此选择Cloudfare Turnstile Captcha服务。
   * **[!UICONTROL 验证码配置]：** 选择为Turnstile配置的云配置。 例如，在此处，您选择 **托管密钥**.
     >[!NOTE]
     >出于类似目的，您的环境中可以有多个云配置。 所以，请仔细选择服务。 如果未列出任何服务，请参阅 [将AEM Forms环境与Turnstile连接](#connect-your-forms-environment-with-turnstile-service) 了解如何创建将AEM FormsCloud Service与Turnstile服务连接起来的环境。

   * **错误消息：** 提供在验证码提交失败时向用户显示的错误消息。
   * **验证码大小：** 选择Turnstile质询对话框的显示大小。 使用 **[!UICONTROL 紧凑]** 用于显示小尺寸和 **[!UICONTROL 普通]** 用于显示相对较大的Turnstile挑战对话框的选项。


     >[!NOTE]
     >这适用于小组件类型的受管和非交互式。 如果构件类型不可见，则不需要使用size属性，并且会禁用该属性。

1. 选择&#x200B;**[!UICONTROL 完成]**。

现在，只有合法的表单，表单填写者才能成功清除Turnstile服务带来的挑战，才能提交表单。

![Turnstile挑战](assets/turnstile-challenge.png)

## 常见问题解答

* **问：能否在自适应表单中使用多个Captcha组件？**
* **Ans：** 不支持在自适应表单中使用多个验证码组件。 此外，不建议在标记为延迟加载的片段或面板中使用验证码组件。

## 另请参阅 {#see-also}

{{see-also}}
