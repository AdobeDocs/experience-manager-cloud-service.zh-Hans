---
title: 创建启动项
description: 您可以创建启动项，以允许更新现有网页的新版本，以便将来激活。
exl-id: 216ccb7a-1409-4f55-8be2-2b088f91a430
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 80%

---

# 创建启动项  {#creating-launches}

可创建启动项，以允许更新现有网页的新版本，以便将来激活。创建启动项时，需要指定标题和源页面：

* 标题会显示在[引用](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references)边栏中，作者可以从中访问这些标题以对其进行处理。
* 默认情况下，源页面的子页面包含在启动项中。必要时，可只使用源页面。
* 默认情况下，[Live Copy](/help/sites-cloud/administering/msm/overview.md) 会在源页面发生更改时自动更新启动页面。您可以指定创建一个静态副本，以防止自动更改。

（可选）您可以指定启 **动日期** （和时间）以定义何时提升和激活启动页面。 但是，启 **动日期仅与生产就绪标** 志结合使用(请 **参阅编辑启动配置**[](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration));要使动作实际自动发生，必须同时设置这两个操作。

>[!NOTE]
>
>创建启动项时，层级中上方的页面不是源页面的副本。 它们是使用模板创建的占位符：
>
>* `/libs/launches/templates/outofscope`
>
>
无法编辑这些页面。 您将看到以下消息：
>
>* **此页面未包含在启动项中。转到生产页面**


## 创建启动项 {#creating-a-launch}

您可以从“站点”或“启动项”控制台中创建启动项：

1. 打开&#x200B;**站点**&#x200B;或&#x200B;**启动项**&#x200B;控制台。

   >[!NOTE]
   >
   >使用&#x200B;**站点**&#x200B;控制台时，通常要导航到源页面的位置，但这不并是强制性的，因为您可以在向导中选择&#x200B;**启动源**&#x200B;时进行导航。

1. 根据您所使用的控制台，执行相应的操作：
   * **启动项**:
      1. 从工具栏中选择&#x200B;**创建启动项**&#x200B;以打开向导。
   * **站点**:
      1. 从工具栏中选择&#x200B;**创建**&#x200B;以打开选择框。
      1. 从该选择框中，选择&#x200B;**创建启动项**&#x200B;以打开向导。

   >[!NOTE]
   >
   >在“站 **点** ”控制台中，您还可以使用选 [择模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) ，在选择创建之前选择 **页面**。
   >
   >这将使用选定的页面作为初始源页面。

1. 在&#x200B;**选择源**&#x200B;步骤中，您需要&#x200B;**添加页面**。您可以通过指定每个页面的路径来选择多个页面：
   * 导航到所需的位置。
   * 选择源页面并确认（复选标记）。

   根据需要重复执行上述步骤。

   ![选择启动源](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >要将页面和/或分支添加到启动项中，它们必须位于站点内；即在通用顶级根目录下。
   >
   >如果站点在顶级目录下包含语言根目录，那么启动项的页面和分支必须位于通用语言根目录下。

1. 对于每个条目，您可以指定是否：

   * **包括子页面**：

      * 指定您希望创建的启动项包括还是不包括子页面。默认情况下，将包括这些子页面。

   单击&#x200B;**下一步**&#x200B;以继续。

   ![选择启动源](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. 在向导的&#x200B;**属性**&#x200B;步骤中，您可以指定：

   * **启动项标题**：启动项的名称。该名称应当体现出作者的相关信息。
   * **包含现有内容**：将使用原始内容创建启动项。
   * **使用新模板替换页面**：有关更多详细信息，请参阅[使用新模板创建启动项](#create-launch-with-new-template)。
   * **继承源页面活动数据**：选中此选项，可在源页面发生更改时自动更新启动页面的内容。此选项通过将启动项设为[Live Copy](/help/sites-cloud/administering/msm/overview.md)来实现此目的。 默认情况下，此选项处于选中状态。—>
   * **启动日期**：激活启动副本的日期和时间（取决于&#x200B;**生产就绪**&#x200B;标记；请参阅[启动项 - 事件的顺序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)）。

   ![启动项属性](/help/sites-cloud/authoring/assets/launches-properties.png)

1. 使用&#x200B;**创建**&#x200B;完成该过程并创建新启动项。确认对话框将询问您是否要立即打开该启动项：

   如果您返回控制台（单击&#x200B;**完成**），则可以从以下任一位置查看（并访问）您的启动项：

   * [**启动项**&#x200B;控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * **站点**&#x200B;控制台](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)中的&#x200B;[**引用**

### 使用新模板创建启动项 {#create-launch-with-new-template}

创建启动项时，您可以选择是否使用新模板：

>[!NOTE]
>
>此选项仅在从&#x200B;**站点**&#x200B;控制台中创建启动项时才可用。在从&#x200B;**启动项**&#x200B;控制台中创建启动项时，此选项不可用。

![使用新模板创建启动项](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

如果选中此选项，则将会：

* 更新其他可用选项，
* 包括一个新步骤，您可以在其中选择所需的模板。

![选择新模板](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>当使用不同的模板时，新页面将为空。由于页面结构不同，因此不会复制内容。
>
>此机制可用于更改[现有页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)的模板，但必须考虑到内容丢失情况。

### 创建嵌套启动项  {#creating-a-nested-launch}

通过创建嵌套启动项（一个启动项嵌套在另一个启动项中），您能够从现有启动项中创建启动项，这样作者便可以利用已经做出的更改，而不必反复地为每个启动项执行相同的更改。

>[!NOTE]
>
>另请参阅[提升嵌套启动项](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch)。

#### 创建嵌套启动项 -“启动项”控制台 {#creating-a-nested-launch-launches-console}

从&#x200B;**启动项**&#x200B;控制台创建嵌套启动项与创建任何其他形式的启动项基本相同，但需要导航到启动项分支`/content/launches`的情况除外：

1. 在&#x200B;**启动项**&#x200B;控制台中，选择&#x200B;**创建**。
1. 选择&#x200B;**添加页面**，然后通过在&#x200B;**筛选器**&#x200B;边栏中指定`/content/launches`，导航到启动项分支。 选择所需的启动项，并通过选择进 **行确认**:

   ![创建嵌套启动项](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. 单击&#x200B;**下一步**&#x200B;以继续。

1. 与任何其他启动项一样，完成&#x200B;**属性**。

1. 使用&#x200B;**Create**&#x200B;完成。

#### 创建嵌套启动项 -“站点”控制台 {#creating-a-nested-launch-sites-console}

要从&#x200B;**站点**&#x200B;控制台中基于现有的启动项创建嵌套启动项，请执行以下操作：

1. [从“引用”（“站点”控制台）中访问启动项](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)以显示可用的操作。
1. 选择 **创建启动项** ，以打开向导(由于已选择源，因此它将跳过选择源 **步骤** )。
1. 输入&#x200B;**启动项标题**&#x200B;和任何其他所需的详细信息（与常规启动项一样）。
1. 使用&#x200B;**创建**&#x200B;完成该过程并创建新启动项。确认对话框将询问您是否要立即打开该启动项：

如果选择 **完成**，您将返回到站点控制台的引 **用边栏****** ，如果您选择了相应的页面，则会显示新的启动项。

### 删除启动项 {#deleting-a-launch}

您可以从[“启动项”控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)中删除启动项：

* 通过点按/单击缩略图选择相应的启动项。
* 此时将显示工具栏 - 选择“删除”。
* 确认该操作。

>[!CAUTION]
>
>删除启动项时，将会删除该启动项本身及其所有下级嵌套启动项。
