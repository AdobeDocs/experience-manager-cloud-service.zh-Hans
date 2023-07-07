---
title: 使用 Universal Editor 创作内容
description: 了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: c6ab2d9b01a3f1abedb06d1d413e7eceb8b1c031
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 58%

---

# 使用 Universal Editor 创作内容 {#authoring}

了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。

## 简介 {#introduction}

Universal Editor 支持在任意实施中编辑任何内容的任何方面，以提供卓越的体验，提升内容速度并提供最先进的开发人员体验。

为此，通用编辑器为内容作者提供了一个直观的UI，只需很少的培训即可跳入并开始编辑内容。

>[!TIP]
>
>有关 Universal Editor 的更详细介绍，请参阅文档 [Universal Editor 简介](introduction.md)。

>[!NOTE]
>
>Universal Editor 仍处于开发阶段，目前无法编辑所有内容类型。

## 准备应用程序 {#prepare-app}

要使用 Universal Editor 为应用程序创作内容，应用程序必须由开发人员进行检测以支持编辑器。

>[!TIP]
>
>参见 [AEM中的通用编辑器快速入门](getting-started.md) 有关如何配置AEM应用程序以使用通用编辑器的示例。

## 登录 {#sign-in}

在应用程序经过检测可使用 Universal Editor 后，您将需要登录 Universal Editor。您将需要一个 Adobe ID 才能登录并[访问 Universal Editor](getting-started.md#request-access)。

登录后，在 [位置栏。](#location-bar) 这样您就可以开始编辑内容，例如 [文本内容](#text-mode) 或 [媒体内容。](#media-mode)

## 了解 UI {#ui}

UI分为五个主要区域。

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

Universal Editor 标题始终显示在屏幕顶部，位于 [Experience Cloud 标题的正下方。](#experience-cloud-header) 通过它，可快速导航到要编辑的其他页面并发布当前页面。

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

点按或单击模拟图标以定义通用编辑器如何渲染页面。

![“模拟器”图标](assets/emulator.png)

点击或单击模拟图标将显示选项。

![模拟选项](assets/emulation-options.png)

默认情况下，该编辑器将在桌面布局中打开，其中高度和宽度由浏览器自动定义。

您还可以选择在Universal Editor中模拟移动设备：

* 定义其方向
* 定义宽度和高度
* 更改方向

#### 打开应用程序预览 {#open-app-preview}

点按或单击“打开应用程序预览”图标可在其自己的浏览器中打开您当前正在编辑的页面，无需编辑器即可预览更改。

![打开应用程序预览](assets/open-app-preview.png)

>[!TIP]
>
>使用热键 `O` （字母O）以打开应用程序预览。

#### 发布 {#publish}

点按或单击“发布”按钮可实时发布对内容的更改以供阅读器使用。

![“发布”按钮](assets/publish.png)

>[!TIP]
>
>有关使用 Universal Editor 发布内容的更多信息，请参阅文档[使用 Universal Visual Editor 发布内容](publishing.md)。

### 模式边栏 {#rail}

模式边栏始终显示在编辑器的左侧。 它允许在不同的编辑模式之间轻松切换编辑器。

![模式边栏](assets/mode-rail.png)

#### 预览模式 {#preview-mode}

在预览模式中，编辑器中呈现的页面与在您发布的服务上看到的一样。这可让内容作者通过单击链接等来导航内容。

![预览模式](assets/preview-mode.png)

>[!TIP]
>
>使用热键 `P` 可切换到预览模式。

#### 文本模式 {#text-mode}

在文本模式下，页面将在编辑器中呈现，但内容作者可以单击以选择文本内容来进行编辑。 在加载页面时，这是编辑器的默认模式。

![文本模式](assets/text-mode.png)

>[!TIP]
>
>使用热键 `T` 切换到文本模式。

#### 媒体模式 {#media-mode}

在媒体模式下，页面会在编辑器中呈现，但内容作者可以单击以选择媒体内容来编辑页面。

![媒体模式](assets/media-mode.png)

>[!TIP]
>
>使用热键 `M` 切换到媒体模式。

#### 组件模式 {#component-mode}

在组件模式下，页面将在编辑器中呈现，但内容作者可以单击选择页面组件。

![组件模式](assets/component-mode.png)

>[!TIP]
>
>使用热键 `C` 切换到组件模式。

>[!NOTE]
>
>组件模式仍在开发中，当前仅限于选择组件。

### 编辑器 {#editor}

编辑器占据大部分窗口，并且是中指定页面的位置 [位置栏](#location-bar) 已呈现。

* 如果编辑器处于编辑模式，例如 [文本模式](#text-mode) 或 [媒体模式，](#media-mode) 内容将可编辑，并且您无法关注链接。
* 如果编辑器位于 [预览模式，](#preview-mode) 内容将可导航，您可以关注链接，但无法编辑内容。

![编辑器](assets/editor.png)

### 组件边栏 {#component-rail}

组件边栏始终位于编辑器的左侧。 根据其模式，它可以显示内容或页面内容层次结构中所选组件的详细信息。

![组件边栏](assets/component-rail.png)

#### 属性模式 {#properties-mode}

在属性模式中，边栏显示编辑器中当前选定组件的属性。 这是加载页面时组件边栏的默认模式。

![属性模式](assets/properties-mode.png)

所选组件的详细信息将显示在边栏中。 请注意，并非所有组件都具有可显示的详细信息。

![组件详细信息](assets/component-details.png)

>[!TIP]
>
>使用热键 `D` 切换到属性模式。

#### 内容树模式 {#Content-tree-mode}

在内容树模式下，边栏显示页面内容的层次结构。

![内容树模式](assets/content-tree-mode.png)

在内容树中选择项目时，编辑器将滚动到该内容并选择它。

![内容树](assets/content-tree.png)

>[!TIP]
>
>使用热键 `F` 切换到内容树模式。


## 编辑内容 {#editing-content}

编辑内容是简单而直观的。在编辑模式中([文本模式](#text-mode)， [媒体模式](#media-mode)、和 [组件模式](#component-mode))，将鼠标悬停在编辑器中的内容上时，可编辑内容会以蓝色框突出显示。

![可编辑内容子用蓝色框突出显示](assets/editable-content.png)

只需点按或单击蓝色框中的内容即可启动就地编辑器来进行更改。按 Enter 键保存更改。

![编辑内容](assets/editing-content.png)

请注意，在编辑模式中，点按或单击内容会尝试选择该内容以进行编辑。如果您要使用链接来导航内容，请切换到[预览模式](#preview-mode)。

根据您所在的模式和您选择的内容，您可能有不同的就地编辑选项。 此外，您还可以使用查看内容的其他属性 [组件边栏。](#component-rail)

## 预览内容 {#previewing-content}

编辑完内容后，您通常需要导航内容以查看它在其他页面内容中的外观。在[预览模式](#preview-mode)中，您可以单击链接来像阅读器一样导航您的内容。内容在编辑器中呈现，就像它将要发布的那样。

请注意，在预览模式中，点按或单击内容的反应与对内容阅读器的反应一样。如果要选择要编辑的内容，请切换到编辑模式，例如 [文本模式](#text-mode) 或 [媒体模式。](#media-mode)

## 其他资源 {#additional-resources}

要了解有关 Universal Editor 的更多信息，请参阅这些文档。

* [Universal Editor 简介](introduction.md) – 了解 Universal Editor 如何支持在任意实施中编辑任何内容的任何方面，以提供卓越的体验，提升内容速度并提供最先进的开发人员体验。
* [使用 Universal Editor 发布内容](publishing.md) – 了解 Universal Visual Editor 如何发布内容以及您的应用程序如何处理发布的内容。
* [AEM Universal Editor 快速入门 ](getting-started.md) – 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
* [Universal Editor 架构](architecture.md) – 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
* [属性和类型](attributes-types.md) – 了解 Universal Editor 所需的数据属性和类型。
* [Universal Editor 身份验证](authentication.md) – 了解 Universal Editor 如何进行身份验证。
