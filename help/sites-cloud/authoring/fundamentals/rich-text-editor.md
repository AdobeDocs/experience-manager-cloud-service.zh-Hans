---
title: 在  [!DNL Adobe Experience Manager]  中使用富文本编辑器创作内容。
description: 使用  [!DNL Experience Manager]  富文本编辑器创作内容。
exl-id: 15c175f8-11de-4475-87a9-920219a4c004
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '286'
ht-degree: 100%

---

# 使用富文本编辑器创作内容 {#use-rich-text-editor-to-author-content}

富文本编辑器 (RTE) 是向 [!DNL Adobe Experience Manager] 添加文本内容的构建基块。此外，许多允许创作的其他组件也都基于 RTE。Experience Manager 开发人员可以自定义 RTE，管理员则可以配置 RTE 以供创作人员使用。

## 就地编辑 {#in-place-editing}

通过单击选择基于文本的组件可显示[组件工具栏](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)。

![组件工具栏](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

再次单击或最初通过缓慢双击选择组件时，将打开就地编辑。编辑模式包含一个工具栏。您可以编辑内容并进行基本的格式更改。

![使用 RTE 就地编辑](/help/sites-cloud/authoring/assets/rte-in-place-editing.png)

通常，工具栏提供以下选项：

* **格式**：以粗体或斜体强调文本，或者为文本加下划线。
* **列表**：创建项目符号或编号列表并设置缩进。
* **超链接**：创建链接。
* **取消链接**：删除超链接。
* **全屏**：以全屏模式打开编辑器。
* **关闭**：停止编辑。
* **保存**：保存更改。

## 全屏编辑 {#full-screen-editing}

对于基于文本的组件，单击[工具栏](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)中的全屏模式 ![RTE 全屏按钮](/help/sites-cloud/authoring/assets/editing-full-screen.png) 以打开富文本编辑器，并隐藏页面内容的其余部分。

全屏模式会显示可用于创作的所有已配置选项。选项的可用性[取决于配置](/help/implementing/developing/extending/rich-text-editor.md)。

![全屏模式下的 RTE](/help/sites-cloud/authoring/assets/rte-full-screen.png)

其他富文本编辑器选项包括：

* **锚点**：在文本中创建一个可在以后链接或引用的锚点。
* **左对齐文本**。
* **居中对齐文本**。
* **右对齐文本**。

单击“最小化”以关闭全屏模式。

>[!TIP]
>
>将嵌套列表从 [!DNL Microsoft Word] 复制到 RTE 中可能会产生不一致的结果。因此，请粘贴为文本并进行手动调整。

>[!MORELIKETHIS]
>
>* [配置富文本编辑器](/help/implementing/developing/extending/rich-text-editor.md)

