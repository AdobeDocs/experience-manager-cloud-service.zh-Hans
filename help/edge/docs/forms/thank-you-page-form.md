---
title: 提交后配置感谢页面或重定向表单
description: 了解如何配置表单区块的感谢页面和重定向，以优化用户体验并简化用户历程。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 81%

---

# 提交后显示感谢页面或重定向表单

用户提交表单后，通过感谢页面或重定向提供无缝体验至关重要。这些元素不仅可以确认提交成功，还可以提高用户满意度并引导他们在历程中走得更远。

* **谢谢页面**：感谢页面是用户体验的基石，在提供保证和传递重要信息的同时，还能强化品牌识别形象。它是对用户行为的直接肯定，可培养用户的完成感和满足感。

* **重定向**：重定向在引导用户前往相关目标、优化参与度并最终提高转化率方面发挥着关键作用。通过无缝引导用户进入历程的下一步，重定向可确保流畅的导航体验。例如，在收集初始详细信息后将用户重定向到付款页面。

在自适应Forms块中，默认行为是显示感谢页面。 但是，您可以灵活地定制此体验以满足您的特定需求。选项包括：

* [配置感谢页面和消息以符合您的品牌和沟通目标](#configuring-the-thank-you-page-and-message)
* [提交后将用户重定向到另一个页面，以便进一步操作](#redirect-users-to-another-page-post-submission)

## 配置感谢页面和消息

自适应Forms块的默认行为是在提交时显示“感谢”页面。 请按照以下步骤为自适应Forms块配置“感谢”页面：

1. 访问 Microsoft SharePoint 或 Google Workspace 上的 AEM Edge Delivery 项目文件夹。
1. 在项目目录中创建一个名为“感谢”的 Microsoft Word 或 Google Docs 文件。
1. 将您的感谢消息添加到“感谢”文件中。</br>

   ![感谢页面示例](/help/edge/assets/sample-thankyou-page.png)

1. 使用 AEM Sidekick 预览和发布“感谢”文件。

在提交表单时，您的自适应Forms块会显示“感谢您”页面。

## 提交后将用户重定向到另一个页面

默认情况下，自适应Forms块会将用户重定向到“感谢您”页面。 要将用户重定向到默认“感谢”页面以外的页面，有两种选项：

* [将“感谢”页面替换为其他页面](#replace-the-existing-thankyou-page)
* [使用网站重定向进行“感谢”页面重定向](#use-website-redirects-for-thankyou-page-redirection)

### 替换“感谢”页面

1. 打开“[ EDS 项目]/blocks/form/form.js”文件进行编辑。
1. 将以下行中的 `thankyou` 页面更改为您选择的页面：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例如，

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'payment';
   ```

   >[!NOTE]
   >
   > 确保Microsoft SharePoint或Google Workspace上的Edge Delivery Services项目文件夹中存在同名页面。 如果该页面不存在，请继续创建并发布它。

1. 继续将更新的“form.js”文件夹及其基础文件签入GitHub上的Edge Delivery Services项目。 此更新可确保表单现在重定向到指定的更新页面。

1. 确保该页面存在于您的 EDS 项目文件夹中并将其发布。


### 使用网站重定向进行“感谢”页面重定向

提交表单后将用户重定向到另一个页面，可以通过提供相关信息、确认操作并引导用户获得期望的结果来增强用户体验。例如，

* 用户填写购买表单后，他们将被重定向到支付页面以安全地完成交易。
* 提交活动或网络研讨会的注册表单后，用户将被重定向到显示活动详细信息（例如日期、时间和地点）的确认页面。

要将“感谢”页面重定向到其他页面，请使用[网站重定向](https://www.aem.live/docs/redirects)电子表格。


## 查看更多

* [表单组件](/help/edge/docs/forms/form-components.md)
* [表单字段属性](/help/edge/docs/forms/eds-form-field-properties)
* [创建并预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单，以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到 Sites 页面](/help/edge/docs/forms/publish-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [改变表单主题和样式](/help/edge/docs/forms/style-theme-forms.md)
