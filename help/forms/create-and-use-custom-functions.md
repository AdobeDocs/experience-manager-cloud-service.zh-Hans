---
title: 在自适应表单中创建和添加自定义函数
description: AEM Forms支持自定义函数，这些函数允许用户在规则编辑器中创建和使用自己的函数。
keywords: 添加自定义函数、使用自定义函数、创建自定义函数、在规则编辑器中使用自定义函数。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
mini-toc-levels: 4
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
source-git-commit: 6f50bdf2a826654e0d5b35de5bd50e66981fb56a
workflow-type: tm+mt
source-wordcount: '3513'
ht-degree: 3%

---


<span class="preview"> 本文包含 `Override form submission success and error handlers` 作为预发行版功能。 预发行功能只能通过我们的 [预发行渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features).

# 自适应Forms中的自定义函数（核心组件）

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | 本文 |

## 简介

AEM Forms支持自定义函数，允许用户定义用于实现复杂业务规则的JavaScript函数。 这些自定义函数通过简化输入数据的操作和处理来扩展表单的功能，以满足特定要求。 它们还支持根据预定义标准动态更改表单行为。

>[!NOTE]
>
> 确保 [核心组件](https://github.com/adobe/aem-core-forms-components) 设置为最新版本以使用最新功能。

### 自定义函数的使用 {#uses-of-custom-function}

在自适应Forms中使用自定义函数的优点包括：
* **数据处理**：自定义函数有助于处理输入到表单字段中的数据。
* **数据验证**：通过自定义函数，可对表单输入执行自定义检查并提供指定的错误消息。
* **动态行为**：自定义函数允许您根据特定条件控制表单的动态行为。 例如，您可以显示/隐藏字段、修改字段值或动态调整表单逻辑。
* **集成**：您可以使用自定义函数与外部API或服务集成。 它有助于从外部源获取数据，将数据发送到外部Rest端点，或根据外部事件执行自定义操作。

自定义函数本质上是添加到JavaScript文件中的客户端库。 创建自定义函数后，该函数即可在规则编辑器中供用户在自适应表单中选择。 自定义函数由规则编辑器中的JavaScript注释标识。

### 自定义函数支持的JavaScript注释 {#js-annotations}

JavaScript注释用于为JavaScript代码提供元数据。 它包含以特定符号(例如/**和@)开头的注释。 注释提供了有关代码中的函数、变量和其他元素的重要信息。 自适应表单支持自定义函数的以下JavaScript注释：

#### 名称

该名称用于标识自适应表单的规则编辑器中的自定义函数。 以下语法用于命名自定义函数：

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`。
  `functionName` 是函数的名称。 不允许使用空格。
  `<Function Name>` 是自适应表单的规则编辑器中函数的显示名称。
如果函数名称与函数本身的名称相同，则可以忽略 `[functionName]` 语法中的。

#### 参数

参数是自定义函数使用的参数列表。 函数可以支持多个参数。 以下语法用于定义自定义函数中的参数：

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`.
  `{type}` 表示参数类型。  允许的参数类型包括：

   * string：表示单个字符串值。
   * 数字：表示单个数值。
   * 布尔值：表示单个布尔值（true或false）。
   * 字符串[]：表示字符串值的数组。
   * 数字[]：表示数字值的数组。
   * 布尔型[]：表示布尔值的数组。
   * 日期：表示单个日期值。
   * 日期[]：表示日期值的数组。
   * array：表示包含各种类型值的泛型数组。
   * 对象：表示传递到自定义函数的表单对象，而不是直接传递其值。
   * 范围：表示全局对象，其中包含只读变量，如表单实例、目标字段实例以及在自定义函数中执行表单修改的方法。 此变量声明为JavaScript注释中的最后一个参数，在自适应表单的规则编辑器中不可见。 scope参数可访问表单或组件的对象，以触发表单处理所需的规则或事件。 有关Globals对象及其使用方式的更多信息， [单击此处](/help/forms/create-and-use-custom-functions.md#support-field-and-global-objects).

参数类型不区分大小写，并且参数名称中不允许有空格。

`<Parameter Description>` 包含有关参数用途的详细信息。 它可以有多个单词。

**可选参数**
默认情况下，所有参数都是必需的。 通过添加以下任一项，可将参数定义为可选参数 `=` 在参数类型后面或将参数名称括在  `[]`. 在JavaScript注释中定义为可选的参数在规则编辑器中显示为可选。
要将变量定义为可选参数，可以使用以下任意语法：

* `@param {type=} Input1`

在上一行代码中， `Input1` 是一个可选参数，没有任何默认值。 使用默认值声明可选参数：
`@param {string=<value>} input1`

`input1` 作为可选参数，默认值设置为 `value`.

* `@param {type} [Input1]`

在上一行代码中， `Input1` 是一个可选参数，没有任何默认值。 使用默认值声明可选参数：
`@param {array} [input1=<value>]`
`input1` 是数组类型的可选参数，其默认值设置为 `value`.
确保将参数类型括在大括号中 {} 并且参数名称用方括号括起来 [].

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

下图使用 `OptionalParameterFunction` 规则编辑器中的自定义函数：

![可选或必需的参数 ](/help/forms/assets/optional-default-params.png)

您可以保存规则而不为所需的参数指定值，但不会执行规则并显示警告消息：

![规则不完整警告](/help/forms/assets/incomplete-rule.png)

当用户将可选参数留空时，“未定义”值将传递到可选参数的自定义函数。

要详细了解如何在JSDocs中定义可选参数， [单击此处](https://jsdoc.app/tags-param).

#### 返回类型

返回类型指定自定义函数在执行后返回的值的类型。 以下语法用于在自定义函数中定义退货类型：

* `@return {type}`
* `@returns {type}`
  `{type}` 表示函数的返回类型。 允许的返回类型包括：
   * string：表示单个字符串值。
   * 数字：表示单个数值。
   * 布尔值：表示单个布尔值（true或false）。
   * 字符串[]：表示字符串值的数组。
   * 数字[]：表示数字值的数组。
   * 布尔型[]：表示布尔值的数组。
   * 日期：表示单个日期值。
   * 日期[]：表示日期值的数组。
   * array：表示包含各种类型值的泛型数组。
   * 对象：表示表单对象，而不是直接表示其值。

  返回类型不区分大小写。

#### 专用

声明为私有的自定义函数不会出现在自适应表单的规则编辑器的自定义函数列表中。 默认情况下，自定义函数是公用的。 将自定义函数声明为私有函数的语法为 `@private`.


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
如果用户没有向自定义函数添加任何JavaScript注释，则它按函数名称在规则编辑器中列出。 但是，建议包含JavaScript注释，以提高自定义函数的可读性。

### 具有必需JavaScript注释或注释的Arrow函数

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

### 具有必需JavaScript注释或注释的函数表达式

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

## 创建自定义功能 {#create-custom-function}

创建客户端库以在规则编辑器中调用自定义函数。 有关更多信息，请参阅 [使用客户端库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

创建自定义函数的步骤包括：
1. [创建客户端库](#create-client-library)
1. [将客户端库添加到自适应表单](#use-custom-function)

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

1. [运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) 以部署自定义函数。

成功执行管道后，客户端库中添加的自定义函数即可在中使用 [自适应表单规则编辑器](/help/forms/rule-editor-core-components.md).

### 将客户端库添加到自适应表单{#use-custom-function}

将客户端库部署到Forms CS环境后，请在自适应表单中使用其功能。 在自适应表单中添加客户端库

1. 在编辑模式下打开表单。 要在编辑模式下打开表单，请选择一个表单，然后选择 **[!UICONTROL 编辑]**.
1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 打开 **[!UICONTROL 基本]** 选项卡并选择的名称 **[!UICONTROL 客户端库类别]** (在本例中，选择 `customfunctionscategory`)。

   ![添加自定义函数客户端库](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > 通过在 **[!UICONTROL 客户端库类别]** 字段。

1. 单击&#x200B;**[!UICONTROL 完成]**。

您可以使用中的自定义函数 [自适应表单的规则编辑器](/help/forms/rule-editor-core-components.md) 使用 [JavaScript注释](##js-annotations).

## 在自适应表单中使用自定义函数

在自适应表单中，您可以使用 [规则编辑器中的自定义函数](/help/forms/rule-editor-core-components.md). 让我们将以下代码添加到JavaScript文件(`Function.js` 文件)，以根据出生日期计算年龄(YYYY-MM-DD)。 创建自定义函数为 `calculateAge()` ，以出生日期作为输入并返回年龄：

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

在上例中，当用户以(YYYY-MM-DD)格式输入出生日期时，自定义函数 `calculateAge` 将调用并返回年龄。

![在规则编辑器中重新计算自定义函数](/help/forms/assets/custom-function-calculate-age.png)

让我们预览表单，观察自定义函数如何通过规则编辑器实现：

![在规则编辑器表单预览中再次计算自定义函数](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 您可以参考以下内容 [自定义函数](/help/forms/assets//customfunctions.zip) 文件夹。 使用下载此文件夹并将其安装到您的AEM实例中 [包管理器](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).


### 使用自定义函数设置下拉列表选项

核心组件中的规则编辑器不支持 **设置选项** 属性，用于在运行时设置下拉列表选项。 但是，您可以使用自定义函数设置下拉列表选项。

查看以下代码，了解如何使用自定义函数设置下拉列表选项：

```javascript
    /**
    * @name setEnums
    * @returns {string[]}
    **/
    function setEnums() {
    return ["0","1","2","3","4","5","6"];   
    }

    /**
    * @name setEnumNames
    * @returns {string[]}
    **/
    function setEnumNames() {
    return ["Sunday","Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
    }
```

在上述代码中， `setEnums` 用于设置 `enum` 属性和 `setEnumNames` 用于设置 `enumNames` 下拉列表的属性。

让我们为 `Next` 按钮，设置用户单击 `Next` 按钮：

![下拉列表选项](/help/forms/assets/drop-down-list-options.png)

请参阅下图以演示单击“显示”按钮时下拉列表的选项设置位置：

![规则编辑器中的下拉选项](/help/forms/assets/drop-down-option-rule-editor.png)



### 在自定义函数中支持异步函数 {#support-of-async-functions}

异步自定义函数未出现在规则编辑器列表中。 但是，可以在使用同步函数表达式创建的自定义函数中调用异步函数。

![同步和异步自定义函数](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> 在自定义函数中调用异步函数的优势在于，异步函数允许并行执行多个任务，并且自定义函数中使用了每个函数的结果。

查看以下代码，了解如何使用自定义函数调用异步函数：

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

在上述示例中，asyncFunction函数是 `asynchronous function`. 它执行异步操作，方法是 `GET` 请求给 `https://petstore.swagger.io/v2/store/inventory`. 它使用以下方式等待响应 `await`，使用将响应正文解析为JSON `response.json()`，然后返回数据。 此 `callAsyncFunction` 函数是一个同步自定义函数，可调用 `asyncFunction` 函数并在控制台中显示响应数据。 尽管 `callAsyncFunction` 函数是同步的，它调用异步asyncFunction函数并使用处理其结果 `then` 和 `catch` 语句。

要查看其是否有效，让我们添加一个按钮，并为按钮创建一个规则，该规则会在单击按钮时调用异步函数。

![创建异步函数的规则](/help/forms/assets/rule-for-async-funct.png)

请参阅下面的控制台窗口插图，以演示当用户单击 `Fetch` 按钮，自定义函数 `callAsyncFunction` 将调用，从而调用异步函数 `asyncFunction`. 在控制台窗口中Inspect以查看对单击按钮的响应：

![控制台窗口](/help/forms/assets/async-custom-funct-console.png)

让我们深入了解一下自定义函数的功能。

## 自定义函数的各种功能

您可以使用自定义函数向表单添加个性化功能。 这些函数支持各种功能，例如使用特定字段、使用全局字段或缓存。 这种灵活性允许您根据组织的要求自定义表单。

### 自定义函数中的字段和全局范围对象 {#support-field-and-global-objects}

字段对象是指表单中的单个组件或元素，例如文本字段和复选框。 全局对象包含只读变量，例如表单实例、目标字段实例以及在自定义函数中修改表单的方法。

>[!NOTE]
>
> 此 `param {scope} globals` 必须是最后一个参数，且不会显示在自适应表单的规则编辑器中。

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

让我们了解自定义函数如何在 `Contact Us` 使用不同用例的表单。

![联系我们表单](/help/forms/assets/contact-us-form.png)

#### 使用SetProperty规则显示面板

在自定义函数中添加以下代码，如 [create-custom-function](#create-custom-function) 部分，将表单字段设置为 `Required`.

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * 您可以使用中的可用属性配置字段属性 `[form-path]/jcr:content/guideContainer.model.json`.
> * 使用对表单进行的修改 `setProperty` globals对象的方法本质上是异步的，在执行自定义函数期间不会反映出来。

在此示例中，验证 `personaldetails` 单击按钮时会出现面板。 如果在面板、其他面板、 `feedback` 面板中，单击按钮后会变为可见。

让我们为 `Next` 按钮，用于验证 `personaldetails` 面板并将 `feedback`  用户单击 `Next` 按钮。

![设置属性](/help/forms/assets/custom-function-set-property.png)

请参阅下图以演示 `personaldetails` 单击 `Next` 按钮。 如果 `personaldetails` 经过验证， `feedback` 面板将变为可见。

![设置属性表单预览](/help/forms/assets/set-property-form-preview.png)

如果的字段中出现错误 `personaldetails` 面板中，单击 `Next` 按钮，以及 `feedback` 面板将保持不可见。

![设置属性表单预览](/help/forms/assets/set-property-panel.png)


#### 验证字段。

在自定义函数中添加以下代码，如 [create-custom-function](#create-custom-function) 部分，以验证字段。

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> 如果未在中传递参数 `validate()` 函数中，它验证表单。

在此示例中，自定义验证模式应用于 `contact` 字段。 用户需要输入以开头的电话号码 `10` 后接 `8` 数字。 如果用户输入的电话号码开头不是 `10` 或包含多于 `8` 数字，单击按钮时将显示验证错误消息：

![电子邮件地址验证模式](/help/forms/assets/custom-function-validation-pattern.png)

现在，下一步是为创建规则 `Next` 验证 `contact` 字段单击。

![验证模式](/help/forms/assets/custom-function-validate.png)

请参阅下图以演示，如果用户输入的电话号码开头不是 `10`，则字段级别会显示一条错误消息：

![电子邮件地址验证模式](/help/forms/assets/custom-function-validate-error-message.png)

如果用户输入有效的电话号码和 `personaldetails` 面板已经过验证， `feedback` 屏幕上会显示以下面板：

![电子邮件地址验证模式](/help/forms/assets/validate-form-preview-form.png)



#### 重置面板

在自定义函数中添加以下代码，如 [create-custom-function](#create-custom-function) 部分，以重置面板。

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> 如果未在中传递参数 `reset()` 函数中，它验证表单。

在此示例中， `personaldetails` 单击 `Clear` 按钮。 下一步是为创建规则 `Clear` 按钮上用于重置面板的按钮单击。

![清除按钮](/help/forms/assets/custom-function-reset-field.png)

请参阅下图以显示，如果用户单击 `clear` 按钮， `personaldetails` 面板重置：

![重置表单](/help/forms/assets/custom-function-reset-form.png)



#### 在字段级别显示自定义消息并将字段标记为无效

您可以使用 `markFieldAsInvalid()` 函数将字段定义为无效，并在字段级别设置自定义错误消息。 此 `fieldIdentifier` 值可以是 `fieldId`，或 `field qualifiedName`，或 `field dataRef`. 名为的对象的值 `option` 可以是 `{useId: true}`， `{useQualifiedName: true}`，或 `{useDataRef: true}`.
用于将字段标记为无效并设置自定义消息的语法包括：

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

在自定义函数中添加以下代码，如 [create-custom-function](#create-custom-function) 部分，以在字段级别启用自定义消息。

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

在此示例中，如果用户在“注释”文本框中输入的字符数少于15个，则会在字段级别显示自定义消息。

下一步是为创建规则 `comments` 字段：

![将字段标记为无效](/help/forms/assets/custom-function-invalid-field.png)

请观看下面的演示，了解如何在 `comments` 字段触发在字段级别显示自定义消息：

![将字段标记为无效预览表单](/help/forms/assets/custom-function-invalidfield-form.png)

如果用户在“注释”文本框中输入的字符数超过15个，则会验证该字段并提交表单：

![将字段标记为有效的预览表单](/help/forms/assets/custom-function-validfield-form.png)



#### 在提交之前更改捕获的数据

以下代码行：
`globals.functions.submitForm(globals.functions.exportData(), false);` 用于在操作后提交表单数据。
* 第一个参数是要提交的数据。
* 第二个参数表示在提交之前是否验证表单。 它是 `optional` 并设置为 `true` 默认情况下。
* 第三个理由是 `contentType` ，此选项也是可选的，默认值为 `multipart/form-data`. 其他值可以是 `application/json` 和 `application/x-www-form-urlencoded`.

在自定义函数中添加以下代码，如 [create-custom-function](#create-custom-function) 部分，在服务器上提交操作数据：

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

在此示例中，如果用户将 `comments` 文本框为空， `NA` 在提交表单时提交到服务器。

现在，为创建规则 `Submit` 提交数据的按钮：

![提交数据](/help/forms/assets/custom-function-submit-data.png)

请参阅图示 `console window` 以下说明，如果用户离开 `comments` 文本框为空，则值为 `NA` 在服务器上提交：

![在控制台窗口中提交数据](/help/forms/assets/custom-function-submit-data-form.png)

您还可以检查控制台窗口以查看提交到服务器的数据：

![控制台窗口中的Inspect数据](/help/forms/assets/custom-function-submit-data-console-data.png)



#### 覆盖自适应表单提交成功和错误消息

添加以下代码行，如 [create-custom-function](#create-custom-function) 部分，自定义表单提交的提交或失败消息，并在模式框中显示表单提交消息：

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

在此示例中，当用户使用 `customSubmitSuccessHandler` 和 `customSubmitErrorHandler` 自定义函数中，成功和失败消息会以模式显示。 JavaScript函数 `showModal(type, message)` 用于在屏幕上动态创建和显示模式对话框。

现在，为成功的表单提交创建规则：

![表单提交成功](/help/forms/assets/form-submission-success.png)

请参阅下图以演示成功提交表单后，成功消息将以模式显示：

![表单提交成功消息](/help/forms/assets/form-submission-success-message.png)

同样，让我们为失败的表单提交创建规则：

![表单提交失败](/help/forms/assets/form-submission-fail.png)

请参阅下图以演示，当表单提交失败时，将以模式模式显示错误消息：

![表单提交失败消息](/help/forms/assets/form-submission-fail-message.png)

要以默认方式显示表单提交成功和失败，请 `Default submit Form Success Handler` 和 `Default submit Form Error Handler` 函数开箱即用。

如果自定义提交处理程序无法按预期在现有AEM项目或表单中执行，请参阅 [故障排除](#troubleshooting) 部分。

<!--


#### Use Case:  Perform actions in a specific instance of the repeatable panel 

Rules created using the visual rule editor on a repeatable panel apply to the last instance of the repeatable panel. To write a rule for a specific instance of the repeatable panel, we can use a custom function.

Let's create a form to collect information about travelers heading to a destination. A traveler panel is added as a repeatable panel, where the user can add details for 5 travelers using the Add button.

Add the following line of code as explained in the [create-custom-function](#create-custom-function) section, to perform actions in a specific instance of the repeatable panel, other than the last one:

```javascript

/**
* @name hidePanelInRepeatablePanel
* @param {scope} globals
*/
function hidePanelInRepeatablePanel(globals)
{    
    var repeatablePanel = globals.form.travelerinfo;
    // hides a panel inside second instance of repeatable panel
    globals.functions.setProperty(repeatablePanel[1].traveler, {visible : false});
}  

```
 
In this example, the `hidePanelInRepeatablePanel` custom function performs action in a specific instance of the repeatable panel. In the above code, `travelerinfo` represents the repeatable panel. The `repeatablePanel[1].traveler, {visible: false}` code hides the panel in the second instance of the repeatable panel. 
Let us add a button labeled `Hide` to add a rule to hide a specific panel.

![Hide Panel rule](/help/forms/assets/custom-function-hidepanel-rule.png)

Refer to the video below to demonstrate that when the `Hide` is clicked, the panel in the second repeatable instance hides:




#### **Usecase**: Pre-fill the field with a value when the form loads

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to load the pre-filled value in a field when the form is initialized:

```javascript
/**
 * @name importData
 * @param {scope} globals
 */
function importData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount',200000]]));
} 
```

In the aforementioned code, the `importData` function updates the value in the `amount` textbox field when the form loads.

Let us create a rule for the `Submit` button, where the value in the `amount` textbox field changes to specified value when the form loads:

![Import Data Rule](/help/forms/assets/custom-function-import-data.png)

Refer to the screenshot below, which demonstrates that when the form loads, the value in the amount textbox is pre-filled with a specified value:

![Import Data Rule](/help/forms/assets/cg)



#### **Usecase**: Set focus on the specific field

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to set focus on the specified field when the `Submit` button is clicked.:

```javascript
/**
 * @name setFocus
 * @param {object} field
 * @param {scope} globals
 */
function setFocus(field, globals)
{
    globals.functions.setFocus(field);
}
```

Let us add a rule to the `Submit` button to set focus on the `email` field when it is clicked:

![Set Focus Rule](/help/forms/assets/custom-function-set-focus.png)

Refer to the screenshot below, which demonstrates that when the `Submit` button is clicked, the focus is set on the `email` field:

![Set Focus Rule](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> You can use the optional `$focusOption` parameter, if you want to focus on the next or previous field relative to the `email` field.

+++

+++ **Usecase**: Add or delete repeatable panel using the `dispatchEvent` property

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to add a panel when the `Add Traveler` button is clicked using the `dispatchEvent` property:

```javascript
/**
 
 * @name addInstance
 * @param {scope} globals
 */
function addInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'addInstance');
} 

```

Let us add a rule to the `Add Traveler` button to add the repeatable panel when it is clicked:

![Add Panel Rule](/help/forms/assets/custom-function-add-panel.png)

Refer to the screenshot below, which demonstrates that when the `Add Traveler` button is clicked, the traveler panel is added using the `dispatchEvent` property:

![Add Panel](/help/forms/assets/customg)

Similarly, add a button labeled `Delete Traveler` to delete a panel. Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to delete a panel when the `Delete Traveler` button is clicked using the `dispatchEvent` property:

```javascript

/**
 
 * @name removeInstance
 * @param {scope} globals
 */
function removeInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 

```
Let us add a rule to the `Delete Traveler` button to delete the repeatable panel when it is clicked:

![Delete Panel Rule](/help/forms/assets/custom-function-delete-panel.png)

Refer to the screenshot below, which demonstrates that when the `Delete Traveler` button is clicked, the traveler panel is deleted using the `dispatchEvent` property:

![Delete Panel](/help/forms/assets/customg)
-->

## 对自定义函数的缓存支持

自适应Forms在规则编辑器中检索自定义函数列表时，为自定义函数实施缓存以增强响应时间。 消息为 `Fetched following custom functions list from cache` 显示在 `error.log` 文件。

![支持缓存的自定义函数](/help/forms/assets/custom-function-cache-error.png)

如果修改了自定义函数，缓存将失效，并且会进行解析。

## 疑难解答 {#troubleshooting}

* 如果自定义提交处理程序无法按预期在现有AEM项目或表单中执行，请执行以下步骤：
   * 确保 [核心组件版本已更新至3.0.18及更高版本](https://github.com/adobe/aem-core-forms-components). 但是，对于现有AEM项目和表单，还需要执行其他步骤：

   * 对于AEM项目，用户应替换 `submitForm('custom:submitSuccess', 'custom:submitError')` 替换为 `submitForm()` 和通过Cloud Manager管道部署项目。

   * 对于现有表单，如果自定义提交处理程序无法正常运行，用户需要打开并保存 `submitForm` 规则 **提交** 按钮。 此操作替换中的现有规则 `submitForm('custom:submitSuccess', 'custom:submitError')` 替换为 `submitForm()` 在表格中。


* 如果包含自定义函数代码的JavaScript文件出错，则自定义函数将不会在自适应表单的规则编辑器中列出。 要检查自定义函数列表，您可以导航到 `error.log` 文件查找错误。 如果出现错误，自定义函数列表显示为空：

  ![错误日志文件](/help/forms/assets/custom-function-list-error-file.png)

  如果没有错误，则会获取自定义函数并显示在 `error.log` 文件。 消息为 `Fetched following custom functions list` 显示在 `error.log` 文件：

  ![使用正确的自定义函数创建错误日志文件](/help/forms/assets/custom-function-list-fetched-in-error.png)

## 注意事项

* 此 `parameter type` 和 `return type` 不支持 `None`.

* 自定义函数列表中不支持的函数包括：
   * 生成器函数
   * 异步/等待函数
   * 方法定义
   * 类方法
   * 默认参数
   * Rest参数

## 另请参阅 {#see-also}

{{see-also}}


