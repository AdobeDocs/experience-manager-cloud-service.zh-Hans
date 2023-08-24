---
title: 学习创作基础知识
description: 了解使用内容片段为 Headless CMS 创作内容的概念和机制。
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: ht
source-wordcount: '1714'
ht-degree: 100%

---

# 使用 AEM 为 Headless 创作基本内容 {#author-headless-basics}

## 迄今为止的故事 {#story-so-far}

在 [AEM Headless 内容作者历程](overview.md)的开头，[简介](introduction.md)涵盖了与针对 Headless 进行创作相关的基本概念和术语。

本文基于这些内容编写，以便您了解如何为 AEM Headless 项目创作您自己的内容。

## 目标 {#objective}

* **受众**：初学者
* **目标**：介绍 Headless CMS 创作的基础知识：
   * 使用 AEMaaCS 进行创作简介
   * 内容片段简介

## 基本处理 {#basic-handling}

在您掌握内容片段之前，这里提供了有关如何使用 AEM 的（非常）简短的介绍....但没有什么能真正取代登录和尝试使用系统的体验。

### “创作”、“预览”和“发布” {#author-preview-publish}

AEM 安装通常包含三个环境：

* 创作
* 发布
* 预览

您登录并使用创作环境来生成您的内容。准备就绪后，您可以发布您的内容以使其公开可用。对于 Headless，这针对的是其他应用程序；对于网页，这针对的是网络上的读者。

有关更多详细信息，请参阅创作概念。

从&#x200B;**内容片段**&#x200B;控制台，您也可以在发布前发布到&#x200B;**预览服务**，以进行测试和预览。请参阅“发布和预览片段”。

### 登录 {#signing-in}

与大多数系统一样，您需要登录。作为作者，您会获得：

* 用户（帐户）名
* 密码
* 用于访问登录屏幕的链接

您的帐户将配置有您需要的任何权限。如果您有任何问题，Adobe 建议您联系您的内部项目支持团队。

### 导航 {#navigation}

首次登录时，简短的在线教程将重点介绍用户界面的一些主要功能。

之后，您可以使用导航面板访问 AEM 的关键区域。对于内容片段，您要使用&#x200B;**内容片段**&#x200B;控制台（对于某些操作，您还将使用 **Assets** 控制台）。

可以通过依次选择左上角的 Adobe 图标和小型指南针图标来打开导航面板。

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>虽然内容片段是 AEM **Sites** 的一项功能，但它们将另存为&#x200B;**资源**。这是一个技术细节，应该不会影响您，但了解它可能会有所帮助。

在控制台中，您可以在左侧面板中选择文件夹以导航到您的内容片段。您也可以过滤和/或搜索。

![内容片段控制台](/help/sites-cloud/administering/content-fragments/assets/cfc-console-filter.png)

### 操作、选择、查看 {#actions-selecting-viewing}

在&#x200B;**内容片段**&#x200B;控制台的工具栏中，为您的内容片段提供了一系列操作：

<!-- ![Console actions](assets/cfm-managing-cf-console-01.png) -->

* **在资源中打开**
* **创建**
* **引用者**&#x200B;列还提供了显示该片段的所有父引用的直接链接；包括引用内容片段、体验片段和页面。
* 将鼠标悬停在文件夹名称上将显示 JCR 路径。

选择片段后，所有适当的操作均可用：

<!-- ![Console actions - fragment selected](assets/cfm-managing-cf-console-selected-01.png) -->

* **打开**
* **发布**（和 **取消发布**）
* **复制**
* **移动**
* **重命名**
* **删除**

>[!NOTE]
>
>“发布”、“取消发布”、“删除”、“移动”、“重命名”、“复制”等操作会触发异步作业。可以通过 AEM 异步作业 UI 监控该作业的进度。

<!--
The **Assets** console has dedicated **Action Toolbars**, and **Quick Actions** that you can use after selecting a resource (for example, a folder or content fragment).

The Quick Actions are available for a single resource, see **Basel** in the example below:

![Quick Actions](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

The Actions Toolbar provides access to the full range of actions - applicable for the current scenario. The actions available can change; for example, dependent on your location, or whether you have selected multiple resources:

![Action Toolbar](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

You can select the format for viewing your resources with the View Selector:

![View Selector](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

You can view additional information about items using the Rail Selector. This also gives access to additional actions.

![Left Rail](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)
-->

## 创作内容片段 {#authoring-content-fragments}

虽然这是对 AEM 用户界面 (UI) 的非常简要的介绍，但希望您有机会尝试一下。现在，我们开始探究您真正感兴趣的内容 – Headless 的内容片段。

我们必须从头到尾探究这些内容，但您的实例可能已创建文件夹和/或片段，并且它们可能位于不同的位置。准则是一样的。

### 编排和导航 {#organizing-and-navigating}

除非您的内容片段非常少，否则您将需要编排内容 - 以便您（和其他人）能够再次找到它们。

#### 创建文件夹 {#creating-folder}

您可以通过在 **Assets** 控制台的&#x200B;**文件**&#x200B;部分中创建一系列文件夹来完成此操作。选择&#x200B;**创建**&#x200B;选项（右上角），然后选择&#x200B;**文件夹**：

![“创建文件夹”选项](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

这将打开一个对话框，可在其中输入详细信息，然后使用&#x200B;**创建**&#x200B;进行确认：

![“创建文件夹”对话框](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### 使用路径和标记限制文件夹中可用的内容片段模型 {#tags-paths-for-models-in-folder}

此部分的内容略为深入一些。如果您刚开始尝试，则并不是真的需要它；但当您有大量片段时，它&#x200B;*非常*&#x200B;有用。即使您尚未使用它，也建议您了解它。

您的内容架构师将创建您的当前项目以及其他一些项目所需的所有内容片段模型。为了帮助您和其他作者简化工作，您可以限制可用于特定文件夹的模型列表。

创建文件夹后，您可以打开文件夹&#x200B;**属性**。这里提供了各种选项卡，其中包含有关文件夹的信息和配置详细信息。具体而言，对于内容片段，您可以使用&#x200B;**策略**&#x200B;选项卡为此文件夹定义特定的路径和/或标记。这将限制可在文件夹中使用的内容片段模型，因为这意味着内容片段模型必须先满足这些要求，之后才能用于在此文件夹中生成片段。

![创建文件夹属性 – 策略](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>您可以参阅“内容片段模型”下的更多详细信息 - 允许 Assets 文件夹中的内容片段模型。

之后，您可以浏览这些文件夹以创建和编辑您的内容片段。

#### 以防万一 – 文件夹云服务配置 {#cloud-services-folder}

以防万一...

您可能会获得一个初始文件夹，可以在其中创建文件夹。这是因为必须将一些配置详细信息应用于根文件夹（此操作通常由开发人员或系统管理员执行）。您可能对此不感兴趣，但如有必要，您可以检查文件夹&#x200B;**属性**&#x200B;的&#x200B;**云服务**&#x200B;中的&#x200B;**配置**：

![创建文件夹属性 – 配置](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>您可以参阅“将配置应用于 Assets 文件夹”下的更多信息。

### 创建内容片段 {#creating-fragment}

在&#x200B;**内容片段**&#x200B;控制台中，您可以使用&#x200B;**创建**&#x200B;打开&#x200B;**新建内容片段**&#x200B;对话框：

![内容片段控制台 – 创建新片段](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

指定：

* **位置**
* **内容片段模型**
* **标题**
* **名称**
* **描述**

然后使用&#x200B;**创建**&#x200B;或&#x200B;**创建并打开**&#x200B;进行确认。

<!--
Creating a Content Fragment is very similar - you just use the **Content Fragment** option instead:

![Create Content Fragment option](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

This time a wizard opens. The first step is to select the Content Fragment Model that your fragment is based on:

![Create Content Fragment - select Model](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

After continuing with **Next** you can supply the details (**Basic** and **Advanced**) for your fragment:

![Create Content Fragment - provide Name](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirm with **Create** and you can then **Open** your fragment in the editor.
-->

### 编辑片段 {#editing-fragment}

您可以在创建片段后立即打开它，或者通过从“内容片段”控制台（也可以从 Assets 控制台）中选择它来将其打开。

在编辑器首次打开时，您将看到：

* 左侧的图标列表 – 可利用这些图标访问各种功能区域。编辑器在&#x200B;**变体**&#x200B;选项卡中打开，将在此处完成大部分编辑工作。您可能还对&#x200B;**批注**&#x200B;和&#x200B;**元数据**&#x200B;选项卡感兴趣。

* 包含有关片段的信息的标头，以及对各种操作的访问权限。

* 主要编辑区域，这取决于用于创建片段的模型。

例如：

* 只需要多条信息（其中一些信息具有特定类型）的片段。对于 Headless 内容，引用很重要（您将在历程的后面部分中了解相关信息）。

  ![内容片段编辑器 – 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* 一个让您编写长段文本的片段。这里提供了用于管理文本并设置其格式的其他选项。您甚至可以在全屏编辑器中打开各个文本字段（使用右侧的类似小屏幕的图标）

  ![内容片段编辑器 – 阿拉斯加烈酒](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>可能需要项目特定的文档来帮助作者详细了解如何成功填写某些字段。
>
>有关一般详细信息，请参阅“内容片段模型 – 数据类型和属性”。

使用&#x200B;**保存**&#x200B;或&#x200B;**保存并关闭**&#x200B;来确认更新。

>[!NOTE]
>
>有关更多详细信息，您可以参阅“变体 – 创作内容片段”。

#### 您（可能）无需担心的事情 {#what-you-probably-do-not-need-to-worry-about}

好吧，这似乎是一个有点奇怪的部分，但在您打开内容片段编辑器并开始浏览之后，您会看到各种选项，它们（可能）不适用于您（作为内容作者）的 Headless 历程。因此，这只是一个快速提示，说明您应该能够在 Headless 上下文中忽略的内容：

* **内容片段模型**

  您将在编辑器顶部看到内容片段模型的名称 - 位于片段名称的正下方。这也是一个可将您转至模型编辑器的链接。
实际上，内容片段模型对您的内容片段至关重要，因为它们定义了您使用的结构。不过，创建和编辑这些模型（通常）是另一个角色（即内容架构师）的责任。

  >[!NOTE]
  >
  >如果您想了解详细信息，可以参阅“AEM Headless 内容架构师历程”。

* **关联的内容**

  这一个非常明显，因为它是编辑器中的一个选项卡。

  对于相当多的版本，内容片段已在 AEM 中提供。最初，它们在创作页面时可用于“传统”用途....并且它们仍在此上下文中使用。这可能涉及关联资源（例如图像），这些资源未嵌入片段中，需要在创作页面提供给作者。

* **预览**

  这是编辑器中的另一个选项卡，它提供了技术视图，主要供开发人员使用。

* **更新页面引用**

  可从 **...**（省略号）下拉列表中执行此操作。Headless 作者对它并不感兴趣，因为它与页面创作有关。

### 发布 {#publishing}

<!-- needs more details -->

完成片段后，您可以&#x200B;**发布**&#x200B;它，以便 Headless 应用程序可使用它。

发布操作在编辑器中可用：

![内容片段编辑器 – 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

>[!NOTE]
>
>您也可以从&#x200B;**Assets**&#x200B;或&#x200B;**内容片段**»控制台发布您的片段。

## 后续内容 {#whats-next}

现在您已了解基础知识，下一步是[了解引用](references.md)。这将介绍和讨论可用的各种引用，以及如何使用片段引用（针对 Headless 的创作的关键部分）创建结构层次。

## 其他资源 {#additional-resources}

* [创作概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [基本处理](/help/sites-cloud/authoring/getting-started/basic-handling.md) – 此页面主要基于&#x200B;**Sites**&#x200B;控制台，但许多/大多数功能也用于在 **Assets** 控制台下创作&#x200B;**内容片段**。

   * [“导航”面板](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [标头](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [操作工具栏](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [查看和选择资源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [边栏选择器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

* [使用内容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)

   * [管理内容片段](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md)

   * [将配置应用到 Assets 文件夹](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

   * [创建内容片段](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [变体 - 创作片段内容](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)

   * 发布

      * 从编辑器或&#x200B;**资源**&#x200B;控制台

         * [快速发布](/help/assets/manage-publication.md#quick-publish)

         * [管理发布](/help/assets/manage-publication.md#manage-publication)

      * 从&#x200B;**内容片段**&#x200B;控制台

         * [发布和预览内容片段](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-previewing-a-fragment)

   * [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

      * [内容片段模型 – 数据类型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

      * [内容片段模型 – 属性](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)

      * [内容片段模型 – 允许 Assets 文件夹中的内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* 快速入门指南
   * [创建 Assets 文件夹 Headless 设置](/help/headless/setup/create-assets-folder.md)

* AEM Headless 内容架构师历程

* AEM Headless 翻译历程
