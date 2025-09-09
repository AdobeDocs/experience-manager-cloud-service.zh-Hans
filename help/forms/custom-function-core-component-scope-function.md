---
title: 介绍自定义函数中的作用域对象
description: 表单支持自定义函数中的范围对象，该对象在执行规则时作为最后一个参数传递给函数。
keywords: 自定义函数中的范围对象、全局对象、字段对象。
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 248c75a5-6335-41d2-aa0a-28a20a710f88
source-git-commit: e2bc958104bd9b75845ad2c213eec18d2560a3a4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# 自定义函数中的范围对象

在自适应Forms中，范围对象在执行规则时作为最后一个参数传递给函数。 它可用于读取表单/字段属性，以及从函数内修改表单。 作用域对象包含表单、触发的事件和目标字段的只读代理对象。 通过分别附加`$`（例如`scope.form.$id`和`scope.field.$id`），可以使用范围对象访问表单和字段属性。

## 使用范围对象的表单修改函数

范围对象具有下列表单修改功能：

| 函数 | 语法 | 描述 | 代码示例 |
|-----------------|--------|-------------|-------------|
| **setProperty** | `setProperty(any $element, any $payload)` | 使用`$payload`在目标字段上设置属性。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule)查看示例。 |
| **验证** | `validate([any $element])` | 在目标字段上运行验证。 如果未提供目标，则会在整个表单上运行验证，并返回一系列验证错误。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#validate-the-field)查看示例。 |
| **重置** *（已弃用）* | `reset([any $element])` | 已弃用。 请改用`dispatchEvent($target, 'reset')`。 重置目标字段，如果未提供目标，则重置整个表单。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel)查看示例。 |
| **importData** | `importData(any $payload)` | 将数据导入表单，并替换任何现有的表单数据。 如果指定了`qualifiedName`，则只将数据导入该容器字段。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads)查看示例。 |
| **exportData** | `exportData()` | 返回表单数据。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server)查看示例。 |
| **提交表单** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | 触发表单提交。 您可以通过`$payload`参数指定要提交的内容，并通过`$contentType`参数设置内容类型。 默认情况下将数据作为`multipart/form-data`提交。 可选的`$validateForm`参数指定是否应在提交之前验证表单（默认值： true）。 成功时触发`submitSuccess`；失败时触发`submitError`。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server)查看示例。 |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | 将焦点设置为目标字段，该字段可以是面板或表单字段。 如果未提供目标，则焦点将设置为触发规则的字段。 可选的`$focusOption`参数指定相对于目标的下一个或上一个项是否应聚焦。 支持的值： `'nextItem'`，`'previousItem'`。 如果与某个面板一起使用，则导航将限制在该面板上。 如果与字段一起使用，则导航将在该字段的父面板中进行。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field)查看示例。 |
| **dispatchEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | 在由`$eventName`确定的元素上调度类型为`$target`的事件。 如果未提供目标，则会在表单上调度事件。 可选`$payload`可用于处理事件的表达式。 可选的`$dispatch`参数控制事件传播行为。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property)查看示例。 |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | 将`$fieldIdentifier`标识的字段标记为无效并显示`$validationMessage`。 可选的`$option`参数指定`$fieldIdentifier`是解释为`id`、`dataRef`还是`qualifiedName`。 默认值为`{useId: true}`。 支持的值： `{useId: true}`、`{useDataRef: true}`、`{useQualifiedName: true}`。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid)查看示例。 |

## 另请参阅

{{see-also-rule-editor}}

