---
title: 使用隐藏条件
description: 隐藏条件可用于确定是否渲染组件资源。
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
translation-type: tm+mt
source-git-commit: fa3280defb2a97954c5ab1b70e7600382e370606
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 4%

---

# 使用隐藏条件{#using-hide-conditions}

隐藏条件可用于确定是否渲染组件资源。 例如，当模板作者在[模板编辑器](/help/sites-cloud/authoring/features/templates.md)中配置核心组件[列表组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/list.html)并决定禁用选项以基于子页面构建列表时，就会出现这种情况。 在设计对话框中禁用此选项会设置一个属性，以便在渲染列表组件时，将评估隐藏条件，而不显示显示子页面的选项。

## 概述 {#overview}

对话框可能会变得非常复杂，用户可能只使用一小部分可供使用的选项。 这会为用户带来压倒性的用户界面体验。

通过使用隐藏条件，管理员、开发人员和超级用户可以根据一组规则隐藏资源。 此功能允许他们决定在作者编辑内容时应显示哪些资源。

>[!NOTE]
>
>根据表达式隐藏资源不会替换ACL权限。 内容仍然可编辑，但不显示。

## 实施和使用详细信息{#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 负责根据要筛选的字段上属性的存在 `granite:hide` 和值来筛选资源。`/libs/cq/gui/components/authoring/dialog/dialog.jsp`的实现包括`FilteringResourceWrapper.`的实例

该实现利用Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html)并通过ExpressionCustomizer添加`cqDesign`自定义变量。

以下是设计节点上隐藏条件的几个示例，该节点位于`etc/design`下或作为内容策略。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定义隐藏表达式时请牢记：

* 要有效，应表示找到属性的范围(例如，`cqDesign.myProperty`)。
* 值为只读。
* 职能（如果需要）应限于服务提供的给定集。

## 示例 {#example}

隐藏条件的示例可在AEM中找到，特别是[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。 例如，考虑[WKND教程中实现的[列表核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/list.html)。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

[使用模板编辑器](/help/sites-cloud/authoring/features/templates.md)，模板作者可以在设计对话框中定义页面作者可以使用的列表组件选项。诸如是否允许列表为静态列表、子页面列表、标记页面列表等选项。 可以启用或禁用。

如果模板作者选择禁用子页面选项，则会设置设计属性并针对该属性评估隐藏条件，这会导致选项不为页面作者呈现。

1. 默认情况下，页面作者可以通过选择选项&#x200B;**子页面**&#x200B;来使用子页面使用列表核心组件构建列表。

   ![列表组件设置](assets/hide-conditions-list-settings.png)

1. 在列表核心组件的设计对话框中，模板作者可以选择选项&#x200B;**禁用子项**，以阻止将基于子页面生成列表的选项显示给页面作者。

   ![列表组件设计对话框](assets/hide-conditions-list-design.png)

1. 在`/conf/wknd/settings/wcm/policies/wknd/components/list`下创建策略节点，其属性`disableChildren`设置为`true`。

   ![隐藏条件的节点结构](assets/hide-conditions-node-structure.png)

1. 隐藏条件定义为对话框属性节点`/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`上`granite:hide`属性的值

   ![隐藏条件的评估](assets/hide-conditions-evaluation.png)

1. `disableChildren`的值从设计配置中提取，表达式`${cqDesign.disableChildren}`的计算结果为`false`，这意味着选项不会作为组件的一部分呈现。

1. 使用列表组件时，不再为页面作者呈现选项&#x200B;**子页面**。

   ![列表组件（已禁用子选项）](assets/hide-conditions-child-disabled.png)
