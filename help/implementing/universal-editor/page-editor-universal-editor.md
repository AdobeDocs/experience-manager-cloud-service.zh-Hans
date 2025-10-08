---
title: 页面编辑器和通用编辑器
description: Adobe 继续支持页面编辑器，但通用编辑器将为您的新项目带来令人激动的可能性。
feature: Developing
role: Admin, Architect, Developer
exl-id: 0a13fb52-623e-4aff-b254-186d8d117e4d
source-git-commit: 90c542bfc6ba6bcab34b640e3539971b8b89034c
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 100%

---

# 页面编辑器和通用编辑器 {#page-editor-universal-editor}

Adobe 继续支持页面编辑器，但通用编辑器将为您的新项目带来令人激动的可能性。

## 背景 {#background}

2024 年，Adobe 推出了[通用编辑器](/help/implementing/universal-editor/introduction.md)，这是一款采用基于 Javascript 的现代开发方法的精简编辑器。通用编辑器体现了 Adobe 对无缝且可扩展的视觉内容创作体验的愿景。

[页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)包含丰富的功能集，而且在 AEM 的长期历史中通过无数项目对其注入了大量投资，因此 Adobe 将继续全力支持页面编辑器，但创新将集中在通用编辑器上。

## 推荐 {#recommendation}

尽管通用编辑器和页面编辑器之间的功能差距正在迅速缩小，但差距仍然存在（[下一节将介绍功能对比](#feature-comparison)）。

根据经验法则：

* **新项目**&#x200B;应默认使用通用编辑器。
* **现有项目**&#x200B;应继续使用页面编辑器，如果开始 Edge Delivery 或无头方式工作，可考虑使用通用编辑器。

**您选择哪种编辑器应该完全取决于您具体项目的需求。**

## 功能对比  {#feature-comparison}

由于两个编辑器之间的功能差距正在不断缩小，请务必阅读[通用编辑器的发行说明](/help/release-notes/universal-editor/current.md)，了解最新进展。

### 交付 {#delivery}

|  | 页面编辑器 | 注释 | 通用编辑器 | 注释 |
|---|---|---|---|---|
| [发布交付](/help/sites-cloud/authoring/author-publish.md) | [!BADGE 可用]{type=Positive} | 建议与核心组件和传统 AEM 项目使用 | [!BADGE 不可用]{type=Negative} | 传统的 AEM 页面通常依赖于页面编辑器几个特有的功能，而这些功能很难通过通用编辑器按原样重现。 |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE 不可用]{type=Negative} |  | [!BADGE 可用]{type=Positive} |  |
| [无头交付](/help/headless/introduction.md) | [!BADGE 部分可用]{type=Caution} | 只能用 [SPA 编辑器](/help/implementing/developing/hybrid/introduction.md)，该编辑器[现已弃用](/help/implementing/developing/hybrid/spa-editor-deprecation.md)，最好改用通用编辑器 | [!BADGE 可用]{type=Positive} | 通用编辑器允许开发人员使用自己的 Web 应用程序，不会施加任何特定的框架要求或实施约束。 |

### 持久性 {#persistence}

|  | 页面编辑器 | 注释 | 通用编辑器 | 注释 |
|---|---|---|---|---|
| 编辑页面组件 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 编辑[内容片段](/help/assets/content-fragments/content-fragments.md) | [!BADGE 不可用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | 包括插入新的和重新排序的片段 |

### 功能 {#capabilities}

|  | 页面编辑器 | 注释 | 通用编辑器 | 注释 |
|---|---|---|---|---|
| 页面模板 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 通用编辑器与所使用的模板系统无关。然而，典型的实施模式倾向于使用开发人员定义的模板，因为现代前端工具使开发人员更容易直接在代码中定义和维护模板逻辑。 |
| 所见即所得编辑 | [!BADGE 可用]{type=Positive} | 仅限页面 | [!BADGE 可用]{type=Positive} | 支持页面和内容片段 |
| [生成变体](/help/generative-ai/generate-variations.md) | [!BADGE 不可用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | [可作为扩展提供](/help/implementing/universal-editor/extending.md) |
| 插入新区块 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 将区块重新排序 | [!BADGE 可用]{type=Positive} | 可以通过在上下文中拖放来实现，但不能在“树形视图”侧边面板中这样操作 | [!BADGE 可用]{type=Positive} | 可以通过在“树形视图”侧边面板中拖放来实现，但在上下文中还不行（已计划） |
| 剪切/复制粘贴区块 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 应用样式 | [!BADGE 可用]{type=Positive} | 可以使用[样式系统](/help/sites-cloud/authoring/page-editor/style-system.md)将样式应用在组件上。 | [!BADGE 可用]{type=Positive} | 可以使用常规组件（或内容片段）属性应用样式。通用编辑器中没有相同的样式选取器，但是通过一个多选小组件可以实现非常相似的用户体验。 |
| 应用布局 | [!BADGE 可用]{type=Positive} | 网站必须实施 [AEM 响应式网格](/help/implementing/developing/introduction/responsive-design.md)，使作者能够跨三个预定义的断点调整组件大小。 | [!BADGE 可用]{type=Positive} | 可以使用常规组件（或内容片段）属性应用布局，但不支持响应式网格。 |
| 撤销-重做 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 发布（也可以发布到预览） | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [开始工作流](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可作为扩展提供 |
| 评论 | [!BADGE 可用]{type=Positive} | 使用[注释](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE 不可用]{type=Negative} | 已计划 |
| Workfront 集成 | [!BADGE 不可用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | 可作为扩展提供 |
| [MSM 和启动项](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可作为扩展提供给页面 |
| 试验和个性化 | [!BADGE 可用]{type=Positive} | 使用[目标模式](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE 可用]{type=Positive} | 可作为扩展提供给 Edge Delivery Services |
| 内容树 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 还允许在树形结构中重新排序 |
| 设备模拟 | [!BADGE 可用]{type=Positive} | [可以模拟已配置的设备，](/help/sites-cloud/administering/responsive-layout.md)但用户无法手动输入任何不同的屏幕尺寸来模拟。 | [!BADGE 可用]{type=Positive} | [可以手动输入任何要模拟的屏幕尺寸，](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)但无法配置默认断点。 |
| [页面锁定](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 遵守 Sites 控制台中设置的锁定状态，通过可用的扩展可以从编辑器锁定/解锁页面 |
| [页面属性](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可从网站管理员处获取，可通过扩展从编辑器访问页面的属性 |
| 多字段属性 | [!BADGE 可用]{type=Positive} |  | [!BADGE 不可用]{type=Negative} | 已计划 |
| [远程 DAM](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [页面版本控制](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [TimeWarp](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp) 和[差异视图](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 不可用]{type=Negative} | 已计划 |
| 在 admin 中查看 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可作为页面扩展提供 |
| 查看页面状态 | [!BADGE 可用]{type=Positive} |  | [!BADGE 不可用]{type=Negative} | 在 Sites 控制台中可用 |
| 可扩展性 | [!BADGE 可用]{type=Positive} | 作为 AEM 叠加 | [!BADGE 可用]{type=Positive} | 作为通过 App Builder 明确定义的扩展点，并且几乎不需要 AEM 特定的知识 |

## 采用通用编辑器 {#adopt-ue}

通用编辑器有许多优势，使其成为新项目的绝佳解决方案。

* **可视化编辑：**&#x200B;与页面编辑器一样，作者可以直接在预览中编辑内容，并立即看到他们的更改如何影响访问者体验。
* **面向未来：** AEM 的路线图优先将通用编辑器作为可视化编辑器。采用这个编辑器可以确保获得最新的创新和增强功能。
* **更简单的集成：**&#x200B;使用通用编辑器不需要 AEM 专用的 SDK，从而减少了技术栈锁定。
* **自带应用程序：**&#x200B;通用编辑器支持任何 Web 框架或架构，无需复杂的重构即可采用。
* **可扩展性：**&#x200B;通用编辑器获益于一个强大的[扩展框架，](/help/implementing/universal-editor/extending.md)包括与生成式 AI、Workfront 等的集成。

### 迁移至通用编辑器 {#migrate-ue}

没有从页面编辑器直接迁移到通用编辑器的路径。这是由于两种技术之间存在根本差异。

* 通用编辑器不重新引入模板编辑器、样式系统或响应式网格等功能。
   * 现在可以使用 Edge Delivery Services 或无头项目中的精益前端 CSS 和 Javascript 更高效地处理这些用例。
* 由于通用编辑器是一种“编辑器即服务”，它不能允许实施者将 CSS 或 JS 注入组件对话框。
   * 这阻止了页面编辑器中自动转换组件对话框的功能。
   * 这涉及到对话框的许多区域，例如自定义小组件、字段验证、显示/隐藏规则和基于模板的自定义。
      * 虽然这些功能仍然可行，但通用编辑器通过配置来解决这些问题，而不是通过对话框中部署的自定义 JavaScript。

虽然通用编辑器在技术上可以支持编辑传统 AEM 项目的页面（例如使用核心组件构建），但这些网站通常依赖于页面编辑器特有的几个功能，例如样式系统、响应式网格、可编辑模板和对话框中的自定义 Javascript。

由于通用编辑器采用了更精简、更现代的方法，不支持这些旧版功能，因此迁移这类网站需要进行大量重构。因此，**只建议要过渡到 Edge Delivery Services 的项目将页面编辑器网站迁移到通用编辑器。**
