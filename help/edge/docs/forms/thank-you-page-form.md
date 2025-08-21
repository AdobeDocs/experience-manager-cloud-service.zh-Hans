---
title: 提交表单后显示自定义感谢消息
description: 了解如何配置 Forms Block 的感谢页面和重定向，优化用户体验并简化用户历程。
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '557'
ht-degree: 100%

---

# 提交表单后显示自定义感谢消息

用户提交表单后，通过感谢消息提供无缝体验至关重要。这不仅确认了提交成功，还可以提高用户满意度并进一步引导他们的历程。

- **感谢消息**：感谢消息是用户体验的基石，在提供保证和传递重要信息的同时，还能强化品牌识别形象。它是对用户行为的直接肯定，可培养用户的完成感和满足感。

- **重定向**：重定向在引导用户前往相关目标、优化参与度并最终提高转化率方面发挥着关键作用。通过无缝引导用户进入历程的下一步，重定向可确保流畅的导航体验。例如，在收集初始详细信息后将用户重定向至付款页面。

Adaptive Forms Block 的默认行为是在提交时显示感谢消息。表单提交成功后，消息将显示在表单顶部。

![默认感谢消息](/help/edge/assets/thank-you-message.png)

但是，您可以灵活地定制此体验以满足您的特定需求。选项包括：

- 提交表单后显示自定义感谢消息
- 提交后将用户重定向到另一个页面以进行进一步的操作

>[!NOTE]
>
> 您可以参考以下 [查询电子表格](/help/edge/docs/forms/assets/enquiry.xlsx)，根据您的要求定制感谢消息。

## 配置自定义感谢消息

如果您希望在成功提交表单后显示个性化的感谢消息，您可以配置电子表格来显示它。

请按照以下步骤为您的 Adaptive Forms Block 配置自定义感谢消息：

1. 转到 Microsoft SharePoint 或 Google Workspace 上的 Edge Deliver 项目文件夹并打开电子表格。
1. 在电子表格中的字段类型的`value`列中`submit`添加自定义的感谢消息。

   ![定制感谢消息](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   例如，在 `Submission Successful!` 字段类型的 `value` 列中添加 `submit` 消息。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布工作表。

   ![定制感谢消息](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## 提交后将用户重定向到另一个页面

提交表单后将用户重定向到另一个页面，可以通过提供相关信息、确认操作并引导用户获得期望的结果来增强用户体验。例如，

- 用户填写购买表单后，他们将被重定向到支付页面以安全地完成交易。
- 提交活动或网络研讨会的注册表单后，用户将被重定向到显示活动详细信息（例如日期、时间和地点）的确认页面。

按照以下步骤将用户重定向到另一个页面：

1. 转到 Microsoft SharePoint 或 Google Workspace 上的 Edge Deliver 项目文件夹并打开电子表格。
1. 将 URL 粘贴到 `value` 字段的 `submit` 列中，输入电子表格以在表单成功提交后重定向用户。
要将页面重定向到其他页面，请使用 [Edge Delivery Documentation](https://www.aem.live/docs/) 页面 URL。

   ![感谢重定向 URL](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布工作表。

   ![重定向感谢消息](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

您还可以创建新的文档文件并在 `value` 字段类型的列中 `submit` 添加其预览 URL。

用户提交表单后，提供清晰的感谢消息非常重要。它确认提交成功并提高用户满意度。

