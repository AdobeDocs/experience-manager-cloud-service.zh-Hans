---
title: 翻译多语言站点的内容
description: 获取有关如何翻译多语言站点内容的概述。
translation-type: tm+mt
source-git-commit: 4fc4dbe2386d571fa39fd6d10e432bb2fc060da1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# 翻译多语言站点的内容{#translating-content-for-multilingual-sites}

自动翻译页面内容和资产，创建和维护多语言网站。 要实现翻译工作流自动化，您可以将翻译服务提供商与AEM集成，并创建将内容翻译成多种语言的项目。 AEM支持人文和机器翻译工作流。

* **人文翻译：内** 容将发送给您的翻译提供商并由专业翻译人员进行翻译。完成后，将返回译文内容并导入AEM。 将您的翻译提供商与AEM集成后，内容会在AEM和翻译提供商之间自动发送。
* **机器翻译：** 机器翻译服务会立即翻译您的内容。

翻译内容涉及以下步骤：

1. [将AEM与您的翻译服务提供商](integration-framework.md#connecting-to-a-translation-service-provider) 连接并 [创建翻译集成框架配置](integration-framework.md)。
1. [将您的语言母版的页](integration-framework.md#configuring-pages-for-translation) 面与翻译服务和框架配置关联。
1. [确定要翻译的](rules.md) 内容类型。
1. [通过创作语言主控](preparation.md) 和创建语言副本的根页面，准备要翻译的内容。
1. [创建翻](managing-projects.md) 译项目以收集要翻译的内容并准备翻译过程。
1. 使用翻译项目来管理[内容翻译过程](managing-projects.md)。

如果您的翻译服务提供商不提供与AEM集成的连接器，AEM支持手动提取和以XML格式重新插入翻译内容。

>[!NOTE]
>
>您的用户必须是`project-administrators`组的成员才能使用语言副本功能。

## 最佳实践 {#best-practices}

“[翻译最佳实践](best-practices.md)”页包含有关您的实施的重要信息。
