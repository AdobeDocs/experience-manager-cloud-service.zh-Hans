---
title: 使用reCAPTCHA保护Forms — 可视化指南
description: 了解如何轻松地将Google reCAPTCHA添加到Edge Delivery Services表单以阻止垃圾邮件和机器人提交
feature: Edge Delivery Services
keywords: 表单中的reCAPTCHA，在通用编辑器中使用reCAPTCHA，在表单中添加reCAPTCHA，表单安全性，垃圾邮件保护
role: Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 1%

---


# 使用Google reCAPTCHA保护您的Forms免受垃圾邮件侵扰

<span class="preview">此功能可通过提前访问计划使用。 若要请求访问，请将您的正式地址中的电子邮件发送至<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，其中包含您的GitHub组织名称和存储库名称。</span>



## 为何要在表单中使用reCAPTCHA？

| ![安全性](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![机器人保护](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![用户体验](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **增强的安全性** | **机器人和垃圾邮件预防** | **无缝用户体验** |
| 保护表单免受欺诈活动和恶意攻击 | 阻止自动机器人向您的表单中添加不相关或有害的内容 | 不可见的reCAPTCHA可在后台工作，而不会中断合法用户 |

例如，具有敏感财务信息的税务计算表单需要防止滥用。 reCAPTCHA会验证提交内容是否来自正版用户，而不是自动系统。

## 选择您的reCAPTCHA解决方案

Edge Delivery Services Forms支持两个Google reCAPTCHA选项：

| ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/enterprise.svg) | ![reCAPTCHA Standard](/help/edge/docs/forms/universal-editor/assets/standard.svg) |
|:-------------:|:-------------:|
| [**reCAPTCHA Enterprise**](#set-up-recaptcha-enterprise) | [**reCAPTCHA Standard**](#set-up-recaptcha-standard) |
| 高级企业级欺诈检测，具有附加功能和定制功能 | 具有基于分数的检测功能的免费服务，在后台以不可见的方式运行 |
| 最适合：具有复杂安全需求的大型组织 | 最适合：具有基本保护需求的中小型项目 |

这两个选项都使用基于分数的检测（0.0到1.0）来识别人与机器人的交互，而不会中断用户体验。

## 设置reCAPTCHA Enterprise

### 步骤1：获取您的Google Cloud凭据

在配置reCAPTCHA Enterprise之前，您需要：

- [Google Cloud项目](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin)，其中包含您的[项目ID](https://support.google.com/googleapi/answer/7014113)
- 为您的项目启用了[reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api)
- 用于身份验证的[API密钥](https://console.cloud.google.com/apis/credentials)
- 您的域的[站点密钥](https://console.cloud.google.com/security/recaptcha)

### 步骤2：创建云配置容器

![逐步云配置设置](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. 登录到您的AEM创作实例
2. 导航到&#x200B;**工具** > **常规** > **配置浏览器**
3. 查找表单并选择&#x200B;**属性**
4. 在对话框中启用&#x200B;**云配置**
5. 保存并发布您的配置

### 步骤3：配置reCAPTCHA Enterprise Service

![reCAPTCHA Enterprise配置屏幕](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. 转到&#x200B;**工具** > **云服务** > **reCAPTCHA**
2. 导航到您的表单，然后单击&#x200B;**创建**
3. 在对话框中：
   - 选择&#x200B;**ReCAPTCHA Enterprise**&#x200B;版本
   - 输入标题和名称
   - 添加您的项目ID、站点密钥和API密钥
   - 选择&#x200B;**基于得分的网站密钥**&#x200B;作为密钥类型
   - 设置阈值分数(0-1)以区分人类和机器人
4. 单击&#x200B;**创建**&#x200B;并发布您的配置

## 设置reCAPTCHA Standard

### 步骤1：获取API密钥

开始之前，请从Google reCAPTCHA控制台[获取reCAPTCHA API密钥对](https://www.google.com/recaptcha/admin)（站点密钥和密钥）。

>[!IMPORTANT]
>
>Edge Delivery Services Forms 仅支持&#x200B;**基于 reCAPTCHA 分数**&#x200B;的版本。

### 步骤2：创建云配置容器

执行与企业版本中相同的步骤创建和发布云配置容器。

### 步骤3：配置reCAPTCHA标准服务

![reCAPTCHA标准配置屏幕](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. 转到&#x200B;**工具** > **云服务** > **reCAPTCHA**
2. 导航到您的表单，然后单击&#x200B;**创建**
3. 在对话框中：
   - 选择&#x200B;**ReCAPTCHA v2**&#x200B;版本
   - 输入标题和名称
   - 添加您的站点密钥和密钥
4. 单击&#x200B;**创建**&#x200B;并发布您的配置

## 将reCAPTCHA添加到表单

现在您已配置reCAPTCHA，是时候将其添加到表单中了：

![正在将reCAPTCHA组件添加到表单](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

1. 在通用编辑器中打开表单
2. 导航到内容树中的自适应表单部分
3. 单击&#x200B;**添加**&#x200B;图标并从自适应表单组件列表中选择&#x200B;**Captcha（不可见）**
   - *或者，将组件拖放到您的表单中*
4. 单击&#x200B;**发布**&#x200B;以更新具有reCAPTCHA保护的表单

您的表单现在已受保护！ 可在以下位置查看它：
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name>`

![已启用reCAPTCHA保护的表单](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## 验证reCAPTCHA集成

将reCAPTCHA添加到表单后，必须验证其是否正常工作。 下面是如何验证实施的：

### 视觉验证

虽然reCAPTCHA v2（基于分数）可隐式运行，但您可以通过以下方式确认其存在：

1. **检查页面源**：右键单击表单页面并选择“查看页面Source”
   - 查找包含您的站点密钥的reCAPTCHA脚本
   - 示例： `<script src="https://www.google.com/recaptcha/api.js?render=YOUR_SITE_KEY"></script>`

2. **检查网络请求**：使用浏览器开发人员工具(F12)
   - 提交您的表单并向`google.com/recaptcha`查找网络请求
   - 这些请求表示reCAPTCHA在您的表单中处于活动状态

### 功能测试

要验证reCAPTCHA是否确实在保护您的表单，请执行以下操作：

1. **正常提交测试**：
   - 使用有效数据填写表单
   - 以正常的人工步调提交表单
   - 验证表单是否已成功提交

2. **机器人样行为测试**：
   - 在无痕浏览/个人浏览窗口中打开表单
   - 极其快速地填写表单（类似自动的行为）
   - 连续快速提交多次
   - 如果reCAPTCHA运行正常，则可能会阻止或标记这些提交

3. **检查表单提交记录**：
   - 审查表单提交数据
   - 每次提交都应包含一个reCAPTCHA分数
   - 得分接近1.0表明可能是人类用户
   - 得分接近0.0表明潜在的机器人活动

### 使用Google reCAPTCHA管理控制台

对于企业用户，Google Cloud Console提供了详细的分析：

1. 转到[Google Cloud Console](https://console.cloud.google.com/)
2. 导航到&#x200B;**安全** > **reCAPTCHA**
3. 选择您的站点密钥
4. 查看评估图表和统计数据
5. 查找：
   - 流量模式
   - 得分分配
   - 潜在的欺诈活动

对于标准reCAPTCHA用户，[reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin/)中提供了基本统计信息。

### 调整实施

根据您的验证结果：

- 如果合法用户被阻止，请考虑降低阈值分数
- 如果您仍收到垃圾邮件，请考虑提高阈值分数
- 对于持续性问题，请检查reCAPTCHA配置并确保正确输入了所有密钥

请记住，reCAPTCHA会使用机器学习来随着时间的推移而改进，因此随着它学习您网站的流量模式，其有效性可能会提高。

## 故障排除和常见问题

| ![问题](/help/edge/docs/forms/universal-editor/assets/question.svg) | ![答案](/help/edge/docs/forms/universal-editor/assets/answer.svg) |
|:-------------:|:-------------:|
| **如果不创建reCAPTCHA配置该怎么办？** | 系统将在全局容器中查找配置。 如果不存在，您将收到一个错误。 |
| **如果我创建多个配置该怎么办？** | 系统会自动使用第一个创建的配置。 |
| **为什么我的更改在已发布的URL上不可见？** | 确保在进行更改后重新发布表单。 |
| **支持哪些reCAPTCHA服务？** | Edge Delivery Services Forms仅支持基于得分的reCAPTCHA服务。 |

## 后续步骤

现在您已使用reCAPTCHA保护您的表单：

- **验证您的实施**：按照[验证步骤](#-validating-your-recaptcha-integration)操作，以确保reCAPTCHA正常工作
- **监测性能**：定期检查Google reCAPTCHA仪表板是否有可疑活动和分数分布
- **微调设置**：根据您的安全需求和用户体验反馈调整阈值分数
- **保持更新**：通过Google的最新安全建议使reCAPTCHA实施保持最新
- **教育您的团队**：共享有关reCAPTCHA的工作方式以及如何解释分析的知识
- **收集反馈**：监视用户体验以确保合法用户不被阻止

请记住，有效的表单保护是一个需要定期监控和调整的持续过程。


