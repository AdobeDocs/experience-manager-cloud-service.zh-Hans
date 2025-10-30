---
title: 内容片段内的启动
description: 了解如何在Adobe Experience Manager as a Cloud Service中使用内容片段启动项 通过启动项，您可以高效地为未来版本开发内容，同时维护当前内容片段。
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
exl-id: c0b9e571-3be5-42ab-8d56-d93e8ef4c2f7
source-git-commit: 39ff527f0082a18f0853964172eabf438caa1098
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 2%

---

# 内容片段内的启动 {#launches-for-content-fragments}

在Adobe Experience Manager (AEM) as a Cloud Service中，通过启动项，您可以高效地为未来版本开发内容。

创建&#x200B;*Launch*&#x200B;是为了允许您进行更改以准备将来发布，同时维护当前内容。 对于内容片段，这意味着您同时有效地编辑两个版本：当前发布的内容以及将来一次发布的该内容的版本。 到达该时间后，您可以替换原始内容片段的内容并发布新版本。

>[!NOTE]
>
>启动项也可用于页面。 基本概念相同，但有关如何在AEM中管理这些概念存在差异。
>
>有关完整的详细信息，请参阅[页面启动项](/help/sites-cloud/authoring/launches/overview.md)。

您创建一个&#x200B;*启动项*，然后在&#x200B;*启动项*&#x200B;中编辑和更新内容片段。 如果在此阶段对&#x200B;*Source*&#x200B;片段进行了更改，则可以使用&#x200B;*重新库*&#x200B;操作将其复制到&#x200B;*Launch*。 准备就绪后，*Promote*&#x200B;将启动内容复制回源。 然后，您可以手动或自动激活源片段（具体取决于创建和编辑启动项时设置的字段）。 您还可以指定是否将引用的片段包含在此进程中。

例如，您在线商店的季节性产品片段每季度更新一次，以便特色产品与当季保持一致。 要准备下一次季度更新，您可以创建相应片段的启动项。 在整个季度期间，启动副本中会累积以下更改：

* 直接在启动片段上执行的编辑，为下一季度做准备。
* 更改您通过&#x200B;*Rebase*&#x200B;传输到启动页面的源内容片段。
* 您还可以导航启动项分支中的内容；根据需要添加或删除片段。

当下一季度到来时，您需要提升启动页面，以便发布源页面（包含更新的内容）。 您可以升级所有片段，也可以仅升级已修改的片段。

![启动项概述 — Rebase和Promote](/help/sites-cloud/administering/content-fragments/assets/cf-launches-overview.png)

本节介绍如何从[内容片段控制台](/help/sites-cloud/administering/content-fragments/managing.md)中创建、编辑、管理、重新设置、提升以及根据需要删除启动项：

* [在内容片段控制台中访问和查看启动项](#launches-in-the-content-fragment-console)
* [创建启动项](#create-a-launch)
* [编辑启动项内容](#edit-launch-content)
* [管理启动项中的内容](#manage-content-within-a-launch)
* [将发布项与源进行比较](#compare-launch-to-source)
* [从Source重新确定启动项的基础](#rebase-a-launch-from-source)
* [将启动项提升至Source](#promote-a-launch-to-source)
* [删除启动项](#delete-a-launch)

## 内容片段控制台中的启动项 {#launches-in-the-content-fragment-console}

内容片段控制台的&#x200B;**启动项**&#x200B;选项卡允许您创建启动项、列出所有现有启动项、查看关键属性并对它们执行操作。

如果未选择任何启动项，您可以[创建新的启动项](#create-a-launch)。

控制台中的![启动项选项卡](/help/sites-cloud/administering/content-fragments/assets/cf-launches-tab.png)

选择要显示的启动项：

* 工具栏，其中包含可用的操作
* 右侧面板，其中显示了属性和进一步操作

控制台![启动操作工具栏](/help/sites-cloud/administering/content-fragments/assets/cf-launches-actions.png)

利用工具栏，您可以：

* **[打开启动项](#edit-launch-content)**
* **[编辑源](#manage-content-within-a-launch)**
* **[将启动项与Source进行比较](#compare-launch-to-source)**
* **[提升](#promote-a-launch-to-source)**
* **[重定基数](#promote-a-launch-to-source)**
* **[删除启动项](#delete-a-launch)**

而右侧面板使您能够：

* 编辑启动项&#x200B;**标题**
* 编辑启动项&#x200B;**描述**
* 更新在[创建启动项](#create-a-launch)时设置的配置详细信息：

   * **包含引用**：创建包含或不包含任何引用的内容片段的启动项。 默认情况下，包含引用的片段。

      * 在稍后阶段，当您[在启动项](#manage-content-within-a-launch)中添加或删除片段时，引用的片段也会受到影响。

     >[!NOTE]
     >
     >查看[有关包含的引用的详细信息](#details-concerning-included-references)

   * **发布就绪**；启用此切换将在启动项提升到源时自动发布片段。

* 并且还定义：

   * **提升日期**&#x200B;和时间：如果要自动提升[启动项](#promote-automatically)

## 创建启动项 {#create-a-launch}

要创建启动项，请执行以下操作：

1. 导航到内容片段控制台。

1. 打开&#x200B;**启动项**&#x200B;选项卡。

1. 选择&#x200B;**创建启动项**。

1. 导航到相应的文件夹，然后选择要包含在启动项中的片段：

   ![为新启动项选择内容片段](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-select-cfs.png)

1. 选择&#x200B;**下一步**。

1. 指定详细信息以配置启动项：

   * **标题**
   * **描述**
   * **包含引用**：创建包含或不包含任何引用的内容片段的启动项。 默认情况下，包含引用的片段。

     >[!NOTE]
     >
     >查看[有关包含的引用的详细信息](#details-concerning-included-references)

   * **发布就绪**：启用此切换将在启动项提升到源时自动发布片段。

   新启动项的![详细信息](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-launch-details.png)

1. **保存**&#x200B;配置。

1. 您将返回到内容片段控制台的&#x200B;**启动项**&#x200B;选项卡，其中：

   * 您的新启动项现已列出
   * 此时将显示一条消息，确认启动项创建已开始：

      * **作业已开始创建新的启动项，在AEM中监视进度并在完成后重新加载页面。**

1. 从消息框中选择&#x200B;**查看**，以便在AEM控制台中查看[后台操作](/help/operations/asynchronous-jobs.md)的详细信息。

   在控制台中![新建启动项](/help/sites-cloud/administering/content-fragments/assets/cf-launches-new-launch-in-console.png)

## 编辑启动项内容 {#edit-launch-content}

要在启动项中编辑内容片段，请执行以下操作：

1. 导航到内容片段控制台。

1. 打开&#x200B;**启动项**&#x200B;选项卡。

1. 选择您的启动项以显示工具栏操作。

1. 选择&#x200B;**打开启动项**。

   此时将显示您的启动项及其包含的片段。

   ![编辑启动项内容](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-launch-content.png)

1. 为要更新的片段选择&#x200B;**编辑**。 它将照常在[片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md)中打开。

## 管理启动项中的内容 {#manage-content-within-a-launch}

要管理启动项中的内容片段并编辑其内容，请执行以下操作：

1. 导航到内容片段控制台。

1. 打开&#x200B;**启动项**&#x200B;选项卡。

1. 选择您的启动项。

1. 选择&#x200B;**编辑源**。

   将显示启动项的源片段。

   ![编辑Source](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-sources.png)

1. 您可以：

   1. **添加源**&#x200B;以将更多片段添加到您的启动项。

      * 如果启动项的&#x200B;**包括引用**&#x200B;为true，则所有引用的内容片段也将引入到启动项中（如果尚不存在）。

   1. 为要更新的源片段选择&#x200B;**编辑**。 它将照常在[片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md)中打开。

   1. 选择一个片段，然后从工具栏中选择&#x200B;**删除源**&#x200B;操作以从启动项中删除该片段。

      * 如果启动项的&#x200B;**包括引用**&#x200B;为true，则所有引用的内容片段也将从启动项中删除 — 除非它们也由仍在启动项中的其他内容片段引用。

   >[!NOTE]
   >
   >查看[有关包含的引用的详细信息](#details-concerning-included-references)

## 将发布项与源进行比较 {#compare-launch-to-source}

建议您在执行任何Rebase或Promote操作之前，始终比较源和启动项，以确认更改及其对内容的影响（这两个操作都会覆盖目标内容）：

1. 导航到内容片段控制台。

1. 打开&#x200B;**启动项**&#x200B;选项卡。

1. 选择您的启动项。

1. 选择&#x200B;**将启动项与Source进行比较**。

   * 源和启动片段并排显示以突出显示差异。
      * Source片段显示在左侧，Launch片段显示在右侧。
      * 更新会突出显示：
         * Source：蓝色
         * 发布：粉红色
         * 冲突：黄色
   * [Promote](#promote-a-launch-to-source)和[Rebase](#rebase-a-launch-from-source)操作在右上角可用。
   * **发现更新**：在左上角显示所有更新的摘要。 以蓝色显示的源更新数、以粉红色显示的启动更新数以及以黄色显示的对两个（冲突）的更新数。
      * 利用眼睛图标，可显示或隐藏实际内容更新，以更清楚地了解概述。
   * **Include**&#x200B;滑块允许您定义要包含在后续Promote或Rebase操作中的内容片段：
      * 右上方的&#x200B;**包含全部**
      * 启动项中每个片段上方的&#x200B;**包含**

     >[!NOTE]
     >
     >滑块仅适用于从“比较”屏幕中执行的“提升”和“重新定位”操作。

   * 片段内容在字段级别（内容片段元素/数据类型级别）显示；突出显示指示更改。
   * 选择&#x200B;**视图**&#x200B;以重新计算差异。

   ![比较Source和Launch](/help/sites-cloud/administering/content-fragments/assets/cf-launches-compare.png)

## 重新确定启动项的基础(来自Source) {#rebase-a-launch-from-source}

当对源片段进行了更新并且您想要将这些更改复制到启动项时：

1. 导航到内容片段控制台。

1. 打开&#x200B;**启动项**&#x200B;选项卡。

1. 选择您的启动项和片段。

1. 选择&#x200B;**重基**。

>[!NOTE]
>
>您也可以&#x200B;**重新定位**&#x200B;从&#x200B;**[比较启动项到Source](#compare-launch-to-source)**&#x200B;的启动项。

## 提升启动项(到Source) {#promote-a-launch-to-source}

当您的启动项准备好发布时，应将其复制到源。 您可以在控制台中执行这项操作，也可以配置设置，使其在特定日期和时间自动执行。

### 手动提升 {#promote-manually}

当您的启动项准备好发布时，可以通过显式操作将其复制到源：

1. 导航到内容片段控制台。

1. 打开&#x200B;**启动项**&#x200B;选项卡。

1. 选择您的启动项和片段。

1. 选择&#x200B;**提升**。

>[!NOTE]
>
>您也可以&#x200B;**将**&#x200B;启动项从&#x200B;**比较启动项与Source**&#x200B;提升。

### 自动提升 {#promote-automatically}

要在指定的日期和时间自动提升启动项，您需要：

1. 从&#x200B;**启动项选项卡**&#x200B;的右侧面板中定义[提升日期](#launches-in-the-content-fragment-console)和时间。

1. 如果内容可以在提升时发布，请在&#x200B;**创建启动项**&#x200B;时设置[发布就绪](#create-a-launch)，或从[启动项选项卡](#launches-in-the-content-fragment-console)的右侧面板设置。

## 删除启动项 {#delete-a-launch}

提升您的启动项，或决定不再需要它后，您可以将其删除：

1. 导航到内容片段控制台。

1. 打开&#x200B;**启动项**&#x200B;选项卡。

1. 选择您的启动项。

1. 选择&#x200B;**删除启动项**。

   系统将会要求您在删除启动项之前确认该操作。

## 有关包含的引用的详细信息 {#details-concerning-included-references}

对于启动项，将考虑以下内容片段引用，具体取决于[数据类型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)：

* **片段引用**&#x200B;数据类型，适用于单片段引用和多字段片段引用。
* 使用&#x200B;**富文本**&#x200B;时，在&#x200B;**多行文本**&#x200B;数据类型内引用的片段。

所有要点也适用于变量中引用的片段

不考虑以下各项：

* 内容引用数据类型内引用的片段，包括&#x200B;**内容引用** （基于路径）和&#x200B;**内容引用(UUID)**。
* 在&#x200B;**片段引用(UUID)**&#x200B;数据类型内引用的片段。
