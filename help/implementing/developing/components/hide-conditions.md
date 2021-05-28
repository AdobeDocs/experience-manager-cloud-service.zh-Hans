---
title: 使用隐藏条件
description: 隐藏条件可用于确定是否渲染组件资源。
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 1%

---

# 使用隐藏条件{#using-hide-conditions}

隐藏条件可用于确定是否渲染组件资源。 例如，当模板作者在[模板编辑器](/help/sites-cloud/authoring/features/templates.md)中配置核心组件[列表组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html)并决定禁用选项以基于子页面构建列表时，就会出现这种情况。 在设计对话框中禁用此选项会设置一个属性，以便在呈现列表组件时，将评估隐藏条件，并且不显示显示子页面的选项。

## 概述 {#overview}

对话框可能会变得非常复杂，用户可能只使用一小部分可供使用的选项。 这可能会为用户带来压倒性的用户界面体验。

通过使用隐藏条件，管理员、开发人员和超级用户可以根据一组规则来隐藏资源。 此功能允许他们决定在作者编辑内容时应显示哪些资源。

>[!NOTE]
>
>根据表达式隐藏资源不会替换ACL权限。 内容仍然可编辑，但根本不显示。

## 实施和使用详细信息{#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 负责根据要筛选的字段上属性的存在 `granite:hide` 性和值来筛选资源。`/libs/cq/gui/components/authoring/dialog/dialog.jsp`的实现包括`FilteringResourceWrapper.`的实例

该实施利用Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html)并通过ExpressionCustomizer添加`cqDesign`自定义变量。

以下是位于`etc/design`下或作为内容策略的设计节点上隐藏条件的一些示例。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

在定义隐藏表达式时，请记住：

* 要有效，应表示找到属性的范围(如`cqDesign.myProperty`)。
* 值为只读。
* 函数（如果需要）应限于服务提供的给定集。

## 示例 {#example}

隐藏条件的示例可在整个AEM中找到，特别是[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)中。 例如，请考虑在[WKND教程中实施的[列表核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html)。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

[使用模板编辑器](/help/sites-cloud/authoring/features/templates.md)，模板作者可以在设计对话框中定义页面作者可以使用的列表组件的选项。诸如是否允许列表为静态列表、子页面列表、标记页面列表等选项。 可以启用或禁用。

如果模板作者选择禁用子页面选项，则会设置设计属性并针对该属性评估隐藏条件，这会导致该选项无法呈现给页面作者。

1. 默认情况下，页面作者可以使用列表核心组件通过选择选项&#x200B;**子页面**&#x200B;来使用子页面构建列表。

   ![列表组件设置](assets/hide-conditions-list-settings.png)

1. 在列表核心组件的设计对话框中，模板作者可以选择选项&#x200B;**禁用子项**，以阻止基于子页面生成列表的选项显示给页面作者。

   ![列出组件设计对话框](assets/hide-conditions-list-design.png)

1. 在`/conf/wknd/settings/wcm/policies/wknd/components/list`下创建策略节点，并将属性`disableChildren`设置为`true`。

   ![隐藏条件的节点结构](assets/hide-conditions-node-structure.png)

1. 隐藏条件定义为对话框属性节点`/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`上`granite:hide`属性的值

   ![隐藏条件的评估](assets/hide-conditions-evaluation.png)

1. `disableChildren`的值从设计配置中提取，表达式`${cqDesign.disableChildren}`的计算结果为`false`，这意味着选项不会作为组件的一部分呈现。

1. 使用列表组件时，选项&#x200B;**子页面**&#x200B;不再呈现给页面作者。

   ![禁用子选项的列表组件](assets/hide-conditions-child-disabled.png)
