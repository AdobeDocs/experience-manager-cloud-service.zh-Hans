---
title: Edge Delivery Services 正在开发中的 Sites 功能
description: 了解哪些 AEM Sites 功能和用例仍在开发中，并在使用 Edge Delivery Services 时探索其他解决方案。
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
source-git-commit: 92da26452438f2b56cdec1aecc76587d4982f00e
workflow-type: ht
source-wordcount: '473'
ht-degree: 100%

---

# Edge Delivery Services 正在开发中的 Sites 功能 {#wip-sites-features}

了解哪些 AEM Sites 功能和用例仍在开发中，并在使用 Edge Delivery Services 时探索其他解决方案。

>[!TIP]
>
>“正在开发中”并不意味着“终点”。如果您需要本文档中列出的正在开发中的功能或用例，请联系您的 Adobe 代表。您可以与 Adobe 携手合作，深入了解您的特定需求，并共同探寻替代解决方案。

## 正在开发的功能 {#wip-features}

当将 Edge Delivery Services 与 AEM Sites 结合使用时，大多数 Sites 功能均可用。例如，[Sites 控制台](/help/sites-cloud/authoring/sites-console/introduction.md)中几乎所有可用的操作都适用于 Edge Delivery Services。

不过，有些功能仍处于开发中 (WIP)。WIP 功能是 Sites 控制台的功能，这些功能要么尚未用于 AEM Sites 的 Edge Delivery Services，要么仅部分可用。因此，WIP 功能的呈现方式可能与 Sites 功能不同，或者相关用例可能有替代解决方案。

以下列表显示了此类 WIP 功能和替代解决方案。如果您的项目需要 WIP 功能，请查看下面建议的替代方案，并联系 Adobe，共同探讨您的用例。

| Sites 功能 | Edge 上的状态 | 注释 | Edge 文件 |
|---|---|---|---|
| [页面继承](/help/sites-cloud/administering/msm-and-translation.md) | 可用 |  | [通用编辑器中的内容继承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [组件继承](/help/sites-cloud/administering/msm-and-translation.md) | 部分可用 | 组件会继承内容，但只能在页面级别还原继承 | [通用编辑器中的内容继承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [语言副本](/help/sites-cloud/administering/translation/overview.md) | 部分可用 | 组件会继承内容，但只能在页面级别还原继承 | [通用编辑器中的内容继承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [多站点管理](/help/sites-cloud/administering/msm/overview.md) | 部分可用 | 组件会继承内容，但只能在页面级别还原继承 | [通用编辑器中的内容继承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [启动项](/help/sites-cloud/authoring/launches/overview.md) | 部分可用 | 组件会继承内容，但只能在页面级别还原继承 | [通用编辑器中的内容继承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [页面模板](/help/sites-cloud/authoring/page-editor/templates.md) | 部分可用 | 从模板创建的页面是原始模板的独立副本。 | [将页面模板与通用编辑器结合使用](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [Context Hub 和目标定位](/help/sites-cloud/authoring/personalization/overview.md) | 不可用 |  |  |
| [时间扭曲](/help/sites-cloud/authoring/launches/preview.md) | 不可用 |  |  |
| [关联的内容](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | 不可用 |  |  |
| [体验片段](/help/sites-cloud/authoring/fragments/experience-fragments.md) | 选择 | 创建页面并使用片段组件 |  |

## 正在开发中的用例 {#wip-use-cases}

由于 Edge Delivery Services 是建立在一个全新的现代技术堆栈上的，因此以下 AEM Sites 的用例尚未完全涵盖，仍在开发中。如果您的项目需要某个 WIP 用例，请联系 Adobe，以便我们共同合作，深入了解您项目的需求。

| Sites 用例 | 详细信息 |
|---|---|
| 用于呈现页面的服务器端逻辑 | 使用 AEM 的运行时作为应用程序服务器 |
| 动态页面 | SSI 或任何动态包含技术 |
| 用户管理 | 使用 AEM 作为 IdP |
| 身份验证 | 使用 AEM 保护内容 |
| 内容权限 | AEM 作为安全的外联网 |
