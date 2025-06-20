---
title: 页面编辑器和通用编辑器
description: 页面编辑器仍受Adobe支持，但通用编辑器为您的新项目带来了令人振奋的可能性。
feature: Developing
role: Admin, Architect, Developer
exl-id: 0a13fb52-623e-4aff-b254-186d8d117e4d
source-git-commit: 3238b11cdd891cf18048199d4103397e3af75edf
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 3%

---

# 页面编辑器和通用编辑器 {#page-editor-universal-editor}

页面编辑器仍受Adobe支持，但通用编辑器为您的新项目带来了令人振奋的可能性。

## 背景 {#background}

Adobe在2024年将[Universal Editor](/help/implementing/universal-editor/introduction.md)作为简化的编辑器引入，采用基于Javascript的现代开发方法。 Universal Editor是Adobe的愿景，即提供无缝且可扩展的视觉内容创作体验。

Adobe认识到[页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)具有丰富的功能集，并且在AEM的悠久历史中投入了大量资金，因此将继续完全支持页面编辑器，但创新将主要针对通用编辑器。

## 推荐 {#recommendation}

虽然快速缩小，但通用编辑器和页面编辑器之间仍存在功能间隙（[可在下一节](#feature-comparison)中找到功能比较）。

根据经验：

* **新项目**&#x200B;应默认使用通用编辑器。
* **现有项目**&#x200B;在启动Edge Delivery或Headless操作时，应继续使用页面编辑器并考虑使用通用编辑器。

**您选择的编辑器应完全由单个项目的需求驱动。**

## 功能比较 {#feature-comparison}

由于两个编辑器之间的功能差距不断缩小，请务必查阅Universal Editor [的发行说明](/help/release-notes/universal-editor/current.md)以了解最新动态。

### 交付 {#delivery}

|  | 页面编辑器 | 注释 | 通用编辑器 | 注释 |
|---|---|---|---|---|
| [发布投放](/help/sites-cloud/authoring/author-publish.md) | [!BADGE 可用]{type=Positive} | 建议与核心组件和传统AEM项目一起使用 | [!BADGE 不可用]{type=Negative} | 传统的AEM页面通常依赖于多个特定于页面编辑器的功能，这些功能在使用通用编辑器时很难按原样复制。 |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE 不可用]{type=Negative} |  | [!BADGE 可用]{type=Positive} |  |
| [Headless投放](/help/headless/introduction.md) | [!BADGE 部分可用]{type=Caution} | 仅对于[SPA编辑器](/help/implementing/developing/hybrid/introduction.md) [已弃用](/help/implementing/developing/hybrid/spa-editor-deprecation.md)而支持通用编辑器 | [!BADGE 可用]{type=Positive} | 通用编辑器允许开发人员自带Web应用程序，而无需强制实施任何特定的框架要求或实施限制。 |

### 持久性 {#persistence}

|  | 页面编辑器 | 注释 | 通用编辑器 | 注释 |
|---|---|---|---|---|
| 编辑页面组件 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 编辑[内容片段](/help/assets/content-fragments/content-fragments.md) | [!BADGE 不可用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | 包括插入新片段和重新排序片段 |

### 功能 {#capabilities}

|  | 页面编辑器 | 注释 | 通用编辑器 | 注释 |
|---|---|---|---|---|
| 页面模板 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 通用编辑器与所使用的模板系统无关。 但是，典型的实施模式倾向于开发人员定义的模板，因为现代前端工具使得开发人员更容易直接在代码中定义和维护模板逻辑。 |
| WYSIWYG编辑 | [!BADGE 可用]{type=Positive} | 仅限于页面 | [!BADGE 可用]{type=Positive} | 支持页面和内容片段 |
| [生成变体](/help/generative-ai/generate-variations.md) | [!BADGE 不可用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | [可用作扩展](/help/implementing/universal-editor/extending.md) |
| 插入新块 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| 对块重新排序 | [!BADGE 可用]{type=Positive} | 上下文中拖放时可能使用，但在“树视图”侧面板中无法使用 | [!BADGE 可用]{type=Positive} | 可以通过“树视图”侧面板中的拖放操作实现，但尚无法实现上下文（已计划） |
| 剪切/复制 — 粘贴块 | [!BADGE 可用]{type=Positive} |  | [!BADGE 不可用]{type=Negative} | 已计划 |
| 应用样式 | [!BADGE 可用]{type=Positive} | 可以使用[样式系统](/help/sites-cloud/authoring/page-editor/style-system.md)将样式应用于组件。 | [!BADGE 可用]{type=Positive} | 可以使用常规组件（或内容片段）属性应用样式。 通用编辑器中没有相同的样式选取器，但是使用多选小组件可以实现非常类似的UX。 |
| 应用布局 | [!BADGE 可用]{type=Positive} | 网站必须实施[AEM响应式网格](/help/implementing/developing/introduction/responsive-design.md)，以使作者能够在三个预定义断点之间调整组件大小。 | [!BADGE 可用]{type=Positive} | 可以使用常规组件（或内容片段）属性应用布局，但不支持响应式网格。 |
| 撤消重做 | [!BADGE 可用]{type=Positive} |  | [!BADGE 不可用]{type=Negative} | 已计划 |
| 发布（也用于预览） | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [开始工作流](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 作为扩展提供 |
| 注释 | [!BADGE 可用]{type=Positive} | 使用[注释](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE 不可用]{type=Negative} | 已计划 |
| Workfront 集成 | [!BADGE 不可用]{type=Negative} |  | [!BADGE 可用]{type=Positive} | 作为扩展提供 |
| [MSM和启动项](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可用于作为扩展的页面 |
| 试验性和个性化 | [!BADGE 可用]{type=Positive} | 使用[目标模式](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE 可用]{type=Positive} | 作为Edge Delivery Services的扩展提供 |
| 内容树 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 还允许在树中重新排序 |
| 设备模拟 | [!BADGE 可用]{type=Positive} | [可以模拟已配置的设备，](/help/sites-cloud/administering/responsive-layout.md)，但用户无法手动输入要模拟的任何不同的屏幕尺寸。 | [!BADGE 可用]{type=Positive} | [可以手动输入要模拟的任何屏幕维度，](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)，但无法配置默认断点。 |
| [页面锁定](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 尊重站点控制台中设置的锁定状态，该控制台中的扩展可用于从编辑器锁定/解锁页面 |
| [页面属性](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可从站点管理员获得，其扩展还可通过编辑器访问页面的属性 |
| 多字段属性 | [!BADGE 可用]{type=Positive} |  | [!BADGE 不可用]{type=Negative} | 已计划 |
| [远程DAM](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [页面版本控制](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} |  |
| [时间扭曲](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp)和[差异视图](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE 可用]{type=Positive} |  | [!BADGE 不可用]{type=Negative} | 已计划 |
| 以管理员身份查看 | [!BADGE 可用]{type=Positive} |  | [!BADGE 可用]{type=Positive} | 可用作页面的扩展 |
| 查看页面状态 | [!BADGE 可用]{type=Positive} |  | [!BADGE 不可用]{type=Negative} | 在站点控制台中可用 |
| 可扩展性 | [!BADGE 可用]{type=Positive} | 作为AEM叠加图 | [!BADGE 可用]{type=Positive} | 使用App Builder明确定义的扩展点，并且几乎没有特定于AEM的知识 |

## 采用通用编辑器 {#adopt-ue}

通用编辑器提供了许多优势，使其成为新项目的绝佳解决方案。

* **可视化编辑：**&#x200B;与页面编辑器类似，作者可以直接在预览中编辑内容，并立即查看其更改如何影响访客体验。
* **面向未来：** AEM的路线图将通用编辑器优先设置为可视编辑器。 采用它可确保访问最新的创新和增强功能。
* **更简单的集成：**&#x200B;无需特定于AEM的SDK即可使用通用编辑器，从而减少技术栈栈锁定。
* **自带应用程序：**&#x200B;通用编辑器支持任何Web框架或架构，允许采用而不需要复杂的重构。
* **可扩展性：**&#x200B;通用编辑器受益于强大的[扩展框架，](/help/implementing/universal-editor/extending.md)，包括与GenAI、Workfront等的集成。

### 迁移到通用编辑器 {#migrate-ue}

没有从页面编辑器直接迁移到通用编辑器的路径。 这是由于这两种技术存在根本性差异。

* 通用编辑器不会重新引入模板编辑器、样式系统或响应式网格等功能。
   * 在Edge Delivery Services或Headless项目中，现在可以使用精简前端CSS和Javascript更高效地处理这些用例。
* 由于通用编辑器是editor-as-a-service，因此它不允许实施者将CSS或JS插入到组件对话框中。
   * 这样可防止从页面编辑器自动转换组件对话框。
   * 这会影响对话框的许多区域，例如自定义构件、字段验证、显示/隐藏规则和基于模板的自定义项。
      * 虽然这些功能仍然可用，但通用编辑器通过配置解决它们，而不是在对话框中部署的自定义JavaScript。

虽然通用编辑器在技术上可以为传统的AEM项目（例如，使用核心组件构建的）启用编辑页面，但这些网站通常依赖于多个页面编辑器特定的功能，例如样式系统、响应式网格、可编辑模板和对话框中的自定义Javascript。

由于通用编辑器遵循一种更精简的现代方法，该方法不支持这些旧功能，因此迁移此类站点将需要大量重构。 因此，仅建议在迁移到Edge Delivery Services的项目中&#x200B;**将页面编辑器站点迁移到通用编辑器。**
