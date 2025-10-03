---
title: 使用 Universal Editor 发布内容
description: 了解 Universal Editor 如何发布内容以及您的应用程序如何处理发布的内容。
exl-id: aee34469-37c2-4571-806b-06c439a7524a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: f1030bf293ee78380bca7bd5d4266f9767677ad7
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 32%

---


# 使用 Universal Editor 发布内容 {#publishing}

了解 Universal Editor 如何发布内容以及您的应用程序如何处理发布的内容。

>[!TIP]
>
>此处介绍的发布过程是通用编辑器的现成标准功能。
>
>通用编辑器还支持[扩展和UI可扩展性](/help/implementing/universal-editor/extending.md)，以允许工作流支持您的发布过程，因此您的发布流程可能会有所不同。

## 从通用编辑器中发布内容 {#publishing-content}

当您作为内容作者准备发布内容时，您只需点按或单击通用编辑器工具栏中的&#x200B;**发布**&#x200B;图标即可。

![正在发布页面](assets/publish-menu.png)

1. 在通用编辑器中，点按或单击通用编辑器工具栏中的[发布&#x200B;**图标。**](/help/sites-cloud/authoring/universal-editor/navigation.md#publish)
1. 如果您有[预览服务](/help/sites-cloud/authoring/sites-console/previewing-content.md)可用，您可以选择发布内容的位置，可以是&#x200B;**[预览](/help/sites-cloud/authoring/sites-console/previewing-content.md)**（如果可用）或&#x200B;**发布**。
1. **项目**&#x200B;部分列出了发布中包含的内容。 点按或单击&#x200B;**查看**&#x200B;以显示详细信息，包括：
   * **个新的**&#x200B;项目尚未发布。
   * **已修改**&#x200B;已发布但自上次发布以来修改的内容。
   * **已发布**&#x200B;自该发布以来已发布且未修改的内容。

   根据需要点按或单击这些项目旁边的复选框以包含/排除它们。 点击或单击&#x200B;**扩展**&#x200B;可查看三个类别总计中包含的单个项目，并可单独将其纳入/排除。

   ![发布项目](assets/publish-items.png)

   点按或单击&#x200B;**项目**&#x200B;标题旁边的返回箭头可返回概述。

1. 点按或单击&#x200B;**发布**&#x200B;以进行发布或单击&#x200B;**取消**&#x200B;中止。

>[!TIP]
>
>如果您发布到预览环境，[您可以使用Experience Manager标题工具栏中的&#x200B;**帐户**&#x200B;菜单](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)中的选项在预览环境和生产环境之间切换。

>[!NOTE]
>
>可以禁用发布到预览[的选项](/help/implementing/universal-editor/customizing.md#publish-preview)，因此可能不会显示在您的编辑器中。

## 从通用编辑器中取消发布内容 {#unpublishing-content}

取消发布内容的工作方式与发布内容类似。 当您作为内容作者准备从出版物中删除内容时，请点按或单击通用编辑器工具栏中的省略号图标，然后&#x200B;**取消发布**。

然后，您可以使用与[发布内容时相同的选项来取消发布内容。](#publishing-content)包括从预览实例取消发布（如果可用）以及要包含在取消发布中的项。

## 从站点控制台中发布和取消发布 {#publishing-sites-console}

您还可以从站点控制台[发布](/help/sites-cloud/authoring/sites-console/publishing-pages.md)，当您希望发布多个内容页面或计划发布或取消发布时，这非常有用。

## 其他资源 {#additional-resources}

要了解如何使用通用编辑器创作内容，请参阅此文档。

* [使用 Universal Editor 创作内容](authoring.md) – 了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。

要了解有关通用编辑器的更多技术细节，请参阅这些开发人员文档。

* [通用编辑器简介](/help/implementing/universal-editor/introduction.md) – 了解通用编辑器如何支持在任何实施中编辑任何内容的任何方面以使您可以提供卓越的体验，提升内容速度，并提供最先进的开发人员体验。
* [AEM Universal Editor 快速入门 &#x200B;](/help/implementing/universal-editor/getting-started.md) – 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
* [Universal Editor 架构](/help/implementing/universal-editor/architecture.md) – 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
* [属性和类型](/help/implementing/universal-editor/attributes-types.md) – 了解 Universal Editor 所需的数据属性和类型。
* [Universal Editor 身份验证](/help/implementing/universal-editor/authentication.md) – 了解 Universal Editor 如何进行身份验证。
