---
title: 页面差异
description: 利用“页面差异”功能，可以方便地并排比较突出显示差异的两个页面。
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 34%

---

# 页面差异 {#page-diff}

## 简介 {#introduction}

内容创建是一个反复的过程。 高效的创作要求能够查看在不同的迭代中发生了什么变化。 查看一个页面版本然后查看另一个页面版本会效率低下，并且容易出错。 作者希望能够轻松地将当前页面与另一个版本并排比较。

利用“页面差异”功能，可以方便地并排比较突出显示差异的两个页面。

>[!NOTE]
>
>用户必须具有 **修改/创建/删除** 节点的权限 `/content/versionhistory` 以使用该功能。
>
>请参阅[开发和页面差异](/help/implementing/developing/introduction/page-diff.md#operation-details)，以了解有关此功能的更多技术详细信息。

## 使用 {#use}

可以并排比较以下内容：

* [版本](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page) - 将页面的以前版本与其当前状态进行比较
* [Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md#comparing-a-live-copy-page-with-a-blueprint-page) – 将 Live Copy 与其 Blueprint 进行比较
* [启动项](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page) – 将启动项与其源进行比较
* [语言副本](/help/sites-cloud/administering/translation/managing-projects.md#comparing-language-copies) – 将翻译之前和翻译之后（重新翻译）的页面进行比较

请参阅相关主题，了解如何在这些上下文中开始差异。

### 差异显示 {#presentation-of-differences}

无论比较的内容是什么，差异的表示形式保持不变。

* 启动差异时选择的内容将显示在左侧（差异入口点）。
* 比较内容显示在右侧（所选内容与之比较）。

例如，如果比较版本，则左侧显示当前版本，右侧显示先前版本。

两个页面的源均清楚地显示在浏览器窗口顶部的标题栏中。

![版本并排视图](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

差异检测组件和HTML级别的更改。 已更改的项目会以不同的颜色突出显示。

**组件更改**

* 浅绿色 — 已添加组件
* 粉红色 — 组件已移除

**HTML更改**

* 深绿色 — 已添加HTML
* 红色 - 删除了 HTML

>[!NOTE]
>
>在比较语言副本时，会取消高亮显示，因为在翻译中，所有内容都会更改并高亮显示，没有任何好处。

### 全屏和退出 {#fullscreen-and-exiting}

要集中查看特定内容，您可以单击并排差异比较中任一“侧”的全屏图标，以将其放大到整个浏览器窗口。

![全屏按钮](/help/sites-cloud/authoring/assets/versions-full-screen.png)

选定的一侧将填满整个窗口，但标题栏仍将保留在顶部，允许您在两个页面之间切换。

![全屏模式](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>如果浏览器宽度不能同时容纳处于全屏视图中的两个页面名称，则只会显示所显示页面的名称，而其他名称将显示在省略号后面。

您也可以选择单击退出全屏图标来关闭全屏视图。

![退出全屏模式](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

您可以随时通过单击标题中的关闭按钮退出并排比较。

## 限制 {#limitations}

在某些情况下，页面差异可能无法按预期检测到差异。

* 当版本和启动次数不同时，差异不会考虑痕迹导航、菜单、产品列表或徽标等动态组件（依赖站点结构呈现其内容的组件）。
* 对于版本，差异不会重新创建访问控制策略和 Live Copy 关系。
* 如果移动了页面，您将无法再对移动前创建的任何版本执行差异分析。
   * 如果您遇到差异问题，请检查页面的[时间线](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)以查看页面是否已被移动。

>[!NOTE]
>
>各版本之间不能相互进行比较。只能将页面的当前版本与其他版本进行比较。当前版本始终是突出显示更改的版本。

>[!NOTE]
>
>有关页面差异机制的操作以及可能影响页面差异的限制的更多详细信息，请参阅 [开发人员文档](/help/implementing/developing/introduction/page-diff.md) 此功能的。
