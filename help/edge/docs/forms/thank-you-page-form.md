---
title: 配置 EDS Forms 的感谢页面
description: 了解如何为EDS Forms配置感谢页面和重新定向，以优化用户体验并简化用户历程。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 2%

---


# 在自适应Forms块中配置感谢页面和重新定向

感谢页面和重新定向是增强用户体验的重要方面，可为用户提供确认、清晰的沟通以及表单提交后的顺畅导航。

## 配置感谢页面

感谢页面是对用户的可靠确认，使组织能够在增强品牌标识的同时传达重要信息。 按照以下步骤为EDS Forms配置感谢页面：

1. 访问Microsoft SharePoint或Google Workspace上的AEM Edge交付项目文件夹。
1. 在您的项目目录中创建名为“thankyou”的Microsoft Word或Google Docs文件。
1. 将您的感谢消息添加到“thankyou”文件。
   ![示例感谢页面](/help/edge/assets/sample-thankyou-page.png)
1. 利用AEM Sidekick预览和发布“感谢您”文件。

## 提交后重定向用户

重定向通过引导用户到相关目标、优化参与和提高转化率，帮助实现无缝用户历程。

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


