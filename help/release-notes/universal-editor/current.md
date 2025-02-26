---
title: 通用编辑器 2025.02.17 发行说明
description: 这些是通用编辑器 2025.02.17 版本的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: c88aa13c6bc75c8f9cd624d00ef768290981c840
workflow-type: ht
source-wordcount: '206'
ht-degree: 100%

---


# 通用编辑器 2025.02.17 发行说明 {#release-notes}

这些是通用编辑器 2025 年 2 月 17 日版本的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **发布到预览** - 使用通用编辑器[发布（或取消发布）内容时](/help/sites-cloud/authoring/universal-editor/publishing.md)，除了发布环境外，您现在还可以选择是否发布到您的[预览环境](/help/sites-cloud/authoring/sites-console/previewing-content.md)
   * 这样就可以在公开发布之前对您的内容进行审核。
* **模型和过滤器可以在组件定义中定义** - 现在，您可以在[组件定义](/help/implementing/universal-editor/component-definition.md#template)中定义组件所使用的模型和过滤器。
   * 这些信息可以在定义中集中维护，无需在插桩中指定。
   * 这样您就能跨容器移动组件。
* **容器的子元素被默认为组件** - 如果将带有 `data-aue-resource`](/help/implementing/universal-editor/attributes-types.md#data-properties) 的[项作为直接子元素放入容器，则该项被视为组件，无需指定 `data-aue-behavior="component"` 即可移动。

## 其他改进 {#other-improvements}

* **AEM 6.5 资产选择器** - 现在，当[使用 AEM 6.5 运行通用编辑器](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)时，6.5 资产选择器可以正常打开。
