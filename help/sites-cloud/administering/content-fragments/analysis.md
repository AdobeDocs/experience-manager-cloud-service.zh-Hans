---
title: 分析内容片段
description: 了解内容片段的结构和内容投放。 这提供了有关headless投放和页面创作的信息。
feature: Content Fragments
role: User, Developer, Architect
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 2%

---


# 分析内容片段结构 {#analyzing-content-fragments-structure}

内容片段专为 [使用GraphQL的Headless投放](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md). 这意味着它们可以具有多层结构。

Experience Manager(AEM)提供了多种查看和分析片段结构的方法。

## 引用 {#references}

结构是使用引用构建的：

* [引用的数据类型在内容片段模型中定义](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* 在创作时，您可以：
   * [管理这些引用](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [查找片段的父引用](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## 结构树 {#structure-tree}

打开 **结构树** 选项卡中显示内容片段的层次结构及其引用。 使用链接图标可打开引用。

例如：

![内容片段编辑器 — 结构树](assets/cf-authoring-structure-tree.png)