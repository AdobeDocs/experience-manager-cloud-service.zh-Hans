---
title: 为通用编辑器配置Assets选择器
description: 了解如何配置资产选择器以与通用编辑器一起使用。
feature: Developing
role: Admin, Developer
source-git-commit: 0ed57393afaf9af3258dacdcb043487f4a098e03
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 1%

---


# 为通用编辑器配置Assets选择器 {#configure-assets-selector}

了解如何配置资产选择器以与通用编辑器一起使用。

## 概述 {#overview}

通用编辑器使用[资源选择器](/help/assets/overview-asset-selector.md#using-asset-selector)允许作者浏览并选择资源以插入其内容中。

可以使用[组件筛选器在通用编辑器中配置资源选择器。](/help/implementing/universal-editor/filtering.md)本文档介绍了可用的配置选项。

>[!NOTE]
>
>在启动通用编辑器项目时，资产选择器没有适当的筛选器。 作者将有权访问其用户权限通常允许的所有资源。

## 筛选器定义 {#filter-definition}

资源选择器的过滤器定义具有简单的结构。

```json
[
  {
    "id": "assets-filter",
    "assets": {...}
   }
]
```

## 筛选器选项 {#filter-options}

`assets`筛选器可以具有以下选项。

* `deliveryTier?`： — 定义要使用下列哪个投放层：
   * `dm`：如有必要，使用回退到`publish`的Dynamic Media（首选）
   * `publish`： AEM发布实例
* `repoNames?`：字符串 — 可用于选择图像的AEM存储库列表。
   * 默认：所有投放存储库
* `selectionTier?`：字符串 — 要从中选择资源的AEM层
   * 默认： `["author", "delivery"]`
* `disableRemote?`：布尔值 — 禁用远程存储库支持
* `preselectedTypes?`：字符串 — 要作为资产选择器中的默认筛选条件应用的预选文件类型
* `minMaxDimensions?`：对象 — 提供最小和/或最大尺寸（以像素为单位），以用作资源选择器中的默认筛选器
   * `widthMin?`：数字 — 最小宽度
   * `widthMax?`：数字 — 最大宽度
   * `heightMin?`：数字 — 最小高度
   * `heightMax?`： Number — 最大高度
* `minMaxFileSize?`：对象 — 提供最小和/或最大文件大小（以字节为单位），以用作资源选择器中的默认筛选器
   * `min?`： Number — 最小文件大小
   * `max?`： number — 最大文件大小
* `customFileTypeFilters?`：对象 — 提供要在资源选择器中显示的自定义文件类型筛选器
   * `label`：字符串 — 要在资源选择UI中显示的标签
   * `value`： String — 要过滤的文件类型的值
* `displayFilters?`：布尔值 — 用于禁用资产选择器中的筛选器UI；默认为true

## 示例 {#example}

以下示例包含大部分用于说明的选项。

```json
[
  {
    "id": "assets-filter",
    "assets": {
      "deliveryTier": "dm",
      "repoNames": ["thisRepo", "thatRepo"],
      "selectionTier": ["author", "delivery"],
      "disableRemote": true,
      "preselectedTypes": ["png", "svg", "jpg", "gif"],
      "minMaxDimensions": {
        "widthMin": 640,
        "widthMax": 640,
        "heightMin": 480,
        "heightMax": 480
      },
      "minMaxFileSize": {
        "min": 1024,
        "max": 1024
      }
    }
   }
]
```

## 其他资源 {#additional-resources}

有关资产选择器的详细信息，请参阅资产文档中的文档[微前端资产选择器](/help/assets/overview-asset-selector.md#using-asset-selector)。
