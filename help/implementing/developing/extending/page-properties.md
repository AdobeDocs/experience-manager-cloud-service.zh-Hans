---
title: 自定义页面属性的视图
description: 了解作者如何查看和编辑页面属性。
exl-id: 363b3c2d-f965-485f-bdae-2ea5b4cecb83
source-git-commit: d2352e66b380f5a3654e2fc99ce4204b32066683
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 92%

---

# 自定义页面属性的视图{#customizing-views-of-page-properties}

每个页面都有一组用户可以查看和编辑的[属性](/help/sites-cloud/authoring/sites-console/page-properties.md)。有些是在创建页面时需要的（创建视图），其他的可以在稍后阶段查看和编辑（编辑视图）。这些页面属性由相应页面组件的对话框 (`cq:dialog`) 定义并提供。

每个页面属性的默认状态是：

* 在创建视图中隐藏（例如，**创建页面**&#x200B;向导）

* 在编辑视图中可用（例如，**查看属性**）

如果需要任何更改，则必须专门配置字段。这是使用相应的节点属性完成的：

* 页面属性在创建视图中可用（例如，**创建页面**&#x200B;向导）：

   * 名称：`cq:showOnCreate`
   * 类型：`Boolean`

* 页面属性在编辑视图中可用，例如&#x200B;**查看**/**编辑****特性**&#x200B;选项：

   * 名称：`cq:hideOnEdit`
   * 类型：`Boolean`

>[!TIP]
>
>请参阅[扩展页面属性教程](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=zh-Hans)，查看有关自定义页面属性的指南。

## 配置页面属性 {#configuring-your-page-properties}

您还可以通过配置页面组件的对话框并应用相应的节点属性来配置可用字段。

例如，默认情况下&#x200B;[**创建页面**&#x200B;向导](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page)会显示在&#x200B;**更多标题和描述**&#x200B;中分组的字段。若要对其进行隐藏，您可以配置：

1. 在 `/apps` 下创建您的页面组件。
1. 为页面组件的 `basic` 部分创建一个覆盖（使用[ Sling 资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md)提供的&#x200B;*对话框差异*）；例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. 将 `basic` 上的 `path` 属性设置为指向基本选项卡的覆盖（另请参阅下一步）。例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 在相应路径上创建 `basic`-`moretitles` 部分的覆盖；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 应用适当的节点属性：

   * **名称**：`cq:showOnCreate`
   * **类型**：`Boolean`
   * **值**：`false`

   **更多标题和描述**&#x200B;部分不会再在&#x200B;**创建页面**&#x200B;向导中显示。

>[!NOTE]
>
>在配置要用于活动副本的页面属性时，请参阅 [扩展多站点管理器](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) 以了解更多详细信息。

## 页面属性的示例配置 {#sample-configuration-of-page-properties}

该示例演示了[ Sling 资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md)的对话框差异技术，其中包括使用 [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties)。它还说明了 `cq:showOnCreate` 和 `cq:hideOnEdit` 的用法。

您可以在此页面中找到代码： [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog).
