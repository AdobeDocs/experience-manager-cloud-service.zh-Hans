---
title: 预览内容片段
description: 了解如何通过一系列方法预览您的内容片段。
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 36%

---

# 预览内容片段 {#previewing-content-fragments}

内容片段可用于Headless投放和页面创作。 由于片段只是内容，没有格式，因此对其进行查看可能更具挑战性。 因此，提供了多种方法，可用于在各种场景中预览片段。

有多种方法可用于内容片段，可从控制台片段控制台和编辑器中访问。 本节中介绍的控制台和编辑器已针对Headless内容投放开发（尽管它们可用于所有场景）。

您可以预览片段：

* 使用[预览URL模式](#preview-url-pattern)

* 通过发布到[预览实例](#preview-instance)并从中取消发布

<!--
* with a HTML template, using **[Preview]()** from the Content Fragments console
-->

当然，您还可以在[内容片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md)中查看您的片段。

>[!IMPORTANT]
>
>可从&#x200B;**内容片段**&#x200B;和&#x200B;**资源**&#x200B;这两个控制台访问内容片段。
>
>还有两个编辑器用于创作内容片段；尽管基本功能相同，但存在一些差异。 两个编辑器都可从两个控制台中访问。
>
>此部分涉及&#x200B;**内容片段**&#x200B;控制台和&#x200B;*新*&#x200B;的内容片段编辑器。这些是专为 Headless 内容投放开发而成（虽然它们可用于所有场景）
>
>有关更多信息，请参阅：
>
>* 使用&#x200B;**资源**&#x200B;控制台[管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)
>* 使用&#x200B;[*原始*&#x200B;内容片段编辑器](/help/assets/content-fragments/content-fragments-variations.md)
>* 使用[内容片段创作页面](/help/sites-cloud/authoring/fragments/content-fragments.md)。

## 预览 URL 模式 {#preview-url-pattern}

利用内容片段编辑器中的选项，作者可以在外部前端应用程序中预览其编辑内容。

要使用此功能，您首先需要：

* 与您的 IT 团队一起设置外部前端应用程序，该应用程序将使用其 JSON 输出来渲染内容片段。

* 设置外部前端应用程序时，**默认预览URL模式**&#x200B;必须定义为相应内容片段模型[的](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#model-properties)属性。

预览URL应遵循以下模式：

    `https://<preview_url>?param=${expression}`

可用的表达式为：

* `${contentFragment.path}`
* `${contentFragment.model.path}`
* `${contentFragment.model.name}`
* `${contentFragment.variation}`
* `${contentFragment.id}`

定义URL后，**[预览](/help/sites-cloud/administering/content-fragments/authoring.md#preview-content-fragment)**&#x200B;按钮在编辑器的顶部工具栏中处于活动状态。 您可以选择此按钮来启动外部应用程序（在单独的选项卡中）以渲染内容片段。

## 预览实例 {#preview-instance}

您可以&#x200B;**发布**&#x200B;和&#x200B;**取消发布**，将片段发布到您的&#x200B;**[预览服务](/help/headless/deployment/architecture.md)**（以及您的发布实例）。

您可以从编辑器或控制台发布片段。

请参阅：

* [发布和预览片段](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment)以了解完整详细信息。

* [正在取消发布片段](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment)，以了解完整的详细信息。

<!--
## Preview based on a HTML Template {#preview-based-on-a-html-template}

The Content Fragment console provides a **Preview** option for every fragment.

The icon can be selected to open a dialog that represents the fragment based on a HTML template. You can use the default template, or develop and load your own.
-->
