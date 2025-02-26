---
title: 将 reCAPTCHA 与 AEM Forms as a Cloud Service 的 Edge Delivery Services 结合使用
description: 在适用于 AEM Forms 的 Edge Delivery Services 的表单中使用 Google reCAPTCHA
feature: Edge Delivery Services
keywords: 表单中的 reCAPTCHA，在通用编辑器中使用 reCAPTCHA，在表单中添加 reCAPTCHA
role: Admin, Architect, Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 96%

---


# 在所见即所得创作中使用 reCAPTCHA

<span class="preview">此功能可通过提前访问计划使用。 要请求访问，请将您的正式地址中的电子邮件发送至<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，其中包含您的GitHub组织名称和存储库名称。 例如，如果存储库URL为https://github.com/adobe/abc，则组织名称为adobe，存储库名称为abc。</span>


CAPTCHA（全自动区分计算机和人类的公共图灵测试）是一种常用工具，用于保护网站免受欺诈活动、垃圾邮件和滥用的攻击。

例如，考虑一个根据额外扣除和税率计算税款的表单。在这种情况下，存在恶意用户利用该表单发送网络钓鱼电子邮件或使用垃圾邮件机器人向其中发送不相关或有害内容的风险。集成 CAPTCHA 可验证提交内容是否来自真实用户，从而提供额外的安全性，有效减少垃圾邮件条目。

![Google reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

在 Edge Delivery Services Forms 中，通过 Form Block 您可以使用 **CAPTCHA（不可见）**&#x200B;组件将 [Google reCAPTCHA 与表单连接起来](#connect-forms-with-recaptcha-service-by-google)，以区分人类和机器人。该功能可帮助作者保护其表单免受垃圾邮件和滥用的攻击。

## 通过 Google 将 Forms 与 reCAPTCHA 服务连接起来

您可以通过创作 Edge Delivery Services Forms 来实施 Google 提供的 reCAPTCHA 服务。您可以根据需要为 Edge Delivery Services Forms 配置以下一项 reCAPTCHA 服务：

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> 有关 reCAPTCHA 如何运作的更多信息，请参阅 [Google reCAPTCHA](https://developers.google.com/recaptcha/)。

### 配置 reCAPTCHA Enterprise

reCAPTCHA Enterprise 是 Google 提供的高级企业级欺诈检测和预防服务。它建立在 reCAPTCHA（基于分数）的基础上，但提供了更多的功能、可扩展性和定制性，以满足企业的复杂需求。

#### 开始之前

在为 Edge Delivery Services Forms 配置 Google reCAPTCHA Enterprise 之前，请确保您已完成以下步骤：

1. 创建或选择一个 [Google Cloud 项目](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin)，并检索[项目 ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed)。

1. 为 Google Cloud 项目[启用 reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api)，并[创建 API 密钥](https://console.cloud.google.com/apis/credentials)。

1. 为 Google Cloud 项目创建[网站密钥](https://console.cloud.google.com/security/recaptcha)，并复制网站密钥。

获得这些凭据后，您可以继续为表单配置 reCAPTCHA Enterprise：

1. [创建云配置容器](#1-create-cloud-configuration-container)
1. [为 reCAPTCHA Enterprise 创建云服务配置](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1. 创建云配置容器

要创建云配置容器，请执行以下步骤：

1. 登录作者实例。
1. 转到&#x200B;**[!UICONTROL 工具]** ![工具 -1](/help/forms/assets/tools-1.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**。

   ![云配置容器](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中，导航到您的表单并选择&#x200B;**[!UICONTROL 属性]**。

   ![云配置属性](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. 在&#x200B;**[!UICONTROL 配置属性]**&#x200B;对话框中，启用&#x200B;**[!UICONTROL 云配置]**。

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**，以保存配置并退出对话框。

   ![启用云配置属性](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
`
创建云配置容器后，将其发布。

   ![发布云配置](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. 为 reCAPTCHA Enterprise 创建云服务配置

要为 reCAPTCHA Enterprise 创建云服务配置，请执行以下步骤：

1. 登录作者实例。
1. 导航到&#x200B;**[!UICONTROL 工具]** ![工具 -1](/help/forms/assets/tools-1.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL reCAPTCHA]**。

   ![reCAPTCHA 云配置](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   **配置**&#x200B;对话框打开。

1. 导航到您的表单并选择&#x200B;**[!UICONTROL 创建]**。

   ![CAPTCHA 配置](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   **[!UICONTROL 创建 reCAPTCHA 配置]**&#x200B;对话框打开。

   ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. 选择版本为 [!DNL ReCAPTCHA Enterprise]，并指定标题、名称、项目 ID、Site 密钥和 API 密钥。

   >[!NOTE]
   >
   > 您可以从[开始之前](#before-you-start)分区获取 reCAPTCHA Enterprise 的项目 ID、Site 密钥和 API 密钥。

1. 选择&#x200B;**[!UICONTROL 密钥类型]**&#x200B;作为&#x200B;**基于分数的 Site 密钥**。
1. 指定[ 0 到 1 范围内的阈值分数](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores)。大于或等于阈值分数可识别为人机交互，否则将视为机器人交互。
1. 选择&#x200B;**[!UICONTROL 创建]**，创建云服务配置。

   创建 reCAPTCHA 云配置后，将其发布。

   ![创建 reCAPTCHA 配置](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

您现在可以创建或编辑表单，并使用所见即所得的创作方式添加 reCAPTCHA 组件。有关将 Google reCAPTCHA 集成到表单的详细说明，请参阅[在表单中使用 reCAPTCHA](#use-recaptcha-in-your-form)。

## 配置 reCAPTCHA

reCAPTCHA 是 Google 提供的一项免费服务，可帮助网站检测和防止滥用流量，包括机器人和垃圾邮件。它支持基于分数的版本，可在后台运行，并为每次用户交互分配一个风险分数（从 0.0 到 1.0）。大于或等于阈值分数可识别为人机交互，否则将视为机器人交互。

#### 开始之前

在为 Edge Delivery Services Forms 配置 Google reCAPTCHA 之前，请从 Google Console 检索 [reCAPTCHA API 密钥对](https://www.google.com/recaptcha/admin)。这对密钥包括一个 Site 密钥和一个密钥。

>[!NOTE]
>
> * Edge Delivery Services Forms 仅支持&#x200B;**基于 reCAPTCHA 分数**&#x200B;的版本。

获得 API 密钥对后，您可以继续为表单配置 reCAPTCHA：

1. [创建云配置容器](#1-create-cloud-configuration-container-1)
1. [为 reCAPTCHA 创建云服务配置](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1. 创建云配置容器

要创建云配置容器，请执行以下步骤：

1. 登录作者实例。
1. 转到&#x200B;**[!UICONTROL 工具]** ![工具 -1](/help/forms/assets/tools-1.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**。

   ![云配置容器](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中，导航到您的表单并选择&#x200B;**[!UICONTROL 属性]**。

   ![云配置属性](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. 在&#x200B;**[!UICONTROL 配置属性]**&#x200B;对话框中，启用&#x200B;**[!UICONTROL 云配置]**。

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**，以保存配置并退出对话框。

   ![启用云配置属性](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   创建云配置容器后，将其发布。

   ![发布云配置](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. 为 reCAPTCHA 创建云服务配置

要为 reCAPTCHA 创建云服务配置，请执行以下步骤：

1. 登录作者实例。
1. 导航到&#x200B;**[!UICONTROL 工具]** ![工具 -1](/help/forms/assets/tools-1.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL reCAPTCHA]**。

   ![reCAPTCHA 云配置](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   **配置**&#x200B;对话框打开。

1. 导航到您的表单并选择&#x200B;**[!UICONTROL 创建]**。

   ![CAPTCHA 配置](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   **[!UICONTROL 创建 reCAPTCHA 配置]**&#x200B;对话框打开。

   ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. 选择版本为 [!DNL ReCAPTCHA v2]，并指定标题和名称。
1. 指定 Site 密钥和密钥。

   >[!NOTE]
   >
   > 您可以从[开始之前](#before-you-begin)分区获取 reCAPTCHA 的 Site 密钥和密钥。

1. 选择&#x200B;**[!UICONTROL 创建]**，创建云服务配置。

   创建 reCAPTCHA 云配置后，将其发布。

   ![创建 reCAPTCHA 配置](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

您现在可以创建和编辑表单，并使用所见即所得的创作方式添加 reCAPTCHA 组件。有关将 Google reCAPTCHA 集成到表单的详细说明，请参阅[在表单中使用 reCAPTCHA](#use-recaptcha-in-your-form)。

### 在表单中使用 reCAPTCHA

要创作表单并添加 reCAPTCHA（不可见）组件，请执行以下步骤：

1. 在通用编辑器中打开表单进行编辑。
1. 导航到内容树中已添加的自适应表单分区。
1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标，然后从&#x200B;**自适应表单组件**&#x200B;列表中添加 **[!UICONTROL CAPTCHA（不可见）]**&#x200B;组件。

   ![添加 reCAPTCHA 组件](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   您还可以拖放所需的自适应表单组件，因为通用编辑器提供了直观的拖放功能。

1. 添加 **[!UICONTROL CAPTCHA（不可见）]**&#x200B;组件后，单击&#x200B;**发布**&#x200B;再次发布表单。

   ![重新发布表单](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

您现在可以通过以下 URL 使用 reCAPTCHA 服务查看表单：
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`。

![使用 reCAPTCHA 查看表单](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## 常见问题解答

* **如果用户没有创建 reCAPTCHA 云配置会怎样？**

  **答**：如果用户没有创建 reCAPTCHA 云配置，AEM 服务器会在全局配置容器中搜索 reCAPTCHA 云配置。如果全局配置容器中不存在配置，AEM 服务器将抛出错误。

* **如果用户创建了多个 reCAPTCHA 云配置会怎样？**
  **答**：如果用户创建了多个 reCAPTCHA 云配置，系统会自动选择第一个创建的 reCAPTCHA 配置。

* **为什么在发布的 URL 上看不到修改或变更？**
如果在发布的 URL 上看不到修改或更改，请确保表单已应用了更新并重新发布。

* **Edge Delivery Services Forms 支持哪种 reCAPTCHA 服务？**
  **答**：Edge Delivery Services Forms 仅支持 Google 提供的基于分数的 reCAPTCHA 服务。


## 另请参阅

{{universal-editor-see-also}}

