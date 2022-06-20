---
title: 翻译多语言站点的内容
description: 大致了解如何翻译多语言站点的内容。
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: ht
source-wordcount: '292'
ht-degree: 100%

---

# 翻译多语言站点的内容 {#translating-content-for-multilingual-sites}

自动翻译页面内容和资产以创建和维护多语言网站。要自动化翻译工作流，您可以将翻译服务提供商与 AEM 集成并创建项目以将内容翻译成多种语言。AEM 支持人工翻译工作流和机器翻译工作流。

* **人工翻译：**&#x200B;内容将发送给您的翻译提供商并由专业翻译人员进行翻译。完成后，将返回翻译的内容并将其导入 AEM。当您的翻译提供商与 AEM 集成时，内容会在 AEM 和翻译提供商之间自动发送。
* **机器翻译：**&#x200B;机器翻译服务将立即翻译您的内容。

>[!TIP]
>
>如果不熟悉如何翻译内容，请参阅我们的[站点翻译历程](/help/journey-sites/translation/overview.md)，将指导您使用 AEM 强大的翻译工具翻译您的 AEM Sites 内容，非常适合没有 AEM 或翻译经验的人士。

翻译内容涉及以下步骤：

1. [将 AEM 连接到翻译服务提供商](integration-framework.md#connecting-to-a-translation-service-provider)和[创建翻译集成框架配置](integration-framework.md)。
1. [将语言母版页面关联到](integration-framework.md#configuring-pages-for-translation)翻译服务和框架配置。
1. [标识要翻译的内容类型](rules.md)。
1. 通过创作语言母版并创建语言副本的根页面来[准备内容以进行翻译](preparation.md)。
1. [创建翻译项目](managing-projects.md)以收集要翻译的内容并准备翻译过程。
1. 使用翻译项目[管理内容翻译过程](managing-projects.md)。

如果您的翻译服务提供商不提供连接器来与 AEM 集成，则 AEM 支持手动提取和重新插入 XML 格式的翻译内容。

>[!NOTE]
>
>您的用户必须是 `project-administrators` 组的成员才能使用语言复制功能。

## 最佳实践 {#best-practices}

[翻译最佳实践](best-practices.md)页面包含有关您的实施的重要信息。
