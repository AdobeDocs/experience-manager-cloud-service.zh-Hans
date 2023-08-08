---
title: 使用 Universal Editor 创作内容
description: 了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: 481202760e0d22cde9c32e0b781dc99f67d463e4
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 100%

---


# 使用 Universal Editor 创作内容 {#authoring}

了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。

## 简介 {#introduction}

Universal Editor 支持在任意实施中编辑任何内容的任何方面，以提供卓越的体验，提升内容速度并提供最先进的开发人员体验。

为此，Universal Editor 为内容作者提供了一个直观的 UI，只需少量培训即可开始编辑内容。本文档介绍了 Universal Editor 的创作体验。

>[!TIP]
>
>有关 Universal Editor 的更详细介绍，请参阅文档 [Universal Editor 简介](introduction.md)。

>[!NOTE]
>
>Universal Editor 仍在开发中。目前，它无法编辑所有内容类型。

## 准备应用程序 {#prepare-app}

要使用 Universal Editor 为应用程序创作内容，应用程序必须由开发人员进行检测以支持编辑器。

>[!TIP]
>
>请参阅 [AEM Universal Editor 快速入门](getting-started.md)，查看有关如何配置 AEM 应用程序以使用 Universal Editor 的示例。

## 登录 {#sign-in}

在应用程序经过检测可使用 Universal Editor 后，您将需要登录 Universal Editor。您将需要一个 Adobe ID 才能登录并[访问 Universal Editor](getting-started.md#request-access)。

登录后，将要编辑的页面的 URL 输入到[地址栏](#location-bar)中，这样您就可以开始编辑内容，例如[文本内容](#text-mode)或[媒体内容](#media-mode)。

## 了解 UI {#ui}

UI 分为五个主要区域。

* [Experience Cloud 标题](#experience-cloud-header)
* [Universal Editor 标题](#universal-editor-header)
* [模式边栏](#mode-rail)
* [编辑器](#editor)
* [组件边栏](#component-rail)

![Universal Editor UI](assets/ui.png)

### Experience Cloud 标题 {#experience-cloud-header}

Experience Cloud 标题始终显示在屏幕顶部。它是一个锚点，可让您知道您在 Experience Cloud 中的位置，并帮助您导航到其他 Experience Cloud 应用程序。

![Experience Cloud 标题](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

选择标题左侧的 Adobe Experience Cloud 链接可导航到 Experience Manager 解决方案的根来访问工具，例如 [Cloud Manager](/help/onboarding/cloud-manager-introduction.md)、[Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) 和 [Software Distribution](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)。

![“全局导航”按钮](assets/global-navigation.png)

#### 组织 {#organization}

这将显示您当前登录的组织。如果您的 Adobe ID 与多个组织关联，请点按或单击以切换到另一个组织。

![组织指示器](assets/organization.png)

#### 解决方案 {#solutions}

点按或单击解决方案切换器可快速跳转到其他 Experience Cloud 解决方案。

![解决方案切换器](assets/solutions.png)

#### 帮助 {#help}

可使用帮助图标快速访问学习和支持资源。

![帮助](assets/help.png)

#### 通知 {#notifications}

此图标带有一个标记，显示当前分配的未完成[通知](/help/implementing/cloud-manager/notifications.md)的数量。

![通知](assets/notifications.png)

#### 用户属性 {#user-properties}

点按或单击代表用户的图标来访问用户设置。如果您尚未配置用户图片，系统会随机分配一个图标。

![用户属性](assets/user-properties.png)

### Universal Editor 标题 {#universal-editor-header}

Universal Editor 标题始终显示在屏幕顶部，位于 [Experience Cloud 标题的正下方。](#experience-cloud-header)它为您提供了快速访问权限，以便导航到另一个页面进行编辑以及发布当前页面。

![Universal Editor 标题](assets/universal-editor-header.png)

#### 汉堡菜单 {#hamburger-menu}

汉堡菜单尚未实施。

![汉堡菜单](assets/hamburger-menu.png)

#### 位置栏 {#location-bar}

位置栏为您显示正在编辑的页面的位置。点按或单击此项可输入要编辑的另一个页面的地址。

![位置栏](assets/location-bar.png)

>[!TIP]
>
>使用热键 `L` 可打开地址栏。

>[!NOTE]
>
>您想使用 Universal Editor 编辑的任何页面都必须[进行插桩以支持 Universal Editor](getting-started.md)。

#### 模拟器设置 {#emulator}

点按或单击模拟图标以定义 Universal Editor 呈现页面的方式。

![“模拟器”图标](assets/emulator.png)

点按或单击模拟图标将显示选项。

![模拟选项](assets/emulation-options.png)

默认情况下，该编辑器将以桌面版面打开，其中由浏览器自动定义高度和宽度。

您还可选择模拟移动设备并在 Universal Editor 中：

* 定义其方向
* 定义宽度和高度
* 更改方向

#### 打开应用程序预览 {#open-app-preview}

点按或单击“打开应用程序预览”图标可在其自己的浏览器标签页中打开您当前正在编辑的页面，无需编辑器即可预览您的内容。

![打开应用程序预览](assets/open-app-preview.png)

>[!TIP]
>
>使用热键 `O`（字母 O）可打开应用程序预览。

#### 发布 {#publish}

点按或单击“发布”按钮可实时发布对内容的更改以供阅读器使用。

![“发布”按钮](assets/publish.png)

>[!TIP]
>
>有关使用 Universal Editor 发布内容的更多信息，请参阅文档[使用 Universal Visual Editor 发布内容](publishing.md)。

### 模式边栏 {#rail}

始终沿该编辑器的左侧显示模式边栏。通过它，可在不同的编辑模式之间轻松切换该编辑器。

![模式边栏](assets/mode-rail.png)

#### 预览模式 {#preview-mode}

在预览模式中，编辑器中呈现的页面与在您发布的服务上看到的一样。这可让内容作者通过单击链接等来导航内容。

![预览模式](assets/preview-mode.png)

>[!TIP]
>
>使用热键 `P` 可切换到预览模式。

#### 文本模式 {#text-mode}

在文本模式下，内容作者可以单击选择文本内容。

![文本模式](assets/text-mode.png)

* 您可以就地[编辑纯文本](#editing-content)。
* 您也可以使用组件边栏上显示的其他格式选项来[编辑富文本](#editing-rich-text)。

>[!TIP]
>
>使用热键 `T` 可切换到文本模式。

#### 媒体模式 {#media-mode}

在媒体模式下，内容作者可以单击以选择媒体内容。

![媒体模式](assets/media-mode.png)

内容详细信息显示在组件边栏中，作者也可以[编辑媒体内容](#editing-media)。

>[!TIP]
>
>使用热键 `M` 可切换到媒体模式。

#### 组件模式 {#component-mode}

在组件模式下，内容作者可以单击以选择[内容片段](/help/assets/content-fragments/content-fragments.md)。

![组件模式](assets/component-mode.png)

在选择内容片段时，其详细信息将会显示在组件边栏中，您可以在其中[编辑内容片段](#edit-content-fragment)。

>[!TIP]
>
>使用热键 `C` 可切换到组件模式。

#### 编辑 {#edit}

在[组件模式](#component-mode)中，如果您选择一个[内容片段](/help/assets/content-fragments/content-fragments.md)，编辑选项将会显示在模式边栏上。

![“编辑”图标](assets/edit.png)

点按或单击编辑按钮将会在新选项卡中打开[内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor)，以便您访问内容片段编辑器的全部功能。

您还可以在[组件边栏](#edit-content-fragment)中编辑内容片段的详细信息，具体取决于工作流的需求。

>[!TIP]
>
>使用热键 `E` 可编辑所选组件。

### 编辑器 {#editor}

编辑器占据窗口的大部分区域，并在其中呈现在[地址栏](#location-bar)中指定的页面。

* 如果编辑器处于[文本模式](#text-mode)或[媒体模式](#media-mode)等编辑模式下，则内容是可编辑的，但您无法访问链接。
* 如果编辑器处于[预览模式](#preview-mode)下，则可在内容中导航并可访问链接，但无法编辑内容。

![编辑器](assets/editor.png)

### 组件边栏 {#component-rail}

始终沿该编辑器的左侧显示组件边栏。根据其模式的不同，它可显示在内容中选择的某个组件或页面内容的层次结构的详细信息。

![组件边栏](assets/component-rail.png)

#### 属性模式 {#properties-mode}

在属性模式中，边栏显示当前在编辑器中选择的组件的属性。在加载页面时，这是组件边栏的默认模式。

![属性模式](assets/properties-mode.png)

根据选择的组件类型，可以在属性边栏中显示和修改详细信息。

![组件详细信息](assets/component-details.png)

请注意，并非所有组件都有可显示和/或编辑的详细信息。

>[!TIP]
>
>使用热键 `D` 可切换到属性模式。

#### 内容树模式 {#Content-tree-mode}

在内容树模式中，边栏显示页面内容的层次结构。

![内容树模式](assets/content-tree-mode.png)

在内容树中选择某个项目时，编辑器将滚动到该内容并将其选定。

![内容树](assets/content-tree.png)

>[!TIP]
>
>使用热键 `F` 可切换到内容树模式。


## 编辑内容 {#editing-content}

编辑内容是简单而直观的。在编辑模式（[文本模式](#text-mode)、[媒体模式](#media-mode)和[组件模式](#component-mode)）下，随着在编辑器中将光标悬停在内容上方，将用蓝色框突出显示可编辑的内容。

![可编辑内容用蓝色框突出显示](assets/editable-content.png)

请注意，在编辑模式中，点按或单击内容会尝试选择该内容以进行编辑。如果您要使用链接来导航内容，请切换到[预览模式](#preview-mode)。

根据使用的[模式](#mode-rail)和选定内容，您可能有不同的就地编辑选项，并且您可以使用[组件边栏](#component-rail)查看内容的其他属性。

### 编辑纯文本 {#edit-plain-text}

如果使用的是[文本模式](#text-mode)并选择一个纯文本组件，则可以就地编辑文本。

![编辑内容](assets/editing-content.png)

只需键入即可更新内容。按“输入/回车”键或点按或单击文本框外部可保存更改。

### 编辑富文本 {#edit-rich-text}

如果使用的是[文本模式](#text-mode)并选择一个富文本组件，则可以就地编辑文本。

只需键入即可更新内容。按“输入/回车”键或点按或单击文本框外部可保存更改。

此外，组件边栏中还提供了格式设置选项和文本详细信息。

![编辑富文本组件](assets/rich-text-editing.png)

格式更改将会自动保存到您的内容中。

### 编辑媒体 {#edit-media}

如果您使用的是[媒体模式](#media-mode)并选择一个图像，则可以在组件边栏中查看其详细信息。

![编辑媒体](assets/ue-edit-media.png)

点按或单击组件边栏中选定图像预览下方的&#x200B;**替换**&#x200B;按钮，以将图像替换为资源库中的另一个图像。

1. [资源选择器](/help/assets/asset-selector.md#using-asset-selector)窗口会打开，以供您选择资源。
1. 点按或单击以选择新资源。
1. 点按或单击&#x200B;**选择**&#x200B;可返回至已替换资源的组件边栏。

更改会自动保存到您的内容中。

>[!TIP]
>
>使用热键 `R` 可打开资源选择器以替换所选图像。

### 编辑内容片段 {#edit-content-fragment}

如果您使用的是[组件模式](#component-mode)并选择一个[内容片段](/help/assets/content-fragments/content-fragments.md)，则可以在组件边栏中编辑其详细信息。

![编辑内容片段](assets/ue-edit-cf.png)

所选内容片段的内容模型中定义的字段可在组件边栏中显示和编辑。

更改将会自动保存到您的内容中。

如果您想改为在[内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor)中编辑您的内容片段，请单击模式边栏中的[编辑按钮](#edit)。

## 预览内容 {#previewing-content}

编辑完内容后，您通常需要导航内容以查看它在其他页面内容中的外观。在[预览模式](#preview-mode)中，您可以单击链接来像阅读器一样导航您的内容。内容在编辑器中呈现，就像它将要发布的那样。

请注意，在预览模式中，点按或单击内容的反应与对内容阅读器的反应一样。如果要选择内容以供编辑，请切换到编辑模式，如[文本模式](#text-mode)或[媒体模式](#media-mode)。

## 其他资源 {#additional-resources}

要了解有关 Universal Editor 的更多信息，请参阅这些文档。

* [Universal Editor 简介](introduction.md) – 了解 Universal Editor 如何支持在任意实施中编辑任何内容的任何方面，以提供卓越的体验，提升内容速度并提供最先进的开发人员体验。
* [使用 Universal Editor 发布内容](publishing.md) – 了解 Universal Visual Editor 如何发布内容以及您的应用程序如何处理发布的内容。
* [AEM Universal Editor 快速入门 ](getting-started.md) – 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
* [Universal Editor 架构](architecture.md) – 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
* [属性和类型](attributes-types.md) – 了解 Universal Editor 所需的数据属性和类型。
* [Universal Editor 身份验证](authentication.md) – 了解 Universal Editor 如何进行身份验证。
