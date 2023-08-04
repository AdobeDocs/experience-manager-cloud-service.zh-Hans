---
title: 配置批量编辑页面属性
description: 了解如何配置批量编辑，以便一次编辑多个页面的属性。
source-git-commit: 9563c24c2794f8209494891da1a4a5a3360781db
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 1%

---


# 配置批量编辑页面属性 {#configuring-bulk-editing-of-page-properties}

[批量编辑页面属性](/help/sites-cloud/authoring/fundamentals/page-properties.md#from-the-sites-console-multiple-pages) 允许您同时编辑多个页面的属性。

## 注意事项 {#considerations}

默认情况下未启用页面属性以进行批量编辑。 必须显式启用它们。 在定义可供批量编辑的页面属性时，您需要考虑某些影响，例如：

* 某些字段通常是唯一的。 您必须确定在应用一个值时启用此类字段进行批量编辑是否有意义。
   * 例如，页面标题几乎总是唯一的。
* 某些字段可能具有多个值，在呈现时需要有意义的表示形式。
   * 例如，状态下拉列表标记为 **准备发布**. 在批量编辑之前，它可能有多个值，例如 **就绪**， **正在审核**， **进行中**，等等。

由于可能存在多个值，因此建议仅启用以下字段类型进行批量编辑。

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## 启用字段 {#enabling-a-field}

这些步骤使用 `/apps/core/wcm/components/page/v1/page` 从 [WKND示例内容](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 例如，在开发环境中的字段上启用批量编辑。

1. 使用CRXDE打开页面组件。
1. 导航到 `cq:dialog` 定义。
1. 在字段节点上定义以下属性：

   * **名称**: `allowBulkEdit`
   * **类型**： `Boolean`
   * **值**: `true`

1. 选择 **全部保存** 以保留您的更新。

## 限制 {#limitations}

批量编辑页面属性是：

* 对Live Copy中的页面不可用。
* 仅适用于具有相同资源类型的页面。
