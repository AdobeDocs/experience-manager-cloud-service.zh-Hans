---
title: 如何使用规则编辑器将规则添加到表单字段，以添加动态行为并根据核心组件向自适应表单构建复杂逻辑？
description: 自适应Forms规则编辑器允许您添加动态行为并将复杂的逻辑构建到表单中，而无需编码或编写脚本。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 1292f729-c6eb-4e1b-b84c-c66c89dc53ae
source-git-commit: 780c68f0c21ef94ff6a73ce991370100b1a88db9
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 4%

---


# 基于核心组件的自适应表单的规则编辑器简介

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service（核心组件） | 本文 |
| AEM as a Cloud Service（基础组件） | [单击此处](/help/forms/rule-editor.md) |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html) |

在基于核心组件的自适应表单中，规则编辑器功能使业务用户和开发人员均可编写自适应表单对象的规则。 这些规则根据预设条件、用户输入和用户对表单的操作，定义要在表单对象上触发的操作。 此功能有助于进一步简化表单填写体验，确保准确性和速度。

规则编辑器为编写规则提供了一个直观、简化的用户界面。 它提供了一个面向所有用户的可视化编辑器，允许用户创建和管理规则，而无需丰富的技术知识。 这种可视化方法使用户更容易理解并在其表单中实施所需的逻辑。

您可以使用规则对自适应表单对象执行的一些关键操作包括：

* 显示或隐藏对象
* 启用或禁用对象
* 为对象设置值
* 验证某个对象的值
* 通过执行函数来计算对象的值
* 调用表单数据模型 (FDM) 服务并执行操作
* 设置对象的属性

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

添加到`forms-power-users`组的用户可以创建脚本并编辑现有脚本。 [!DNL forms-users]组中的用户可以使用脚本，但不能创建或编辑脚本。

有关详细比较，请参阅Foundation规则编辑器与核心组件规则编辑器之间的[差异](/help/forms/rule-editor-core-components-difference-tables.md)一文。

<!--
## Difference between Rule editor in Core Components and Rule Editor in Foundation Components

{{rule-editor-diff}}

>[!NOTE]
>
> To see how to create and use custom functions in detail, refer to [Custom functions in Adaptive Forms (Core Components)](/help/forms/create-and-use-custom-functions.md) article.

-->

## 了解规则 {#understanding-a-rule}

规则是操作和条件的组合。 在规则编辑器中，操作包括隐藏、显示、启用、禁用或计算表单中对象值等活动。 条件是对表单对象的状态、值或属性执行检查和操作而计算的布尔表达式。 根据通过评估条件返回的值（`True`或`False`）执行操作。

规则编辑器提供了一组预定义的规则类型（如When、Show、Hide、Enable、Disable、Set Value Of和Validate）以帮助您编写规则。 每种规则类型均允许您定义规则中的条件和操作。 本文档进一步详细说明了每种规则类型。

规则通常遵循以下结构之一：

**Condition-Action**&#x200B;在此构造中，规则首先定义条件，然后定义要触发的操作。 该构造与编程语言中的if-then语句类似。

在规则编辑器中，**When**&#x200B;规则类型强制使用condition-action结构。

**Action-Condition**&#x200B;在此构造中，规则首先定义要触发的操作，然后定义评估条件。 此结构的另一个变体是action-condition-alternate action ，它还会定义在条件返回False时要触发的替代操作。

规则编辑器中的“显示”、“隐藏”、“启用”、“禁用”、“设置值”和“验证”规则类型强制实施操作条件规则结构。 默认情况下，“显示”的替代操作是“隐藏”，而“启用”的替代操作是“禁用”，反之亦然。 您不能更改默认替代操作。

>[!NOTE]
>
>可用的规则类型（包括在规则编辑器中定义的条件和操作）还取决于创建规则的表单对象的类型。 规则编辑器仅显示有效的规则类型和选项，用于为特定表单对象类型编写条件和操作语句。 例如，您看不到面板对象的“验证并设置类型的值”。

有关规则编辑器中可用规则类型的详细信息，请参阅规则编辑器中的[可用规则类型](rule-editor.md#p-available-rule-types-in-rule-editor-p)。

### 选择规则结构的准则 {#guidelines-for-choosing-a-rule-construct}

虽然您可以使用任何规则构建来实现大多数用例，但以下是选择一种构建而不是另一种构建的一些准则。 有关规则编辑器中可用规则的更多信息，请参阅规则编辑器中的[可用规则类型](rule-editor.md#p-available-rule-types-in-rule-editor-p)。

* 创建规则时，一个典型的经验法则是考虑您所编写规则的对象的上下文。 假定您要根据用户在字段A中指定的值隐藏或显示字段B。在这种情况下，您要评估字段A的条件，并根据它返回的值，触发字段B的操作。

  因此，如果您在字段B（评估条件的对象）上编写规则，请使用condition-action结构或When规则类型。 同样，在字段A上使用操作条件结构或显示或隐藏规则类型。

* 有时，您必须根据一个条件执行多个操作。 在这种情况下，建议使用条件 — 操作构造。 在此构造中，您可以计算一次条件并指定多个操作语句。

  例如，要根据检查用户在字段A中指定的值的条件隐藏字段B、C和D，请编写一条规则，其中在字段A上使用condition-action结构或When规则类型，并指定操作以控制字段B、C和D的可见性。否则，您需要在字段B、C和D上分别使用三个规则，其中每个规则都会检查条件，并显示或隐藏各自的字段。 在此示例中，在一个对象上编写When规则类型比在三个对象上编写Show或Hide规则类型更有效。

* 要根据多个条件触发操作，建议使用操作条件构造。 例如，要通过评估字段B、C和D的条件来显示和隐藏字段A，请使用字段A上的显示或隐藏规则类型。
* 如果规则包含一个条件的一个操作，则使用condition-action或action condition结构。
* 如果规则检查条件，并在字段中提供值或退出字段时立即执行操作，则建议在评估条件的字段中编写具有condition-action结构或When规则类型的规则。
* 当用户更改应用When规则的对象的值时，将评估When规则中的条件。 但是，如果您希望操作在服务器端更改时触发（如预填充值），则建议编写一个When规则以在字段初始化时触发操作。
* 在编写下拉列表、单选按钮或复选框对象的规则时，表单中这些表单对象的选项或值会在规则编辑器中预填充。

## 后续步骤

要了解如何使用用户界面在规则编辑器中编写和管理规则，请参阅[基于核心组件的自适应Forms的规则编辑器用户界面](/help/forms/rule-editor-core-components-user-interface.md)一文。

## 另请参阅

{{see-also-rule-editor}}