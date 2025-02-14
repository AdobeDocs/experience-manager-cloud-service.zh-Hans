---
title: 支持的客户端平台
description: 了解哪些浏览器支持使用Adobe Experience Manager as a Cloud Service创作内容以及访问使用AEM发布的站点。
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 22d4e6b5f87221b2739cf1dd9d59b4652a014316
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---


# 支持的客户端平台 {#supported-platforms}

了解哪些浏览器支持使用Adobe Experience Manager as a Cloud Service创作内容以及访问使用AEM发布的站点。

>[!TIP]
>
>本文档介绍AEM as a Cloud Service支持的客户端平台。 有关用于开发AEM项目的生成环境的详细信息，请参阅文档[生成环境。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)

## 支持级别 {#support-levels}

Adobe定义了对AEM客户端平台的以下支持级别。

| 支持级别 | 描述 |
|---|---|
| 答：支持 | Adobe为此配置提供全面支持和维护。 Adobe的质量保证流程涵盖此配置。 |
| R：有限的支持 | 支持需要向Adobe发出正式请求，才能在项目中使用配置。 获得Adobe确认后，Adobe将在受限支持项目中提供全面支持。 有关更多信息，请联系Adobe客户关怀部门。 |
| Z：不支持 | 不支持该配置。 Adobe不声明配置是否有效，也不支持该配置。 |

## 受支持的内容创作浏览器 {#authoring}

AEM用户界面已针对笔记本、台式计算机和平板电脑设备(如Apple iPad或Microsoft Surface)中的较大屏幕进行了优化。 任何创作用例均不支持电话外形。

根据[创作方法，Adobe Experience Manager用户界面可与以下客户端平台配合使用。](/help/edge/authoring-methods.md)

* [通用编辑器](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)
* 使用[Sidekick](/help/edge/docs/sidekick.md)的[基于文档的创作](/help/edge/docs/authoring.md)

所有浏览器都使用默认插件和加载项集进行测试。

| 浏览器 | 通用编辑器支持级别 | 页面编辑器支持级别 | Sidekick支持级别 |
|---|---|---|---|
| Google Chrome（常绿市） | 答：支持 | 答：支持 | 答：支持 |
| Microsoft Edge（常绿市） | 答：支持 | 答：支持 | Z：不支持 |
| Mozilla Firefox （常绿） | 答：支持 | 答：支持 | Z：不支持 |
| Mozilla Firefox最新的ESR [1] | 答：支持 | 答：支持 | Z：不支持 |
| macOS上的Safari （常青） | 答：支持 | 答：支持 | Z：不支持 |
| iOS上的Safari （常青） [2] | Z：不支持 | 答：支持 | Z：不支持 |

1. Firefox的扩展支持版本（[了解有关mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/)的更多信息）
1. 仅支持Apple iPad

>[!NOTE]
>
>**对具有快速发布周期的浏览器的支持：**
>
>Firefox、Chrome和Edge会定期发布更新。 Adobe致力于为这些浏览器即将发布的版本保持如上列出的支持级别。

## 支持的网站浏览器 {#websites}

浏览器对AEM渲染的网站的支持取决于AEM页面模板、块、设计和组件输出的实施。 因此，实施项目的开发人员最终将控制您网站的兼容性。

AEM [项目样板、](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md#create-github-project) [核心组件、](/help/implementing/developing/components/overview.md#aem-core-components)和[WKND示例站点](/help/implementing/developing/introduction/develop-wknd-tutorial.md)都与所有新式浏览器兼容。
