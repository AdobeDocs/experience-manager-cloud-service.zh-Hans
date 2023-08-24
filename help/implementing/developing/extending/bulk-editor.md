---
title: 配置对页面属性的批量编辑
description: 了解如何配置批量编辑，以便您可以一次编辑多个页面的属性。
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 100%

---


# 配置对页面属性的批量编辑 {#configuring-bulk-editing-of-page-properties}

[批量编辑页面属性](/help/sites-cloud/authoring/fundamentals/page-properties.md#from-the-sites-console-multiple-pages)功能让您一次编辑多个页面的属性。

## 注意事项 {#considerations}

默认情况下，页面属性未启用批量编辑。必须明确启用这些属性。在定义可用于批量编辑的页面属性时，您需要考虑某些事项，例如：

* 某些字段通常是唯一的。当应用一个值时，您必须确定启用此类字段进行批量编辑是否有意义。
   * 例如，页面标题几乎总是唯一的。
* 某些字段可能会有多个值，在呈现时需要以有意义的方法进行表示。
   * 例如，标记为&#x200B;**准备发布**&#x200B;的状态下拉列表。在批量编辑之前，这可能有几个值，例如&#x200B;**就绪**、**审核中**、**进行中**&#x200B;等。

由于可能存在多个值，建议仅启用以下字段类型进行批量编辑。

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## 启用字段 {#enabling-a-field}

这些步骤使用 [WKND 示例内容](/help/implementing/developing/introduction/develop-wknd-tutorial.md)中的 `/apps/core/wcm/components/page/v1/page` 作为示例，以便在开发环境中对字段进行批量编辑。

1. 使用 CRXDE 打开您的页面组件。
1. 导航至`cq:dialog` 定义中的必填字段。
1. 在字段节点上定义以下属性：

   * **名称**：`allowBulkEdit`
   * **类型**：`Boolean`
   * **值**：`true`

1. 选择&#x200B;**保存全部**，以保留您的更新。

## 限制 {#limitations}

页面属性的批量编辑：

* 不适用于 Live Copy 中的页面。
* 仅适用于具有相同资源类型的页面。
