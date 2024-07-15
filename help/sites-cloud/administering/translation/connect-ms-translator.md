---
title: 连接到 Microsoft Translator
description: 了解如何将 AEM 连接到现成的 Microsoft Translator 以自动化您的翻译工作流。
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 81%

---

# 连接到 Microsoft Translator {#connecting-to-microsoft-translator}

为 [Microsoft Translator](https://www.microsoft.com/en-us/translator/business/) 云服务创建配置以使用 Microsoft Translation 帐户来翻译 AEM 页面内容或资源。

>[!TIP]
>
>如果不熟悉如何翻译内容，请参阅[站点翻译历程](/help/journey-sites/translation/overview.md)，将指导您使用 AEM 强大的翻译工具翻译您的 AEM Sites 内容，非常适合没有 AEM 或翻译经验的人士。

>[!NOTE]
>
>AEM 提供了一个 Microsoft Translation 试用帐户，每月最多允许 200 万个免费翻译的字符。要获得足以用于生产系统的帐户订阅，请参阅[升级 Microsoft Translator 试用许可证配置](#upgrading-the-microsoft-translator-trial-license-configuration)。

| 属性 | 描述 |
|---|---|
| 翻译标签 | 翻译服务的显示名称 |
| 翻译属性 | （可选）对于用户生成的内容，为已翻译文本旁边显示的属性，例如`Translations by Microsoft` |
| 工作区 ID | （可选）要使用的自定义 Microsoft Translator 引擎的 ID |
| 订阅密钥 | 您的 Microsoft Translator 的 Microsoft 订阅密钥 |

在创建配置后，您需要[激活它](#activating-the-translator-service-configurations)。

以下过程将创建 Microsoft Translator 配置。

1. 在[导航面板中，](/help/sites-cloud/authoring/basic-handling.md#first-steps)选择&#x200B;**工具** > **Cloud Service** > **翻译Cloud Service**。
1. 导航到要创建配置的位置。 通常它在您的站点根中，也可以是全局默认配置。
1. 选择&#x200B;**创建**&#x200B;按钮。
1. 定义您的配置。
   1. 在下拉列表中选择 **Microsoft Translator**。
   1. 为您的配置键入标题。标题在 Cloud Service 控制台中以及页面属性下拉列表中标识该配置。
   1. （可选）键入一个名称以用于存储该配置的存储库节点。

   ![创建翻译配置](../assets/create-translation-config.png)

1. 单击&#x200B;**创建**。
1. 在&#x200B;**编辑配置**&#x200B;窗口中，提供上一个表中描述的翻译服务的值。

   ![编辑翻译配置](../assets/edit-translation-config.png)

1. 选择&#x200B;**连接**&#x200B;以验证连接。
1. 选择&#x200B;**保存并关闭**。

## 升级 Microsoft Translator 试用许可证配置 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft Translation 配置页面提供了指向 Microsoft 网站的便利链接，可用于获取足够用于生产系统的帐户订阅。

1. 在[导航面板中，](/help/sites-cloud/authoring/basic-handling.md#first-steps)选择&#x200B;**工具** > **Cloud Service** > **翻译Cloud Service**。
1. 选择您现有的Microsoft Translator配置。
1. 选择&#x200B;**编辑**。
1. 在&#x200B;**编辑配置**&#x200B;窗口中，选择&#x200B;**升级订阅**。 这将打开一个 Microsoft 网页，其中包含有关该服务的更多详细信息。

## 自定义 Microsoft Translator 引擎 {#customizing-your-microsoft-translator-engine}

Microsoft Translation 配置页面提供了指向 Microsoft 网站的便利链接，可用于自定义 Microsoft Translator 引擎。

1. 在[导航面板中，](/help/sites-cloud/authoring/basic-handling.md#first-steps)选择&#x200B;**工具** > **Cloud Service** > **翻译Cloud Service**。
1. 选择您现有的Microsoft Translator配置。
1. 选择&#x200B;**编辑**。
1. 在&#x200B;**编辑配置**&#x200B;窗口中，选择&#x200B;**自定义Translator**。 使用打开的 Microsoft 网页来自定义您的服务。

## 激活 Translator 服务配置 {#activating-the-translator-service-configurations}

您需要激活云服务配置以支持复制到发布实例的已翻译内容。使用[发布树](/help/sites-cloud/authoring/sites-console/publishing-pages.md#publishing-and-unpublishing-a-tree)的方法激活存储了 Microsoft Translator 配置的存储库节点。这些节点位于以下父节点的下方：

* `/libs/settings/cloudconfigs/translation/msft-translation`
