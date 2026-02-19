---
title: 为通用编辑器配置RTE
description: 了解如何在通用编辑器中配置富文本编辑器(RTE)。
feature: Developing
role: Admin, Developer
exl-id: 350eab0a-f5bc-49c0-8e4d-4a36a12030a1
source-git-commit: 39137052e9fa409f7f5494be53fa7693aaa60b17
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 1%

---

# 为通用编辑器配置RTE {#configure-rte}

了解如何在通用编辑器中配置富文本编辑器(RTE)。

## 概述 {#overview}

通用编辑器在就地和属性面板中提供富文本编辑器(RTE)，以允许作者在编辑文本时应用格式更改。

此RTE可使用[组件筛选器进行配置。](/help/implementing/universal-editor/filtering.md)本文档介绍了可用的配置选项以及示例。

>[!NOTE]
>
>在启动通用编辑器项目时，后端支持的所有富文本功能(AEM与Edge Delivery或headless实施)会自动处于活动状态。
>
>* 您可以停用这些不需要的选项。
>* 不支持激活与您的项目类型不兼容的选项。

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

## 操作配置 {#action}

操作配置允许您自定义各个编辑操作的行为和外观。 这些是可用的部分。

### 常用操作选项 {#common-action-options}

大多数操作支持以下常用选项：

* `shortcut?`： string — 覆盖操作的默认键盘快捷键（如果有）
* `label?`：字符串 — 覆盖UI中操作使用的标签
* `hideInline?`：布尔值 — 当`true`时，从上下文（内联）RTE编辑器工具栏中隐藏此操作

```json
{
  "actions": {
    "bold": {
      "label": "Bold",
      "shortcut": "Mod-B",
      "hideInline": true
    }
  }
}
```

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

### 表格操作 {#table-actions}

表操作支持内容封装，以控制表单元格中的HTML结构：

```json
{
  "actions": {
    "table": {
      "wrapInParagraphs": false, // <td>content</td> (default)
      "shortcut": "Mod-Alt-T",   // Custom shortcut
      "label": "Insert Table"    // Custom label
    }
  }
}
```

#### 表配置选项 {#table-configuration-options}

* `wrapInParagraphs`： `false` （默认） — 表单元格包含未换行的文本内容
* `wrapInParagraphs`： `true` — 表单元格将内容包裹在段落标记中

示例：

当`wrapInParagraphs`： `false`：

```html
<!-- Single line -->
<td>Cell content</td>

<!-- Multiple paragraphs get <br> separation -->
<td>Line 1<br />Line 2</td>
```

当`wrapInParagraphs`： `true`：

```html
<!-- Single paragraph -->
<td><p>Cell content</p></td>

<!-- Multiple paragraphs preserved -->
<td>
  <p>Line 1</p>
  <p>Line 2</p>
</td>
```

>[!NOTE]
>
>展开段落(`wrapInParagraphs`： `false`)时，清理器会自动在多个段落之间插入`<br>`标记，以保留可视换行符。 这遵循HTML标准和主要富文本编辑器的常见实践。

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

### 缩进配置 {#indentation}

缩进具有控制缩进行为范围的功能级配置，以及快捷方式和标签的单个操作配置。

```json
{
  "actions": {
    // Feature-level configuration
    "indentation": {
      "scope": "all"  // Controls what content can be indented (default: "all")
    },

    // Individual action configurations
    "indent": {
      "shortcut": "Tab",           // Custom keyboard shortcut
      "label": "Increase Indent"   // Custom button label
    },
    "outdent": {
      "shortcut": "Shift-Tab",     // Custom keyboard shortcut
      "label": "Decrease Indent"   // Custom button label
    }
  }
}
```

#### 缩进范围选项 {#indentation-options}

* `scope`： `all` （默认） — 缩进/减少缩进适用于所有内容：
   * 列表：嵌套/取消嵌套列表项
   * 段落和标题：增加/减少一般缩进级别
* `scope`： `lists` — 缩进/减少缩进仅适用于列表项：
   * 列表：嵌套/取消嵌套列表项
   * 段落和标题：无缩进（这些按钮已禁用）

>[!NOTE]
>
>通过Tab/Shift+Tab键进行列表嵌套的工作方式与常规缩进设置无关。

### 粘贴为文本 {#paste-as-text}

`paste_text`编辑器操作可启用标准的纯文本粘贴工作流。

* **默认快捷键：** Mod-Shift-V(在macOS上为Cmd+Shift+V，在Windows/Linux上为Ctrl+Shift+V)
* **行为：**&#x200B;从文本/纯文本粘贴（忽略源格式）
   * 在列表中，新行将创建新列表项。

```json
{
  "toolbar": {
    "editor": ["removeformat", "paste_text"]
  },
  "actions": {
    "paste_text": {
      "shortcut": "Mod-Shift-v",
      "label": "Paste as Text"
    }
  }
}
```

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

### `wrapInPicture`{#wrapinpicture}

图像的`wrapInPicture`选项控制为图像内容生成的HTML结构。

#### wrapInPicture： false（默认） {#wrapinpicture-false}

```html
<img src="image.jpg" alt="Description" />
```

#### wrapInPicture： true {#wrapinpicture-true}

```html
<picture>
  <img src="image.jpg" alt="Description" />
</picture>
```

在需要时使用`wrapInPicture: true`：

* 具有`<source>`个元素的响应式图像支持。
* 艺术指导功能。
* 高级图像功能经得起未来考验。
* 图素结构一致。

>[!NOTE]
>
>启用`wrapInPicture: true`后，可以为不同的媒体查询和格式使用其他`<source>`元素来增强图像，使它们对于响应式设计更加灵活。

### 链接目标选项 {#link-target}

链接的`hideTarget`选项控制`target`属性是否包含在生成的链接中，以及链接创建对话框是否包含用于选择目标的字段。

#### `hideTarget: false`（默认） {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

#### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

### 禁用图像上的链接 {#disableforimages}

链接的`disableForImages`选项控制用户是否可以在图像和图片元素上创建链接。 这适用于内联`<img>`元素和块级`<picture>`元素。

#### `disableForImages: false`（默认） {#disableforimages-false}

用户可以选择图像并将其包装在链接中。

```html
<!-- Inline image with link -->
<a href="https://example.com">
  <img src="image.jpg" alt="Description" />
</a>

<!-- Block-level picture with link -->
<a href="https://example.com">
  <picture>
    <img src="image.jpg" alt="Description" />
  </picture>
</a>
```

#### disableForImages： true {#disableforimages-true}

选择图像或图片时，将禁用链接按钮。 用户只能对文本内容创建链接。

```html
<!-- Images remain standalone without links -->
<img src="image.jpg" alt="Description" />

<picture>
  <img src="image.jpg" alt="Description" />
</picture>

<!-- Links work normally on text -->
<a href="https://example.com">Link text</a>
```

当您想要：`disableForImages: true`

* 通过防止链接的图像保持视觉一致性。
* 通过将图像和导航分离，简化内容结构。
* 强制实施限制图像链接的内容策略。
* 降低内容中的辅助功能复杂性。

>[!NOTE]
>
>此设置仅影响在图像上创建新链接的功能。 它不会从内容中的图像删除现有链接。

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

## 不支持的HTML {#unsupported-html}

默认情况下，编辑器解析未知HTML标记时，会去除这些标记。 要保留它们，请通过`unsupportedHtml`配置选项选择加入：

```javascript
const rteConfig = {
  unsupportedHtml: true, // preserve unknown HTML tags (default: false)
};
```

| 值 | 行为 |
|---|---|
| `false`（默认） | 解析期间会删除未知的HTML标记。 |
| `true` | 未知HTML标记将封装在自定义的不支持块节点中，以便内容可以安全地来回传输。 |

启用后，编辑器将渲染带有`rte-unsupported-block`类的不支持的节点。 使用者应用程序应提供此类的样式（例如，边框、填充、背景）。 块中的标记标签使用`rte-unsupported-label`，也可以对其进行自定义。
