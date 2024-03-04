---
title: 在自适应表单中创建和添加自定义函数
description: AEM Forms支持自定义函数，这些函数允许用户在规则编辑器中创建和使用自己的函数。
keywords: 添加自定义函数、使用自定义函数、创建自定义函数、在规则编辑器中使用自定义函数。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: 46fbed98a806f62dd1882eb0085d4338c5cd51a7
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 8%

---


# 自适应Forms中的自定义函数（核心组件）

## 简介

AEM Forms支持自定义函数，允许用户定义JavaScript函数以实现复杂的业务规则。 这些自定义函数通过简化输入数据的操作和处理来扩展表单的功能，以满足特定要求。 它们还支持根据预定义标准动态更改表单行为。
在自适应Forms中，您可以使用中的自定义函数 [自适应表单的规则编辑器](/help/forms/rule-editor-core-components.md) 创建表单字段的特定验证规则。

让我们了解自定义功能的使用，用户可以在其中输入电子邮件地址，您希望确保输入的电子邮件地址遵循特定格式（其中包含“@”符号和域名）。 创建自定义函数为“ValidateEmail”，该函数将电子邮件地址作为输入，如果有效，则返回true；否则返回false。

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

在上述示例中，当用户尝试提交表单时，将调用自定义函数“ValidateEmail”以检查输入的电子邮件地址是否有效。

### 自定义函数的使用 {#uses-of-custom-function}

在自适应Forms中使用自定义函数的优点包括：

* **数据操作**：自定义函数处理并处理输入到表单字段中的数据。
* **数据验证**：通过自定义函数，可对表单输入执行自定义检查并提供指定的错误消息。
* **动态行为**：自定义函数允许您根据特定条件控制表单的动态行为。 例如，您可以显示/隐藏字段、修改字段值或动态调整表单逻辑。
* **集成**：您可以使用自定义函数与外部API或服务集成。 它有助于从外部源获取数据，将数据发送到外部Rest端点，或根据外部事件执行自定义操作。

## 支持的JS注释

请确保您编写的自定义函数附带 `jsdoc` 高于它。

支持 `jsdoc` 标记：

* **私有**
语法： `@private`
专用函数未作为自定义函数包含在内。

* **名称**
语法： `@name funcName <Function Name>`
或者 `,` 您可以使用： `@function funcName <Function Name>` **或** `@func` `funcName <Function Name>`.
  `funcName` 是函数的名称（不允许有空格）。
  `<Function Name>` 是函数的显示名称。

* **参数**
语法： `@param {type} name <Parameter Description>`
或者，您可以使用： `@argument` `{type} name <Parameter Description>` **或** `@arg` `{type}` `name <Parameter Description>`.
显示函数使用的参数。 一个函数可以有多个参数标记，每个参数按其出现顺序对应一个标记。
  `{type}` 表示参数类型。 允许的参数类型包括：

   1. 字符串
   2. 数字
   3. 布尔型
   4. 范围
   5. 字符串[]
   6. 数字[]
   7. 布尔型[]
   8. 日期
   9. 日期[]
   10. 数组
   11. 对象

  `scope` 指由forms运行时提供的特殊全局对象。 该参数必须是最后一个参数，并且在规则编辑器中对用户不可见。 您可以使用作用域访问可读的表单和字段代理对象来读取属性、触发规则的事件和一组处理表单的函数。

  `object` type用于将参数中的可读字段对象传递到自定义函数，而不是传递值。

  所有参数类型均被归入上述参数类型之一。 不支持无。 确保选择以上类型之一。 类型不区分大小写。 参数名称中不允许有空格。  参数描述可以有多个单词。

* **可选参数**
语法： `@param {type=} name <Parameter Description>`
或者，您可以使用： `@param {type} [name] <Parameter Description>`
默认情况下，所有参数都是必需的。 可以通过添加参数将参数标记为可选 `=` 键入参数类型或将参数名称放在方括号中。
例如，让我们声明 `Input1` 作为可选参数：
   * `@param {type=} Input1`
   * `@param {type} [Input1]`

* **返回类型**
语法： `@return {type}`
或者，您可以使用 `@returns {type}`.
添加有关函数的信息，例如其目标。
{type} 表示函数的返回类型。 允许的返回类型包括：

   1. 字符串
   2. 数字
   3. 布尔型
   4. 字符串[]
   5. 数字[]
   6. 布尔型[]
   7. 日期
   8. 日期[]
   9. 数组
   10. 对象

所有其他退货类型均归入上述任一类型下。 不支持无。 确保选择以上类型之一。 返回类型不区分大小写。

## 创建自定义函数时的注意事项 {#considerations}

要在规则编辑器中列出自定义函数，可以使用以下任意格式之一声明它们：

* **包含或不包含jsdoc注释的函数语句**

您可以创建包含或不包含jsdoc注释的自定义函数。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
<!--

* **Arrow function with mandatory jsdoc comment**

Some of the examples to create Arrow functions are:
```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} a some parameter description
    * @param {string} b another parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
```

    * @param {string=} b another parameter description
      /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;-->

* **具有必需jsdoc注释的函数表达式**

要在自适应表单的规则编辑器中列出自定义函数，请以下列格式创建自定义函数：

```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} input1 parameter description
    * @param {string} input2 another parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

<!--
* @param {string=} input2 another parameter description
The functions that are not supported in the custom function list are:
* Generator functions
* Async/Await functions 
* Method definitions
* Class methods
* Default parameters
* Rest parameters -->

>[!NOTE]
>
> 您可以检查 `error.log` 文件以查找任何错误，如规则编辑器中未列出自定义函数。

<!--The `error.log` file also displays the methods and parameters that are not supported for custom functions. -->


## 创建自定义函数 {#create-custom-function}

创建客户端库以在规则编辑器中调用自定义函数。 有关更多信息，请参阅 [使用客户端库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

创建自定义函数的步骤包括：
1. [创建客户端库](#create-client-library)
1. [在自适应表单中添加客户端库](#use-custom-function)

### 创建客户端库 {#create-client-library}

您可以通过添加客户端库来添加自定义函数。 要创建客户端库，请执行以下步骤：

1. [克隆AEM Formsas a Cloud Service存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).
1. 在 `[AEM Forms as a Cloud Service repository folder]/apps/` 文件夹下创建一个文件夹。例如，创建一个名为的文件夹 `experience-league`.
1. 导航到 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` 并创建 `ClientLibraryFolder`. 例如，创建客户端库文件夹为 `customclientlibs`.
1. 添加属性 `categories` 字符串类型值的组合。 例如，分配值 `customfunctionscategory` 到 `categories` 的属性 `customclientlibs` 文件夹。

   >[!NOTE]
   >
   > 您可以选择任意名称 `client library folder` 和 `categories` 属性。

1. 创建一个名为 `js` 的文件夹。
1. 导航到 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` 文件夹。
1. 添加JavaScript文件，例如， `function.js`. 该文件包含自定义函数的代码。

   >[!NOTE]
   >
   > 如果包含自定义函数代码的JavaScript文件出错，则自定义函数不会列在自适应表单的规则编辑器中。 您还可以检查 `error.log` 文件查找错误。

   <!-- 
    >* AEM Adaptive Form supports the caching of custom functions. If the JavaScript is modified, the caching becomes invalidated, and it is parsed. You can see a message as `Fetched following custom functions list from cache` in the `error.log` file.  -->

1. 保存 `function.js` 文件。
1. 导航到 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` 文件夹。
1. 添加文本文件作为 `js.txt`。该文件包含：

   ```javascript
       #base=js
       functions.js
   ```

1. 保存 `js.txt` 文件。
1. 使用以下命令在存储库中添加、提交和推送更改：

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. [运行管道。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline)

成功执行管道后，客户端库中添加的自定义函数即可在中使用 [自适应表单规则编辑器](/help/forms/rule-editor-core-components.md).

### 在自适应表单中添加客户端库{#use-custom-function}

将客户端库部署到Forms CS环境后，请在自适应表单中使用其功能。 在自适应表单中添加客户端库

1. 在编辑模式下打开表单。 要在编辑模式下打开表单，请选择一个表单，然后选择 **[!UICONTROL 编辑]**.
1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 打开 **[!UICONTROL 基本]** 选项卡并选择的名称 **[!UICONTROL 客户端库类别]** (在本例中，选择 `customfunctionscategory`)。

   ![添加自定义函数客户端库](/help/forms/assets/clientlib-custom-function.png)

1. 单击 **[!UICONTROL 完成]** .

现在，您可以创建规则以在规则编辑器中使用自定义函数。

<!--

Create a rule to use custom function in the rule editor. 

### Support for the optional parameters in custom functions{#support-for-optional-parameter}

AEM supports including optional parameters in JSDocs. These parameters are displayed as optional in the rule editor. There are two ways to add optional parameters in JSDocs:
*  `@param {string=abc} b -- some description for b which is optional`

    In the above line of code, `b` is an optional parameter with the default value set to `abc`. 
    Alternatively, you can define `b` as an optional parameter without assigning any default value as `@param {string=} b -- some description for b which is optional`

* `@param {array} [z=[def,xyz]] - - some description for z which is optional`

    In the above line of code, `z` is an optional parameter of array type with the default value set to `[def , xyz]`. 
    Alternatively, you can define `z` as an optional parameter without assigning any default value as `@param {array} [z=] - - some description for z which is optional`

>[!NOTE]
>
> Ensure that the parameter name is enclosed in square brackets [] and the parameter type is enclosed in curly brackets {}. 

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

In the rule editor of an Adaptive Form, the parameters are displayed as `required`. By default the parameters are `required`, if not defined as optional in JSDocs.

  ![Optional or required parameters](/help/forms/assets/optional-default-params.png) 

  You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

  ![incomplete rule warning message](/help/forms/assets/incomplete-rule.png) 
  
  The rule is executed even if you do not specify a value for optional parameters. Undefined values are passed for optional parameters on executing the rule.

  ### Support for field and globals objects in custom functions {#support-field-and-global-objects}

  needs to be discussed

  -->

## 另请参阅 {#see-also}

{{see-also}}





