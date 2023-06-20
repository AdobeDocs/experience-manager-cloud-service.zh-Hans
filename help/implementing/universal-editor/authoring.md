---
title: 使用 Universal Editor 创作内容
description: 了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 84%

---

# 使用 Universal Editor 创作内容 {#authoring}

了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。

## 简介 {#introduction}

通用编辑器支持编辑任何实施中任何内容的任何方面，因此您可以提供卓越的体验、提高内容速度并提供一流的开发人员体验。

为此，它为内容作者提供了一个直观的 UI，只需进行最少培训即可轻松使用它开始编辑内容。

>[!TIP]
>
>有关 Universal Editor 的更详细介绍，请参阅文档 [Universal Editor 简介](introduction.md)。

>[!NOTE]
>
>Universal Editor 仍处于开发阶段，目前无法编辑所有内容类型。

## 准备应用程序 {#prepare-app}

要使用通用编辑器为应用程序创作内容，应用程序必须由开发人员检测才能支持该编辑器。

>[!TIP]
>
>请参阅文档 [AEM Universal Editor 快速入门](getting-started.md)，查看有关如何配置 AEM 应用程序以使用 Universal Editor 的示例。

## 登录 {#sign-in}

在应用程序经过检测可使用 Universal Editor 后，您将需要登录 Universal Editor。您将需要一个 Adobe ID 才能登录并[访问 Universal Editor](getting-started.md#request-access)。

登录后，在 [地址栏。](#address-bar) 这样你就可以开始 [编辑内容。](#edit-content)

## 了解 UI {#ui}

UI 分为四个主要区域。

* [Experience Cloud 标题](#experience-cloud-header)
* [Universal Editor 标题](#universal-editor-header)
* [边栏](#rail)
* [编辑器](#editor)

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

此图标带有当前分配的未完成数量的标记 [通知。](/help/implementing/cloud-manager/notifications.md)

![通知](assets/notifications.png)

#### 用户属性 {#user-properties}

点按或单击代表用户的图标来访问用户设置。如果您未配置用户图片，则会随机分配一个图标。

![用户属性](assets/user-properties.png)

### Universal Editor 标题 {#universal-editor-header}

Universal Editor 标题始终显示在屏幕顶部，位于 [Experience Cloud 标题的正下方。](#experience-cloud-header)它为您提供了快速访问权限，以便导航到另一个页面进行编辑以及发布当前页面。

![Universal Editor 标题](assets/universal-editor-header.png)

#### 汉堡菜单 {#hamburger-menu}

汉堡菜单尚未实施。

![汉堡菜单](assets/hamburger-menu.png)

#### 位置栏 {#Location-bar}

位置栏为您显示正在编辑的页面的位置。点按或单击此项可输入要编辑的另一个页面的地址。

![位置栏](assets/address-bar.png)

>[!TIP]
>
>使用热键 `L` 可打开地址栏。

>[!NOTE]
>
>您想使用 Universal Editor 编辑的任何页面都必须[进行插桩以支持 Universal Editor](getting-started.md)。

#### 打开应用程序预览 {#open-app-preview}

点按或单击“打开应用程序预览”图标可在其自己的浏览器中打开您当前正在编辑的页面，无需编辑器即可预览更改。

![打开应用程序预览](assets/open-app-preview.png)

>[!TIP]
>
>使用热键 `O` 可打开应用程序预览。

#### 发布 {#publish}

点按或单击发布按钮，以便您可以将更改发布到实时内容以供读者使用。

![“发布”按钮](assets/publish.png)

>[!TIP]
>
>有关使用 Universal Editor 发布内容的更多信息，请参阅文档[使用 Universal Visual Editor 发布内容](publishing.md)。

### 边栏 {#rail}

边栏始终显示在编辑器的左侧。可利用它在预览模式和编辑模式之间轻松切换编辑器。

![边栏](assets/rail.png)

#### 预览模式 {#preview-mode}

在预览模式中，编辑器中呈现的页面与在您发布的服务上看到的一样。这可让内容作者通过单击链接等来导航内容。

![预览模式](assets/preview-mode.png)

>[!TIP]
>
>使用热键 `P` 可切换到预览模式。

#### 编辑模式 {#edit-mode}

在编辑模式中，页面在编辑器中呈现，但内容作者可以单击以选择内容进行编辑。在加载页面时，这是编辑器的默认模式。

![编辑模式](assets/edit-mode.png)

### 编辑器 {#editor}

编辑器占据了窗口的大部分区域，并且其中将呈现[地址栏](#address-bar)中指定的页面。

根据编辑器是处于[编辑模式](#edit-mode)还是[预览模式](#edit-mode)，内容将分别可编辑或可导航。

![编辑器](assets/editor.png)

## 编辑内容 {#editing-content}

编辑内容是简单而直观的。In [编辑模式，](#edit-mode) 将鼠标悬停在编辑器中的内容上时，可编辑内容会以蓝色框突出显示。

![可编辑内容子用蓝色框突出显示](assets/editable-content.png)

只需点按或单击蓝色框中的内容即可启动就地编辑器来进行更改。按 Enter 键保存更改。

![编辑内容](assets/editing-content.png)

请注意，在编辑模式中，点按或单击内容会尝试选择该内容以进行编辑。如果您要使用链接来导航内容，请切换到[预览模式](#preview-mode)。

## 预览内容 {#previewing-content}

编辑完内容后，您通常需要导航内容以查看它在其他页面内容中的外观。在[预览模式](#preview-mode)中，您可以单击链接来像阅读器一样导航您的内容。内容在编辑器中呈现，就像它将要发布的那样。

请注意，在预览模式中，点按或单击内容的反应与对内容阅读器的反应一样。如果您想选择内容以进行编辑，请切换到[编辑模式](#edit-mode)。

## 其他资源 {#additional-resources}

要了解有关 Universal Editor 的更多信息，请参阅这些文档。

* [通用编辑器简介](introduction.md)  — 了解通用编辑器如何支持编辑任何实施中任何内容的任何方面，以便您能够提供卓越的体验、提高内容速度并提供一流的开发人员体验。
* [使用 Universal Editor 发布内容](publishing.md) – 了解 Universal Visual Editor 如何发布内容以及您的应用程序如何处理发布的内容。
* [AEM Universal Editor 快速入门 ](getting-started.md) – 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
* [Universal Editor 架构](architecture.md) – 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
* [属性和类型](attributes-types.md) – 了解 Universal Editor 所需的数据属性和类型。
* [Universal Editor 身份验证](authentication.md) – 了解 Universal Editor 如何进行身份验证。
