---
title: 分析内容片段
description: 了解用于内容投放的内容片段的结构。 这提供了与headless投放和页面创作相关的信息。
feature: Content Fragments
role: User, Developer, Architect
exl-id: d9268c1a-bfe6-4df7-bad9-6007dd79e0aa
source-git-commit: 19685cb952a890731bd7d75a2adf3cfd841a465f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 分析内容片段结构 {#analyzing-content-fragments-structure}

内容片段设计用于[使用 GraphQL 的 Headless 投放](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)。这意味着它们可具有多层结构。

Experience Manager (AEM) 提供了多种查看和分析片段结构的方法。

## 引用 {#references}

多层结构使用引用来构建：

* [在内容片段模型中定义引用的数据类型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* 在创作时，您可以：
   * [管理这些引用](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [查找片段的父引用](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## 结构树 {#structure-tree}

从编辑器工具栏打开&#x200B;**结构树**&#x200B;选项卡以显示内容片段及其引用的层次结构。使用链接图标打开引用。

例如：

![内容片段编辑器 - 结构树](assets/cf-authoring-structure-tree.png)
