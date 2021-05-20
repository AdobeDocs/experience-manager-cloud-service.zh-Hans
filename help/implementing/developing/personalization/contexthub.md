---
title: ContextHub
description: ContextHub是用于存储、处理和呈现上下文数据的框架
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub是用于存储、处理和呈现上下文数据的框架。 其主要功能是提供在模拟和切换各种角色时查看[上下文数据的功能。](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub允许您：

* [在使用上下文数据创作页面时，显示、](#presentation) 查看、切换角色和模拟用户体验。
* [将网站上](#persistence) 的上下文数据保留为数据层表示形式。
* [管理](#segmentation) 选定上下文的区段。

客户端Javascript API允许您访问用于个性化内容的数据。

## 演示文稿 {#presentation}

[ContextHub工具栏](/help/sites-cloud/authoring/personalization/contexthub.md)使营销人员和作者能够查看和处理存储数据，以模拟创作页面时的用户体验。 工具栏由UI模块组成，这些模块提供对[ContextHub存储的访问，](#persistence)在客户端上保留ContextHub数据。

每个ContextHub UI模块都是预定义模块类型的实例：

* ContextHub提供了多种[示例模块类型](sample-modules.md)。
* 使用AEM控制台可以[添加UI模块](configuring-contexthub.md#adding-a-ui-module)，并以UI模式](configuring-contexthub.md#adding-a-ui-mode)将它们分组到[中。
* 开发人员可以[创建自定义模块类型](extending-contexthub.md#creating-contexthub-ui-module-types)。

开发人员需要[将ContextHub组件添加到页面](configuring-contexthub.md)。

## 持久性 {#persistence}

ContextHub存储客户端上的持久上下文数据。 ContextHub Javascript API允许您访问存储区，以根据需要创建、更新和删除数据。 因此， ContextHub表示页面上的数据层。

每个ContextHub存储都是预定义存储类型的实例：

* ContextHub提供了多种[示例存储类型](sample-stores.md)。
* 使用AEM控制台创建存储](configuring-contexthub.md#creating-a-contexthub-store)。[
* 开发人员可以[创建自定义存储类型](extending-contexthub.md#creating-custom-store-candidates)。
* 开发人员可以通过Javascript[访问存储数据](adding-contexthub.md#interacting-with-contexthub-stores)。

## 分段 {#segmentation}

ContextHub包括一个分段引擎，用于管理区段并确定哪些区段针对当前上下文进行解析。 定义了多个区段。 您可以使用Javascript API确定[已解析的区段](adding-contexthub.md#determining-resolved-contexthub-segments)。
