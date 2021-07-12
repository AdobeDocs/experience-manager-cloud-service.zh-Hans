---
title: 翻译多语言站点的内容
description: 获取有关如何翻译多语言站点内容的概述。
feature: 语言复制
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# 翻译多语言站点的内容 {#translating-content-for-multilingual-sites}

自动翻译页面内容和资产以创建和维护多语言网站。 要实现翻译工作流程的自动化，您需要将翻译服务提供商与AEM集成，并创建项目以将内容翻译成多种语言。 AEM支持人工和机器翻译工作流。

* **人文翻译：** 内容将发送给您的翻译提供商，并由专业翻译人员翻译。完成后，将返回翻译内容并将其导入AEM。 将您的翻译提供商与AEM集成后，内容会在AEM和翻译提供商之间自动发送。
* **机器翻译：** 机器翻译服务会立即翻译您的内容。

翻译内容涉及以下步骤：

1. [将AEM与您的翻译服务提供商](integration-framework.md#connecting-to-a-translation-service-provider) 连接并 [创建翻译集成框架配置](integration-framework.md)。
1. [将语言母版的页面与](integration-framework.md#configuring-pages-for-translation) 翻译服务和框架配置相关联。
1. [识别要翻译的](rules.md) 内容类型。
1. [通过创作语言](preparation.md) 主控并创建语言副本的根页面，准备翻译内容。
1. [创建翻](managing-projects.md) 译项目以收集要翻译的内容并准备翻译过程。
1. 使用翻译项目到[管理内容翻译流程](managing-projects.md)。

如果您的翻译服务提供商未提供与AEM集成的连接器，则AEM支持以XML格式手动提取和重新插入翻译内容。

>[!NOTE]
>
>要使用语言副本功能，用户必须是`project-administrators`组的成员。

## 最佳实践 {#best-practices}

[翻译最佳实践](best-practices.md)页面包含有关您的实施的重要信息。
