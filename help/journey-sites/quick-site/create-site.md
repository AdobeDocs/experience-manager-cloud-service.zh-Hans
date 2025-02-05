---
title: 从模板创建站点
description: 了解如何使用站点模板快速创建 AEM 站点。
exl-id: 31bb04c2-b3cc-44ca-b517-5b0d66d9b1fa
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1485'
ht-degree: 89%

---

# 从模板创建站点 {#create-site-from-template}

了解如何使用站点模板快速创建 AEM 站点。

## 迄今为止的故事 {#story-so-far}

在AEM快速站点创建历程的上一个文档[了解Cloud Manager和快速站点创建工作流](cloud-manager.md)中，您已了解Cloud Manager以及它如何将新的快速站点创建流程联系起来，您现在应：

* 了解 AEM Sites 和 Cloud Manager 如何协作来推动前端开发
* 了解如何在不具有 AEM 知识的情况下将前端自定义步骤与 AEM 完全分离开来。

本文建立在这些基础知识之上，于是您可迈出配置的第一步并为模板创建一个站点，以后可使用前端工具自定义该站点。

## 目标 {#objective}

本文档有助于您了解如何使用站点模板快速创建 AEM 站点。阅读本文档后，您应：

* 了解如何获取 AEM 站点模板。
* 了解如何使用模板创建站点。
* 了解如何从新站点下载模板以提供给前端开发人员。

## 负责角色 {#responsible-role}

此历程的这一部分适用于 AEM 管理员。

## 站点模板 {#site-templates}

站点模板是一种将基本站点内容组合成方便且可重用的包的方法。站点模板通常包含基本站点内容和结构以及站点样式信息，以便快速启动新的站点。实际结构如下：

* `files`：包含 UI 套件、XD 文件和可能的其他文件的文件夹
* `previews`：包含站点模板的屏幕截图的文件夹
* `site`：为从此模板创建的每个站点复制的内容的内容包，例如页面模板、页面等。
* `theme`：用于修改站点外观的模板主题的来源，包括 CSS、JavaScript 等。

模板具有强大的功能，它们可重用，这使得内容作者能够快速创建站点。由于您可以在 AEM 安装中使用多个模板，因此可以灵活地满足各种业务需求。

>[!NOTE]
>
>不要将站点模板与页面模板混淆。此处描述的站点模板定义了站点的整体结构。页面模板定义了单个页面的结构和初始内容。

## 获取站点模板 {#obtaining-template}

最简单的入门方法是从其GitHub存储库[下载最新版本的AEM标准站点模板](https://github.com/adobe/aem-site-template-standard/releases)。

下载后，您可以像上传任何其他包一样将它上传到您的 AEM 环境。如果您想了解有关此主题的更多信息，请参阅[“其他资源”部分](#additional-resources)，了解有关如何使用包的详细信息。

>[!TIP]
>
>可以自定义 AEM 标准站点模板以满足您的项目需求，并且可以消除进一步自定义的需要。但这个主题超出了此历程的范围。有关更多信息，请参阅“标准站点模板”的 GitHub 文档。

>[!TIP]
>
>您也可以选择在项目工作流中从来源构建模板。但这个主题超出了此历程的范围。有关更多信息，请参阅“标准站点模板”的 GitHub 文档。

## 安装站点模板 {#installing-template}

可以使用模板轻松创建站点。

1. 登录到您的 AEM 创作环境，并导航到 Sites 控制台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 在屏幕的右上角选择&#x200B;**创建**，然后从下拉菜单中选择&#x200B;**从模板创建站点**。

   ![从模板创建新站点](assets/create-site-from-template.png)

1. 在“创建站点向导”中，在左栏的顶部选择&#x200B;**导入**。

   ![站点创建向导](assets/site-creation-wizard.png)

1. 在文件浏览器中，找到[以前下载的](#obtaining-template)模板并选择&#x200B;**上传**。

1. 上传模板后，该模板将显示在可用模板列表中。选择它（这样还将在右栏中显示关于该模板的信息），然后选择&#x200B;**下一步**。

   ![选择模板](assets/select-site-template.png)

1. 为站点提供标题。可以提供站点名称，也可以从标题生成站点名称（如果被忽略）。

   * 站点标题显示在浏览器标题栏中。
   * 站点名称会成为 URL 的一部分。

1. 选择&#x200B;**创建**，然后将从站点模板创建新站点。

   ![新站点的详细信息](assets/create-site-details.png)

1. 在显示的确认对话框中，选择&#x200B;**完成**。

   ![“成功”对话框](assets/success.png)

1. 在 Sites 控制台中，新站点是可见的，并且可以导航以探索其由模板定义的基本结构。

   ![新站点结构](assets/new-site.png)

内容作者现在可以开始创作。

## 是否需要进一步自定义？ {#customization-required}

站点模板非常强大且灵活，可以为一个项目创建任意数量的模板，从而轻松创建站点变体。根据对您使用的站点模板执行的自定义级别，您甚至可能不需要额外的前端自定义。

* 如果您的站点不需要额外的自定义，恭喜您！您的历程到此结束！
* 如果您仍需进行额外的前端自定义，或者您只是希望了解整个流程，以防将来需要进行自定义，请继续阅读。

## 示例页面 {#example-page}

如果您确实需要额外的前端自定义，请记住，前端开发人员可能不熟悉您的内容的详细信息。因此，最好是为开发人员提供典型内容，在自定义主题时，该内容可以用作参考基础。一个典型示例是站点主语言的主页。

1. 在站点浏览器中，导航到站点主语言的主页，选择该页面以选择它，然后在菜单栏中选择&#x200B;**编辑**。

   ![典型主页](assets/home-page-in-console.png)

1. 在编辑器中，选择工具栏中的&#x200B;**页面信息**&#x200B;按钮，然后选择&#x200B;**以发布的形式查看**。

   ![编辑主页](assets/home-page-edit.png)

1. 在打开的选项卡中，从地址栏中复制内容的路径。它类似于 `/content/<your-site>/en/home.html?wcmmode=disabled`。

   ![主页](assets/home-page.png)

1. 保存路径以便稍后提供给前端开发人员。

## 下载主题 {#download-theme}

现已创建站点，可以下载模板生成的站点主题，并将它提供给前端开发人员进行自定义。

1. 在 Sites 控制台上，显示&#x200B;**站点**&#x200B;边栏。

   ![显示站点边栏](assets/show-site-rail.png)

1. 选择新站点的根，然后在站点边栏中选择&#x200B;**下载主题源**。

   ![下载主题源](assets/download-theme-sources.png)

您的下载文件中现已拥有主题源文件的副本。

## 设置代理用户 {#proxy-user}

为了让前端开发人员使用您站点中的实际 AEM 内容预览自定义项，您必须设置代理用户。

1. 在 AEM 中，从主导航转至&#x200B;**工具** > **安全性** > **用户**。
1. 在用户管理控制台中，选择&#x200B;**创建**。

   ![User Management 控制台](assets/user-management-console.png)
1. 在&#x200B;**创建新用户**&#x200B;窗口中，您必须至少提供：
   * **ID** – 记下此值，因为您必须将它提供给前端开发人员。
   * **密码** – 将此值安全地保存在密码库中，因为您必须将它提供给前端开发人员。

   ![新用户详细信息](assets/new-user-details.png)

1. 在&#x200B;**组**&#x200B;选项卡上，将代理用户添加到 `contributors` 组。
   * 键入 `contributors` 一词会触发 AEM 的自动完成功能，以便轻松选择组。

   ![添加到组](assets/add-to-group.png)

1. 选择&#x200B;**保存并关闭**。

您现在已完成配置。内容作者现在可以开始在站点上创建内容，为历程的下一步中的前端自定义做准备。

## 后续内容 {#what-is-next}

现在您已完成 AEM 快速站点创建历程的这一部分，您应：

* 了解如何获取 AEM 站点模板。
* 了解如何使用模板创建站点。
* 了解如何从新站点下载模板以提供给前端开发人员。

在此知识的基础上继续您的AEM快速站点创建历程，接下来查看文档[设置您的管道](pipeline-setup.md)，其中您将创建前端管道来管理站点主题的自定义。

## 其他资源 {#additional-resources}

我们建议您查看文档[设置管道](pipeline-setup.md)来继续快速站点创建历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续此历程所必需的。

* [AEM 标准站点模板](https://github.com/adobe/aem-site-template-standard) – 这是 AEM 标准站点模板的 GitHub 存储库。
* [组织页面](/help/sites-cloud/authoring/sites-console/organizing-pages.md) - 本指南详细介绍如何组织 AEM 站点的页面。
* [创建页面](/help/sites-cloud/authoring/sites-console/creating-pages.md) - 本指南详细介绍如何将新页面添加到您的网站。
* [管理页面](/help/sites-cloud/authoring/sites-console/managing-pages.md) - 本指南详细介绍如何管理站点页面，包括移动、复制和删除。
* [如何使用包](/help/implementing/developing/tools/package-manager.md) – 可使用包导入和导出存储库内容。本文档说明了在 AEM 6.5 中使用包的方式，此方式也适用于 AEMaaCS。
* [站点管理文档](/help/sites-cloud/administering/site-creation/create-site.md) – 查看有关站点创建的技术文档，了解有关快速站点创建工具的功能的更多详细信息。
* [创建表格或将表格添加到 AEM Sites 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md) - 分步学习将表单集成到您的网站中并优化您的数字体验以尽量提高影响力的技巧和最佳实践。
