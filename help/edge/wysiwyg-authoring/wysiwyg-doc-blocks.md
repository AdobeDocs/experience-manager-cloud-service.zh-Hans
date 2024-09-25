---
title: 用于WYSIWYG和基于文档的创作的块
description: 了解如何创建可用于WYSIWYG创作和基于文档的创作的块。
feature: Edge Delivery Services
role: User
source-git-commit: 3419fa943eb865d87467443527ea97fcd64909c2
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 用于WYSIWYG和基于文档的创作的块 {#wysiwyg-and-doc-blocks}

了解如何创建可用于WYSIWYG创作和基于文档的创作的块。

## 概述 {#overview}

在某些项目中，您可能希望支持使用通用编辑器](/help/edge/wysiwyg-authoring/authoring.md)进行[WYSIWYG创作以及基于[文档的创作。](/help/edge/docs/authoring.md)为了最大限度地缩短开发时间并确保相同的站点体验，您可以创建一组块来支持这两个用例。

为此，您必须对WYSIWYG创作设置以及基于文档的创作设置使用相同的内容建模方法。

## 方针 {#approach}

在AEM的WYSIWYG创作中，您[声明模型](/help/edge/wysiwyg-authoring/content-modeling.md)并提供命名约定。 然后，使用Edge Delivery以类似表的块结构呈现数据，其方式与使用基于文档的创作手动创建表的方式相同。

为此，进行了某些假设，例如，对于像Teaser这样的简单块，所有属性和属性组都以1呈现。n行，每行具有单列。 对于具有1..n个项目（例如轮播和卡片），这些项目会附加到这些行之后，每个行包含一行，每个属性/属性组包含一列。

如果您对基于文档的创作采用相同的方法，则可以重用WYSIWYG块。
