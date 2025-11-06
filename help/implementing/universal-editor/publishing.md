---
title: 通用编辑器如何发布内容
description: 了解通用编辑器如何发布其内容、它与 Sites 控制台中的过程有何不同，以及开发您自己的应用程序与其一起使用时需要考虑的事项。
feature: Developing
role: Admin, Developer
exl-id: 60f0bb4a-ee60-4f73-83ae-8568735474ad
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 100%

---

# 通用编辑器如何发布内容 {#publishing}

了解通用编辑器如何发布其内容、它与 Sites 控制台中的过程有何不同，以及开发您自己的应用程序与其一起使用时需要考虑的事项。

>[!TIP]
>
>本文介绍了通用编辑器为开发人员提供的发布流程的详细信息。为内容作者提供的[发布内容的过程请参阅这里。](/help/sites-cloud/authoring/universal-editor/publishing.md)

## 与 Sites 控制台过程的相似之处 {#similarities}

对于 [AEM 页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)和 [Sites 控制台](/help/sites-cloud/authoring/sites-console/introduction.md)的用户来说，使用通用编辑器发布内容的过程与习惯做法一样：在 AEM 中发布时，内容从作者服务复制到发布服务（或者在可用的情况下复制到[预览服务](/help/sites-cloud/authoring/sites-console/previewing-content.md)，这取决于作者在发布时选择的选项。）

## 差异 {#differences}

使用 Universal Editor 进行发布的不同之处，与其说是与编辑器本身相关，不如说是 Universal Editor 使应用程序的外部托管成为可能。

在外部托管的情况下，Web 应用程序需要注意的是，确保当作者在编辑器中打开应用程序时从作者服务加载内容，在访问者访问应用程序时从发布服务加载内容。

## 检测应用程序中的服务 {#detecting}

可以通过应用程序中的一个简单的条件语句来确定是否要访问作者或发布服务，以便在检测到编辑器中打开此应用时选择适当的作者或发布端点。

另一种方法是将应用程序部署到配置不同的两个不同环境，以便一个环境从作者服务检索其内容，另一个从发布服务检索。为了允许作者在通用编辑器中打开已发布的 URL，可以创建一个小脚本来将发布端 URL“转换”为作者环境中的等效 URL（例如在前面添加一个 `author` 子域），以便作者自动被重定向。

## 摘要 {#summary}

Universal Editor 的目标是不强加任何特定模式，以便以完全解耦的方式最大限度地实现实施目标，同时仍然保持简单和直接的实施。

类似地，通用编辑器对于任何特定项目应如何确定从哪个服务交付内容不提出任何要求。相反，它支持几种可能性，并允许项目确定最适合其自身需求的解决方案。

## 其他资源 {#additional-resources}

要了解有关通用编辑器的更多技术细节，请参阅这些开发人员文档。

* [通用编辑器简介](/help/implementing/universal-editor/introduction.md) – 了解通用编辑器如何支持在任何实施中编辑任何内容的任何方面以使您可以提供卓越的体验，提升内容速度，并提供最先进的开发人员体验。
* [AEM Universal Editor 快速入门 ](/help/implementing/universal-editor/getting-started.md) – 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
* [Universal Editor 架构](/help/implementing/universal-editor/architecture.md) – 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
* [属性和类型](/help/implementing/universal-editor/attributes-types.md) – 了解 Universal Editor 所需的数据属性和类型。
* [Universal Editor 身份验证](/help/implementing/universal-editor/authentication.md) – 了解 Universal Editor 如何进行身份验证。
