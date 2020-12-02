---
title: ContextHub
description: ContextHub是存储、处理和呈现上下文数据的框架
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---


# ContextHub {#contexthub}

ContextHub是存储、处理和呈现上下文数据的框架。 它的主要功能是提供在模拟和切换各种角色时[视图上下文数据的能力。](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub允许您：

* [在使用上下文数据创作页面时，呈现、视图、](#presentation) 切换角色和模拟用户体验。
* [将网站](#persistence) 上的上下文数据作为数据层表示。
* [管理](#segmentation) 所选上下文的段。

客户端Javascript API允许您访问数据以个性化内容。

## 演示文稿 {#presentation}

[ContextHub工具栏](/help/sites-cloud/authoring/personalization/contexthub.md)使营销人员和作者能够查看和操作存储数据，以在创作页面时模拟用户体验。 工具栏由UI模块组成，这些模块提供对[ContextHub存储区的访问，](#persistence)这些存储区将ContextHub数据保留在客户端上。

每个ContextHub UI模块都是预定义模块类型的实例：

* ContextHub提供多种[示例模块类型](sample-modules.md)。
* 使用AEM控制台添加[UI模块](configuring-contexthub.md#adding-a-ui-module)，并以UI模式](configuring-contexthub.md#adding-a-ui-mode)将它们分组。[
* 开发人员可以[创建自定义模块类型](extending-contexthub.md#creating-contexthub-ui-module-types)。

开发人员需要[将ContextHub组件添加到页面](configuring-contexthub.md)。

## 持久性{#persistence}

ContextHub在客户端上存储持续的上下文数据。 ContextHub Javascript API允许您根据需要访问存储以创建、更新和删除数据。 因此，ContextHub表示页面上的数据层。

每个ContextHub存储都是预定义存储类型的实例：

* ContextHub提供多种[示例存储类型](sample-stores.md)。
* 使用AEM控制台创建[商店](configuring-contexthub.md#creating-a-contexthub-store)。
* 开发人员可以[创建自定义存储类型](extending-contexthub.md#creating-custom-store-candidates)。
* 开发人员可以通过Javascript[访问存储数据](adding-contexthub.md#interacting-with-contexthub-stores)。

## 分段 {#segmentation}

ContextHub包含一个分段引擎，它管理区段并确定为当前上下文解析哪些区段。 定义了多个区段。 您可以使用Javascript API确定已解析的段](adding-contexthub.md#determining-resolved-contexthub-segments)。[
