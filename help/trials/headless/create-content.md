---
title: 创建无头内容
description: 使用您之前创建的内容片段模型来创建可用于页面创作的内容，或者用作无标题内容的基础。
hidefromtoc: true
index: false
source-git-commit: 7d5161d97a93d4731e33eda586179560a6a55ef3
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---


# 创建无头内容 {#create-content}

通过学习产品内学习模块，了解如何使用 [您之前创建的内容片段模型](content-structure.md) 创建可用于页面创作的内容，或作为无标题内容的基础。 本文档是交互式导览的补充，涵盖相同的步骤，并酌情链接到其他资源。

## 内容片段 {#introduction}

在AEMas a Cloud Service中，内容片段是基于内容片段模型定义的结构的无标题内容片段。 您可以从内容片段控制台中开始，创建您自己的内容片段。 “内容片段”控制台可以被视为无标题内容的库。 您可以使用控制台创建新的内容片段并管理现有的片段。 您的控制台启动为空，因此让我们创建一个新片段！

![编辑片段的内容](assets/create-content/content-fragment-console.png)

如果您希望自己在应用程序内指南之外导航到内容片段控制台，可以使用页面左上角的Adobe图标找到该控制台。 此时将打开AEM的全局导航。 从此处，您选择 **导航** 选项卡，然后 **内容片段**.

>[!TIP]
>
>如果您想进一步了解在AEM中导航的信息，请参阅 [“其他资源”部分](#additional-resources) 的文档，以了解有关AEM基本操作的更多信息。

## 创建内容片段 {#create-fragment}

内容片段代表您的无头内容。 但是，它们只能基于预定义的内容结构创建。 您之前创建的内容片段模型将用作该结构。

1. 点按或单击 **创建** 按钮以打开 **新内容片段** 对话框以开始创建新的内容片段。

   ![“创建内容片段”对话框](assets/create-content/create-content-fragment.png)

1. 如果您遵循应用程序内指南， **位置** 将自动填充。

   1. 如果您没有遵循指南，请使用路径浏览器选择您的项目文件夹。

   1. 在 **新内容片段** 对话框，点按或单击 **选择位置** 按钮 **位置** 字段。

      ![“选择位置”对话框](assets/create-content/choose-location.png)
   * 或者，在单击之前，在内容片段控制台的左侧导航面板中选择路径 **创建**.


1. 在 **内容片段模型** 下拉菜单中，从下拉菜单中选择您之前创建的内容片段模型。

1. 添加 **标题** （对于内容片段）。

1. 点按或单击 **创建并打开**.

## 内容片段编辑器 {#edit-fragment}

保存新的内容片段后，将打开内容片段编辑器，您可以在其中提供片段的实际内容。

1. 编辑器会显示在所选模型中定义的字段。 您可以在此编辑它们以完成内容片段。 您的进度会自动保存。

   ![内容片段编辑器](assets/create-content/content-fragment-editor.png)

1. 如果内容片段的模型具有多个字段，则可以使用 **变量** 面板。 此处将标记有错误的字段。

1. 为了让内容片段可供外部应用程序使用，您需要发布该内容片段。 点按或单击 **发布** 按钮。

1. 选择 **现在** 从下拉菜单中。 您还可以安排在以后发布。

   ![“发布”按钮](assets/create-content/publish.png)

   >[!TIP]
   >
   >如果您想进一步了解有关在AEM中发布内容的信息，请参阅 [“其他资源”部分](#additional-resources) 的详细信息。

1. AEM会自动执行引用检查，以确保为内容片段发布了所有必需的资源。 在这种情况下，您还需要发布您创建的模型。 点按或单击&#x200B;**发布**。

   ![引用检查](assets/create-content/references.png)

1. 在横幅中确认发布。

   ![发布确认](assets/create-content/publish-confirm.png)

## 您已学习如何创建内容片段！ {#conclusion}

在本模块中，您学习了如何根据之前创建的模型创建内容片段。 这是内容作者如何创建结构化无标题内容的。

现在，您的内容已创建并发布，接下来可以通过AEM API通过图形QL提取该内容。 您将在模块中了解此信息 [通过GraphQL API提取内容。](extract-content.md)

您可以通过单击返回到试用版主屏幕 **解决方案** 按钮，然后选择 **Experience Manager**.

![导航主页](assets/create-content/home.png)

## 其他资源 {#additional-resources}

有关内容片段和AEM的更多信息，请考虑查看此附加文档。

* [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 有关如何导航和为新用户使用AEM的文档
* [管理内容片段 — 发布和引用](/help/assets/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment)  — 有关如何在AEM中发布内容的详细信息
* [内容片段](/help/assets/content-fragments/content-fragments.md)  — 内容片段概述以及指向有关内容片段的完整文档的链接
* [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)  — 如何创建和管理内容片段
