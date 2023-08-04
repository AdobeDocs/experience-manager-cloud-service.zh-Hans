---
title: 自定义页面属性视图
description: 了解作者如何查看和编辑页面属性。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---


# 自定义页面属性视图{#customizing-views-of-page-properties}

每个页面都有一组 [属性](/help/sites-cloud/authoring/fundamentals/page-properties.md) 可供用户查看和编辑的区域。 有些是在创建页面（创建视图）时必需的，而另一些则可以在以后的阶段查看和编辑（编辑视图）。 这些页面属性通过对话框(`cq:dialog`)。

每个页面属性的默认状态为：

* 在创建视图中隐藏(例如， **创建页面** 向导)

* 在编辑视图中可用(例如， **查看属性**)

如果需要进行任何更改，则必须专门配置字段。 可使用相应的节点属性完成此操作：

* 创建视图中可用的页面属性(例如， **创建页面** 向导)：

   * 名称: `cq:showOnCreate`
   * 类型: `Boolean`

* 要在编辑视图中可用的页面属性，例如 **视图**/**编辑**  **属性** 选项：

   * 名称: `cq:hideOnEdit`
   * 类型: `Boolean`

>[!TIP]
>
>请参阅 [扩展页面属性教程](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) 有关自定义页面属性的指南。

## 配置页面属性 {#configuring-your-page-properties}

您还可以通过配置页面组件的对话框并应用适当的节点属性来配置可用的字段。

例如，默认情况下， [**创建页面** 向导](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) 显示分组在 **更多标题和描述**. 要隐藏这些内容，请配置：

1. 在下创建页面组件 `/apps`.
1. 创建覆盖(使用 *对话框差异* 由 [Sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md)) `basic` 部分，例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. 设置 `path` 属性 `basic` 指向基本选项卡的覆盖（另请参阅下一步）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 创建覆盖 `basic` - `moretitles` 部分；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 应用相应的节点属性：

   * **名称**: `cq:showOnCreate`
   * **类型**： `Boolean`
   * **值**: `false`

   此 **更多标题和描述** 部分将不再显示在 **创建页面** 向导。

>[!NOTE]
>
>在配置要用于活动副本的页面属性时，请参阅文档 [扩展多站点管理器](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) 以了解更多详细信息。

## 页面属性的配置示例 {#sample-configuration-of-page-properties}

此示例演示了 [Sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md) 包括使用 [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). 它还说明了这两种方法的用法 `cq:showOnCreate` 和 `cq:hideOnEdit`.

您可以在此页面中找到代码： [GitHub。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
