---
title: 使用通用编辑器创作内容
description: 了解内容作者使用通用编辑器创建内容是多么简单直观。
source-git-commit: f454475b65da8f410812bbbe30ca5fc393be410a
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 2%

---


# 使用通用编辑器创作内容 {#authoring}

了解内容作者使用通用编辑器创建内容是多么简单直观。

## 简介 {#introduction}

通用编辑器允许编辑任何实施中任何内容的任何方面，以便提供卓越的体验、提高内容速度，并提供一流的开发人员体验。

为此，它为内容作者提供了一个直观的UI，只需要极少的培训，即可轻松进入并开始编辑内容。

>[!TIP]
>
>有关通用编辑器的更详细介绍，请参阅此文档 [通用编辑器简介。](introduction.md)

>[!NOTE]
>
>通用编辑器仍在开发中，当前只能创作文本。

## 准备应用程序 {#prepare-app}

要使用通用编辑器为应用程序创作内容，开发人员必须对应用程序进行指令以支持该编辑器。

>[!TIP]
>
>请查看文档 [AEM中通用编辑器快速入门](getting-started.md) 有关如何配置AEM应用程序以与通用编辑器一起使用的示例。

## 登录 {#sign-in}

在指令应用程序与通用编辑器一起使用后，您需要登录到通用编辑器。 您需要Adobe ID才能登录和 [具有通用编辑器的访问权限。](getting-started.md#request-access)

登录后，在 [地址栏。](#address-bar) 以便开始 [编辑内容。](#edit-content)

## 了解UI {#ui}

UI分为四个主要区域。

* [Experience Cloud标题](#experience-cloud-header)
* [通用编辑器标题](#universal-editor-header)
* [边栏](#rail)
* [编辑者](#editor)

![通用编辑器UI](assets/ui.png)

### Experience Cloud标题 {#experience-cloud-header}

Experience Cloud标题始终显示在屏幕顶部。 它是一个锚点，用于告知您Experience Cloud中的位置，并帮助您导航到其他Experience Cloud应用程序。

![Experience Cloud标题](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

选择标题左侧的Adobe Experience Cloud链接，以导航到Experience Manager解决方案的根目录以访问工具，例如 [Cloud Manager、](/help/onboarding/cloud-manager-introduction.md) [Cloud Acceleration Manager、](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) 和 [软件分发。](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)

![“全局导航”按钮](assets/global-navigation.png)

#### 组织 {#organization}

此时会显示您当前已登录的组织。 点按或单击，以切换到其他组织(如果您的Adobe ID与多个组织关联)。

![组织指标](assets/organization.png)

#### 解决方案 {#solutions}

通过点按或单击解决方案切换器，您可以快速跳转到其他Experience Cloud解决方案。

![解决方案切换器](assets/solutions.png)

#### 帮助 {#help}

通过帮助图标，可快速访问学习和支持资源。

![帮助](assets/help.png)

#### 通知 {#notifications}

此图标将带有标记，显示当前分配的未完成数量 [通知。](/help/implementing/cloud-manager/notifications.md)

![通知](assets/notifications.png)

#### 用户属性 {#user-properties}

点按或单击表示您的用户的图标，以访问您的用户设置。 如果您未配置用户图片，则会随机分配一个图标。

![用户属性](assets/user-properties.png)

### 通用编辑器标题 {#universal-editor-header}

通用编辑器标题始终显示在屏幕顶部的正下方 [Experience Cloud标题。](#experience-cloud-header) 利用该功能，可快速导航到要编辑的其他页面以及发布当前页面。

![通用编辑器标题](assets/universal-editor-header.png)

#### 汉堡菜单 {#hamburger-menu}

尚未实施汉堡包菜单。

![汉布格菜单](assets/hamburger-menu.png)

#### 地址栏 {#address-bar}

地址栏显示您正在编辑的页面的位置。 点按或单击以输入要编辑的其他页面的地址。

![地址栏](assets/address-bar.png)

>[!TIP]
>
>使用热键 `L` 打开地址栏。

>[!NOTE]
>
>您希望通过通用编辑器编辑的任何页面都必须 [支持通用编辑器的工具。](getting-started.md)

#### 协作指标 {#collaboration}

如果在通用编辑器中加载了具有相同页面的其他作者，则会显示这些作者的图像。 将鼠标悬停在图像上可查看完整的用户名

![协作指标](assets/collaboration.png)

#### 打开应用程序预览 {#open-app-preview}

点按或单击打开的应用程序预览图标，以打开您当前在其浏览器中编辑的页面（不带编辑器）以预览更改。

![打开应用程序预览](assets/open-app-preview.png)

>[!TIP]
>
>使用热键 `O` 打开应用程序预览。

#### 发布 {#publish}

点按或单击发布按钮，以将更改发布到实时内容，以供您的读者使用。

![“发布”按钮](assets/publish.png)

### 边栏 {#rail}

边栏始终沿编辑器的左侧显示。 它允许在预览模式和编辑模式之间轻松切换编辑器。

![边栏](assets/rail.png)

#### 预览模式 {#preview-mode}

在预览模式下，页面在编辑器中呈现，就像在已发布的服务中看到的一样。 这允许内容作者通过单击链接等方式导览内容。

![预览模式](assets/preview-mode.png)

>[!TIP]
>
>使用热键 `P` 切换到预览模式。

#### 编辑模式 {#edit-mode}

在编辑模式下，页面会在编辑器中呈现，但内容作者可以单击以选择要编辑的内容。 这是加载页面时编辑器的默认模式。

![编辑模式](assets/edit-mode.png)

### 编辑者 {#editor}

编辑器占据窗口的大部分，位于中指定页面的位置 [地址栏](#address-bar) 呈现。

根据编辑器是否在 [编辑模式](#edit-mode) 或 [预览模式，](#edit-mode) 内容将分别可编辑或可导航。

![编辑者](assets/editor.png)

## 编辑内容 {#editing-content}

编辑内容既简单又直观。 在 [编辑模式，](#edit-mode) 将鼠标悬停在编辑器中的内容上时，可编辑内容将以蓝框突出显示。

![可编辑内容以蓝框突出显示](assets/editable-content.png)

只需点按或单击蓝框中的内容，即可启动就地编辑器以进行更改。 按Enter键或返回以保存更改。

![编辑内容](assets/editing-content.png)

请注意，在编辑模式下，点按或单击内容会尝试选择该内容进行编辑。 如果您希望通过以下链接导航内容，请切换到 [预览模式。](#preview-mode)

## 预览内容 {#previewing-content}

编辑完内容后，您通常希望通过导航内容来查看内容在其他页面内容中的外观。 在 [预览模式](#preview-mode) 您可以单击链接以像读者一样导览内容。 内容在编辑器中呈现时与发布时一样。

请注意，在预览模式下，点按或单击内容会像点按或单击内容一样对内容的读者产生反应。 如果要选择要编辑的内容，请切换到 [编辑模式。](#edit-mode)

## 其他资源 {#additional-resources}

要了解有关通用编辑器的更多信息，请参阅这些文档。

* [通用编辑器简介](introduction.md)  — 了解通用编辑器如何允许编辑任何实施中任何内容的任何方面，以便提供卓越的体验、提高内容速度，并提供一流的开发人员体验。
* [AEM中通用编辑器快速入门](getting-started.md)  — 了解如何访问通用编辑器，以及如何开始检测您的第一个AEM应用程序以使用它。
* [通用编辑器架构](architecture.md)  — 了解通用编辑器的架构以及数据如何在其服务和层之间流动。
* [属性和类型](attributes-types.md)  — 了解通用编辑器所需的数据属性和类型。
* [通用编辑器身份验证](authentication.md)  — 了解通用编辑器如何进行身份验证。
