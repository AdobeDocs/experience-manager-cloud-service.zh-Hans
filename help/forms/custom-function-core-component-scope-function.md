---
title: 介绍自定义函数中的作用域对象
description: 表单支持自定义函数中的范围对象，该对象在执行规则时作为最后一个参数传递给函数。
keywords: 自定义函数中的范围对象、全局对象、字段对象。
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: af211649a4f22d06f4e8669335a8267ee948a408
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# 自定义函数中的范围对象

在自适应Forms中，范围对象在执行规则时作为最后一个参数传递给函数。 它可用于读取表单/字段属性，以及从函数内修改表单。 作用域对象包含表单、触发的事件和目标字段的只读代理对象。 通过分别附加`$`（例如`scope.form.$id`和`scope.field.$id`），可以使用范围对象访问表单和字段属性。

## 使用范围对象的表单修改函数

范围对象具有下列表单修改功能：

| 函数 | 语法 | 描述 | 代码示例 |
|-----------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------|
| **setProperty** | `setProperty(any $element, any $payload)` | 使用`$payload`设置`$element`的属性。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule)查看示例。 |
| **验证** | `validate([any $element])` | 在`$element`上运行验证。 如果未提供任何元素，则会验证整个表单。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#validate-the-field)查看示例。 |
| **重置** | `reset([any $element])` | 重置`$element`。 如果未提供元素，则会重置整个表单。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel)查看示例。 |
| **importData** | `importData(any $payload)` | 将数据导入表单，并替换任何现有的表单数据。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads)查看示例。 |
| **exportData** | `exportData()` | 返回表单数据。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server)查看示例。 |
| **提交表单** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | 触发表单提交。 `$data`参数指定要提交的内容，`$submit_as`定义内容类型（默认为“multipart/form-data”）。 可选的`$validate_form`确定是否应当验证表单（默认值： true）。 成功时触发`submitSuccess`；失败时触发`submitError`。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server)查看示例。 |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | 将焦点设置为`$element`，它可以是面板或字段。 如果未提供任何元素，则焦点将设置为触发规则的字段。 可选`$focusOption`参数（枚举类型`FocusOption`）指定是关注相对于`$element`的“nextItem”还是“previousItem”。 如果指定了面板，则导航将限制到该面板；对于字段，导航会在父面板中进行。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field)查看示例。 |
| **dispatchEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | 在`$element`指定的元素上调度类型为`$eventName`的事件。 如果未提供任何元素，则会在表单上调度事件。 可选`$payload`可供处理该事件的表达式使用。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property)查看示例。 |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | 将`$fieldIdentifier`标识的字段标记为无效，并将验证消息设置为`$validationMessage`。 可选的`$option`参数指定`$fieldIdentifier`是解释为`id`、`name`还是`dataRef`。 默认值为`{useId: true}`，支持的值包括`{useId: true}`、`{useDataRef: true}`和`{useQualifiedName: true}`。 | [单击此处](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid)查看示例。 |

## 另请参阅

{{see-also-rule-editor}}