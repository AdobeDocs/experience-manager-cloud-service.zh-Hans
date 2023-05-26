---
title: 管理项目
description: 通过“项目”，您可以将资源分组到一个实体中，以便在“项目”控制台中对其进行访问和管理，从而组织项目
exl-id: be4616e7-18bc-4b2d-89f6-d04178ac7f3a
source-git-commit: 54a098d8986c8bbd740bed50f8625c1025d2f6f4
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 51%

---

# 管理项目 {#managing-projects}

通过“项目”，您可以将资源分组到一个实体中来组织项目。

在 **项目** 控制台中，您可以访问您的项目并对其执行操作：

![“项目”控制台](/help/sites-cloud/authoring/assets/projects-console.png)

在“项目”中，您可以创建项目、将资源与项目相关联，还可以删除项目或资源链接。 您可能需要打开图块以查看其内容并向图块中添加项目。 本主题将介绍这些过程。

## 创建项目 {#creating-a-project}

AEM提供了这些现成的模板，可在创建项目时从中进行选择：

* 简单项目
* 媒体项目
* 翻译项目

<!-- Hiding product photoshoot via cqdoc-18072 as it is not available in Skyline.
* Product Photo Shoot Project 
-->

从项目到项目，创建项目的过程相同。 项目类型之间的差异包括可用的用户角 [色](/help/sites-cloud/authoring/projects/overview.md) 和工 [作流](/help/sites-cloud/authoring/projects/workflows.md)。  要创建新项目，请执行以下操作：

1. 在“ **项目**”中，点按／单 **击创建** ，以打开创 **建项目向导** :
1. 选择模板并单击&#x200B;**下一步**。

   ![创建项目](/help/sites-cloud/authoring/assets/projects-create.png)

1. 定义&#x200B;**标题**&#x200B;和&#x200B;**描述**，然后根据需要添加&#x200B;**缩略图**&#x200B;图像。您还可以添加或删除用户及其所属的组。 此外，单击 **高级** 以添加URL中使用的名称。

   ![添加项目详细信息](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. 点按/单击&#x200B;**创建**。确认会询问您是要打开新项目还是返回到控制台。

### 将资源与项目关联 {#associating-resources-with-your-project}

由于项目允许您将资源分组到一个实体中，因此要将资源与项目相关联。 这些资源称为 **磁贴**. 有关可添加的资源类型的说明，请参见 [项目拼贴](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

要将资源与项目关联，请执行以下操作：

1. 从打开您的项目 **项目** 控制台。
1. 点按/单击 **添加拼贴** 并选择要链接到项目的拼贴。 您可以选择多种类型的拼贴。

   ![将拼贴添加到项目](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >有关可与项目关联的项目拼贴的详细说明，请参阅[项目拼贴](/help/sites-cloud/authoring/projects/overview.md#project-tiles)。

1. 点按/单击&#x200B;**创建**。您的资源随即会链接到项目，从现在开始，您便可以从项目中访问该资源。

### 删除项目或资源链接 {#deleting-a-project-or-resource-link}

可使用同样的方法从控制台中删除项目或项目中的链接资源：

1. 导航到相应的位置：

   * 要删除项目，请转到 **项目** 控制台。
   * 要删除项目中的资源链接，请在&#x200B;**项目**&#x200B;控制台中打开相应的项目。

1. 单击&#x200B;**选择**&#x200B;并选择您的项目或资源链接，以进入选择模式。
1. 点按/单击&#x200B;**删除**。

1. 您需要在对话框中确认删除。 如果确认，将删除项目或资源链接。 点按/单击&#x200B;**取消选择**&#x200B;可退出选择模式。

>[!NOTE]
>
>在创建项目并将用户添加各种角色时，将自动创建与项目关联的组以管理关联的权限。例如，名为 Myproject 的项目将有三个组，分别为 **Myproject 所有者**、**Myproject 编辑者**、**Myproject 观察者**。但是，如果删除了项目，这些组不会自动删除。管理员需要在&#x200B;**工具** > **安全** > **组**&#x200B;中手动删除这些组。

### 将项目添加到图块 {#adding-items-to-a-tile}

在某些图块中，您可能希望添加多个项目。 例如，您可能同时运行多个工作流或多个体验。

要将项目添加到拼贴，请执行以下操作：

1. 在&#x200B;**项目**&#x200B;中，导航到相应的项目，然后点按或单击要将项目添加到的拼贴上的向下 V 形。

   ![将项目添加到拼贴](/help/sites-cloud/authoring/assets/project-workflows.png)

1. 像创建新图块时一样将项目添加到图块。 描述了项目拼贴 [此处](/help/sites-cloud/authoring/projects/overview.md#project-tiles). 在此示例中，添加了另一个工作流。

### 打开拼贴 {#opening-a-tile}

您可能希望查看当前图块中包含哪些项目，或者修改或删除图块中的项目。

要打开拼贴以便查看或修改项目，请执行以下操作：

1. 在“项目”控制台中，点按/单击信息卡底部的省略号(...)图标。

   ![打开拼贴](/help/sites-cloud/authoring/assets/project-links.png)

1. AEM会列出该图块中的项目。 您可以进入选择模式以修改或删除项目。

   ![已打开拼贴](/help/sites-cloud/authoring/assets/projects-add-link.png)

## 查看项目统计信息 {#viewing-project-statistics}

您可以在&#x200B;**项目**&#x200B;控制台中查看项目统计信息。

### 查看项目时间线 {#viewing-a-project-timeline}

项目时间线提供了项目中的资产上次使用时间的相关信息。要查看项目时间线，请单击/点按&#x200B;**时间线**，然后进入选择模式并选择项目。资产会显示在左侧窗格中。单击/点按&#x200B;**时间线**&#x200B;可返回到&#x200B;**项目**&#x200B;控制台。

![项目时间线](/help/sites-cloud/authoring/assets/projects-timeline.png)

### 查看活动/不活动的项目 {#viewing-active-inactive-projects}

要在活动和不活动的项目之间切换，请在&#x200B;**项目**&#x200B;控制台中单击&#x200B;**切换活动的项目**。如果该图标旁边显示有复选标记，则显示的是活动的项目。

![“切换活动项目”按钮](/help/sites-cloud/authoring/assets/projects-active.png)

如果该图标旁边显示有一个 x，则显示的是不活动的项目。

![“切换不活动项目”按钮](/help/sites-cloud/authoring/assets/projects-inactive.png)

## 使项目处于非活动或活动状态 {#making-projects-inactive-or-active}

如果您已完成某个项目，但仍希望保留该项目上的信息，则可能需要使该项目处于非活动状态。

要使项目处于非活动状态（或活动状态），请执行以下操作：

1. 在 **项目** 控制台，打开您的项目，然后找到 **项目信息** 图块。

   >[!NOTE]
   如果此图块尚未在项目中存在，您可能需要添加它。 参见 [添加拼贴](#adding-items-to-a-tile).

1. 点按/单击&#x200B;**编辑**。
1. 将选择器从&#x200B;**活动**&#x200B;更改为&#x200B;**不活动**（反之亦然）。

   ![激活项目](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. 点按/单击&#x200B;**完成**&#x200B;以保存更改。
