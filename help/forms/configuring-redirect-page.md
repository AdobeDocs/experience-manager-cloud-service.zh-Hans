---
title: 如何配置重定向页面？
description: 了解如何将用户重定向到表单作者在创建表单时可以配置的网页。
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 6%

---

# 配置重定向页面 {#configuring-redirect-page}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-redirect-page.html) |
| AEM as a Cloud Service | 本文 |

表单作者可为每个表单配置一个页面，表单用户在提交表单后会重定向到该页面。

1. 在编辑模式下，选择一个组件，然后单击![字段级](assets/select_parent_icon.svg) > **[!UICONTROL 自适应表单容器]**，然后单击![cmppr](assets/configure-icon.svg)。

1. 在侧栏中，单击&#x200B;**[!UICONTROL 提交]**。

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;部分的&#x200B;**[!UICONTROL 重定向URL/路径]**&#x200B;下提供重定向页面的URL。
1. 或者，在提交操作下，对于提交到REST端点操作，您可以配置要传递到重定向页面的参数。

   ![重定向页面配置](assets/redirect-url.png)

   重定向页面配置

表单作者可以使用传递到“感谢”页面的以下参数。 对于所有可用的提交操作，传递`status`和`owner`参数。 除了这两个参数之外，还会为以下提交操作传递一些其他参数：

* **[!UICONTROL 提交到REST终结点]**：传递为字段内到参数映射添加的参数。 未在此提交操作中传递`status`和`owner`参数。 有关详细信息，请参阅[配置提交到REST终结点提交操作](configuring-submit-actions.md)。

>[!MORELIKETHIS]
>
>* [配置重定向页面或感谢消息](/help/forms/configure-redirect-page-or-thank-you-message.md)
