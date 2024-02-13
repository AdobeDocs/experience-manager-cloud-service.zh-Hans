---
title: 在自适应表单中创建和添加自定义函数
description: AEM Forms支持自定义函数，这些函数允许用户在规则编辑器中创建和使用自己的函数。
keywords: 添加自定义函数、使用自定义函数、创建自定义函数、在规则编辑器中使用自定义函数。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: 28020b05e4aaaa3f066943e0504f05e307c7020b
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 8%

---


# 自适应Forms中的自定义函数（核心组件）

## 简介

AEM Forms支持自定义函数，允许用户定义JavaScript函数以实现复杂的业务规则。 这些自定义函数通过简化输入数据的操作和处理来扩展表单的功能，以满足特定要求。 它们还支持根据预定义标准动态更改表单行为。
在自适应Forms中，您可以使用中的自定义函数 [自适应表单的规则编辑器](/help/forms/rule-editor.md#custom-functions) 创建表单字段的特定验证规则。

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

在自适应Forms中使用自定义函数的一些优势包括：

* **数据操作**：自定义函数可处理输入到表单字段中的数据。
* **数据验证**：通过自定义函数，可对表单输入执行自定义检查并提供指定的错误消息。
* **动态行为**：自定义函数允许您根据特定条件控制表单的动态行为。 例如，您可以显示/隐藏字段、修改字段值或动态调整表单逻辑。
* **集成**：您可以使用自定义函数与外部API或服务集成。 它有助于从外部源获取数据，将数据发送到外部Rest端点，或根据外部事件执行自定义操作。

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

创建以下格式的自定义函数以在自适应表单的规则编辑器中列出它们。 例如：

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
> 您可以检查 `error.log` 文件，以防在规则编辑器中未列出自定义函数等任何错误。

<!--The `error.log` file also displays the methods and parameters that are not supported for custom functions. -->


## 创建自定义函数 {#create-custom-function}

创建客户端库以在规则编辑器中调用自定义函数。 有关更多信息，请参阅 [使用客户端库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

创建自定义函数的步骤包括：
1. [创建客户端库](#create-client-library)
1. [在自适应表单中添加客户端库](#use-custom-function)

### 创建客户端库 {#create-client-library}

您可以通过添加客户端库来添加自定义函数。 要创建客户端库，请执行以下步骤：

1. [克隆AEM Formsas a Cloud Service存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).
1. 在 `[AEM Forms as a Cloud Service repository folder]/apps/` 文件夹下创建一个文件夹。例如，创建一个名为 `experience-league` 的文件夹
1. 导航到 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` 并创建一个`ClientLibraryFolder` 作为 `es6clientlibs`。
1. 添加属性 `categories`字符串类型值为 `es6customfunctions` 到 `es6clientlibs` 文件夹。

   >[!NOTE]
   >
   >`es6customfunctions`是一个示例类别。 您可以为类别选择任意名称。

1. 创建一个名为 `js` 的文件夹。
1. 导航到 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/es6clientlibs/js` 文件夹。
1. 添加JavaScript文件，例如， `function.js`. 该文件包含自定义函数的代码。

   >[!NOTE]
   >
   >* 如果包含自定义函数代码的JavaScript文件出错，则自定义函数不会列在自适应表单的规则编辑器中。 您还可以检查 `error.log` 文件查找错误。

   <!-- 
    >* AEM Adaptive Form supports the caching of custom functions. If the JavaScript is modified, the caching becomes invalidated, and it is parsed. You can see a message as `Fetched following custom functions list from cache` in the `error.log` file.  -->

1. 保存 `function.js` 文件。
1. 导航到 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/es6clientlibs/js` 文件夹。
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

成功执行管道后，客户端库中添加的自定义函数即可在中使用 [自适应表单规则编辑器](/help/forms/rule-editor.md).

### 在自适应表单中添加客户端库{#use-custom-function}

添加客户端库后，在自适应表单中使用它。 这让您能够使用 [自定义函数作为表单中的规则](/help/forms/rule-editor.md#custom-functions). 要在自适应表单中添加客户端库，请执行以下步骤：

1. 在编辑模式下打开表单。
要在编辑模式下打开表单，请选择一个表单，然后选择 **[!UICONTROL 打开]**.
1. 在编辑模式下，选择一个组件，然后选择 ![字段级](assets/select_parent_icon.svg) > **[!UICONTROL 自适应表单容器]**，然后选择 ![cmppr](assets/configure-icon.svg).
1. 在侧栏中的“Name of Client Library”（客户端库名称）下，添加您的客户端库。 ( `es6customfunctions` 在此示例中。)

   ![添加自定义函数客户端库](/help/forms/assets/clientlib-custom-function.png)

创建规则以在规则编辑器中使用自定义函数。

<!--

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





