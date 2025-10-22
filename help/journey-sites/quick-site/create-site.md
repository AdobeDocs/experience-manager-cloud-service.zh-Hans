---
title: 从模板创建 Site
description: 了解如何使用 Site 模板快速创建 AEM Site。
exl-id: 31bb04c2-b3cc-44ca-b517-5b0d66d9b1fa
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: noDisplay, noCatalog
source-git-commit: 8c4b34a77ef85869048fae254728c58cf0d99b66
workflow-type: tm+mt
source-wordcount: '1485'
ht-degree: 100%

---


# 从模板创建 Site {#create-site-from-template}

{{traditional-aem}}

了解如何使用 Site 模板快速创建 AEM Site。

## 迄今为止的故事 {#story-so-far}

在 AEM 快速 Site 创建历程的上一个文档[了解 Cloud Manager 和快速 Site 创建工作流](cloud-manager.md)中，您已了解 Cloud Manager 以及它如何将新的快速 Site 创建流程联系起来，现在应：

* 了解 AEM Site 和 Cloud Manager 如何协作来推动前端开发
* 了解如何在不具有 AEM 知识的情况下将前端自定义步骤与 AEM 完全分离开来。

本文建立在这些基础知识之上，于是您可迈出配置的第一步并为模板创建一个 Site，以后可使用前端工具自定义该 Site。

## 目标 {#objective}

本文档有助于您了解如何使用 Site 模板快速创建 AEM Site。阅读本文档后，您应：

* 了解如何获取 AEM Site 模板。
* 了解如何使用模板创建 Site。
* 了解如何从新 Site 下载模板以提供给前端开发人员。

## 负责角色 {#responsible-role}

此历程的这一部分适用于 AEM 管理员。

## Site 模板 {#site-templates}

Site 模板是一种将基本 Site 内容组合成方便且可重用的包的方法。Site 模板通常包含基本 Site 内容和结构以及 Site 样式信息，以便快速启动新的 Site。实际结构如下：

* `files`：包含 UI 套件、XD 文件和可能的其他文件的文件夹
* `previews`：包含 Site 模板的屏幕截图的文件夹
* `site`：为从此模板创建的每个 Site 复制的内容的内容包，例如页面模板、页面等。
* `theme`：用于修改 Site 外观的模板主题的来源，包括 CSS、JavaScript 等。

模板具有强大的功能，它们可重用，这使得内容作者能够快速创建 Site。由于您可以在 AEM 安装中使用多个模板，因此可以灵活地满足各种业务需求。

>[!NOTE]
>
>不要将 Site 模板与页面模板混淆。此处描述的 Site 模板定义了 Site 的整体结构。页面模板定义了单个页面的结构和初始内容。

## 获取 Site 模板 {#obtaining-template}

最简单的入门方法是[从其 GitHub 存储库下载最新版本的 AEM 标准 Site 模板](https://github.com/adobe/aem-site-template-standard/releases)。

下载后，您可以像上传任何其他包一样将它上传到您的 AEM 环境。如果您想了解有关此主题的更多信息，请参阅[“其他资源”部分](#additional-resources)，了解有关如何使用包的详细信息。

>[!TIP]
>
>可以自定义 AEM 标准 Site 模板以满足您的项目需求，并且可以消除进一步自定义的需要。但这个主题超出了此历程的范围。有关更多信息，请参阅“标准 Site 模板”的 GitHub 文档。

>[!TIP]
>
>您也可以选择在项目工作流中从来源构建模板。但这个主题超出了此历程的范围。有关更多信息，请参阅“标准 Site 模板”的 GitHub 文档。

## 安装 Site 模板 {#installing-template}

可以使用模板轻松创建 Site。

1. 登录到您的 AEM 创作环境，并导航到 Site 控制台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 在屏幕的右上角选择&#x200B;**创建**，然后从下拉菜单中选择&#x200B;**从模板创建 Site**。

   ![从模板创建新 Site](assets/create-site-from-template.png)

1. 在“创建 Site 向导”中，在左栏的顶部选择&#x200B;**导入**。

   ![Site 创建向导](assets/site-creation-wizard.png)

1. 在文件浏览器中，找到[以前下载的](#obtaining-template)模板并选择&#x200B;**上传**。

1. 上传模板后，该模板将显示在可用模板列表中。选择它（这样还将在右栏中显示关于该模板的信息），然后选择&#x200B;**下一步**。

   ![选择模板](assets/select-site-template.png)

1. 为 Site 提供标题。可以提供 Site 名称，也可以从标题生成 Site 名称（如果被忽略）。

   * Site 标题显示在浏览器标题栏中。
   * Site 名称会成为 URL 的一部分。

1. 选择&#x200B;**创建**，然后将从 Site 模板创建新 Site。

   ![新 Site 的详细信息](assets/create-site-details.png)

1. 在显示的确认对话框中，选择&#x200B;**完成**。

   ![“成功”对话框](assets/success.png)

1. 在 Site 控制台中，新 Site 是可见的，并且可以导航以探索其由模板定义的基本结构。

   ![新 Site 结构](assets/new-site.png)

内容作者现在可以开始创作。

## 是否需要进一步自定义？ {#customization-required}

Site 模板非常强大且灵活，可以为一个项目创建任意数量的模板，从而轻松创建 Site 变体。根据对您使用的 Site 模板执行的自定义级别，您甚至可能不需要额外的前端自定义。

* 如果您的 Site 不需要额外的自定义，恭喜您！您的历程到此结束！
* 如果您仍需进行额外的前端自定义，或者您只是希望了解整个流程，以防将来需要进行自定义，请继续阅读。

## 示例页面 {#example-page}

如果您确实需要额外的前端自定义，请记住，前端开发人员可能不熟悉您的内容的详细信息。因此，最好是为开发人员提供典型内容，在自定义主题时，该内容可以用作参考基础。一个典型示例是 Site 主语言的主页。

1. 在 Site 浏览器中，导航到 Site 主语言的主页，选择该页面以选择它，然后在菜单栏中选择&#x200B;**编辑**。

   ![典型主页](assets/home-page-in-console.png)

1. 在编辑器中，选择工具栏中的&#x200B;**页面信息**&#x200B;按钮，然后选择&#x200B;**以发布的形式查看**。

   ![编辑主页](assets/home-page-edit.png)

1. 在打开的选项卡中，从地址栏中复制内容的路径。它类似于 `/content/<your-site>/en/home.html?wcmmode=disabled`。

   ![主页](assets/home-page.png)

1. 保存路径以便稍后提供给前端开发人员。

## 下载主题 {#download-theme}

现已创建 Site，可以下载模板生成的 Site 主题，并将它提供给前端开发人员进行自定义。

1. 在 Site 控制台上，显示 **Site** 边栏。

   ![显示 Site 边栏](assets/show-site-rail.png)

1. 选择新 Site 的根，然后在 Site 边栏中选择&#x200B;**下载主题源**。

   ![下载主题源](assets/download-theme-sources.png)

您的下载文件中现已拥有主题源文件的副本。

## 设置代理用户 {#proxy-user}

为了让前端开发人员使用您 Site 中的实际 AEM 内容预览自定义项，您必须设置代理用户。

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

您现在已完成配置。内容作者现在可以开始在 Site 上创建内容，为历程的下一步中的前端自定义做准备。

## 后续内容 {#what-is-next}

现在您已完成 AEM 快速 Site 创建历程的这一部分，您应：

* 了解如何获取 AEM Site 模板。
* 了解如何使用模板创建 Site。
* 了解如何从新 Site 下载模板以提供给前端开发人员。

在此知识的基础上继续您的 AEM 快速 Site 创建历程，接下来查看文档[设置您的管道](pipeline-setup.md)，其中您将创建前端管道来管理 Site 主题的自定义。

## 其他资源 {#additional-resources}

我们建议您查看文档[设置管道](pipeline-setup.md)来继续快速 Site 创建历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续此历程所必需的。

* [AEM 标准 Site 模板](https://github.com/adobe/aem-site-template-standard) - 这是 AEM 标准 Site 模板的 GitHub 存储库。
* [组织页面](/help/sites-cloud/authoring/sites-console/organizing-pages.md) - 本指南详细介绍如何组织 AEM Site 的页面。
* [创建页面](/help/sites-cloud/authoring/sites-console/creating-pages.md) - 本指南详细介绍如何将新页面添加到您的 Site。
* [管理页面](/help/sites-cloud/authoring/sites-console/managing-pages.md) - 本指南详细介绍如何管理 Site 页面，包括移动、复制和删除。
* [如何使用包](/help/implementing/developing/tools/package-manager.md) - 可使用包导入和导出存储库内容。本文档说明了在 AEM 6.5 中使用包的方式，此方式也适用于 AEMaaCS。
* [Site 管理文档](/help/sites-cloud/administering/site-creation/create-site.md) - 查看有关 Site 创建的技术文档，了解有关快速 Site 创建工具的功能的更多详细信息。
* [创建表格或将表格添加到 AEM Site 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md) - 分步学习将表单集成到您的网站中并优化您的数字体验以尽量提高影响力的技巧和最佳实践。
