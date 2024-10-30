---
title: 如何在AEM自适应表单核心组件中使用Captcha&amp；reg；？
description: 使用 hCaptcha 服务轻松增强表单安全性。里面有分步指南！
topic-tags: Adaptive Forms, author
keywords: 验证码&amp；reg；服务，自适应Forms， CAPTCHA挑战，机器人预防，核心组件，表单提交安全性，表单垃圾邮件预防
feature: Adaptive Forms, Core Components
hide: true
hidefromtoc: true
exl-id: 6c559df2-7b6a-42fe-b44c-29a782570a0c
role: User, Developer
source-git-commit: bba5e5d283da616baa57b788181af73d59d86ee3
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 25%

---

# 使用hCaptcha连接AEM Forms环境® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview">此功能在早期采用者计划下。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

CAPTCHA（区分计算机和人类的完全自动化公共图灵测试）是一种在线交易中常用的程序，用于区分人类和自动化程序或机器人。它提出了一个挑战，并评估用户响应以确定是人还是机器人与网站交互。如果测试失败，它会阻止用户继续操作，并通过阻止机器人发布垃圾邮件或恶意目的来帮助确保在线交易的安全。

AEM Formsas a Cloud Service支持以下CAPTCHA解决方案：

* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [验证码](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

## 将AEM Forms环境与hCaptcha验证码集成

hCaptcha® 服务项目可保护您的表单免受机器人、垃圾邮件和自动滥用的侵害。它提出一个复选框小部件挑战，并评估用户响应以确定与表单交互的是人还是机器人。如果测试失败，它会阻止用户继续操作，并通过阻止机器人发布垃圾邮件或恶意活动来帮助确保在线交易的安全。

AEM Formsas a Cloud Service支持自适应Forms核心组件中的hCaptcha®。 您可以用它来在提交表单时显示复选框构件质询。

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### 将AEM Forms环境与hCaptcha集成的先决条件® {#prerequisite}

要使用AEM Forms配置hCaptcha®，您需要从hCaptcha®网站获取[hCaptcha®站点密钥和密钥](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key)。

### 配置验证码® {#steps-to-configure-hcaptcha}

要将AEM Forms与hCaptcha®服务集成，请执行以下步骤：

1. 在AEM Formsas a Cloud Service环境中创建配置容器。 配置容器包含用于将AEM连接到外部服务的云配置。 要创建并配置配置容器以使用hCaptcha连接AEM Forms环境，请执行以下操作®：
   1. 打开您的AEM Formsas a Cloud Service实例。
   1. 转到&#x200B;**[!UICONTROL 工具>常规>配置浏览器]**。
   1. 在配置浏览器中，您可以选择现有文件夹或创建文件夹。 您可以创建文件夹并为其启用云配置选项，也可以为现有文件夹启用云配置选项：

      * 要创建文件夹并为其启用云配置选项，请执行以下操作：
         1. 在配置浏览器中，单击&#x200B;**[!UICONTROL 创建]**。
         1. 在创建配置对话框中，指定名称、标题，然后选择&#x200B;**[!UICONTROL 云配置]**&#x200B;选项。
         1. 单击&#x200B;**[!UICONTROL 创建]**。
      * 要为现有文件夹启用云配置选项，请执行以下操作：
         1. 在配置浏览器中，选择文件夹，然后选择&#x200B;**[!UICONTROL 属性]**。
         1. 在配置属性对话框中，启用&#x200B;**[!UICONTROL 云配置]**。
         1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置并退出对话框。

1. 配置Cloud Service：
   1. 在您的AEM创作实例上，转到![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**&#x200B;并选择&#x200B;**[!UICONTROL hCaptcha®]**。
      ui中的![hCaptcha®](assets/hcaptcha-in-ui.png)
   1. 选择已创建或已更新的配置容器，如上一节所述。 选择&#x200B;**[!UICONTROL 创建]**。
      ![配置hCaptcha®](assets/config-hcaptcha.png)
   1. 指定在必备项](#prerequisite)中获取的hCaptcha®服务[的&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 名称]**、**[!UICONTROL 站点密钥]**&#x200B;和&#x200B;**[!UICONTROL 密钥]**。 选择&#x200B;**[!UICONTROL 创建]**。

      ![配置Cloud Service以使用hCaptcha连接AEM Forms环境®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > 用户无需修改[客户端JavaScript验证URL](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage)和[服务器端验证URL](https://docs.hcaptcha.com/#verify-the-user-response-server-side)，因为它们已预填充hCaptcha®验证。

   配置hCAPTCHA服务后，便可在基于核心组件的[自适应表单](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction)中使用。

## 在自适应Forms核心组件®0}中使用hCaptcha}{#using-hCaptcha®-core-components}

1. 打开您的AEM Formsas a Cloud Service实例。
1. 转到&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择自适应表单并选择&#x200B;**[!UICONTROL 属性]**。 对于&#x200B;**[!UICONTROL 配置容器]**&#x200B;选项，请选择包含将AEM Forms与hCaptcha连接的云配置的配置容器®并选择&#x200B;**[!UICONTROL 保存并关闭]**。

   如果您没有此类配置容器，请参阅[使用hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service)连接您的AEM Forms环境部分，以了解如何创建配置容器。

   ![选择配置容器](/help/forms/assets/captcha-properties.png)

1. 选择自适应表单并选择&#x200B;**[!UICONTROL 编辑]**。 自适应表单在自适应Forms编辑器中打开。
1. 从组件浏览器中，拖放&#x200B;**[!UICONTROL 自适应表单hCaptcha®]**&#x200B;组件或将其添加到自适应表单上。
1. 选择&#x200B;**[!UICONTROL 自适应表单hCaptcha®]**&#x200B;组件并单击属性![属性图标](assets/configure-icon.svg)图标。 此时将打开“属性”对话框。 指定以下属性：

   ![hCaptcha® v2](assets/config-hcaptcha-v2.png)

   * **[!UICONTROL 名称]：**&#x200B;指定验证码组件的名称，您可以在表单和规则编辑器中使用表单组件的唯一名称轻松识别表单组件。
   * **[!UICONTROL 标题]：**&#x200B;指定验证码组件的标题。
   * **[!UICONTROL 配置设置]：** 选择为 hCaptcha® 配置的云配置。
   * **验证码大小：**&#x200B;您可以选择hCaptcha®质询对话框的显示大小。 使用 **[!UICONTROL 紧凑]** 选项显示小尺寸，使用 **[!UICONTROL 正常]** 选项显示相对大尺寸的 hCaptcha® 挑战对话框。<!-- or **[!UICONTROL Invisible]** to validate hCaptcha&reg; without explicitly rendering the checkbox widget on the user interface. -->
   * **[!UICONTROL 验证消息]：**&#x200B;为表单提交时的验证码验证提供验证消息。
   * **[!UICONTROL 脚本验证消息]** - 通过此选项，可输入如果脚本验证失败，所显示的消息。
     >[!NOTE]
     >出于类似目的，您的环境中可以有多个云配置。 所以，请仔细选择服务。 如果未列出任何服务，请参阅[使用hCaptcha®连接您的AEM Forms环境](#connect-your-forms-environment-with-hcaptcha-service)，了解如何创建将AEM Forms环境与hCaptcha®服务连接的Cloud Service。
     <!--* **Error Message:** Provide the error message to display to the user when the Captcha submission fails.-->

1. 选择&#x200B;**[!UICONTROL 完成]**。


现在，只有合法表单(表单填充程序成功清除hCaptcha®服务带来的挑战)才允许表单提交。 hCaptcha®

**hCaptcha® 是 Intuition Machines, Inc. 的注册商标。**


## 常见问题解答

* **问：能否在自适应表单中使用多个Captcha组件？**
* 不支持在自适应表单中使用多个Captcha组件的&#x200B;**Ans：**。 此外，不建议在标记为延迟加载的片段或面板中使用验证码组件。

## 另请参阅 {#see-also}

{{see-also}}
