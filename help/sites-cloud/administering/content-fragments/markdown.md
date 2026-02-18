---
title: Markdown
description: 了解内容片段编辑器如何使用 Markdown 语法，轻松地为页面创作和无头投放创建内容。
feature: Content Fragments
role: User
exl-id: 6fbf8128-3b7f-4eda-bbbd-3336578d2586
solution: Experience Manager Sites
source-git-commit: be60f0371e652549cec6e57d1449b6e07b996514
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 77%

---

# Markdown {#markdown}

当您[创作](/help/sites-cloud/administering/content-fragments/authoring.md#edit-multi-line-text-fields-plaintext-markdown)内容片段时，您可能使用[Markdown](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)的&#x200B;**默认类型**&#x200B;定义了&#x200B;**多行文本字段**。 内容片段编辑器使用 *markdown* 语法使您可轻松地为创作页面和投放 Headless 编写内容：

![编辑器中的 Markdown 多行文本字段](/help/sites-cloud/administering/content-fragments/assets/cf-markdown-field-edit.png)

您可以定义：

* [标题符号](/help/sites-cloud/administering/content-fragments/markdown.md#heading-notation)
* [段落和换行符](/help/sites-cloud/administering/content-fragments/markdown.md#paragraphs-and-line-breaks)
* [链接](/help/sites-cloud/administering/content-fragments/markdown.md#links)
* [图像](/help/sites-cloud/administering/content-fragments/markdown.md#images)
* [块引号](/help/sites-cloud/administering/content-fragments/markdown.md#block-quotes)
* [列表](/help/sites-cloud/administering/content-fragments/markdown.md#lists)
* [强调](/help/sites-cloud/administering/content-fragments/markdown.md#emphasis)
* [代码块](/help/sites-cloud/administering/content-fragments/markdown.md#code-blocks)
* [反斜线转义](/help/sites-cloud/administering/content-fragments/markdown.md#backslash-escapes)

## 标题符号 {#heading-notation}

要创建标题，请在标题前面放置一个井号(#)。 一个哈希符号(#)表示H1，两个哈希符号(##)表示H2，依此类推。 您最多可以使用6个哈希符号。 例如：

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

或者，您也可以通过等号加下划线来创建一级标题，并通过减号加下划线来创建二级标题。例如：

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落和换行符 {#paragraphs-and-line-breaks}

段落只是一行或多行连续的文本，用一行或多行空白行分隔。空行是只包含空格或制表符的行。不应使用空格或制表符缩进普通段落。

换行符的创建方法是：在返回后，用两个或多个空格结束一行。

## 链接 {#links}

您可以创建内联链接和引用链接。

在这两种样式中，链接文本都由方括号分隔 `[]`.

以下是内联链接的示例：

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example (non-standard) of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

引用链接的语法如下：

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 图像 {#images}

图像的语法与链接类似。您可以创建内联和引用的图像。

例如，内联图像的语法如下：

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

语法包括：

* 一个感叹号：!;
* 后跟一组方括号，其中包含图像的 alt 属性文本；
* 后跟一组括号（包含图像的 URL 或路径），以及一个用双引号或单引号括起来的可选标题属性。

引用样式图像的语法如下：

    `![Alt text][id]`

其中，“id”是定义的图像引用的名称。图像引用是使用与链接引用相同的语法来定义的：

    `[id]: url/to/image "Optional title attribute"`

## 块引号 {#block-quotes}

可以在文本前添加 > 符号来引用文本。例如：

    `>This is block quotes`

您可以使用嵌套的块引号。例如：

    `> This is the first level of quoting.`

    `>`

        `>> This is a nested blockquote.`

    `>`

    `> Back to the first level.`

## 列表 {#lists}

您可以创建已排序和未排序的列表。

要创建未排序列表，请在列表中项目之前使用&amp;amp；ast；（星号）符号。 例如：

    `* item in list`

    `* item in list`

    `* item in list`

要创建有序列表，请在列表中每个项目之前添加数字，后跟一个句点。例如：

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 强调 {#emphasis}

您可以为文本添加斜体或粗体样式。

您可以按如下方式添加斜体：

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

您可以按如下方式显示粗体文本：

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

要指示代码跨度，请用反勾号 (&grave;) 将代码换行。与预格式化的代码块不同，代码范围表示普通段落中的代码。

例如：

    ``Use the `printf()` function.``

## 代码块 {#code-blocks}

代码块通常用于说明源代码。您可以通过使用制表符缩进代码，或者最少 4 个空格来创建代码块。例如：

    `This is a normal paragraph.`

        `This is a code block.`

## 反斜线转义 {#backslash-escapes}

您可以使用反斜杠转义生成在格式语法中也具有特殊含义的文字字符。 例如，如果要用文字星号括住单词(而不是HTML &lt;em>标记)，则可以在星号前使用反斜杠，如下所示：

    `\\*literal asterisks\\*`

反斜杠转义可用于以下字符：

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
