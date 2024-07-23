---
title: 在自适应表单中使用自定义函数
description: AEM Forms支持自定义函数，这些函数允许用户在规则编辑器中创建和使用自己的函数。
keywords: 添加自定义函数、使用自定义函数、创建自定义函数、在规则编辑器中使用自定义函数。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: a35556164ace2245577c3e22da1bc276fc3d98d0
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 1%

---


# 基于核心组件的自适应Forms的自定义函数简介

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | 本文 |

AEM Forms支持自定义函数，允许用户定义JavaScript函数以实施复杂的业务规则。 这些自定义函数通过简化输入数据的操作和处理来扩展表单的功能，以满足特定要求。 它们允许根据预定义的标准动态更改表单行为。 通过自定义函数，开发人员还可以实施复杂的验证逻辑、执行动态计算，以及根据用户交互或预定义标准控制表单元素的显示或行为。

>[!NOTE]
>
> 确保[核心组件](https://github.com/adobe/aem-core-forms-components)设置为最新版本以使用最新功能。

## 自定义函数的使用 {#uses-of-custom-function}

在自适应Forms中使用自定义函数的优点包括：
* **正在处理数据**：自定义函数可帮助处理输入到表单字段中的数据。
* **数据验证**：自定义函数允许您对表单输入执行自定义检查并提供指定的错误消息。
* **动态行为**：自定义函数允许您根据特定条件控制表单的动态行为。 例如，您可以显示/隐藏字段、修改字段值或动态调整表单逻辑。
* **集成**：您可以使用自定义函数与外部API或服务集成。 它有助于从外部源获取数据，将数据发送到外部Rest端点，或根据外部事件执行自定义操作。

自定义函数本质上是添加到JavaScript文件中的客户端库。 创建自定义函数后，该函数即可在规则编辑器中供用户在自适应表单中选择。 自定义函数由规则编辑器中的JavaScript注释标识。

## 自定义函数支持的JavaScript批注 {#js-annotations}

JavaScript注释用于为JavaScript代码提供元数据。 它包含以特定符号(例如/**和@)开头的注释。 注释提供了有关代码中的函数、变量和其他元素的重要信息。 自适应表单支持自定义函数的以下JavaScript注释：

### 名称

该名称用于标识自适应表单的规则编辑器中的自定义函数。 以下语法用于命名自定义函数：

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`。
  `functionName`是函数的名称。 不允许使用空格。
  `<Function Name>`是自适应表单的规则编辑器中函数的显示名称。
如果函数名称与函数本身的名称相同，则可以在语法中省略`[functionName]`。

### 参数

参数是自定义函数使用的参数列表。 函数可以支持多个参数。 以下语法用于定义自定义函数中的参数：

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`。
  `{type}`表示参数类型。  允许的参数类型包括：

   * string：表示单个字符串值。
   * 数字：表示单个数值。
   * 布尔值：表示单个布尔值（true或false）。
   * string[]：表示字符串值的数组。
   * number[]：表示数值的数组。
   * 布尔值[]：表示布尔值的数组。
   * 日期：表示单个日期值。
   * date[]：表示日期值的数组。
   * array：表示包含各种类型值的泛型数组。
   * 对象：表示传递到自定义函数的表单对象，而不是直接传递其值。
   * 范围：表示全局对象，其中包含只读变量，如表单实例、目标字段实例以及在自定义函数中执行表单修改的方法。 此变量声明为JavaScript注释中的最后一个参数，在自适应表单的规则编辑器中不可见。 scope参数可访问表单或组件的对象，以触发表单处理所需的规则或事件。 有关Globals对象及其使用方法的详细信息，[单击此处](/help/forms/custom-function-core-component-create-function.md#field-and-global-scope-objects-support-in-custom-functions)。

参数类型不区分大小写，并且参数名称中不允许有空格。

`<Parameter Description>`包含有关参数用途的详细信息。 它可以有多个单词。

#### 可选参数

默认情况下，所有参数都是必需的。 您可以在参数类型后添加`=`或在`[]`中封闭参数名称，从而将参数定义为可选参数。 在JavaScript注释中定义为可选的参数在规则编辑器中显示为可选。
要将变量定义为可选参数，可以使用以下任意语法：

* `@param {type=} Input1`

在上一行代码中，`Input1`是一个可选参数，没有任何默认值。 使用默认值声明可选参数：
`@param {string=<value>} input1`

`input1`作为可选参数，默认值设置为`value`。

* `@param {type} [Input1]`

在上一行代码中，`Input1`是一个可选参数，没有任何默认值。 使用默认值声明可选参数：
`@param {array} [input1=<value>]`
`input1`是数组类型的可选参数，默认值设置为`value`。
请确保将参数类型括在大括号{}中，并将参数名称括在方括号中。

请考虑以下代码段，其中input2被定义为可选参数：

```javascript
        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

下图显示了在规则编辑器中使用`OptionalParameterFunction`自定义函数：

![可选或必需的参数](/help/forms/assets/optional-default-params.png)

您可以保存规则而不为所需的参数指定值，但不会执行规则并显示警告消息：

![不完整的规则警告](/help/forms/assets/incomplete-rule.png)

当用户将可选参数留空时，“未定义”值将传递到可选参数的自定义函数。

要了解有关如何在JSDocs中定义可选参数的更多信息，[单击此处](https://jsdoc.app/tags-param)。

### 返回类型

返回类型指定自定义函数在执行后返回的值的类型。 以下语法用于在自定义函数中定义退货类型：

* `@return {type}`
* `@returns {type}`
  `{type}`表示函数的返回类型。 允许的返回类型包括：
   * string：表示单个字符串值。
   * 数字：表示单个数值。
   * 布尔值：表示单个布尔值（true或false）。
   * string[]：表示字符串值的数组。
   * number[]：表示数值的数组。
   * 布尔值[]：表示布尔值的数组。
   * 日期：表示单个日期值。
   * date[]：表示日期值的数组。
   * array：表示包含各种类型值的泛型数组。
   * 对象：表示表单对象，而不是直接表示其值。

  返回类型不区分大小写。

### 专用

声明为私有的自定义函数不会出现在自适应表单的规则编辑器的自定义函数列表中。 默认情况下，自定义函数是公用的。 将自定义函数声明为private的语法为`@private`。


## 创建自定义函数时的准则

要在规则编辑器中列出自定义函数，您可以使用以下任意格式：

### 包含或不包含jsdoc注释的函数语句

您可以创建包含或不包含jsdoc注释的自定义函数。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
如果用户没有将任何JavaScript注释添加到自定义函数，则它按函数名称在规则编辑器中列出。 但是，建议包含JavaScript注释，以提高自定义函数的可读性。

### 带有强制JavaScript注释或注释的Arrow函数

您可以使用箭头函数语法创建自定义函数：

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

如果用户没有将任何JavaScript注释添加到自定义函数，则该自定义函数不会列在自适应表单的规则编辑器中。

### 带有必需JavaScript注释或注释的函数表达式

要在自适应表单的规则编辑器中列出自定义函数，请以下列格式创建自定义函数：

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

如果用户没有将任何JavaScript注释添加到自定义函数，则该自定义函数不会列在自适应表单的规则编辑器中。

## 后续步骤

要在自适应表单中创建和使用自定义函数，请参阅[基于核心组件创建自适应表单的自定义函数](/help/forms/custom-function-core-component-create-function.md)一文。

## 另请参阅

{{see-also-rule-editor}}