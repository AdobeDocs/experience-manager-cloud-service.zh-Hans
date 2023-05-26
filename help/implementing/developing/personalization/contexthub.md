---
title: ContextHub
description: ContextHub是一个用于存储、操作和呈现上下文数据的框架
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub是一个用于存储、操作和呈现上下文数据的框架。 它的主要功能是提供 [在模拟各种角色并在这些角色之间切换时查看上下文数据。](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub允许您：

* [呈现、查看、切换角色和模拟用户体验](#presentation) 使用上下文数据创作页面时。
* [保留上下文数据](#persistence) 作为数据层表示形式。
* [管理区段](#segmentation) 所选上下文的权限。

通过客户端Javascript API，可访问数据以个性化内容。

## 演示文稿 {#presentation}

此 [ContextHub工具栏](/help/sites-cloud/authoring/personalization/contexthub.md) 使营销人员和作者能够查看和处理存储数据，以便在创作页面时模拟用户体验。 工具栏由提供访问权限的UI模块组组成 [ContextHub存储，](#persistence) 会将ContextHub数据保留在客户端上。

每个ContextHub UI模块都是预定义模块类型的实例：

* ContextHub提供了多个 [示例模块类型](sample-modules.md).
* 使用AEM控制台可以 [添加用户界面模块](configuring-contexthub.md#adding-a-ui-module)、和 [在UI模式下对这些组件进行分组](configuring-contexthub.md#adding-a-ui-mode).
* 开发人员可以 [创建自定义模块类型](extending-contexthub.md#creating-contexthub-ui-module-types).

开发人员需要 [将ContextHub组件添加到页面](configuring-contexthub.md).

## 持久性 {#persistence}

ContextHub存储保留在客户端上的上下文数据。 通过ContextHub Javascript API，您可以访问存储区，以根据需要创建、更新和删除数据。 因此，ContextHub表示页面上的数据层。

每个ContextHub存储都是预定义存储类型的实例：

* ContextHub提供了多个 [示例存储类型](sample-stores.md).
* 使用AEM控制台可以 [创建商店](configuring-contexthub.md#creating-a-contexthub-store).
* 开发人员可以 [创建自定义商店类型](extending-contexthub.md#creating-custom-store-candidates).
* 开发人员可以 [访问存储数据](adding-contexthub.md#interacting-with-contexthub-stores) 通过Javascript。

## 分段 {#segmentation}

ContextHub包括一个分段引擎，该引擎管理区段并确定在当前上下文中解析哪些区段。 定义了多个区段。 您可以使用Javascript API执行以下操作 [确定已解析的区段](adding-contexthub.md#determining-resolved-contexthub-segments).
