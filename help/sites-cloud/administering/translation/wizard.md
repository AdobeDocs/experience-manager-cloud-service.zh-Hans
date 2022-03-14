---
title: 语言复制向导
description: 了解如何在AEM中使用语言副本向导。
feature: Language Copy
role: Admin
exl-id: bf8bdc53-0248-47de-bb9d-c884a7179ab0
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 3%

---

# 语言复制向导 {#language-copy-wizard}

语言副本向导是用于创建和检测多语言内容结构的引导式体验。 该向导使创建语言副本变得简单而快速。

>[!TIP]
>
>如果您是翻译内容的新用户，请参阅 [站点翻译历程、](/help/journey-sites/translation/overview.md) 这是使用AEM强大的翻译工具翻译AEM Sites内容的指导路径，非常适合那些没有AEM或翻译经验的用户。

>[!NOTE]
>
>用户需要是 `project-administrators` 组创建网站的语言副本。

要访问向导，请执行以下操作：

1. 在站点控制台中，选择一个页面，然后点按或单击 **创建** 选择 **语言副本**.

   ![从向导创建语言副本](../assets/language-copy-wizard.png)

1. 向导将打开 **选择源** 步骤来添加/删除页面。 您还可以选择包含或排除子页面。 选择要包含的页面，然后点按或单击 **下一个**.

   ![使用向导添加页面](../assets/language-copy-wizard-add-pages.png)

1. 的 **配置** 在向导的步骤中，可添加/删除语言并选择翻译方法。 单击或点按&#x200B;**下一步**。

   ![配置向导步骤](../assets/language-copy-wizard-configure.png)

   >[!NOTE]
   >
   >默认情况下，只有一个翻译设置。 要选择其他设置，您必须先配置云配置。 请参阅 [配置翻译集成框架](integration-framework.md).

1. 在 **翻译** 在向导的步骤中，您可以选择是仅创建结构、创建新翻译项目，还是添加到现有翻译项目。

   >[!NOTE]
   >
   >如果您在上一步中选择了多种语言，则会创建多个翻译项目。

   ![向导的翻译步骤](../assets/language-copy-wizard-translate.png)

1. 的 **创建** 按钮结束向导。 点按或单击 **完成** 关闭向导或 **打开** 查看生成的翻译项目。

   ![结束向导](../assets/language-copy-wizard-done.png)
