---
title: 为您的应用程序创建内容结构
description: 了解如何使用 AEM 的内容片段模型创建用作 Headless 内容的基础的内容结构。
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
feature: Headless
role: Admin, User, Developer
source-git-commit: c9cddf9f0e344a2a24ee1a608b3ea920e258f34a
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 100%

---


# 为您的应用程序创建内容结构 {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="为您的应用程序创建内容结构"
>abstract="您按照此系列的交互式指南学习如何创建一个结构（也称为内容片段模型），它充当您的 Headless 内容的基础结构。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="启动模型控制台"
>abstract="让我们探讨如何在 Adobe Experience Manager as a Cloud Service 中为您的内容创建一个可重复使用的架构，即内容片段模型。观看视频以了解为什么这一步很重要。<br><br>在本学习单元中，您会以一个旅游网站为例，演练如何创建一个展示旅行的模型。<br><br>单击下方按钮在新选项卡中启动该模块，然后遵循该指南。"
>additional-url="https://video.tv.adobe.com/v/3436550?captions=chi_hans" text="内容结构介绍视频"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="恭喜！您学习了如何创建内容片段模型来表示 Headless 数据的结构，并迈出了以缩放和标准方式交付全渠道内容的第一步。"
>abstract=""

## 创建模型 {#create-model}

内容片段模型控制台将在新选项卡中打开。将内容片段模型控制台想象为您的模型库，您可以在其中创建模型和管理现有模型。

在该示例中，您通过创建一个模型来表示旅游网站上的旅行数据结构。此模型中使用的旅行被称为&#x200B;**冒险。**

1. 在屏幕的右上角，单击&#x200B;**创建**&#x200B;以开始创建内容片段模型。

1. 创建模型向导会引导您完成模型的创建。提供必要信息。

   * **模型标题** – 这是模型的简要标记，通常指明了该模型的用途。您可以调用新模型。`Adventure`
   * **启用模型** – 此选项默认处于选中状态，必须选中它才能基于此模型创建内容片段。

1. 填充必填字段后，单击右上角的&#x200B;**创建**&#x200B;以创建模型。

1. **成功**&#x200B;对话框用于确认模型已创建。单击对话框中的&#x200B;**打开**&#x200B;以在一个新选项卡的编辑器中打开新的内容片段模型。然后继续下一步，将数据字段添加到您的模型中。

![创建内容片段模型的第二步和第三步](assets/do-not-localize/create-model.png)

## 使用模型编辑器 {#configure-model}

您现在有一个叫做&#x200B;**冒险**&#x200B;的模型，但它没有持续时间、目的地、活动等详细信息。您必须先定义模型的数据结构，之后才能使用模型。

内容片段模型编辑器是您配置用于定义模型内容的数据类型和属性的地方。

>[!TIP]
>
>遵循以下说明中的命名模式非常重要，因为在后面的模块中会引用这些特定名称。

1. 从编辑器右侧的&#x200B;**数据类型**&#x200B;面板中拖动一个&#x200B;**单行文本**&#x200B;字段，并将该字段放置到您的内容片段模型上。

1. 放置数据类型后，**数据类型**&#x200B;列将自动变为&#x200B;**属性**&#x200B;选项卡，您可以在其中定义放置的数据类型的详细信息。对于第一个字段，您要存储旅行或冒险的标题。输入以下属性：

   * **呈现为：****文本字段** – 当您创建冒险时，此字段会存储该冒险的标题。
   * **字段标签：**`Title` – 创建冒险时为该字段显示的标签。

1. 定义字段属性后，您可以切换回右侧面板中的&#x200B;**数据类型**&#x200B;选项卡，并通过拖放添加其他字段。

通过这种方式，您可以根据需要向模型添加尽可能多的字段，以支持您需要的任何数据结构。数据字段的类型各不相同，但将它们添加到模型的流程是一样的。

继续下一节，添加完成和保存&#x200B;**冒险**&#x200B;模型所需的字段

![向模型添加字段的第一步、第二步和第三步](assets/do-not-localize/define-model-fields.png)

## 将字段添加到模型 {#additional-fields}

您已经有一个用于冒险标题的字段。现在您需要通过添加字段来捕获该冒险的描述、价格和代表性图像。

>[!TIP]
>
>该&#x200B;**冒险**&#x200B;模型基于 AEM 的 WKND 示例站点。您可以[在这里访问 WKND 网站](https://wknd.site/us/en/adventures/yosemite-backpacking.html)，以查看使用&#x200B;**冒险**&#x200B;模型的内容。

按照与上述相同的步骤添加这些附加字段。其中唯一的区别是您必须设置的属性。

1. 通过拖放&#x200B;**多行文本**&#x200B;字段，添加一个字段来存储冒险的描述，并输入以下属性：

   * **呈现为：****文本域** – 当您创建冒险时，此字段会存储该旅行的简要描述。
   * **字段标签：**`Description` – 创建冒险时为该字段显示的标签。
   * **默认类型**：**纯文本** - 此示例所需的格式。

1. 通过拖放&#x200B;**单行文本**&#x200B;字段，添加一个字段来存储冒险的价格，并输入以下属性：

   * **呈现为：****文本字段** – 当您创建冒险时，此字段会存储该行程的价格。
   * **字段标签：**`Price` – 创建冒险时为该字段显示的标签。

1. 添加一个字段来存储表示行程的图像。AEM 中的图像会存储为另一种类型的内容，称为&#x200B;**资源**。要为他们创建一个字段，拖放一个引用图像资源的&#x200B;**内容引用**&#x200B;字段。

   * **呈现为：****内容引用** – 当您创建冒险时，此字段会指向代表此旅行的图像资源。
   * **字段标签：**`Image` – 创建冒险时为该字段显示的标签。
   * **根路径：**`/content/dam/aem-demo-assets/en` - 此项指定在用资源选择器浏览资源时的起点路径。

1. 添加内容片段模型所需的字段后，在窗口右上角，请单击&#x200B;**保存。**

1. 模型将进行保存，并且您将返回到内容片段模型控制台。
