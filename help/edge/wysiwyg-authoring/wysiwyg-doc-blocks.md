---
title: 用于所见即所得和基于文档创作的块
description: 了解如何创建可用于所见即所得创作和基于文档创作的块。
feature: Edge Delivery Services
role: User
source-git-commit: 3419fa943eb865d87467443527ea97fcd64909c2
workflow-type: ht
source-wordcount: '235'
ht-degree: 100%

---


# 用于所见即所得和基于文档的创作的块 {#wysiwyg-and-doc-blocks}

了解如何创建可用于所见即所得创作和基于文档的创作的块。

## 概述 {#overview}

在某些项目中，您可能希望同时支持[使用通用编辑器进行所见即所得创作](/help/edge/wysiwyg-authoring/authoring.md)以及[基于文档的创作。](/help/edge/docs/authoring.md) 为了最大限度地减少开发时间并确保相同的网站体验，您可以创建一组块来支持这两种用例。

为此，您必须对所见即所得的创作设置和基于文档的创作设置使用相同的内容建模方法。

## 方法 {#approach}

在 AEM 中的所见即所得创作中，您可以[声明一个模型](/help/edge/wysiwyg-authoring/content-modeling.md)并提供命名惯例。然后，使用 Edge Delivery 将数据呈现为表格状的块结构，其方式与使用基于文档的创作手动创建表格的方式相同。

为了实现这一点，做出了某些假设，例如对于像 Teaser 这样的简单块，所有属性和属性组都在 1..n 行中呈现，每行一列。对于具有 1..n 个项目的块（如轮播和卡片），这些项目将附加在这些行之后，每行一行，每个属性/属性组一列。

如果您遵循相同的基于文档的创作方法，则可以重复使用所见即所得的块。
