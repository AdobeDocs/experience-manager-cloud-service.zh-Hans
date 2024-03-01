---
title: 配置 EDS Forms 的感谢页面
description: 了解如何为EDS Forms配置感谢页面和重新定向，以优化用户体验并简化用户历程。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: cadeccd916884ca2437e2b2684771c181cc8281e
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 7%

---


# 提交后显示感谢页面或重定向表单

用户提交表单后，通过感谢页面或重定向提供无缝体验至关重要。 这些要素不仅确认了提交成功，而且还提高了用户满意度，并指导他们进一步开展工作。

* **感谢页面**：感谢页面是用户体验的基石，可在增强品牌标识的同时提供保证和传达重要信息。 它是对用户行为的直接承认，培养了完成感和满意感。

* **重定向**：重定向在引导用户访问相关目标、优化参与以及最终提高转化率方面起着关键作用。 通过无缝引导用户进入其历程的下一步，重定向可确保顺畅的导航体验。 例如，在收集初始详细信息后将用户重定向到支付页面。

在自适应Forms块中，默认行为是显示感谢页面。 但是，您可以灵活地定制此体验，以满足您的特定需求。 选项包括：

* [配置感谢页面和消息以符合您的品牌和沟通目标](#configuring-the-thank-you-page-and-message)
* [在提交后将用户重定向到另一个页面](#redirect-users-to-another-page-post-submission)，进一步增强其历程

## 配置感谢页面和消息

自适应Forms块的默认行为是在提交时显示“感谢”页面。 请按照以下步骤为自适应Forms块配置“感谢”页面：

1. 访问Microsoft SharePoint或Google Workspace上的AEM Edge交付项目文件夹。
1. 在您的项目目录中创建名为“thankyou”的Microsoft Word或Google Docs文件。
1. 将您的感谢消息添加到“thankyou”文件。 </br>

   ![示例感谢页面](/help/edge/assets/sample-thankyou-page.png)

1. 使用AEM Sidekick预览和发布“感谢”文件。

您的自适应Forms块会在表单提交时显示“感谢您”页面。

## 提交后将用户重定向到其他页面

默认情况下，自适应Forms块会将用户重定向到“感谢您”页面。 要将用户重定向到默认“感谢”页面以外的其他页面，您有两个选项：

* 将现有的“感谢”页面替换为其他页面，或者
* 将“感谢您”页面重定向到您选择的另一个页面。

### 替换现有的“感谢”页面

1. 打开&quot;[EDS项目]/blocks/form/form.js”文件进行编辑。
1. 更改 `thankyou` 页面放入您选择的页面中的以下行：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例如，

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'payment';
   ```

   >[!NOTE]
   >
   > 确保Microsoft SharePoint或Google Workspace上的边缘交付服务项目文件夹中存在同名页面。 如果页面不存在，请继续创建和发布页面。

1. 继续将更新的“form.js”文件夹及其基础文件签入到GitHub上的边缘交付服务项目。 此更新确保表单现在重定向到指定的更新页面。

1. 确保EDS项目文件夹中存在该页面并将其发布。


### 使用网站重定向

配置网站重定向以将“感谢您”页面定向到其他页面。 请参阅 [重定向文档](https://www.aem.live/docs/redirects) 以获取详细说明。

## 查看更多

* [表单组件](/help/edge/docs/forms/form-components.md)
* [表单字段属性](/help/edge/docs/forms/eds-form-field-properties)
* [创建并预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单，以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到 Sites 页面](/help/edge/docs/forms/publish-eds-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [改变表单主题和样式](/help/edge/docs/forms/style-theme-forms.md)
