---
title: 使用内容片段AJO外部引用扩展
description: 了解内容片段AJO外部引用扩展
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
source-git-commit: f755a5c621b68b3110642e6cfe150798555b6707
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---


# 内容片段AJO外部引用扩展 {#content-fragment-external-references-extension}

要预览其他Adobe产品上的AEM体验，您可以启用UI扩展：

* **AJO外部引用**

AJO外部引用扩展可通过从与预定义标记关联的所有组织和沙盒中获取对内容片段的引用来发挥作用。 然后，扩展会显示详细信息。

例如，对于与Adobe Journey Optimizer (AJO)的集成，详细信息取决于引用是营销策划、历程还是模板。

>[!NOTE]
>
>有关如何启用扩展的详细信息，请参阅AEM Experience Manager中的[Extension Manager。](https://developer.adobe.com/uix/docs/extension-manager/)

例如，要将扩展与AJO一起使用：

>[!NOTE]
>
>另请参阅[AJO集成](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/integrations/aem-fragments)。

1. 打开[内容片段控制台](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)。

1. 导航到您的内容片段 — 在各种AJO渠道中创建和使用的片段。

1. 在[编辑器](/help/sites-cloud/administering/content-fragments/managing.md#editing-the-content-of-your-fragment)中打开您的内容片段。

1. AJO外部引用扩展在右侧面板中作为选项卡提供。 选择选项卡以打开扩展：

   ![AJO外部引用扩展](/help/sites-cloud/administering/content-fragments/assets/cf-ajo-fragment-external-references-extension.png)

   选择参照类型后，扩展会将相应的外部参照显示为具有列的表格：

   * **名称**：使用内容片段的引用的名称
   * **预览**&#x200B;选择此链接以开始预览
   * **状态**：引用的状态

1. 您可以从下拉列表中选择&#x200B;**引用类型**&#x200B;以在三种引用类型之间切换：

   * **营销活动**
      * 显示所有营销活动的列表，其中包含指向当前内容片段的链接。
      * 然后，您可以预览选定的营销策划。
      * 默认
   * **历程**
      * 显示最新的历程。
      * 然后，您可以选择并预览选定的历程。
   * **模板**
      * 显示与内容片段相关的模板。
      * 然后，您可以选择并预览选定的模板。