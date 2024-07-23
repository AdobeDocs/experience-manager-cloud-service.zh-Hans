---
title: 选择创作方法
description: 了解在决定如何在AEM中创作内容时的重要注意事项，以帮助您为内容作者做出最佳决策。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 15eef2d3790d1c0cf5414ca55b191de5b644fed0
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# 选择创作方法 {#authoring-methods}

了解在决定如何在AEM中创作内容时的重要注意事项，以帮助您为内容作者做出最佳决策。

## 注意事项概述 {#overview}

无论您选择基于文档的创作还是WYSIWYG创作，AEM的灵活性都能确保满足您的创作需求。 在开始考虑时，请牢记以下事实。

* **始终让内容作者参与决策。** — 您的内容作者是您的专家，他们的见解至关重要。
* **可以实施多种创作方法。** — 虽然Adobe建议根据需要开始简单并对复杂性进行分层，但多个创作方法可以在一个项目中同时使用。
* **您始终可以在事后更改您的创作方法。** — 无论您决定要锁定哪项。 在Adobe的自动迁移工具的帮助下，您可以直接更改方法。
* **您不能在实施之前做出决定，而是作为实施的一部分做出决定。** - AEM是一个统一产品，因此此重要决策不必包含在合同谈判中。 当你买AEM的时候，你就能得到所有的。 相反，这是在执行期间做出的决定。

Adobe可以帮助您确定在实施过程中最符合要求的方法（或方法）。

## 一种尺寸无法适用于所有尺寸 {#one-size}

AEM的每个实施都有自己的工作流和目标。 一个项目可能涉及一个简单的创作模型，其内容作者负责自己的出版物。 而另一个组织可能拥有由参与者和批准组成的复杂网络。

![其他创作工作流](assets/authoring-workflows.png)

不同的项目可能具有不同的（或多个）用例。

![用例](assets/use-cases.png)

Adobe明白这一点，因此不提供放之四海而皆准的方法。 AEM是您的单一解决方案，可提供各种不同的内容交付和内容创建方法以最好地满足您的需求。

要确定最佳方法，您需要考虑四个项目。

1. [您有内容投放偏好设置吗？](#content-delivery)
1. [您是否有内容创作首选项？](#content-authoring)
1. [您的项目目标是什么？](#project-goals)
1. [您现在面临着哪些创作挑战？](#authoring-challenges)

## 内容交付首选项 {#content-delivery}

您首先要考虑的应该是您希望如何交付内容。 Edge Delivery Services提供闪电般快速的网站，但也许您关注的重点在于headless投放。 以下诊断树可以帮助您考虑各种选项。

![内容投放决策树](assets/content-delivery-decision-tree.png)

这可以帮助您确定是否需要执行以下操作：

* 使用内容片段编辑器和/或通用编辑器将[AEM作为Headless CMS](/help/headless/introduction.md)。
* 使用基于文档的[编辑](/help/edge/docs/authoring.md)或通用编辑器的[WYSIWYG创作的AEMEdge Delivery Services。](/help/edge/wysiwyg-authoring/authoring.md)

## 内容创作首选项 {#content-authoring}

您下一个需要考虑的应该是您希望如何创作内容。 以下诊断树可以帮助您考虑各种选项。

![内容创作决策树](assets/content-authoring-decision-tree.png)

这可以帮助您确定是否需要执行以下操作：

* 使用[基于Edge Delivery Services的编辑](/help/edge/docs/authoring.md)的AEM文档
* [使用通用编辑器进行WYSIWYG创作。](/help/edge/wysiwyg-authoring/authoring.md)

## 项目目标 {#project-goals}

您认为创作成功是什么样的？ 如何定义项目的成功情况？

* 您可能需要让更多人能够创建内容，但希望避免接受有关新工具集的培训。 （考虑基于文档的创作。）
* 您可能需要增加生成的内容量。 （考虑基于文档的创作。）
* 也许您需要专注于视觉内容布局，但最大限度地减少对编码知识的需求。 （想想所见即所得创作。）

在实施之初明确阐述的项目目标将帮助您针对创作方法做出明智的决定。

## 创作挑战 {#authoring-challenges}

最后，请思考您在创作内容时面临的具体挑战。

* 也许您会遇到与在CMS外部创建的内容重复的工作，然后需要导入或复制并粘贴这些内容。 （考虑基于文档的创作。）
* 也许您需要缩短培训作者如何使用CMS所需的时间。 （考虑基于文档的创作。）
* 也许您的作者需要经常编辑内容的可视布局，从而需要经常获得开发人员的支持。 （想想所见即所得创作。）
