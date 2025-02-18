---
title: 通用编辑器如何发布内容
description: 了解通用编辑器如何发布其内容、它与站点控制台中的过程有何不同以及开发您自己的应用程序以与它一起使用时的注意事项。
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0ee6689460ac0ecc5c025fb6a940d69a16699c85
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 31%

---


# 通用编辑器如何发布内容 {#publishing}

了解通用编辑器如何发布其内容、它与站点控制台中的过程有何不同以及开发您自己的应用程序以与它一起使用时的注意事项。

>[!TIP]
>
>本文介绍了适用于开发人员的通用编辑器的发布过程的详细信息。 对于内容作者，[此处介绍了发布内容的过程。](/help/sites-cloud/authoring/universal-editor/publishing.md)

## 与Sites控制台过程的相似之处 {#similarities}

对于[AEM页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)和[Sites控制台的用户，](/help/sites-cloud/authoring/sites-console/introduction.md)使用通用编辑器发布内容的过程按您习惯的方式运行：在AEM中发布时，内容将从作者服务复制到发布服务（或者[预览服务](/help/sites-cloud/authoring/sites-console/previewing-content.md)，如果可用，具体取决于作者在发布时选择的选项）。

## 差异 {#differences}

使用 Universal Editor 进行发布的不同之处，与其说是与编辑器本身相关，不如说是 Universal Editor 使应用程序的外部托管成为可能。

在外部托管时，Web应用程序需要确保在作者在编辑器中打开应用程序时从作者服务加载内容，在访客访问应用程序时从发布服务加载内容。

## 检测应用程序中的服务 {#detecting}

当检测到作者或发布服务正在编辑器中打开时，可以通过应用程序中的简单条件语句选择相应的作者或发布端点来确定是否应访问作者或发布服务。

另一个选项是将应用程序部署到两个配置不同的环境，以便一个环境从创作服务检索其内容，另一个环境从发布服务检索内容。 要允许作者在通用编辑器中打开已发布的URL，可以创建一个小型脚本将发布端URL“转换”为创作环境中的等效项（例如，通过在前面`author`个子域中添加前缀），以便自动重定向作者。

## 摘要 {#summary}

Universal Editor 的目标是不强加任何特定模式，以便以完全解耦的方式最大限度地实现实施目标，同时仍然保持简单和直接的实施。

同样，Universal Editor也不要求任何特定项目如何确定从哪个服务交付内容。 相反，它可以启用多种可能性，并允许项目确定哪种解决方案最适合其自身需求。

## 其他资源 {#additional-resources}

要了解有关通用编辑器的技术详细信息的更多信息，请参阅这些开发人员文档。

* [Universal Editor 简介](/help/implementing/universal-editor/introduction.md) – 了解 Universal Editor 如何支持在任意实施中编辑任何内容的任何方面，以提供卓越的体验，提升内容速度并提供最先进的开发人员体验。
* [AEM Universal Editor 快速入门 ](/help/implementing/universal-editor/getting-started.md) – 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
* [Universal Editor 架构](/help/implementing/universal-editor/architecture.md) – 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
* [属性和类型](/help/implementing/universal-editor/attributes-types.md) – 了解 Universal Editor 所需的数据属性和类型。
* [Universal Editor 身份验证](/help/implementing/universal-editor/authentication.md) – 了解 Universal Editor 如何进行身份验证。
