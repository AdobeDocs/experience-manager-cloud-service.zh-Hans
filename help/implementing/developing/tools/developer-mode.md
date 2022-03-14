---
title: 开发人员模式
seo-title: Developer Mode
description: 开发人员模式会打开包含多个选项卡的侧面板，这些选项卡为开发人员提供有关当前页面的信息
seo-description: Developer mode opens a side panel with several tabs that provide a developer with information about the current page
exl-id: fbf11c0f-dc6e-43f3-bcf2-080eacc6ba99
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---

# 开发人员模式 {#developer-mode}

在AEM中编辑页面时， [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 包括开发人员模式。 开发人员模式会打开一个侧面板，其中包含多个选项卡，为开发人员提供有关当前页面的技术信息。

有两个选项卡：

* **[组件](#components)** 以查看结构和性能信息。
* **[错误](#errors)** 以查看出现的任何问题。

这些帮助开发人员：

* **Discover** 页面的构成方式。
* **调试：** 发生在何处和何时的事件，这反过来有助于解决问题。

>[!NOTE]
>
>开发人员模式：
>
>* 在移动设备上或桌面上的小窗口上不可用（由于空间限制）。
>  * 当宽度小于1024像素时，会发生这种情况。
>* 仅适用于 `administrators` 群组。


## 打开开发人员模式 {#opening-developer-mode}

开发人员模式作为页面编辑器的侧面板来实施。 要打开面板，请选择 **开发人员** 从页面编辑器工具栏的模式选择器中：

![打开开发人员模式](assets/developer-mode.png)

该面板分为两个选项卡：

* **[组件](#components)**  — 此时会显示组件树，与 [内容树](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree) 对于作者
* **[错误](#errors)**  — 当出现问题时，将显示每个组件的详细信息。

### “组件”选项卡 {#components}

![“组件”选项卡](assets/developer-mode-components-tab.png)

此时将显示一个组件树，该组件树：

* 概述页面上呈现的组件和模板链。 可以展开树以显示层次结构中的上下文。
* 显示呈现组件所需的服务器端计算时间。
* 用于展开树并选择树中的特定组件。 通过选择组件，可以访问组件详细信息；例如：
   * 存储库路径
   * 指向脚本的链接(在CRXDE Lite中访问)
   * 组件详细信息，如 [组件控制台](/help/sites-cloud/authoring/features/components-console.md)
* 树中选定的组件在编辑器中以蓝色边框表示。

此组件选项卡有助于：

* 确定并比较每个组件的渲染时间。
* 查看并了解层级。
* 通过查找慢速组件，了解并改进页面加载时间。

每个组件条目可以具有以下选项：

![开发人员模式组件示例](assets/developer-mode-component-example.png)

* **查看详细信息：** 指向列表的链接，其中显示：
   * 用于呈现组件的所有组件脚本。
   * 此特定组件的存储库内容路径。

      ![查看详细信息](assets/developer-mode-view-details.png)

* **编辑脚本：** 在CRXDE Lite中打开组件脚本的链接。

* **查看组件详细信息：** 在 [组件控制台。](/help/sites-cloud/authoring/features/components-console.md)

通过点按或单击V形标记来展开组件条目还可能显示：

    *选定组件中的层次结构。
    *单独呈现选定组件、其中嵌套的任何单个组件的呈现时间以及组合的总计。

### “错误”选项卡 {#errors}

![“错误”选项卡](assets/developer-mode-errors-tab.png)

希望 **错误** 选项卡将始终为空（如上所示），但是当出现问题时，可能会为每个组件显示以下详细信息：

* 当组件将条目写入错误日志、错误详细信息以及指向CRXDE Lite中相应代码的链接时，会出现警告。
* 组件打开管理员会话时出现警告。

例如，如果调用了未定义的方法，则生成的错误将显示在 **错误** 选项卡和 **组件** 选项卡在发生错误时也会使用指示器进行标记。
