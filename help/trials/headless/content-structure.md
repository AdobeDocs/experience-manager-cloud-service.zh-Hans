---
title: 为您的应用程序创建内容结构
description: 了解如何使用 AEM 的内容片段模型创建用作所有 Headless 内容的基础的结构。
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 38%

---


# 为您的应用程序创建内容结构 {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="为您的应用程序创建内容结构"
>abstract="按照本系列交互式指南，您将学习如何创建一个结构（称为内容片段模型），该结构将用作无头内容的基础。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="启动模型控制台"
>abstract="让我们来探索如何在Adobe Experience Manager as a Cloud Service中为您的内容创建一个称为内容片段模型的可重用架构。 请观看视频，以了解为什么这是一个重要步骤。 <br><br>在新选项卡中单击下面的按钮以启动此模块，然后按照本指南操作。"
>additional-url="https://video.tv.adobe.com/v/3413261" text="内容结构介绍视频"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="恭喜！您学习了如何创建内容片段模型以表示无头数据的结构，并采取了第一步，以缩放和标准方式提供全渠道内容。"
>abstract=""

## 创建模型 {#create-model}

单击 **启动模型控制台** 上方的按钮会在新选项卡中打开内容片段模型控制台。

![内容片段模型控制台](assets/content-structure/content-fragment-model-console.png)

将内容片段模型控制台视为模型库，您可以在此创建新模型并管理现有模型。 您的控制台最初是空的，让我们创建一个新模型！

1. 在内容片段模型控制台中，单击屏幕右上角的&#x200B;**创建**&#x200B;按钮开始创建内容片段模型。

1. 此时将启动“创建模型”向导，该向导将指导您。

   ![内容片段模型向导](assets/content-structure/model-wizard.png)

   提供必要信息。

   * **模型标题**  — 这是对模型的简要描述，通常指明模型的用途。
   * **启用模型**  — 默认勾选此选项，并且必须选中此选项才能基于此模型创建内容片段。

1. 填写必填字段后，单击 **创建** 创建模型。

1. **成功**&#x200B;对话框用于确认模型已创建。

   ![用于创建新内容片段模型的“成功”对话框](assets/content-structure/success.png)

## 将字段添加到模型 {#configure-model}

在使用模型之前，您需要定义其数据的结构。

1. 单击 **打开** 在 **成功** 对话框，以在内容片段模型编辑器中打开新模型，您可以在其中定义其字段。

1. 从 **数据类型** 面板，并将其拖放到内容片段模型中。

   ![添加数据类型](assets/content-structure/drop-fields.png)

1. 放置数据类型后，**数据类型**&#x200B;列将自动变为&#x200B;**属性**&#x200B;选项卡，您可以在其中定义刚刚放置的数据类型的详细信息。

   ![数据字段的“属性”选项卡](assets/content-structure/data-type-properties.png)

1. 添加内容片段模型所需的所有字段后，单击窗口右上角的&#x200B;**保存**。

随即会保存模型，并返回到内容片段模型控制台，您可以在该控制台中根据需要添加更多模型。

![模块完成](assets/content-structure/content-fragment-model-console-populated.png)
