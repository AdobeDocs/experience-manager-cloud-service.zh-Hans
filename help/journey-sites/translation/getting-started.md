---
title: AEM Sites翻译入门
description: 了解如何组织AEM Sites内容以及AEM翻译工具的工作方式。
index: true
hide: false
hidefromtoc: false
source-git-commit: 8c04ffde2cbafcb6d556de8d48fc19f5b130a2c1
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---


# AEM Sites翻译入门 {#getting-started}

了解如何组织AEM Sites内容以及AEM翻译工具的工作方式。

## 迄今为止的故事 {#story-so-far}

在AEM Sites翻译历程的上一个文档中， [了解AEM Sites内容以及如何在AEM中进行翻译](learn-about.md)您学习了AEM Sites的基本理论，现在您应该：

* 了解AEM Sites内容创建的基本概念。
* 熟悉AEM如何支持翻译。

本文基于这些基础知识，以便您了解AEM如何存储和管理内容，以及如何使用AEM翻译工具翻译该内容。

## 目标 {#objective}

本文档可帮助您了解如何开始在AEM中翻译网站内容。 阅读后，您应该：

* 了解内容结构对翻译的重要性。
* 了解AEM如何存储内容。
* 熟悉AEM翻译工具。

## 要求和先决条件 {#requirements-prerequisites}

在开始翻译AEM内容之前，有许多要求。

### 知识 {#knowledge}

* 在CMS中翻译内容的体验
* 使用大型CMS基本功能的经验
* 具有AEM基本操作的工作知识
* 了解您使用的翻译服务
* 基本了解您翻译的内容

>[!TIP]
>
>如果您不熟悉使用大型CMS(如AEM)，请考虑先查看[基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)文档，然后再继续。 基本处理文档未包含在历程中，因此，完成后请返回本页。

### 工具 {#tools}

* 用于测试内容翻译的沙盒访问权限
* 连接到首选翻译服务的凭据
* 是AEM中`project-administrators`组的成员

## AEM如何存储内容 {#content-in-aem}

对于翻译专家而言，深入了解AEM如何管理内容并不重要。 但是，熟悉基本概念和术语后来使用AEM翻译工具时将会很有帮助。 最重要的是，您需要了解您自己的内容及其结构，以便有效地翻译内容。

### 站点控制台 {#sites-console}

“站点”控制台概述了内容的结构，以便通过创建新页面、移动和复制页面以及发布内容来轻松导航和管理内容。

要访问站点控制台，请执行以下操作：

1. 在全局导航菜单中，单击或点按&#x200B;**导航** -> **站点**。
1. 站点控制台将打开到内容的顶级。
1. 确保使用窗口右上角的视图选择器选择&#x200B;**列视图**。

   ![选择列视图](assets/selecting-column-view.png)

1. 通过点按或单击列中的某个项目，它会在右列的层级中显示该项目下方的内容。

   ![内容层次结构](assets/sites-console-hierarchy.png)

1. 通过点按或单击列中某个项目的复选框，该复选框将选择该项目并在右侧的列中显示选定项目的详细信息，同时还会显示上面工具栏中选定项目的许多可用操作。

   ![内容选择](assets/sites-console-selection.png)

1. 通过点按或单击左上角的边栏选择器，还可以显示&#x200B;**内容树**&#x200B;视图，以获取内容的树概述。

   ![内容树视图](assets/sites-console-content-tree.png)

使用这些简单的工具，您可以直观地导览内容结构。

>[!NOTE]
>
>内容架构师通常定义内容结构，而内容作者在该结构中创建内容。
>
>作为翻译专家，简单了解如何导航该结构并了解内容的位置非常重要。

### 页面编辑器 {#page-editor}

站点控制台允许您导航内容并提供其结构的概述。 要查看单个页面的详细信息，您需要使用站点编辑器。

要编辑页面，请执行以下操作：

1. 使用站点控制台可查找并选择页面。 请记住，您需要点按或单击单个页面的复选框才能选择该页面。

   ![选择要编辑的页面](assets/sites-editor-select-page.png)

1. 点按工具栏中的&#x200B;**编辑**&#x200B;选项。
1. 站点编辑器随即会打开，并且选定的页面会加载以在新的浏览器选项卡中进行编辑。
1. 将鼠标悬停或点按内容会显示适用于各个组件的选择器。 组件是构成页面的拖放构建基块。

   ![编辑页面](assets/sites-editor-title.png)

您可以随时切换回浏览器中的相应选项卡，以返回到站点控制台。 使用站点编辑器，您可以在内容作者和受众将看到页面内容时快速查看页面内容。

>[!NOTE]
>
>内容作者使用站点编辑器创建您的网站内容。
>
>作为翻译专家，简单地了解如何使用站点编辑器查看该内容的详细信息非常重要。

## 结构是关键 {#content-structure}

AEM内容由其结构驱动。 AEM对内容结构要求很少，但在项目规划中仔细考虑内容层次结构可以使翻译更简单。

>[!TIP]
>
>在您的AEM项目开始时计划翻译。 及早与项目经理和内容架构师密切合作。
>
>国际化项目经理可以作为单独的角色，其职责是定义哪些内容应翻译、哪些不翻译，哪些翻译内容可由区域或本地内容制作者修改。

## 推荐的内容结构 {#recommended-structure}

如前所建议，请与您的内容架构师合作，为您自己的项目确定适当的内容结构。 但是，下面是一个经过验证、简单且直观的结构，它非常有效。

在`/content`下为项目定义基本文件夹。

```text
/content/<your-project>
```

创作内容的语言称为语言根。 在我们的示例中，它是英语，它应位于此路径下方。

```text
/content/<your-project>/en
```

所有可能需要本地化的项目内容都应置于语言根目录下。

```text
/content/<your-project>/en/<your-project-content>
```

翻译应创建为同级文件夹，并位于语言根目录旁边，其文件夹名称代表语言的ISO-2语言代码。 例如，德语将具有以下路径。

```text
/content/<your-project>/de
```

>[!NOTE]
>
>内容架构师通常负责创建这些语言文件夹。 如果未创建翻译作业，AEM将无法在以后创建翻译作业。

最终结构可能如下所示。

```text
/content
    |- your-project
        |- en
            |- some
            |- exciting
            |- sites
            |- content
        |- de
        |- fr
        |- it
        |- ...
    |- another-project
    |- ...
```

您应该注意内容的特定路径，因为以后配置翻译时需要该路径。

>[!NOTE]
>
>通常，内容架构师负责定义内容结构，通常与翻译专家合作。
>
>此处详细说明了完整性。

## AEM翻译工具 {#translation-tools}

现在，您已了解站点控制台和编辑器以及内容结构的重要性，接下来我们可以了解如何翻译内容。 AEM中的翻译工具非常强大，但在高级别上很容易理解。

* **翻译连接器**  — 连接器是AEM与您使用的翻译服务之间的链接。
* **翻译规则**  — 规则定义特定路径下应翻译的内容。
* **翻译项目**  — 翻译项目收集应作为单次翻译工作处理的内容，并跟踪翻译的进度，与连接器连接以传输要翻译的内容并从翻译服务接收回该内容。

通常，您只为实例设置一次连接器，并为每个项目设置规则。 然后，您使用翻译项目来翻译内容并持续更新其翻译。

## 下一步 {#what-is-next}

现在，您已完成AEM Sites翻译历程的这一部分，接下来您应该：

* 了解内容结构对翻译的重要性。
* 了解AEM如何存储内容。
* 熟悉AEM翻译工具。

在此知识的基础上，通过下一步查看文档[配置翻译连接器](configure-connector.md)来继续您的AEM Sites翻译历程，您将在其中了解如何将AEM连接到翻译服务。|

## 其他资源 {#additional-resources}

虽然建议您通过查看文档[配置翻译连接器](configure-connector.md)来继续翻译历程的下一部分，但以下是一些其他的可选资源，可更深入地了解本文档中提到的一些概念，但不需要继续这些概念。

* [AEM基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 了解AEM UI的基础知识，以便能够轻松导航并执行基本任务，如查找内容。
* [识别要翻译的内容](/help/sites-cloud/administering/translation/rules.md)  — 了解翻译规则如何识别需要翻译的内容。
* [配置翻译集成框架](/help/sites-cloud/administering/translation/integration-framework.md)  — 了解如何配置翻译集成框架以与第三方翻译服务相集成。
* [管理翻译项目](/help/sites-cloud/administering/translation/managing-projects.md)  — 了解如何在AEM中创建和管理机器翻译项目和人工翻译项目。
