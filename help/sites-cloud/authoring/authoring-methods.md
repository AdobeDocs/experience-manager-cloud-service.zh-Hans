---
title: 在AEM中创作内容的方法
description: 了解在AEM中创作内容的不同方式以及它们之间的差异。
feature: Authoring
exl-id: ef482843-451b-474e-a8d0-d0bfcc17221b
solution: Experience Manager Sites
role: User
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# 在AEM中创作内容的方法 {#authoring-methods}

了解在AEM中创作内容的不同方式、它们的不同之处，以及何时可以相互使用内容。

## AEM创作灵活性 {#authoring-flexibility}

AEM as a Cloud Service提供了多个不同的编辑器，用于编辑不同类型的内容并支持不同的创作用例。

* [使用页面编辑器进行WYSIWYG创作](#page-editor) — 页面编辑器是AEM中创作内容的经典编辑器，已尝试数千个网站并受其信任。
* [使用通用编辑器进行WYSIWYG创作](#universal-editor) — 通用编辑器是一个新式UI，允许您以与内容无关的方式创作AEM内容，可用于利用Edge Delivery Services的AEM项目。
* [基于文档的创作](#document-based) — 如果您使用Edge Delivery服务，则可以选择在AEM控制台之外完全作为常规文档(如Microsoft Word或Google文档)创作内容。
* [AEM内容片段编辑器](#cf-editor) — 这是创建Headless内容的首选编辑器。

由于AEM的集成和可伸缩性质，这些方法可单独使用，也可以根据项目的需求相互组合使用。

如果您不确定可以使用哪些创作选项，或者您想探索用于创作内容的新选项，请与您的系统管理员或项目经理联系。

## 使用页面编辑器进行WYSIWYG创作 {#page-editor}

这是用于在AEM中创作内容的经典编辑器，已尝试并受数千个网站的信任。

![AEM页面编辑器](assets/authoring-methods-page-editor.png)

AEM页面编辑器提供了一个集成环境，用于使用“所见即所得”(WYSIWYG)界面创作内容。 拖放预定义组件以就地构建页面和编辑内容。

要了解有关AEM页面编辑器的更多信息，请参阅文档[AEM页面编辑器。](/help/sites-cloud/authoring/page-editor/introduction.md)

## 使用通用编辑器进行WYSIWYG创作 {#universal-editor}

通用编辑器是一个现代化的用户界面，可让您以与内容无关的方式创作AEM内容，并且是利用Edge Delivery Services的AEM项目的首选。

![Universal Editor](assets/authoring-methods-ue.png)

通用编辑器通过AEM中的站点控制台访问，但它提供了强大且与内容无关的灵活性，不仅可以创作AEM内容，还可以创作正确仪表化的外部内容。

要了解有关通用编辑器的更多信息，请参阅文档[使用通用编辑器创作内容。](/help/sites-cloud/authoring/universal-editor/authoring.md)

## 基于文档的创作  {#document-based}

如果您使用Edge Delivery服务，则可以选择在[AEM **Sites**&#x200B;控制台之外将内容创作为常规文档，如Microsoft Word或Google Docs。](/help/sites-cloud/authoring/sites-console/introduction.md)

![正在编辑基于文档的内容](assets/authoring-methods-document.jpg)

通过基于文档的创作，作者可以使用他们已知并且仍从AEMEdge Delivery Services的速度和性能中受益的工具来发布其内容。 基于文档的创作不需要使用AEM控制台。

若要了解有关基于文档的创作的更多信息，请参阅文档[创作和发布内容。](/help/edge/docs/authoring.md)

## AEM内容片段编辑器 {#cf-editor}

AEM内容片段编辑器是创建Headless内容的首选编辑器。

![AEM内容片段编辑器](assets/authoring-methods-cf-editor.png)

AEM内容片段编辑器提供了一个清晰的界面，用于创建和管理结构化内容，非常适用于Headless投放。

要了解有关AEM内容片段编辑器的更多信息，请参阅文档[管理内容片段](/help/sites-cloud/administering/content-fragments/managing.md)和[创作内容片段](/help/sites-cloud/administering/content-fragments/managing.md)。

>[!NOTE]
>
>在本地为AEM as a Cloud Service开发时，此部分突出显示的&#x200B;*新*&#x200B;编辑器不可用。
>
>[*原始*&#x200B;内容片段编辑器](/help/assets/content-fragments/content-fragments-variations.md)也可用。
