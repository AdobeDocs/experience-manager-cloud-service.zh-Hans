---
title: 语言复制向导
description: 了解如何在 AEM 中使用语言复制向导。
feature: Language Copy
role: Admin
exl-id: bf8bdc53-0248-47de-bb9d-c884a7179ab0
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 100%

---

# 语言复制向导 {#language-copy-wizard}

语言复制向导是一种用于创建和检测多语言内容结构的引导式体验。利用此向导，可以轻松快速地创建语言副本。

>[!TIP]
>
>如果不熟悉如何翻译内容，请参阅我们的[站点翻译历程](/help/journey-sites/translation/overview.md)，将指导您使用 AEM 强大的翻译工具翻译您的 AEM Sites 内容，非常适合没有 AEM 或翻译经验的人士。

>[!NOTE]
>
>用户必须是 `project-administrators` 组的成员才能创建站点的语言副本。

要访问该向导，请执行以下操作：

1. 在站点控制台中，选择页面，然后点按或单击&#x200B;**创建**&#x200B;并选择&#x200B;**语言复制**。

   ![从向导创建语言副本](../assets/language-copy-wizard.png)

1. 此向导将打开并显示&#x200B;**选择源**&#x200B;步骤，可让您添加/删除页面。您还可以选择包含或排除子页面。选择要包含的页面，然后点按或单击&#x200B;**下一步**。

   ![使用向导添加页面](../assets/language-copy-wizard-add-pages.png)

1. 利用该向导的&#x200B;**配置**&#x200B;步骤，可以添加/删除语言并选择翻译方法。点按或单击&#x200B;**下一步**。

   ![向导的配置步骤](../assets/language-copy-wizard-configure.png)

   >[!NOTE]
   >
   >默认情况下，只有一种翻译设置。要能够选择其他设置，您必须先配置云配置。请参阅[配置翻译集成框架](integration-framework.md)。

1. 在该向导的&#x200B;**翻译**&#x200B;步骤中，您可以选择仅创建结构、创建新翻译项目或添加到现有翻译项目。

   >[!NOTE]
   >
   >如果您在上一步中选择了多种语言，则将创建多个翻译项目。

   ![向导的翻译步骤](../assets/language-copy-wizard-translate.png)

1. 最后，该向导将显示&#x200B;**创建**&#x200B;按钮。点按或单击&#x200B;**完成**&#x200B;以关闭向导，或者，点按或单击&#x200B;**打开**&#x200B;以查看生成的翻译项目。

   ![结束向导](../assets/language-copy-wizard-done.png)
