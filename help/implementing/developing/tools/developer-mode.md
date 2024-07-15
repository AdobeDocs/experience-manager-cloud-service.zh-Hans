---
title: 开发人员模式
seo-title: Developer Mode
description: 开发人员模式会打开一个侧面板，其中包含多个选项卡，为开发人员提供有关当前页面的信息
seo-description: Developer mode opens a side panel with several tabs that provide a developer with information about the current page
exl-id: fbf11c0f-dc6e-43f3-bcf2-080eacc6ba99
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# 开发人员模式 {#developer-mode}

在AEM中编辑页面时，有多种[模式](/help/sites-cloud/authoring/sites-console/introduction.md#page-modes)可用，包括开发人员模式。 开发人员模式会打开一个侧面板，其中包含多个选项卡，为开发人员提供有关当前页面的技术信息。

有两个选项卡：

* 用于查看结构和性能信息的&#x200B;**[组件](#components)**。
* **[错误](#errors)**&#x200B;以查看发生的任何问题。

这些功能可帮助开发人员：

* **了解**&#x200B;页面的撰写方式。
* **调试：**&#x200B;随时随地发生的情况，这反过来有助于解决问题。

>[!NOTE]
>
>开发人员模式：
>
>* 在移动设备或桌面上的小窗口中不可用（由于空间限制）。
>  * 当宽度小于1024像素时，会发生这种情况。
>* 仅适用于属于`administrators`组的用户。

## 打开开发人员模式 {#opening-developer-mode}

开发人员模式作为页面编辑器的侧面板实施。 要打开面板，请从页面编辑器工具栏的模式选择器中选择&#x200B;**开发人员**：

![正在打开开发人员模式](assets/developer-mode.png)

该面板分为两个选项卡：

* **[组件](#components)** — 这将显示组件树，类似于作者的[内容树](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#content-tree)
* **[错误](#errors)** — 出现问题时，将显示每个组件的详细信息。

### “组件”选项卡 {#components}

![组件选项卡](assets/developer-mode-components-tab.png)

这显示了一个组件树，该组件树：

* 概述页面上呈现的组件和模板链。 可以展开树以显示层次结构中的上下文。
* 显示呈现组件所需的服务器端计算时间。
* 允许您展开树并选择树中的特定组件。 选择提供对组件详细信息的访问；例如：
   * 存储库路径
   * 脚本链接(在CRXDE Lite中访问)
   * 组件详细信息，如[组件控制台](/help/sites-cloud/authoring/components-console.md)中所示
* 在树中选择的组件在编辑器中以蓝色边框指示。

此组件选项卡有助于：

* 确定并比较每个组件的渲染时间。
* 查看并了解层级。
* 通过查找较慢的组件，了解并缩短页面加载时间。

每个组件条目可以具有以下选项：

![开发人员模式组件示例](assets/developer-mode-component-example.png)

* **查看详细信息：**&#x200B;显示以下内容的列表链接：
   * 用于呈现组件的所有组件脚本。
   * 此特定组件的存储库内容路径。

     ![查看详细信息](assets/developer-mode-view-details.png)

* **编辑脚本：**&#x200B;在CRXDE Lite中打开组件脚本的链接。

* **查看组件详细信息：**&#x200B;在[组件控制台](/help/sites-cloud/authoring/components-console.md)中打开组件的详细信息。

通过点按或单击V形标记来展开组件条目也可显示：

    *选定组件中的层次结构。
    *单独呈现选定组件、嵌套在其中的任何单个组件以及合并的总计的次数。

### “错误”选项卡 {#errors}

![错误选项卡](assets/developer-mode-errors-tab.png)

希望&#x200B;**错误**&#x200B;选项卡始终为空（如上所述），但在出现问题时，可能会显示每个组件的以下详细信息：

* 如果组件将条目写入错误日志，同时记录错误详细信息并指向CRXDE Lite中相应代码的链接，则会发出警告。
* 如果组件打开管理会话，会出现警告。

例如，如果调用了未定义的方法，则生成的错误将显示在&#x200B;**错误**&#x200B;选项卡中，并且&#x200B;**组件**&#x200B;选项卡树中的组件项在出现错误时也会标记一个指示符。
