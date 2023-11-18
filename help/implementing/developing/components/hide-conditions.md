---
title: 使用隐藏条件
description: 隐藏条件可用于确定是否呈现组件资源。
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 2%

---

# 使用隐藏条件 {#using-hide-conditions}

隐藏条件可用于确定是否呈现组件资源。 例如，当模板作者配置核心组件时 [列表组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html) 在 [模板编辑器](/help/sites-cloud/authoring/features/templates.md) 并决定禁用基于子页面构建列表的选项。 在“设计”对话框中禁用此选项可设置属性，以便在呈现列表组件时，计算隐藏条件并且不显示显示子页面的选项。

## 概述 {#overview}

对于用户而言，对话框可能会变得非常复杂，因为用户只能使用他们能够使用的选项中的一小部分。 这可能会导致用户获得铺天盖地的用户界面体验。

通过使用隐藏条件，管理员、开发人员和超级用户能够基于一组规则来隐藏资源。 此功能允许他们决定在作者编辑内容时应该显示哪些资源。

>[!NOTE]
>
>基于表达式隐藏资源不会替换ACL权限。 内容保持可编辑状态，但只是不显示。

## 实施和使用详细信息 {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 负责根据资源的存在和价值对资源进行筛选 `granite:hide` 属性，位于要过滤的字段上。 实施 `/libs/cq/gui/components/authoring/dialog/dialog.jsp` 包含实例 `FilteringResourceWrapper.`

实施使用Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) 并添加 `cqDesign` 自定义变量。

以下是位于下的设计节点上的几个隐藏条件示例 `etc/design` 或作为内容策略。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定义隐藏表达式时，请牢记：

* 要使其有效，应表示找到属性的范围(例如， `cqDesign.myProperty`)。
* 值为只读。
* 功能（如有必要）应限于服务提供的一组给定功能。

## 示例 {#example}

隐藏条件的示例可在整个AEM和 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 尤其是这样。 例如，请考虑 [列出核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html) 在中实施 [wknd教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

[使用模板编辑器](/help/sites-cloud/authoring/features/templates.md)中，模板作者可以在“设计”对话框中定义列表组件中哪些选项可供页面作者使用。 可以启用或禁用此类选项，例如是否允许列表为静态列表、子页面的列表、已标记页面的列表等。

如果模板作者选择禁用子页面选项，则会设置设计属性并根据该属性评估隐藏条件，这会导致不为页面作者呈现该选项。

1. 默认情况下，页面作者可以使用列表核心组件，通过选择选项来使用子页面构建列表 **子页面**.

   ![列表组件设置](assets/hide-conditions-list-settings.png)

1. 在列表核心组件的“设计”对话框中，模板作者可以选择选项 **禁用子项** 以防止向页面作者显示基于子页面生成列表的选项。

   ![列表组件设计对话框](assets/hide-conditions-list-design.png)

1. 策略节点创建于 `/conf/wknd/settings/wcm/policies/wknd/components/list` 具有属性 `disableChildren` 设置为 `true`.

   ![隐藏条件的节点结构](assets/hide-conditions-node-structure.png)

1. 隐藏条件定义为 `granite:hide` 对话框属性节点上的属性 `/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`

   ![隐藏条件的评估](assets/hide-conditions-evaluation.png)

1. 的值 `disableChildren` 从设计配置和表达式中提取 `${cqDesign.disableChildren}` 评估为 `false`，这意味着选项将不会作为组件的一部分渲染。

1. 选项 **子页面** 使用列表组件时，不再为页面作者渲染。

   ![已禁用子选项的列表组件](assets/hide-conditions-child-disabled.png)
