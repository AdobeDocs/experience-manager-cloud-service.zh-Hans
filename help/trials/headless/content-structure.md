---
title: 为应用程序创建内容结构
description: 了解如何使用AEM内容片段模型创建结构，该结构将作为所有无头内容的基础。
hidefromtoc: true
index: false
source-git-commit: 6010fb398ec8c04ae9153f313585bcf38ccaa26d
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---


# 为应用程序创建内容结构 {#content-structure}

您可使用内容片段设计、创建、管理和发布独立于页面的内容。利用这些渠道，您可以准备内容以供在多个位置和多个渠道上使用，非常适合无头投放。 内容片段模型用于定义此内容的结构，这是您管理无头内容时首先需要创建的内容。

为了帮助您了解如何实现此目的，AEM Trials的此模块将带您完成该过程，您可以快速、交互式地浏览，首先创建模型，然后添加其结构。 本文档是对产品内导览的补充，涵盖相同步骤并在适当时链接到其他资源。

## 内容片段模型控制台 {#content-fragment-model-console}

您可以从内容片段模型控制台开始。 内容片段模型控制台可以被视为模型库。 您可以使用控制台创建新模型并管理现有模型。 控制台启动为空，因此我们创建一个新模型！

![内容片段模型控制台](assets/content-structure/content-fragment-model-console.png)

如果您希望自己在应用程序内指南之外导航到内容片段模型控制台，可以使用页面左上角的Adobe图标找到该控制台。 此时将打开AEM的全局导航。 从此处，您选择 **工具** 选项卡，然后 **常规** -> **内容片段模型**.

>[!TIP]
>
>如果您想进一步了解在AEM中导航的信息，请参阅 [“其他资源”部分](#additional-resources) 的文档，以了解有关AEM基本操作的更多信息。

## 创建模型 {#create-model}

进入内容片段模型控制台后，您可以创建一个新模型来表示您自己的无标题内容。

1. 在内容片段模型控制台中，单击 **创建** 按钮以开始创建内容片段模型。

1. 将启动“创建模型”向导，该向导将指导您创建内容片段模型。

   ![内容片段模型向导](assets/content-structure/model-wizard.png)

   提供必备信息。

   * **模型标题**  — 这是模型的简要描述，通常指明其用途。
   * **启用模型**  — 默认勾选此选项，并且必须选中此选项才能稍后基于此模型创建内容片段。

   您还可以选择添加更长的 **描述** 还有 **标记** 以便日后在内容片段模型控制台中对其进行分类并将其区分开来。

   >[!TIP]
   >
   >如果您对标记如何组织内容感兴趣，请参阅 [“其他资源”部分](#additional-resources) 的文档，以了解有关AEM中标记的更多信息。

1. 填充必填字段后，单击 **创建** 创建模型。

1. 的 **成功** 对话框确认已创建模型。

   ![用于创建新内容片段模型的成功对话框](assets/content-structure/success.png)

1. 在使用模型之前，还需要定义其数据的结构。 单击 **打开** ，以将其打开并继续定义模型。

## 向模型添加字段 {#configure-model}

内容片段模型本质上是内容片段的架构。 即，它定义模型包含的字段/数据类型。

![内容片段模型编辑器](assets/content-structure/model-editor.png)

使用内容片段模型编辑器，您可以使用拖放界面定义内容片段模型的字段。

1. 从 **数据类型** 面板，并将其拖放到内容片段模型中。 有多种数据类型可供选择，例如单行文本、多行文本、编号以及对其他片段的引用。

   ![添加数据类型](assets/content-structure/drop-fields.png)

   >[!TIP]
   >
   >如果您希望了解有关可用数据类型的更多信息，请参阅 [“其他资源”部分](#additional-resources) 文档的“内容片段模型”文档。

1. 放置数据类型后， **数据类型** 列自动更改为 **属性** 选项卡，您可以在其中定义刚刚放置的数据类型的详细信息。

   ![数据字段的属性选项卡](assets/content-structure/data-type-properties.png)

   模型的属性可能包括字段名称、字段类型、字段长度（如果为必填字段）等。

1. 使用 **属性** 选项卡来定义属性，如默认值、最大长度（如果为必填字段）等。

   >[!TIP]
   >
   >如果您希望了解有关可用属性的更多信息，请参阅 [“其他资源”部分](#additional-resources) 文档的“内容片段模型”文档。

1. 添加内容片段模型所需的所有字段后，单击 **保存** 在窗口的右上方。

1. 这会保存模型，并将您返回到内容片段模型控制台，您可以在该控制台中添加更多模型。

![模块完成](assets/content-structure/content-fragment-model-console-populated.png)

## 您已学会创建内容片段模型 {#conclusion}

在本模块中，您学习了如何创建内容片段模型以表示无头数据的结构。 首先创建模型，然后使用数据类型及其相关属性对其进行填充，从而为无头内容定义架构。

现在，您拥有自己的内容片段模型，接下来可以使用该模型创建内容片段。 模块 [创建新内容](create-content.md) 详细信息，以使用新的内容片段模型创建无标题内容。

您可以通过单击返回到试用版主屏幕 **解决方案** 按钮，然后选择 **Experience Manager**.

![导航主页](assets/content-structure/home.png)

## 其他资源 {#additional-resources}

有关内容片段和AEM的更多信息，请考虑查看此附加文档。

* [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 有关如何导航和为新用户使用AEM的文档
* [使用标记](/help/sites-cloud/authoring/features/tags.md)  — 有关如何在AEM中使用标记来组织内容的文档
* [内容片段](/help/assets/content-fragments/content-fragments.md)  — 内容片段概述以及指向有关内容片段的完整文档的链接
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 有关内容片段模型的完整文档
* [内容片段模型 — 数据类型](/help/assets/content-fragments/content-fragments-models.md#data-types)  — 有关可用于内容片段模型的各种数据类型的详细信息
* [内容片段模型 — 属性](/help/assets/content-fragments/content-fragments-models.md#data-types)  — 有关可用于内容片段模型数据类型的各种属性的详细信息
