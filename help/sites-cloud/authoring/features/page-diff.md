---
title: 页面差异
description: 通过页面差异功能，可以方便地将两个页面并排比较，并突出显示它们的差异。
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 100%

---

# 页面差异 {#page-diff}

## 简介 {#introduction}

内容创建是一个迭代过程。要进行高效创作，需要能够发现从一次迭代到另一次迭代所发生的更改。逐个查看页面版本的方式效率低下且容易出错。作者希望能够方便地将当前页面与另一个版本并排比较。

通过页面差异功能，可以方便地将两个页面并排比较，并突出显示它们的差异。

>[!NOTE]
>
>用户必须具有针对节点 `/content/versionhistory` 的&#x200B;**修改/创建/删除**&#x200B;权限，才能使用此功能。
>
>请参阅[开发和页面差异](/help/implementing/developing/introduction/page-diff.md#operation-details)，以了解有关此功能的更多技术详细信息。

## 使用 {#use}

可以并排比较以下内容：

* [版本](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page) - 将页面的以前版本与其当前状态进行比较
* [Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md#comparing-a-live-copy-page-with-a-blueprint-page) – 将 Live Copy 与其 Blueprint 进行比较
* [启动项](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page) – 将启动项与其源进行比较
* [语言副本](/help/sites-cloud/administering/translation/managing-projects.md#comparing-language-copies) – 将翻译之前和翻译之后（重新翻译）的页面进行比较

请参阅有关如何在这些情况下启动差异比较的相关主题。

### 差异表示形式 {#presentation-of-differences}

无论比较何种内容，差异的表示形式都保持相同。

* 启动差异比较时选择的内容显示在左侧（差异入口点）。
* 要与之比较的内容则显示在右侧（要将所选内容与之比较的内容）。

例如，如果要比较版本，则当前版本显示在左侧，以前的版本显示在右侧。

两个页面的源会清楚地显示在浏览器窗口顶部的标题栏中。

![版本并排视图](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

差异比较会检测在组件和 HTML 级别发生的更改。发生更改的项目会以不同的颜色突出显示。

**组件更改**

* 浅绿色 - 添加了组件
* 粉红色 - 删除了组件

**HTML 更改**

* 深绿色 - 添加了 HTML
* 红色 - 删除了 HTML

>[!NOTE]
>
>在比较语言副本时，会取消激活突出显示功能，因为在翻译中，所有内容都会发生更改，突出显示没有任何用处。

### 全屏和退出 {#fullscreen-and-exiting}

为了集中查看特定内容，您可以单击并排差异比较任何一侧的全屏图标，以将其放大到整个浏览器窗口。

![全屏按钮](/help/sites-cloud/authoring/assets/versions-full-screen.png)

选定的一侧将填满整个窗口，但标题栏仍将保留在顶部，允许您在两个页面之间切换。

![全屏模式](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>如果浏览器宽度不能同时容纳处于全屏视图中的两个页面名称，则只会显示所显示页面的名称，而其他名称将显示在省略号后面。

您也可以选择单击退出全屏图标来关闭全屏视图。

![退出全屏模式](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

您可以通过单击标题中的“关闭”按钮，随时退出并排差异比较。

## 限制 {#limitations}

在某些情况下，页面差异功能可能检测不到预期的差异。

* 在比较版本和启动项时，差异不会考虑动态组件，如痕迹导航、菜单、产品列表或徽标（依赖站点结构呈现其内容的组件）。
* 对于版本，差异不会重新创建访问控制策略和 Live Copy 关系。
* 如果页面发生移动，将无法再使用移动前制作的任何版本执行差异。
   * 如果您遇到差异问题，请检查页面的[时间线](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)以查看页面是否已被移动。

>[!NOTE]
>
>各版本之间不能相互进行比较。只能将页面的当前版本与其他版本进行比较。当前版本始终是突出显示更改的版本。

>[!NOTE]
>
>有关页面差异机制的操作以及可能影响页面差异的限制的更多详细信息，请参阅此功能的[开发人员文档](/help/implementing/developing/introduction/page-diff.md)。
