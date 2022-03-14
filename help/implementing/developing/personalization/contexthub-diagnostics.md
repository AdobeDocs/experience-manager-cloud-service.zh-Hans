---
title: ContextHub 诊断
description: ContextHub提供了诊断页面，您可以在其中查看ContextHub框架的概述
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# ContextHub 诊断 {#contexthub-diagnostics}

ContextHub提供了诊断页面，您可以在其中查看ContextHub框架的概述。 要打开页面，请转到 `contexthub.diagnostics.html` 页面，例如：

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

ContextHub诊断页面提供有关已创建的存储和UI模块、已加载的客户端库文件夹以及指向有用页面的链接的信息。

>[!NOTE]
>
>要返回诊断信息，必须启用调试模式，否则诊断页面将为空。 请参阅 [本文档](configuring-contexthub.md#debugging-contexthub) 以了解有关如何启用调试模式的详细信息。

## 商店 {#stores}

“存储”部分列出了已配置的所有ContextHub存储。 列表中的每个项目都包含以下信息：

* **标题：** 的 [存储类型](sample-stores.md) 商店所基于的。
* **路径：** 保存配置的存储库节点的路径。
* **resourceType:** 定义存储类型的存储库节点的路径。
* **clientlibs:** 所加载用于实施存储类型的客户端库的类别。

## 模块 {#modules}

“模块”部分列出了已配置的所有ContextHub UI模块。 列表中的每个项目都包含以下信息：

* **标题：** 的 [UI模块类型](sample-modules.md) UI模块所基于的信息。
* **路径：** 保存配置的存储库节点的路径。
* **resourceType:** 定义UI模块类型的存储库节点的路径。
* **clientlibs:** 加载的用于实施UI模块类型的客户端库的类别。

## Clientlibs {#clientlibs}

Clientlibs部分列出了 [客户端库文件夹](/help/implementing/developing/introduction/clientlibs.md) ContextHub已加载。 客户端库分类如下：

* **kernel.js:** 实施ContextHub框架、区段引擎和存储类型的客户端库。
* **ui.js:** 实施ContextHub UI和UI模块类型的客户端库。
* **style.css:** 从客户端库加载的CSS文件。

## URL {#urls}

URL部分包含指向ContextHub功能的链接：

* **配置编辑器：** 打开 [“ContextHub配置”页](configuring-contexthub.md) 您可以在其中配置存储、UI模式和UI模块。
* **ContextHub模块的配置：** 打开 `/etc/cloudsettings/default/contexthub.config.kernel.js` 文件，其中包含ContextHub存储配置的Javascript对象表示形式。
* **ContextHub UI的配置：** 打开 `/etc/cloudsettings/default/contexthub.config.ui.js` 文件，其中包含ContextHub UI模式配置的Javascript对象表示形式。
* **kernel.js:** 打开 `/etc/cloudsettings/default/contexthub.kernel.js` 文件，其中包含实施ContextHub框架、区段引擎和存储类型的客户端库的源代码。
* **ui.js:** 打开 `/etc/cloudsettings/default/contexthub.ui.js` 文件，其中包含实施ContextHub UI和UI模块类型的客户端库的源代码。
* **style.css:** 打开 `/etc/cloudsettings/default/contexthub.styles.css` 文件，其中包含ContextHub UI和UI模块的CSS样式。
