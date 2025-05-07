---
title: 扩展通用编辑器
description: 了解用于扩展Universal Editor功能以支持内容作者需求的不同选项。
feature: Developing
role: Admin, Architect, Developer
exl-id: 2f487fa5-57a7-477a-ad68-590e6cc12f4e
source-git-commit: 36a27d7fb36c9832b78c13d7544a43df2cbd0fa0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# 扩展通用编辑器 {#extending}

了解用于扩展Universal Editor功能以支持内容作者需求的不同选项。

>[!TIP]
>
>通用编辑器还提供多个[自定义选项，](/help/implementing/universal-editor/customizing.md)允许您更好地满足项目需求。

## 扩展名 {#extensions}

作为Adobe Experience Cloud服务，可以使用App Builder和Experience Manager扩展通用编辑器的UI。 Adobe提供了许多可用于项目的现成扩展。

* **[AEM多站点管理(MSM)扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)**：在组件级别中断或恢复继承
* **[AEM页面属性扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties)**：在通用编辑器中访问该页面的页面属性窗口
* **[AEM站点管理扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#sites-console)**：打开站点控制台，以在通用编辑器中访问页面的位置
* **[AEM页面锁定扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#locking-pages)**：从通用编辑器查看和更改页面锁定状态
* **[AEM Workflows扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#workflows)**：从通用编辑器启动页面工作流和页面内容
* **[AEM Universal Editor开发登录扩展](/help/sites-cloud/authoring/universal-editor/authoring.md#developer-login)**：在本地开发时轻松验证本地AEM SDK
* **[生成变体](/help/generative-ai/generate-variations-integrated-editor.md)**：使用生成人工智能(AI)直接在属性面板中为您的内容创建变体。
* **[通用编辑器的AEM产品选取器](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**：通过选择编辑器中的产品数据或删除产品数据来集成Adobe Commerce数据。
* **[通用编辑器内容草稿](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**：创建、编辑和管理多个内容草稿。
* **[可配置的资产选取器](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**：启用从已编辑页面使用的存储库以外的存储库中选择资产。
* **Forms规则编辑器**：将动态行为以可视方式添加到AEM Forms字段，而无需编码。
* **[将内容片段导出到Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**：将在Adobe Experience Manager as a Cloud Service中创建的内容片段导出到Adobe Target，以在Target活动中用作选件，从而测试和大规模个性化体验。
* **[内容片段工作流](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**：为选定的内容片段启动AEM工作流。

## 扩展UI {#extending-ui}

通用编辑器的UI扩展是使用Adobe App Builder构建的JavaScript应用程序。 使用这些相同的工具，您还可以将自己的按钮和操作添加到标题菜单和属性面板，并为通用编辑器创建自己的事件。

如果您想探索创建您自己的扩展的可能性，请参阅以下资源：

1. [UI可扩展性](https://developer.adobe.com/uix/docs/) — 这是UI扩展的开发人员文档。
1. [UI扩展性指南](https://developer.adobe.com/uix/docs/guides/) — 有关如何开发您自己的扩展的分步说明
1. [通用编辑器UI扩展点](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) — 特定于通用编辑器的扩展点文档

>[!TIP]
>
>如果您希望通过示例学习，请参阅[AEM UI可扩展性教程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview)。 虽然它侧重于扩展内容片段控制台，但在通用编辑器中实施UI扩展的概念是相同的。

[在AEM Sites中使用Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/)，您可以为每个实例启用或禁用扩展，访问Adobe的第一方扩展（包括通用编辑器的第一方扩展）等等。

## 扩展点 {#extension-points}

除了UI可扩展性之外，通用编辑器还提供了许多其他灵活的扩展点，以实现自定义业务要求的无缝集成。

* **[块](/help/edge/developer/block-collection.md)**：在简单的JSON格式中，项目可以调整可用于内容创建的块和UE功能。
* **[自定义用户界面](#extending-ui)**：扩展可以在侧面板或模式对话框中显示必要的UI。
* **[事件](/help/implementing/universal-editor/events.md)**：扩展将接收有关作者在页面上的操作和选择的事件，以便做出适当响应。
