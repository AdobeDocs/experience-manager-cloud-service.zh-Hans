---
title: Edge Delivery Services的进行中网站功能
description: 了解哪些AEM Sites功能和用例正在使用，并在使用Edge Delivery Services时发现替代解决方案。
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
source-git-commit: dbe4cd619f4dc680e6fc4826f6a4fea92bab9707
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# Edge Delivery Services的进行中网站功能 {#wip-sites-features}

了解哪些AEM Sites功能和用例正在使用，并在使用Edge Delivery Services时发现替代解决方案。

>[!TIP]
>
>在建工程并不意味着道路的尽头。 如果您需要本文档中列出的功能或用例正在使用，请联系您的Adobe代表。 您和Adobe可以一起工作，了解您的特定需求并找到替代解决方案。

## 工作进行中的功能 {#wip-features}

在将Edge Delivery Services与AEM Sites结合使用时，大多数Sites功能都可用。 例如，[站点控制台](/help/sites-cloud/authoring/sites-console/introduction.md)中几乎任何可用的操作都适用于Edge Delivery Services。

但是，某些功能是work-in-progress (WIP)。 WIP功能是站点控制台的功能，这些功能既不适用于具有AEM Sites的Edge Delivery Services，也仅部分可用。 因此，WIP功能的呈现方式可能不同于其Sites对应功能，或者对于使用案例可能有替代解决方案。

下表显示了此类WIP功能和替代解决方案。 如果您的项目需要WIP功能，请查看下面建议的替代方案，并联系Adobe以一起了解您的用例。

| 站点功能 | Edge状态 | 注释 | Edge文档 |
|---|---|---|---|
| [页面继承](/help/sites-cloud/administering/msm-and-translation.md) | 可用 |  | 通用编辑器中的[内容继承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [组件继承](/help/sites-cloud/administering/msm-and-translation.md) | 部分可用 | 组件继承内容，但继承只能在页面级别还原 | 通用编辑器中的[内容继承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [语言副本](/help/sites-cloud/administering/translation/overview.md) | 部分可用 | 组件继承内容，但继承只能在页面级别还原 | 通用编辑器中的[内容继承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [多站点管理](/help/sites-cloud/administering/msm/overview.md) | 部分可用 | 组件继承内容，但继承只能在页面级别还原 | 通用编辑器中的[内容继承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [启动项](/help/sites-cloud/authoring/launches/overview.md) | 部分可用 | 组件继承内容，但继承只能在页面级别还原 | 通用编辑器中的[内容继承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [页面模板](/help/sites-cloud/authoring/page-editor/templates.md) | 即将推出！ | 从模板创建的页面是原始模板的独立副本。 | [将页面模板与通用编辑器一起使用](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [上下文中心和定位](/help/sites-cloud/authoring/personalization/overview.md) | 不可用 |  |  |
| [时间扭曲](/help/sites-cloud/authoring/launches/preview.md) | 不可用 |  |  |
| [关联的内容](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | 不可用 |  |  |
| [体验片段](/help/sites-cloud/authoring/fragments/experience-fragments.md) | 替代 | 创建页面并使用片段组件 |  |

## 工作进行中的用例 {#wip-use-cases}

由于Edge Delivery Services构建在全新的现代技术栈栈上，因此AEM Sites的以下用例尚未完全涵盖并在进行中。 如果您的项目需要WIP用例，请联系Adobe以一起工作并了解项目的需求。

| 站点用例 | 详细信息 |
|---|---|
| 用于呈现页面的服务器端逻辑 | 将AEM运行时用作应用程序服务器 |
| 动态页面 | SSI或任何动态include技术 |
| 用户管理 | 将AEM用作IdP |
| 身份验证 | 将AEM用于安全内容 |
| 内容权限 | AEM作为安全外联网 |
