---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: ce4646d8db1870f8ec85faddeb4e0a6a04f4c46e
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 8%

---

# 将现有表单的提交操作配置到 Marketo Engage

<span class="preview">该功能在早期采用者计划下可用。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

![工作流](/help/forms/assets/workflow-marketo-3.png)

自适应Forms编辑器提供&#x200B;**提交到Marketo Engage**&#x200B;提交操作，以将自适应Forms数据发送到Adobe Marketo Engage进行处理。 您可以将现有自适应表单配置为在提交时将数据提交到[Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)。

提供了用于处理表单提交的各种现成提交操作。 您可以在[自适应表单提交操作](/help/forms/configure-submit-actions-core-components.md)文章中了解有关这些选项的更多信息。

## 将提交操作配置到Marketo Engage以进行表单处理时的注意事项

* 确保使用Marketo Engage数据源配置自适应表单，以便在提交表单时将数据提交到Marketo Engage。 但是，您可以将提交操作更改为替代操作，例如&#x200B;**提交到OneDrive**&#x200B;或&#x200B;**提交到SharePoint**，即使表单配置了Marketo Engage数据架构也是如此。

## 为现有表单配置提交操作到Marketo Engage的先决条件

将提交操作配置到Marketo Engage的先决条件：

* 为自适应表单[配置](/help/forms/use-marketo-engage-data-source-in-form.md)Marketo Engage数据源，并将表单元素与Marketo Engage字段绑定。

## 如何为现有表单配置提交到Marketo Engage的操作？

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

>[!BEGINTABS]

>[!TAB 基础组件]

您可以配置基于基础组件的自适应表单的提交操作以将数据提交到Adobe Marketo Engage。 要配置提交到Marketo Engage的操作，请执行以下步骤：

1. 登录到[!DNL Experience Manager Forms]作者实例。
1. 打开自适应表单进行编辑，然后导航到自适应表单容器属性的&#x200B;**[!UICONTROL 提交]**&#x200B;部分，并选择提交操作作为&#x200B;**提交到Marketo Engage**。
1. 单击&#x200B;**[!UICONTROL 完成]**。

![Marketo提交操作](/help/forms/assets/marketo-engage-submit-action-af.png){width=50%, height=50%}

将自适应表单的提交操作配置为&#x200B;**提交到Marketo Engage**&#x200B;后，您可以将数据发送到Adobe Marketo Engage进行处理。 这些数据可用于分析和优化营销活动、自动跟进电子邮件以及根据表单提交触发工作流。

>[!TAB 核心组件]

您可以配置基于核心组件的自适应表单的提交操作，将数据提交到Adobe Marketo Engage。 要配置提交到Marketo Engage的操作，请执行以下步骤：

1. 打开自适应表单进行编辑。
1. 打开内容树并选择&#x200B;**[!UICONTROL 指南容器]**。
1. 单击自适应表单容器属性![自适应表单容器属性](/help/forms/assets/configure-icon.svg)图标。 将打开用于配置提交操作的自适应表单容器对话框。
1. 打开&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡并选择提交操作作为&#x200B;**提交到Marketo Engage**。
1. 单击&#x200B;**[!UICONTROL 完成]**。

![Marketo提交操作](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}

将自适应表单的提交操作配置为&#x200B;**提交到Marketo Engage**&#x200B;后，您可以将数据发送到Adobe Marketo Engage进行处理。 这些数据可用于分析和优化营销活动、自动跟进电子邮件以及根据表单提交触发工作流。

>[!TAB 通用编辑器]

您可以配置在Universal Editor中创作的自适应表单的提交操作，以将数据提交到Adobe Marketo Engage。 要配置提交到Marketo Engage的操作，请执行以下步骤：

1. 打开自适应表单进行编辑。
1. 单击编辑器上的&#x200B;**编辑表单属性**扩展。
出现**表单属性**&#x200B;对话框。

   >[!NOTE]
   >
   > * 如果您在通用编辑器界面中未看到&#x200B;**编辑表单属性**&#x200B;图标，请在Extension Manager中启用&#x200B;**编辑表单属性**&#x200B;扩展。
   > * 请参阅[Extension Manager功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)一文，了解如何在通用编辑器中启用或禁用扩展。

1. 单击&#x200B;**提交**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 提交到Marketo Engage]**&#x200B;提交操作。

   ![Marketo提交操作](/help/forms/assets/marketo-engage-submit-action-ue.png)

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。

将自适应表单的提交操作配置为&#x200B;**提交到Marketo Engage**&#x200B;后，您可以将数据发送到Adobe Marketo Engage进行处理。 这些数据可用于分析和优化营销活动、自动跟进电子邮件以及根据表单提交触发工作流。

>[!ENDTABS]

## 常见问题解答(FAQ)

**问：是否可以更改配置为与Marketo Engage架构连接的表单的提交操作？**
**A：**&#x200B;默认情况下，将表单配置为连接Marketo架构时，将选择&#x200B;**提交到Marketo Engage**&#x200B;操作。 但是，您可以根据需要更改表单的提交操作。

## 下一步

您还可以将自适应表单与[Munchkin库](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin)连接以跟踪访问次数、点击次数和表单提交次数。

## 相关文章

{{af-submit-action}}

## 另请参阅

{{marketo-engage-see-also}}
