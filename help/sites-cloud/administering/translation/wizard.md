---
title: 语言复制向导
description: 了解如何在 AEM 中使用语言复制向导。
feature: Language Copy
role: Admin
exl-id: bf8bdc53-0248-47de-bb9d-c884a7179ab0
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 70%

---

# 语言复制向导 {#language-copy-wizard}

语言复制向导是一种用于创建和检测多语言内容结构的引导式体验。利用此向导，可以轻松快速地创建语言副本。

>[!TIP]
>
>如果不熟悉如何翻译内容，请参阅[站点翻译历程](/help/journey-sites/translation/overview.md)，将指导您使用 AEM 强大的翻译工具翻译您的 AEM Sites 内容，非常适合没有 AEM 或翻译经验的人士。

>[!NOTE]
>
>用户必须是 `project-administrators` 组，以创建站点的语言副本。

要访问该向导，请执行以下操作：

1. 在站点控制台中，选择一个页面，然后选择 **创建** 并选择 **语言复制**.

   ![从向导创建语言副本](../assets/language-copy-wizard.png)

1. 此向导将打开并显示&#x200B;**选择源**&#x200B;步骤，可让您添加/删除页面。您还可以选择包含或排除子页面。选择要包含的页面，然后选择 **下一个**.

   ![使用向导添加页面](../assets/language-copy-wizard-add-pages.png)

1. 利用该向导的&#x200B;**配置**&#x200B;步骤，可以添加/删除语言并选择翻译方法。选择&#x200B;**下一步**。

   ![向导的配置步骤](../assets/language-copy-wizard-configure.png)

   >[!NOTE]
   >
   >默认情况下，只有一种翻译设置。要能够选择其他设置，您必须先配置云配置。请参阅[配置翻译集成框架](integration-framework.md)。

1. 在 **Translate** 向导的步骤，您可以选择仅创建结构、创建翻译项目或添加到现有翻译项目。

   >[!NOTE]
   >
   >如果您在上一步中选择了多种语言，则会创建多个翻译项目。

   ![向导的翻译步骤](../assets/language-copy-wizard-translate.png)

1. 最后，该向导将显示&#x200B;**创建**&#x200B;按钮。选择 **完成** 关闭向导或 **打开** 以查看生成的翻译项目。

   ![结束向导](../assets/language-copy-wizard-done.png)
