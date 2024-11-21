---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
source-git-commit: 681c194f997ab66f93beedad4eea273614e6797d
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 7%

---


# 配置提交操作以Marketo Engage现有表单

<span class="preview">该功能在早期采用者计划下可用。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

![工作流](/help/forms/assets/workflow-marketo-3.png)

自适应Forms编辑器提供&#x200B;**提交到Marketo Engage**&#x200B;提交操作，以将自适应Forms数据发送到Adobe Marketo Engage进行处理。 您可以将现有自适应表单配置为在提交时将数据提交到[Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)。

提供了用于处理表单提交的各种现成提交操作。 您可以在[自适应表单提交操作](/help/forms/configure-submit-actions-core-components.md)文章中了解有关这些选项的更多信息。

## 配置提交操作以Marketo Engage表单时的注意事项

* 确保使用Marketo Engage数据源配置自适应表单，以便在提交表单时将数据提交到Marketo Engage。 但是，您可以将提交操作更改为替代操作，例如&#x200B;**提交到OneDrive**&#x200B;或&#x200B;**提交到SharePoint**，即使表单配置了Marketo Engage数据架构也是如此。

## 将提交操作配置为Marketo Engage现有表单的先决条件

将提交操作配置为Marketo Engage的先决条件：

* 为自适应表单](/help/forms/use-marketo-engage-data-source-in-form.md)配置[Marketo Engage数据源，并将表单元素与Marketo Engage字段绑定。

## 如何配置提交操作以Marketo Engage现有表单？

您可以配置自适应表单的提交操作以将数据提交到Adobe Marketo Engage。 要将提交操作配置为Marketo Engage，请执行以下步骤：

1. 打开自适应表单进行编辑。
1. 打开内容树并选择&#x200B;**[!UICONTROL 指南容器]**。
1. 单击自适应表单容器属性![自适应表单容器属性](/help/forms/assets/configure-icon.svg)图标。 将打开用于配置提交操作的自适应表单容器对话框。
1. 打开&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡并选择提交操作作为&#x200B;**提交到Marketo Engage**。
1. 单击&#x200B;**[!UICONTROL 完成]**。

![Marketo提交操作](/help/forms/assets/marketo-engage-submit-action.png){width=50%， height=50%}


将自适应表单的提交操作配置为&#x200B;**提交到Marketo Engage**&#x200B;后，您可以将数据发送到Adobe Marketo Engage进行处理。 这些数据可用于分析和优化营销活动、自动跟进电子邮件以及根据表单提交触发工作流。

## 常见问题解答(FAQ)

**问：是否可以更改配置为与Marketo Engage架构连接的表单的提交操作？**
**A：**&#x200B;默认情况下，将表单配置为与Marketo Engage架构连接时，将选择&#x200B;**提交到Marketo**&#x200B;操作。 但是，您可以根据需要更改表单的提交操作。

## 下一步

您还可以将自适应表单与[Munchkin库](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin)连接以跟踪访问次数、点击次数和表单提交次数。

## 相关文章

{{af-submit-action}}

## 另请参阅

{{marketo-engage-see-also}}
