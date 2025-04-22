---
title: 为内容创作配置站点身份验证
description: 了解AEM Live如何支持基于令牌的身份验证，以及如何将AEM配置为将身份验证与WYSIWYG创作结合使用。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: b2838da2-79c7-49b1-a101-15c21e80197e
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 2%

---

# 为内容创作配置站点身份验证 {#site-authentication}

了解AEM Live如何支持基于令牌的身份验证，以及如何将AEM配置为将身份验证与WYSIWYG创作结合使用。

## 概述 {#overview}

AEM Live支持基于令牌的身份验证。 站点身份验证通常同时应用于预览站点和发布站点，但也可以配置为仅单独保护任一站点。

>[!NOTE]
>
>如果选择激活站点身份验证，则还必须在AEM创作环境中对其进行配置

## 要求 {#requirements}

要配置用于内容创作的站点身份验证，必须首先完成以下任务：

* 本文档假定您已根据[使用Edge Delivery Services创作WYSIWYG的开发人员快速入门指南为您的项目创建了一个站点。](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* 您必须已[为项目启用重写功能。](/help/edge/wysiwyg-authoring/repoless.md)

## 配置站点身份验证 {#configure-authentication}

有关如何配置站点身份验证的详细信息，请参阅文档[配置站点身份验证](https://www.aem.live/docs/authentication-setup-site)。

配置身份验证时，请注意以下信息：

* 技术帐户的ID
* 您的站点身份验证令牌

要为AEM创作环境完成站点身份验证配置，需要这些项目。

## 配置创作环境 {#authoring-environment}

配置站点身份验证后，您可以在AEM创作环境中启用它。

1. 登录到AEM创作实例，然后转到&#x200B;**工具** -> **Cloud Services** -> **Edge Delivery Services配置**，选择为您的站点自动创建的配置，然后点按或单击工具栏中的&#x200B;**属性**。
1. 在&#x200B;**Edge Delivery Services配置**&#x200B;窗口中，选择&#x200B;**身份验证**&#x200B;选项卡，提供您之前复制的&#x200B;**站点身份验证令牌**。

   ![Edge Delivery Services配置](/help/edge/wysiwyg-authoring/assets/site-authentication/configure-aem-author.png)

1. 验证&#x200B;**技术帐户ID**&#x200B;是否与您之前复制的技术帐户ID匹配。

   * 此字段为只读并预定义。
   * 对于单个AEM创作环境中的所有站点，技术帐户是相同的。

1. 点击或单击&#x200B;**保存并关闭**。
