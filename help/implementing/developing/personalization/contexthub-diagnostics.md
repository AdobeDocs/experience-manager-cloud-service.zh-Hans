---
title: ContextHub诊断
description: ContextHub提供诊断页面，您可以在其中看到ContextHub框架的概述
translation-type: tm+mt
source-git-commit: 1c518830f0bc9d9c7e6b11bebd6c0abd668ce040
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# ContextHub诊断 {#contexthub-diagnostics}

ContextHub提供诊断页面，您可以在其中查看ContextHub框架的概述。 要打开页面，请转 `contexthub.diagnostics.html` 到AEM作者实例的页面，例如：

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

ContextHub诊断页面提供有关已创建的商店和UI模块、已加载的客户端库文件夹以及指向有用页面的链接的信息。

>[!NOTE]
>
>要返回诊断信息，必须启用调试模式，否则诊断页面将为空。 有关如 [何启用调试模式](configuring-contexthub.md#debugging-contexthub) 的详细信息，请参阅此文档。

## 商店 {#stores}

“存储”部分列表所有已配置的ContextHub存储。 该列表中的每个项目都包含以下信息：

* **标题：** 存 [储所基](sample-stores.md) 于的存储类型。
* **路径：** 保存配置的存储库节点的路径。
* **resourceType:** 定义存储类型的存储库节点的路径。
* **clientlibs:** 加载的实现存储类型的客户端库的类别。

## 模块 {#modules}

“模块”部分列表已配置的所有ContextHub UI模块。 该列表中的每个项目都包含以下信息：

* **标题：** UI [模块所基](sample-modules.md) 于的UI模块类型。
* **路径：** 保存配置的存储库节点的路径。
* **resourceType:** 定义UI模块类型的存储库节点的路径。
* **clientlibs:** 加载的实现UI模块类型的客户端库的类别。

## Clientlibs {#clientlibs}

Clientlibs部分列表ContextHub已加 [载的所有客户](/help/implementing/developing/introduction/clientlibs.md) 端库文件夹。 客户端库分为以下几类：

* **kernel.js:** 实现ContextHub框架、区段引擎和存储类型的客户端库。
* **ui.js:** 实现ContextHub UI和UI模块类型的客户端库。
* **style.css:** 从客户端库加载的CSS文件。

## URL {#urls}

URL部分包含指向ContextHub功能的链接：

* **配置编辑器：** 打开“ [ContextHub配置](configuring-contexthub.md) ”页，在该页中可以配置存储、UI模式和UI模块。
* **配置ContextHub模块：** 打开文 `/etc/cloudsettings/default/contexthub.config.kernel.js` 件，其中包含ContextHub存储配置的Javascript对象表示。
* **ContextHub UI的配置：** 打开文 `/etc/cloudsettings/default/contexthub.config.ui.js` 件，其中包含ContextHub UI模式配置的Javascript对象表示。
* **kernel.js:** 打开文 `/etc/cloudsettings/default/contexthub.kernel.js` 件，该文件包含实现ContextHub框架、段引擎和存储类型的客户端库的源代码。
* **ui.js:** 打开文 `/etc/cloudsettings/default/contexthub.ui.js` 件，该文件包含实现ContextHub UI和UI模块类型的客户端库的源代码。
* **style.css:** 打开文 `/etc/cloudsettings/default/contexthub.styles.css` 件，其中包含ContextHub UI和UI模块的CSS样式。
