---
title: 如何配置重定向页面？
description: 了解如何将用户重定向到表单作者在创建表单时可以配置的网页。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 配置重定向页面 {#configuring-redirect-page}

表单作者可以为每个表单配置一个页面，表单用户在提交表单后将被重定向到该页面。

1. 在编辑模式下，选择一个组件，然后单击 ![字段级别](assets/select_parent_icon.svg) > **[!UICONTROL 自适应表单容器]**，然后单击 ![cppr](assets/configure-icon.svg).

1. 在侧栏中，单击 **[!UICONTROL 提交]**.

1. 在 **[!UICONTROL 重定向URL/路径]** 在 **[!UICONTROL 提交]** 中。
1. 或者，在提交操作下方的提交到REST端点操作中，您可以配置要传递到重定向页面的参数。

   ![重定向页面配置](assets/redirect-url.png)

   重定向页面配置

表单作者可以使用传递到感谢页面的以下参数。 对于所有可用的提交操作， `status` 和 `owner` 参数被传递。 除了这两个参数之外，还会为以下提交操作传递一些其他参数：

* **[!UICONTROL 提交到REST端点]**:将传递为字段内参数映射添加的参数。 `status` 和 `owner` 参数不会在此提交操作中传递。 有关更多信息，请参阅 [配置提交到REST端点提交操作](configuring-submit-actions.md).
