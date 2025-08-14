---
title: 支持的客户端平台
description: 了解哪些浏览器受到支持，可使用 Adobe Experience Manager as a Cloud Service 创作内容以及访问用 AEM 发布的 Sites。
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 7ddd0a75-621a-4499-91d1-7b3408a68269
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 99%

---

# 支持的客户端平台 {#supported-platforms}

了解哪些浏览器受到支持，可使用 Adobe Experience Manager as a Cloud Service 创作内容以及访问用 AEM 发布的 Sites。

>[!TIP]
>
>此文档涵盖 AEM as a Cloud Service 支持的客户端平台。有关用于 AEM 项目开发的构建环境的详细信息，请参阅文档[构建环境。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)

## 支持级别 {#support-levels}

Adobe 为 AEM 的客户端平台定义了以下支持级别。

| 支持级别 | 描述 |
|---|---|
| A：受到支持 | Adobe 为此配置提供全面的支持和维护。此配置包含在 Adobe 质量保证流程中。 |
| R：有限的支持 | 需要向 Adobe 提出正式的支持请求才能在项目中使用此配置。获得 Adobe 确认后，Adobe 将在有限支持计划范围内提供全面支持。有关详细信息，请联系 Adobe 客户关怀团队。 |
| Z：不受支持 | 此配置不受支持。Adobe 未做出此配置是否有效的声明，也不支持此配置。 |

## 可用于内容创作的受支持浏览器 {#authoring}

AEM 用户界面针对笔记本电脑、台式电脑和平板电脑设备（例如 Apple iPad 或 Microsoft Surface）中的较大屏幕进行了优化。任何创作用例都不支持手机外形规格。

Adobe Experience Manager 用户界面可在以下客户端平台上使用，具体取决于[创作方法。](/help/edge/overview.md#authoring-method)

* [通用编辑器](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)
* [基于文档的创作](https://www.aem.live/docs/aem-authoring)使用 [Sidekick](https://www.aem.live/docs/sidekick)

所有浏览器都用默认的插件和附加功能进行了测试。

| 浏览器 | 通用编辑器支持级别 | 页面编辑器支持级别 | Sidekick 支持级别 |
|---|---|---|---|
| Google Chrome（常青内容） | A：受到支持 | A：受到支持 | A：受到支持 |
| Microsoft Edge（常青内容） | A：受到支持 | A：受到支持 | Z：不受支持 |
| Mozilla Firefox（常青内容） | A：受到支持 | A：受到支持 | Z：不受支持 |
| Mozilla Firefox 最新 ESR [1] | A：受到支持 | A：受到支持 | Z：不受支持 |
| macOS 上的 Safari（常青内容） | A：受到支持 | A：受到支持 | Z：不受支持 |
| iPadOS 上的 Safari（常青内容） | Z：不受支持 | A：受到支持 | Z：不受支持 |

1. Firefox 的扩展支持版本（[访问 mozilla.org 了解更多信息](https://www.mozilla.org/en-US/firefox/enterprise/)）

>[!NOTE]
>
>**支持发布周期较快的浏览器：**
>
>Firefox、Chrome 和 Edge 定期发布更新。Adobe 致力于对这些浏览器即将推出的版本保持上述支持级别。

## 可用于网站的受支持的浏览器 {#websites}

浏览器对 AEM 渲染的网站的支持取决于 AEM 页面模板、块、设计和组件输出的实施。因此，实施网站项目的开发人员最终可以控制网站的兼容性。

AEM [项目样板代码、](https://www.aem.live/developer/ue-tutorial#create-github-project)[核心组件](/help/implementing/developing/components/overview.md#aem-core-components)和 [WKND 示例网站](/help/implementing/developing/introduction/develop-wknd-tutorial.md)全都与所有现代浏览器兼容。
