---
title: 如何配置重定向页面或感谢消息
description: 了解如何向用户显示感谢消息或重定向到表单作者在创建表单时可以配置的网页。
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 配置重定向或感谢消息

在使用通用编辑器创建的表单中，表单作者可以配置用户提交表单后发生的情况。 您可以显示感谢消息，也可以使用编辑表单属性扩展中的提交选项卡将用户重定向到特定网页。

您可以使用&#x200B;**AEM表单属性**&#x200B;扩展的&#x200B;**提交**&#x200B;选项卡为在Universal Editor中创建的表单配置感谢消息或重新定向URL。

## 先决条件

您可以使用&#x200B;**编辑表单属性**&#x200B;扩展的&#x200B;**提交**&#x200B;选项卡为在Universal Editor中创建的表单配置提交操作。

![表单属性图标](/help/forms/assets/ue-form-properties-icon.png)

![通用编辑器表单属性](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
>* 如果您在通用编辑器界面中未看到&#x200B;**表单属性**&#x200B;图标，请在Extension Manager中启用&#x200B;**编辑表单属性**&#x200B;扩展。
>* 请参阅[Extension Manager功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)一文，了解如何在通用编辑器中启用或禁用扩展。

## 如何配置重定向或感谢消息？

在提交表单时，您可以将用户重定向到其他网页或显示消息。

配置重定向页面或感谢消息：

1. 打开自适应表单进行编辑。
1. 打开内容树并选择&#x200B;**[!UICONTROL 指南容器]**。
1. 单击自适应表单容器属性![自适应表单容器属性](/help/forms/assets/configure-icon.svg)图标。 此时将打开用于配置数据模型的自适应表单容器对话框。
1. 打开&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。 显示用于配置重定向页面或消息的选项：

   向导容器的![提交对话框用于配置重定向页面或消息](/help/forms/assets/adaptive-forms-core-components-redirect-page-or-thank-you-message.png)

**配置重定向URL**

* 要配置重定向URL，请为提交选项选择&#x200B;**[!UICONTROL 重定向到URL选项]**，并提供绝对地址、重定向URL或AEM Sites页面的相对路径。

![重定向](/help/edge/docs/forms/universal-editor/assets/redirect-ue.png)

**配置感谢消息**

* 要配置自定义消息或感谢消息，请选择&#x200B;**[!UICONTROL 显示消息]**&#x200B;选项，然后在“消息内容”框中提供消息。 它是一个富文本框，您可以使用全屏选项查看所有可用的富文本项。

![感谢](/help/edge/docs/forms/universal-editor/assets/thankyou-ue.png)

表单作者可为每个表单配置一个页面，表单用户在提交表单后会重定向到该页面。
