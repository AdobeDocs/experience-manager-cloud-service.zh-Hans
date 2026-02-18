---
title: 提交PDF中支持的HTML标记标记（以前称为记录文档）
description: 有关在生成提交PDF（以前为记录文档）时支持的HTML标记标记的参考指南，包括渲染行为和辅助功能注意事项。
feature: Adaptive Forms
role: Developer, User
exl-id: 8481b0dc-aae7-4bd2-acfe-1f1b6d747683
source-git-commit: 0b112a5a1830fac9d0170771e052bbb2ef3cadbf
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 6%

---


# 提交PDF中支持的HTML标记标记（以前称为记录文档）

## 本参考包含哪些内容？

在生成提交PDF（以前为记录文档）PDF时，AEM Forms现在支持富文本字段中的HTML标记标记。 本指南介绍您可以在自适应Forms中安全地使用哪些HTML标记标记，以及这些标记在生成的提交PDF中如何呈现。

如果向表单添加富文本内容（例如粗体格式、列表或链接），请务必了解支持的标记以及标记可能具有的任何限制。 此参考资料可帮助您选择适当的标记，以确保您的内容在提交PDF中正确显示并保持可访问性。

## 开始之前

### 先决条件

您应该熟悉：

- 基本HTML标记语法
- [提交PDF（以前称为记录文档）基础知识](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- 辅助功能原则和WCAG准则
- PDF辅助功能要求
- 接受HTML标记的自适应表单组件

### 注意事项

提交PDF（以前称为记录文档）可以是一个带标记的PDF，这有助于确保辅助型技术的可访问性和正确结构。 要启用标记的PDF输出，[将XCI属性`config/present/pdf/tagged`设置为`true`](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file)。 生成PDF后，请务必验证辅助功能标记是否已正确应用。 您可以使用[Adobe Acrobat检查辅助功能标记](https://helpx.adobe.com/in/acrobat/using/create-verify-pdf-accessibility.html)并确保您的文档符合辅助功能标准。

### 新增功能

提交PDF中支持富文本是最近的一项增强功能。 以前，富文本内容在生成的文档中显示为纯文本。 这项新功能允许格式化内容在PDF输出中正确呈现。

## HTML标记支持参考

### 完全支持的标记

创建适当的辅助功能节点后，将完全支持这些标记：

| HTML标记 | 描述 | 提交PDF支持 | 辅助功能 | 示例 |
|----------|-------------|-------------|---------------|---------|
| `<p>` | 段落 | 是 | 完全支持 — 正确的`<P>`节点 | `<p>This is a paragraph.</p>` |
| `<br/>` | 换行符 | 是 | 完全支持 — 在`<P>`节点内 | `<p>Line 1<br/>Line 2</p>` |
| `<b>` | 粗体文本 | 是 | 完全支持 — 在`<P>`节点内 | `<b>bold text</b>` |
| `<i>` | 斜体文本 | 是 | 完全支持 — 在`<P>`节点内 | `<i>italic text</i>` |
| `<span>` | 通用内联容器 | 是 | 在块元素内 | `<span>styled text</span>` |
| `<sub>` | 下标 | 是 | 完全支持 — 在块元素内 | `H<sub>2</sub>O` |
| `<sup>` | 上标 | 是 | 完全支持 — 在块元素内 | `E=mc<sup>2</sup>` |
| `<a>` | 超链接 | 是 | 支持有限 — 需要适当的嵌套 | `<a href="url">link text</a>` |


#### 列表辅助功能问题

当前列表渲染创建`<P>`节点，而不是正确的列表结构：

```
Current: <P>1. First item
Current: <P>2. Second item

Expected: <L>
Expected:   <LI>
Expected:     <LBL>1.
Expected:     <LBody>First item
```

### 不支持的标记

这些标记不受支持，并且无法正确呈现：

| HTML标记 | 描述 | 替代解决方案 |
|----------|-------------|---------------------|
| `<h1>` - `<h6>` | 标题标记 | 使用样式化的`<p>`标记或设计级别的标头 |
| `<img>` | 图像 | 使用单独的图像字段或设计模板 |
| `<code>` | 代码块 | 将等宽字体与`<span>`样式一起使用 |
| `<blockquote>` | 块报价 | 使用带缩进的样式化`<p>`标记 |
| `<table>` | 表格 | 使用自适应表单组件 |

## 代码示例

### 基本文本格式

```html
<!--  Supported - renders correctly -->
<p>This paragraph contains <b>bold text</b> and <i>italic text</i>.</p>

<!--  Supported - combined formatting -->
<p>This text is <i><b>bold and italic</b></i>.</p>

<!--  Unsupported - headings don't work -->
<h1>This won't render as a heading</h1>
```

### 列表

```html
<!-- ⚠️ Partially supported - renders but not accessible -->
<ol>
  <li>First numbered item</li>
  <li>Second numbered item</li>
</ol>

<ul>
  <li>First bullet point</li>
  <li>Second bullet point</li>
</ul>
```

### 链接

```html
<!--  Supported - but must be within block elements -->
<p>Visit our <a href="https://example.com">website</a> for more information.</p>

<!--  Incorrect - link not properly nested -->
<a href="https://example.com">Standalone link</a>
```

### 科学记号

```html
<!--  Supported - but limited accessibility -->
<p>Water formula: H<sub>2</sub>O</p>
<p>Einstein's equation: E=mc<sup>2</sup></p>
```

## 相关内容


- [为自适应Forms生成提交PDF（以前称为记录文档）](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- [为核心组件生成提交PDF](/help/forms/generate-document-of-record-core-components.md)
- [提交PDF模板自定义](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record)

