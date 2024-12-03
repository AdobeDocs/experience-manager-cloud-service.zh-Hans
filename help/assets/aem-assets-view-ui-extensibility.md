---
title: AEM Assets视图UI可扩展性
description: 了解AEM Assets视图的UI可扩展性功能。 AEM Assets视图UI允许添加自定义UI组件以满足特定业务需求。
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: bbb183470e12c0fc81c821fc2e0c1e7d77c33707
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 3%

---

# AEM Assets视图UI可扩展性{#AEM-Assets-View-UI-Extensibility}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

AEM Assets视图具有UI可扩展性功能。 此功能允许用户将自定义UI组件添加到Assets视图UI，以满足AEM Assets视图的现成功能无法满足的特定业务需求。 此可扩展性功能增强了AEM Assets View的灵活性，使组织能够调整界面以满足特定工作流和要求。
您可以将扩展添加到资产、文件夹和收藏集级别。 添加的扩展将显示在“资产”、“收藏集”或“文件夹详细信息”页面的专用面板中。

>[!IMPORTANT]
>
> * AEM Assets视图UI可扩展性在[Assets Ultimate](/help/assets/assets-ultimate-overview.md)中可用。
> * 要访问Assets视图UI可扩展性，请[创建并提交Adobe的客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)。
> * 您可以通过展开“详细反馈”选项并单击“报告问题”来提供文档反馈。

## <a id="1"></a>如何访问Assets视图

通过以下方式访问Assets视图：
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## UI扩展在Assets视图UI上的什么位置显示？ {#ui-extensibility-panel-assets-view}

在Assets视图中，导航到资产、文件夹或收藏集的详细信息页面。 此详细信息页面有一个专用面板，用于显示添加的UI扩展。
![我的工作区](/help/assets/assets/my-workspace-assets-view3.png)


## 添加可扩展性组件的先决条件

* [访问Assets视图](#1)。
* 访问[Adobe应用生成器](https://developer.adobe.com/app-builder/docs/overview/)。
* 拥有组织内系统管理员角色的开发人员。 有关详细信息，请参阅[此](https://developer.adobe.com/uix/docs/guides/get-access/)。
* 必须在本地计算机上安装AdobeIO命令行工具(AIO CLI)。 此工具对于创建和部署扩展项目至关重要。 有关详细信息，请参阅[此](https://developer.adobe.com/app-builder/docs/getting_started/#local-environment-set-up)。
* 很好地了解JavaScript、Node.js和React技术。

## 在Assets视图UI上添加UI可扩展性组件{#Adding-UI-Extensibility-Component-on-Assets-View}

1. 有关UI扩展和AdobeApp Builder框架的基本信息，请参阅[快速入门](https://developer.adobe.com/uix/docs/getting-started/)。 了解UI可扩展性如何支持在Adobe Experience Cloud服务中集成自定义逻辑和UI，并了解用于实施UI扩展的架构和工作流。
1. 有关UI可扩展性的常规信息，包括本地环境设置、本地预览、发布和管理，请参阅[指南](https://developer.adobe.com/uix/docs/guides/)。
1. 请参阅创建扩展中的[常见概念](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/)，了解为AEM Assets视图开发UI扩展所需的基础。
1. 将自定义侧面板添加到Assets视图界面。 主机应用程序(Assets视图)管理这些面板以处理UI交互，例如切换和深层链接。 扩展使用`aem/assets/details/1`扩展点来集成指定属性的自定义面板，如面板ID、标题和内容URL。 开发人员使用`getPanels()`方法注册自定义面板，并构建显示自定义内容的路由。 有关详细实施（包括API引用和代码示例），请参阅[详细信息视图](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/)。
1. 设置您的本地环境，并通过创建您的第一个UI扩展来体验在Assets视图中开发UI扩展的过程。 有关更多详细信息，请参阅[AEM Assets分步查看扩展开发](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/)。
1. 使用AIO CLI设置应用程序以生成基本扩展结构和所需代码。 有关详细信息，请参阅AEM Assets视图](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/)的[代码生成。
1. 在本地测试您的扩展，以确保它们在部署之前可按预期工作。 在完全隔离的环境中或以部分隔离的方式运行扩展，然后将扩展连接到生产AEM Assets视图进行测试。 有关详细信息，请参阅[疑难解答 — AEM Assets视图可扩展性](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/)。
