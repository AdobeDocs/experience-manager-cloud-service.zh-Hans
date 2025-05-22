---
title: 配置内容创作的 Site 身份验证
description: 了解 AEM Live 如何支持基于令牌的身份验证，以及如何配置 AEM 以使用所见即所得创作的身份验证方法。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: b2838da2-79c7-49b1-a101-15c21e80197e
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '324'
ht-degree: 100%

---

# 配置内容创作的 Site 身份验证 {#site-authentication}

了解 AEM Live 如何支持基于令牌的身份验证，以及如何配置 AEM 以使用所见即所得创作的身份验证方法。

## 概述 {#overview}

AEM Live 支持基于令牌的身份验证。Site 身份验证通常应用于预览和发布 Sites，但也可以配置为仅单独保护两者中的一个 Site。

>[!NOTE]
>
>如果您选择激活 Site 身份验证，就必须在 AEM 创作环境中进行配置

## 要求 {#requirements}

要配置用于内容创作的 Site 身份验证，您必须首先完成以下任务：

* 此文档假设您已经根据[使用 Edge Delivery Services 进行所见即所得创作的开发人员快速入门指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)为您的项目创建了一个 Site。
* 您必须已经[为您的项目启用了无重复功能。](/help/edge/wysiwyg-authoring/repoless.md)

## 配置 Site 身份验证 {#configure-authentication}

请参阅文档[配置 Site 身份验证](https://www.aem.live/docs/authentication-setup-site)，了解有关如何配置 Site 身份验证的详细信息。

配置身份验证时请注意以下信息：

* 技术帐号 ID
* 您的 Site 身份验证令牌

这几项是为您 AEM 创作环境完成 Site 身份验证配置所必需的。

## 配置创作环境 {#authoring-environment}

Site 身份验证配置之后，您可以在 AEM 创作环境中启用它。

1. 登录 AEM 创作实例，然后前往&#x200B;**工具** -> **Cloud Services** -> **Edge Delivery Services 配置**，然后选择为您的 Site 自动创建的配置，然后点击或单击工具栏中的&#x200B;**属性**。
1. 在 **Edge Delivery Services 配置**&#x200B;窗口中选择&#x200B;**身份验证**&#x200B;选项卡，然后提供您之前复制的 **Site 身份验证令牌**。

   ![Edge Delivery Services 配置](/help/edge/wysiwyg-authoring/assets/site-authentication/configure-aem-author.png)

1. 验证&#x200B;**技术帐户 ID**&#x200B;是否与您之前复制的 ID 匹配。

   * 此字段是已预定义的只读字段。
   * 同一个 AEM 创作环境中的所有 Sites 的技术帐户都是相同的。

1. 点击或单击&#x200B;**保存并关闭**。
