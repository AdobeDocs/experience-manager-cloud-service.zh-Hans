---
title: 为通用编辑器配置RTE
description: 了解如何在通用编辑器中配置富文本编辑器(RTE)。
feature: Developing
role: Admin, Developer
exl-id: 350eab0a-f5bc-49c0-8e4d-4a36a12030a1
source-git-commit: edcba16831a40bd03c1413b33794268b6466d822
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# 为通用编辑器配置RTE {#configure-rte}

了解如何在通用编辑器中配置富文本编辑器(RTE)。

## 概述 {#overview}

通用编辑器在就地和属性面板中提供富文本编辑器(RTE)，以允许作者在编辑文本时应用格式更改。

此RTE可使用[组件筛选器进行配置。](/help/implementing/universal-editor/filtering.md)本文档介绍了可用的配置选项以及示例。

## 配置结构 {#structure}

RTE配置由两部分组成：

* [`toolbar`](#toolbar)：工具栏配置控制UI中可用的编辑选项及其组织方式。
* [`actions`](#actions)：操作配置允许您自定义单个编辑操作的行为和外观。

这些配置可以定义为具有属性[的](/help/implementing/universal-editor/filtering.md)组件筛选器`rte`的一部分。

```json
[
  {
    "id": "richtext",
    "rte": {
      "toolbar": {
        // Toolbar configuration
      },
      "actions": {
        // Action-specific configurations
      }
    },
    "components": [
      "richtext"
    ]
  }
]
```

## 工具栏配置 {#toolbar}

工具栏配置控制UI中可用的编辑选项及其组织方式。 这些是可用的部分

```json
{
  "toolbar": {
    // Text formatting options
    "format": ["bold", "italic", "underline", "strike"],
    // Text alignment options
    "alignment": ["left", "center", "right", "justify"],
    // Text direction options, right-to-left or left-to-right
    "direction": ["rtl", "ltr"],
    // Indentation controls
    "indentation": ["indent", "outdent"],
    // Block-level elements
    "blocks": ["paragraph", "h1", "h2", "h3", "h4", "h5", "h6", "code_block"],
    // List options
    "list": ["bullet_list", "ordered_list"],
    // Content insertion
    "insert": ["link", "unlink", "image"],
    // Superscript/subscript
    "sr_script": ["superscript", "subscript"],
    // Editor utilities
    "editor": ["removeformat"],
    // Section ordering (optional)
    "sections": ["format", "alignment", "list"]
  }
}
```

## 操作配置 {#actions}

操作配置允许您自定义各个编辑操作的行为和外观。 这些是可用的部分。

### 设置操作格式 {#format}

格式操作用于应用格式设置，并且支持HTML标记切换以便在语义变体之间进行选择。 以下部分可供使用。

```json
{
  "actions": {
    "bold": {
      "tag": "strong",      // Use <strong> instead of <b>
      "shortcut": "Mod-B",  // Custom keyboard shortcut
      "label": "Make Bold"  // Custom button label 
    },
    "italic": {
      "tag": "em",          // Use <em> instead of <i>
      "shortcut": "Mod-I",
      "label": "Italicize"
    },
    "strike": {
      "tag": "del"          // Use <del> instead of <s>
    }
  }
}
```

### 列出操作 {#list}

列表操作支持内容封装，以控制HTML结构。 以下部分可供使用。

```json
{
  "actions": {
    "bullet_list": {
      "wrapInParagraphs": true,    // <ul><li><p>content</p></li></ul>
      "shortcut": "Mod-Shift-8",   // Custom shortcut
      "label": "Bullet List"       // Custom label
    },
    "ordered_list": {
      "wrapInParagraphs": false,   // <ol><li>content</li></ol> (default)
      "shortcut": "Mod-Shift-9"
    }
  }
}
```

### 链接操作 {#link}

链接操作支持目标属性控制以管理链接行为。 以下部分可供使用。

```json
{
  "actions": {
    "link": {
      "hideTarget": false,       // Show target attribute options (default)
      "shortcut": "Mod-K",       // Custom keyboard shortcut
      "label": "Insert Link"     // Custom button label
    },
    "unlink": {
      "shortcut": "Mod-Shift-K", // Custom keyboard shortcut
      "label": "Remove Link"     // Custom button label
    }
  }
}
```

#### 链接配置选项 {#link-options}

* `hideTarget`： `false`（默认） — 在链接中包含目标属性，允许`_self`、`_blank`等
* `hideTarget`： `true` — 从链接中完全排除目标属性

仅当光标位于现有链接内时，`unlink`操作才会出现。 它删除链接格式，同时保留文本内容。

### 图像操作 {#image}

图像操作支持图片元素封装以生成响应式图像标记。 以下部分可供使用。

```json
{
  "actions": {
    "image": {
      "wrapInPicture": false,     // Use <img> tag (default)
      "shortcut": "Mod-Shift-I",  // Custom keyboard shortcut
      "label": "Insert Image"     // Custom button label
    }
  }
}
```

#### 图像配置选项 {#image-options}

* `wrapInPicture`： `false` （默认） — 生成简单的`<img>`元素
* `wrapInPicture`： `true` — 将图像包装在`<picture>`个元素中以用于响应式设计

### 其他操作 {#other}

所有其他操作都支持基本自定义。 以下部分可供使用。

```json
{
  "actions": {
    "h1": {
      "shortcut": "Mod-Alt-1",
      "label": "Large Heading"
    },
    "paragraph": {
      "shortcut": "Mod-Alt-0",
      "label": "Normal Text"
    },
    "link": {
      "shortcut": "Mod-K",
      "label": "Insert Link",
      "hideTarget": false    // Show target attribute options (default: false)
    }
  }
}
```

## 完整示例 {#example}

以下是完整配置的示例。

```json
[
  {
    "id": "richtext",
    "rte": {
      // Configure which tools appear in toolbar
      "toolbar": {
        "format": [
          "bold",
          "italic"
        ],
        "blocks": [
          "paragraph",
          "h1",
          "h2"
        ],
        "list": [
          "bullet_list",
          "ordered_list"
        ],
        "insert": [
          "link",
          "unlink"
        ],
        "sections": [
          "format",
          "blocks",
          "list",
          "insert"
        ]
      },
      // Customize individual action behavior
      "actions": {
        // Format actions with HTML tag choices
        "bold": {
          "tag": "strong",
          "shortcut": "Mod-B",
          "label": "Bold"
        },
        "italic": {
          "tag": "em",
          "shortcut": "Mod-I"
        },
        // List actions with content wrapping
        "bullet_list": {
          "wrapInParagraphs": true,
          "label": "Bullet List"
        },
        "ordered_list": {
          "wrapInParagraphs": false
        },
        // Link actions with target control
        "link": {
          "hideTarget": false,
          "shortcut": "Mod-K",
          "label": "Add Link"
        },
        "unlink": {
          "label": "Remove Link"
        },
        // Other actions with basic customization
        "h1": {
          "shortcut": "Mod-Alt-1",
          "label": "Main Heading"
        }
      }
    }
  }
]
```

## 操作选项详细信息 {#action-details}

有几个选项提供了一些需要牢记的其他详细信息。

### `wrapInParagraphs` {#wrapInParagraphs}

列表的`wrapInParagraphs`选项控制HTML结构。

#### `wrapInParagraphs: false`（默认） {#wrapInParagraphs-false}

```html
<ul>
  <li>Simple text content</li>
  <li>Another item</li>
</ul>
```

#### `wrapInParagraphs: true` {#wrapInParagraphs-true}

```html
<ul>
  <li><p>Text wrapped in paragraphs</p></li>
  <li><p>Supports rich formatting within items</p></li>
</ul>
```

在需要时使用`wrapInParagraphs: true`：

* 列表项中的丰富格式
* 每个列表项包含多个段落
* 一致的块级样式

### 链接目标选项 {#link-target}

链接的`hideTarget`选项控制`target`属性是否包含在生成的链接中，以及链接创建对话框是否包含用于选择目标的字段。

#### `hideTarget: false`（默认） {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

### 标记选项 {#tag}

格式操作允许在HTML变体之间进行切换。

| 操作 | 默认标记 | 替代标记 | 用例 |
|---|---|---|---|
| `bold` | `<strong>` | `<b>` | 语义与视觉强调 |
| `italic` | `<em>` | `<i>` | 语义与视觉样式 |
| `strike` | `<del>` | `<s>` | 视觉与语义删除 |

选择语义标记(`<strong>`、`<em>`、`<del>`)以获得更好的可访问性和SEO。

### 键盘快捷键 {#keyboard-shortcuts}

快捷方式使用`Mod-Key`格式，其中：

* 在Mac上，`Mod` = `Cmd`，在Windows/Linux上，`Ctrl`
* 示例： `Mod-B`，`Mod-Shift-8`，`Mod-Alt-1`
