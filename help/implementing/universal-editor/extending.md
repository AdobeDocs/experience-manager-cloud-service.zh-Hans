---
title: 扩展通用编辑器
description: 了解用于扩展通用编辑器功能的不同选项，以满足内容作者需求。
feature: Developing
role: Admin, Developer
exl-id: 2f487fa5-57a7-477a-ad68-590e6cc12f4e
source-git-commit: d938abce2b46786343b19113454da1738a824ed0
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 100%

---

# 扩展通用编辑器 {#extending}

了解用于扩展通用编辑器功能的不同选项，以满足内容作者需求。

>[!TIP]
>
>通用编辑器还提供多种[自定义选项](/help/implementing/universal-editor/customizing.md)，让您能更好地满足项目需求。

## 扩展 {#extensions}

作为 Adobe Experience Cloud 服务，通用编辑器的 UI 可以使用 App Builder 和 Experience Manager 进行扩展。Adobe 通过[扩展管理器](https://experience.adobe.com/aem/extension-manager)提供许多现成的扩展，您可以为您的项目使用它们。

* **[AEM 多网站管理 (MSM) 扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)**：在组件级别中断或恢复继承
* **[AEM 页面属性扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties)**：访问通用编辑器中页面的页面属性窗口
* **[AEM 网站管理扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#sites-console)**：打开 Sites 控制台，前往通用编辑器中页面的位置
* **[AEM 页面锁定扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#locking-pages)**：从通用编辑器查看和更改页面锁定状态
* **[AEM 工作流扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#workflows)**：从通用编辑器启动页面和页面内容上的工作流
* **[生成变体](/help/generative-ai/generate-variations-integrated-editor.md)**：使用生成式人工智能 (AI) 直接在属性面板中为您的内容创建变体。
* **[通用编辑器的 AEM 产品选取器](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**：通过从编辑器中选择或移除产品数据集成 Adobe Commerce 数据。
* **[通用编辑器内容草稿](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**：创建、编辑和管理内容的多个草稿。
* **[可配置的资产选取器](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**：可以从被编辑页面使用的存储库以外的存储库中选择资产。
* **表单规则编辑器**：直观地为 AEM Forms 字段添加动态行为，无需编码。
* **[将内容片段导出到 Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**：将在 Adobe Experience Manager as a Cloud Service 中创建的内容片段导出到 Adobe Target，将其用作 Target 活动中的产品建议，用于大规模的测试和个性化体验。
* **[内容片段工作流](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**：为选定的内容片段启动 AEM 工作流。

有关如何启用这些扩展的信息，[请参阅扩展管理器文档。](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)

## 扩展 UI {#extending-ui}

通用编辑器的 UI 扩展是使用 Adobe App Builder 构建的 JavaScript 应用程序。使用这些相同的工具，您还可以在标题菜单和属性面板中添加自己的按钮和操作，还可以为通用编辑器创建自己的事件。

如果您想了解有哪些方法可以创建自己的扩展，请参阅以下资源：

1. [UI 可扩展性](https://developer.adobe.com/uix/docs/) - 这是 UI 扩展的开发人员文档。
1. [UI 扩展指南](https://developer.adobe.com/uix/docs/guides/) - 关于如何开发您自己的扩展的分步说明
1. [通用编辑器 UI 扩展点](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - 关于通用编辑器特有扩展点的文档

>[!TIP]
>
>如果您更希望通过示例学习，请参阅 [AEM UI 可扩展性教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview)。虽然它的重点是扩展内容片段控制台，但实施通用编辑器中 UI 扩展的概念是相同的。

[使用 AEM Sites 中的扩展管理器](https://developer.adobe.com/uix/docs/extension-manager/)，您可以根据每个实例的情况启用或禁用扩展、访问 Adobe 的第一方扩展等，包括通用编辑器的扩展。

## 扩展点 {#extension-points}

除了 UI 可扩展性之外，通用编辑器还提供许多其他灵活的扩展点，以实现自定义业务需求的无缝集成。

* **[区块](https://www.aem.live/developer/block-collection)**：采用简单的 JSON 格式，项目可以调整可用于内容创建的区块和 UE 功能。
* **[自定义用户界面](#extending-ui)**：扩展可以在侧边面板或模态对话框中显示必要的 UI。
* **[事件](/help/implementing/universal-editor/events.md)**：扩展可以接收关于作者在页面上的操作和选择的事件，以做出适当的响应。
