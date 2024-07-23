---
title: 本文介绍了基于核心组件的自适应表单的规则编辑器用户界面。
description: 自适应Forms规则编辑器帮助用户编写规则，以根据条件、用户输入和交互触发操作。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
source-git-commit: 780c68f0c21ef94ff6a73ce991370100b1a88db9
workflow-type: tm+mt
source-wordcount: '2298'
ht-degree: 0%

---


# 基于核心组件的自适应Forms的规则编辑器用户界面

基于核心组件的自适应Forms的规则编辑器用户界面增强了Adobe Experience Manager (AEM)中的表单创建过程。 它使商业用户和开发人员能够通过编写规则来根据预定义的条件、用户输入和交互触发操作，从而将动态行为和复杂逻辑实施到表单中。 此功能支持现代JavaScript功能（包括ES10功能），并提供了一个直观的可视化编辑器，从而简化了规则编写过程。
规则编辑器有助于简化表单填写体验，确保准确性和效率。 它允许验证或重置面板和表单，并执行自定义函数以计算表单对象的值。 由于规则编辑器用户界面支持嵌套条件和能够调用表单数据模型服务，因此它是创建响应式、用户友好和自适应表单的关键组件。

## 了解规则编辑器用户界面 {#understanding-the-rule-editor-user-interface}

规则编辑器提供了一个全面而简单的用户界面来编写和管理规则。 您可以在创作模式下从自适应表单中启动规则编辑器用户界面。

要启动规则编辑器用户界面，请执行以下操作：

1. 在创作模式下打开自适应表单。
1. 选择要为其编写规则的表单对象，然后在组件工具栏中选择![edit-rules](assets/edit-rules-icon.svg)。 此时将显示规则编辑器用户界面。

   ![create-rules](assets/create-rules.png)

   此视图中列出了选定表单对象上的任何现有规则。 有关管理现有规则的信息，请参阅[管理规则](rule-editor.md#p-manage-rules-p)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以编写新规则。 默认情况下，首次启动规则编辑器时会打开规则编辑器用户界面的可视化编辑器。

   ![规则编辑器UI](assets/rule-editor-ui.png)

让我们详细了解一下规则编辑器UI的每个组件。

### A.组件规则显示 {#a-component-rule-display}

显示自适应表单对象的标题（通过自适应表单对象启动规则编辑器）和当前选定的规则类型。 在上述示例中，规则编辑器从标题为问题1的自适应表单对象启动，并且选定的规则类型为何时。

### B.表单对象和功能 {#b-form-objects-and-functions-br}

规则编辑器用户界面左侧的窗格包含两个选项卡 — **[!UICONTROL Forms对象]**&#x200B;和&#x200B;**[!UICONTROL 函数]**。

“表单对象”选项卡显示自适应表单中包含的所有对象的分层视图。 它显示对象的标题和类型。 在编写规则时，可以将表单对象拖放到规则编辑器中。 在将对象或函数拖放到占位符中时，在创建或编辑规则时，占位符会自动采用相应的值类型。

应用了一个或多个有效规则的表单对象将标有绿点。 如果应用于表单对象的任意规则无效，则表单对象将标有黄点。

“函数”选项卡包含一组内置函数，例如“总和”、“最小值”、“最大值”、“平均值”、“数目”和“验证表单”。 您可以使用这些函数计算可重复面板和表格行中的值，并在编写规则时在操作和条件语句中使用它们。 但是，您也可以创建自定义函数。

图中显示了一些函数列表：

![函数选项卡](assets/functions.png)

>[!NOTE]
>
>您可以在Forms的“对象”和“函数”选项卡中对对象和函数名称和标题执行文本搜索。

在表单对象的左树中，您可以选择表单对象以显示应用于每个对象的规则。 您不仅可以浏览各种表单对象的规则，还可以复制粘贴表单对象之间的规则。 有关详细信息，请参阅[复制粘贴规则](rule-editor.md#p-copy-paste-rules-p)。

### C.表单对象和功能切换 {#c-form-objects-and-functions-toggle-br}

点按切换按钮可切换表单对象和函数窗格。

### D.可视规则编辑器 {#visual-rule-editor}

可视规则编辑器是规则编辑器用户界面的可视编辑器模式中用于编写规则的区域。 它允许您选择规则类型并相应地定义条件和操作。 在规则中定义条件和操作时，您可以从表单对象和函数窗格中拖放表单对象和函数。

有关使用可视规则编辑器的详细信息，请参阅[编写规则](rule-editor.md#p-write-rules-p)。
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and conversely, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E.完成和取消按钮 {#done-and-cancel-buttons}

**[!UICONTROL Done]**&#x200B;按钮用于保存规则。 您可以保存不完整的规则。 但是，不完整部分无效，因此不会运行。 当您下次从同一表单对象启动规则编辑器时，会列出表单对象中已保存的规则。 您可以在该视图中管理现有规则。 有关详细信息，请参阅[管理规则](rule-editor.md#p-manage-rules-p)。

使用&#x200B;**[!UICONTROL 取消]**&#x200B;按钮可放弃对规则所做的任何更改并关闭规则编辑器。

## 写入规则 {#write-rules}

您可以使用可视规则编辑器<!-- or the code editor. When you launch the rule editor the first time, it opens in the visual editor mode. You can switch to the code editor mode and write rules. However, if you write or modify a rule in code editor, you cannot switch to the visual editor for that rule unless you clear the code editor. When you launch the rule editor next time, it opens in the mode that you used last to create rule. -->编写规则

我们首先看一下如何使用可视编辑器编写规则。

+++

+++ 使用可视编辑器{#using-visual-editor}

让我们了解如何使用以下示例表单在可视编辑器中创建规则。

![Create-rule-example](assets/create-rule-example.png)

示例贷款申请表中的“贷款要求”部分要求申请人指定其婚姻状况、工资，如果已婚，还须指定其配偶的工资。 根据用户输入，规则将计算贷款资格金额，并显示在贷款资格字段中。 应用以下规则来实施方案：

* 配偶的“薪金”字段仅在婚姻状况为已婚时显示。
* 贷款资格金额为工资总额的50%。

要编写规则，请执行以下步骤：

1. 首先，根据用户为“婚姻状况”单选按钮选择的选项，编写规则以控制“配偶薪金”字段的可见性。

   以创作模式打开贷款申请表单。 选择&#x200B;**[!UICONTROL 婚姻状况]**&#x200B;组件并选择![编辑 — 规则](assets/edit-rules-icon.svg)。 接下来，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以启动规则编辑器。

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1-cc.png)

   在启动规则编辑器时，默认情况下会选中When规则。 此外，从中启动规则编辑器的表单对象（在本例中为“婚姻状况”）在When语句中指定。

   虽然不能更改或修改所选对象，但可以使用如下所示的规则下拉列表选择其他规则类型。 如果要在其他对象上创建规则，请选择“取消”以退出规则编辑器，然后从所需的表单对象中再次启动该编辑器。

1. 选择&#x200B;**[!UICONTROL 选择状态]**&#x200B;下拉列表并选择&#x200B;**[!UICONTROL 等于]**。 出现&#x200B;**[!UICONTROL 输入字符串]**&#x200B;字段。

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2-cc.png)

1. 在规则的&#x200B;**[!UICONTROL 输入字符串]**&#x200B;字段中，从下拉菜单中选择&#x200B;**已婚**。

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4-cc.png)

   您已将条件定义为`When Marital Status is equal to Married`。 接下来，定义此条件为True时要执行的操作。

1. 在Then语句中，从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 显示]**。

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5-cc.png)

1. 从“表单对象”选项卡中拖放&#x200B;**[!UICONTROL 放置对象上的**[!UICONTROL  Warbant Salary ]**字段，或选择此处]**&#x200B;字段。 或者，选择&#x200B;**[!UICONTROL Drop对象或选择此处]**&#x200B;字段，然后从弹出菜单中选择&#x200B;**[!UICONTROL Berpha Salary]**&#x200B;字段，该字段列出了表单中的所有表单对象。

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6-cc.png)

   接下来，定义此条件为False时要执行的操作。
1. 单击&#x200B;**[!UICONTROL 添加其他部分]**&#x200B;为&#x200B;**[!UICONTROL 配偶薪金]**&#x200B;字段添加其他条件，以防您选择婚姻状况作为单身。

   ![when-else](assets/when-else.png)


1. 在Else语句中，从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 隐藏]**。
   ![when-else](assets/when-else-1.png)

1. 从“表单对象”选项卡中拖放&#x200B;**[!UICONTROL 放置对象上的**[!UICONTROL  Warbant Salary ]**字段，或选择此处]**&#x200B;字段。 或者，选择&#x200B;**[!UICONTROL Drop对象或选择此处]**&#x200B;字段，然后从弹出菜单中选择&#x200B;**[!UICONTROL Berpha Salary]**字段，该字段列出了表单中的所有表单对象。
   ![when-else](assets/when-else-2.png)

   规则在规则编辑器中如下所示。

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7-cc.png)

1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存规则。

<!--
1. Repeat steps 1 through 5 to define another rule to hide the Spouse Salary field if the marital Status is Single. The rule appears as follows in the rule editor.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8-cc.png) -->

>[!NOTE]
>
> 或者，您可以在“配偶薪金”字段上编写显示规则，而不是“婚姻状况”字段上的显示规则，以实施相同的行为。

![write-rules-visual-editor-9](assets/write-rules-visual-editor-9-cc.png)

1. 接下来，编写规则以计算贷款资格金额（占总薪金的50%），并在“贷款资格”字段中显示。 若要获得此结果，请在“贷款资格”字段中创建&#x200B;**[!UICONTROL 设置值]**。

   在创作模式下，选择&#x200B;**[!UICONTROL 贷款资格]**&#x200B;字段并选择![编辑规则](assets/edit-rules-icon.svg)。 接下来，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以启动规则编辑器。

1. 从规则下拉列表中选择&#x200B;**[!UICONTROL 设置规则值]**。

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10-cc.png)

1. 选择&#x200B;**[!UICONTROL 选择选项]**&#x200B;并选择&#x200B;**[!UICONTROL 数学表达式]**。 用于编写数学表达式的字段打开。

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11-cc.png)

1. 在表达式字段中：

   * 从Forms的“对象”选项卡中，选择或拖放第一个&#x200B;**[!UICONTROL 放置对象中的**[!UICONTROL  Salary ]**字段，或选择此处]**&#x200B;字段。

   * 从&#x200B;**[!UICONTROL 选择运算符]**&#x200B;字段中选择&#x200B;**[!UICONTROL 加号]**。

   * 从Forms的“对象”选项卡中选择或拖放另一个&#x200B;**[!UICONTROL 拖放对象中的**[!UICONTROL  Berphor Salary ]**字段，或选择此处]**&#x200B;字段。

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. 接下来，在表达式字段周围高亮显示的区域中选择，然后选择&#x200B;**[!UICONTROL 扩展表达式]**。

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13-cc.png)

   在扩展表达式字段中，从&#x200B;**[!UICONTROL Select Operator]**&#x200B;字段中选择&#x200B;**[!UICONTROL 除以]**&#x200B;并从&#x200B;**[!UICONTROL Select Option]**&#x200B;字段中选择&#x200B;**[!UICONTROL Number]**。 然后在数字字段中指定&#x200B;**[!UICONTROL 2]**。

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14-cc.png)

   >[!NOTE]
   >
   >您可以从“选择选项”字段中使用组件、函数、数学表达式和属性值来创建复杂表达式。

   接下来，创建一个条件，当该条件返回True时，表达式将执行。

1. 选择&#x200B;**[!UICONTROL 添加条件]**&#x200B;以添加When语句。

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15-cc.png)

   在When语句中：

   * 从Forms对象选项卡中选择或拖放第一个&#x200B;**[!UICONTROL 放置对象中的**[!UICONTROL &#x200B;婚姻状况&#x200B;]**字段，或选择此处]**&#x200B;字段。

   * 从&#x200B;**[!UICONTROL Select Operator]**&#x200B;字段中选择&#x200B;**[!UICONTROL 等于]**。

   * 在其他&#x200B;**[!UICONTROL 放置对象中选择String或选择此处]**&#x200B;字段，并在&#x200B;**[!UICONTROL 输入字符串]**&#x200B;字段中指定&#x200B;**[!UICONTROL 已婚]**。

   规则编辑器中的结果如下所示。  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16-cc.png)

1. 选择&#x200B;**[!UICONTROL 完成]**。 保存规则。

1. 重复步骤7至14，定义另一条规则，以计算婚姻状况为“单身”的贷款资格。 规则在规则编辑器中如下所示。

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17-cc.png)

或者，您可以使用设置值规则在您创建的When规则中计算贷款资格，以显示 — 隐藏“配偶薪金”字段。 当“婚姻状况”为“单身”时，生成的合并规则将在规则编辑器中显示如下。

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18-cc.png)

您可以使用Else条件编写组合规则，以控制“配偶薪金”字段的可见性，并在婚姻状况为“已婚”时计算贷款资格。

![write-rules-visual-editor-19](assets/write-rules-visual-editor-19-cc.png)

+++


<!-- ### Using code editor {#using-code-editor}

Users added to the forms-power-users group can use code editor. The rule editor auto generates the JavaScript code for any rule you create using visual editor. You can switch from visual editor to the code editor to view the generated code. However, if you modify the rule code in the code editor, you cannot switch back to the visual editor. If you prefer writing rules in code editor rather than visual editor, you can write rules afresh in the code editor. The visual-code editors switcher helps you switch between the two modes.

The code editor JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. These expressions return values of certain types. For the complete list of Adaptive Forms classes, events, objects, and public APIs, see [JavaScript Library API reference for Adaptive Forms](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

For more information about guidelines to write rules in the code editor, see [Adaptive Form Expressions](adaptive-form-expressions.md).

While writing JavaScript code in the rule editor, the following visual cues help you with the structure and syntax:

* Syntax highlights

* Auto Indentation

* Hints and suggestions for Form objects, functions, and their properties

* Auto completion of form component names and common JavaScript functions

![javascriptruleeditor](assets/javascriptruleeditor.png)
-->

#### 规则编辑器中的自定义函数 {#custom-functions}

除了在&#x200B;**函数输出**&#x200B;下列出的现成函数（如&#x200B;*总和*）之外，您还可以在规则编辑器中使用自定义函数。 规则编辑器支持脚本和自定义函数的JavaScript ECMAScript 2019语法。 有关创建自定义函数的说明，请参阅文章[自适应Forms中的自定义函数](/help/forms/create-and-use-custom-functions.md)。

<!--

Ensure that the function you write is accompanied by the `jsdoc` above it. Adaptive Form supports the various [JavaScript annotations for custom functions](/help/forms/create-and-use-custom-functions.md#js-annotations).

For more information, see [jsdoc.app](https://jsdoc.app/).

Accompanying `jsdoc` is required:

* If you want custom configuration and description
* Because there are multiple ways to declare a function in `JavaScript,` and comments let you keep a track of the functions.

Supported `jsdoc` tags:

* **Private**
  Syntax: `@private`
  A private function is not included as a custom function.

* **Name**
  Syntax: `@name funcName <Function Name>`
  Alternatively `,` you can use: `@function funcName <Function Name>` **or** `@func` `funcName <Function Name>`.
  `funcName` is the name of the function (no spaces allowed).
  `<Function Name>` is the display name of the function.

* **Parameter**
  Syntax: `@param {type} name <Parameter Description>`
  Alternatively, you can use: `@argument` `{type} name <Parameter Description>` **or** `@arg` `{type}` `name <Parameter Description>`.
  Shows parameters used by the function. A function can have multiple parameter tags, one tag for each parameter in the order of occurrence.
  `{type}` represents parameter type. Allowed parameter types are:

    1. string
    2. number
    3. boolean
    4. scope
    5. string[]
    6. number[]
    7. boolean[]
    8. date
    9. date[]
    10. array
    11. object

   `scope` refers to a special globals object which is provided by forms runtime. It must be the last parameter and is not be visible to the user in the rule editor. You can use scope to access readable form and field proxy object to read properties, event which triggered the rule and a set of functions to manipulate the form.

   `object` type is used to pass readable field object in parameter to a custom function instead of passing the value.

   All parameter types are categorized under one of the above. None is not supported. Ensure that you select one of the types above. Types are not case-sensitive. Spaces are not allowed in the parameter name.  Parameter description can have multiple words.

* **Optional Parameter**
Syntax: `@param {type=} name <Parameter Description>` 
Alternatively, you can use: `@param {type} [name] <Parameter Description>`
By default all parameters are mandatory. You can mark a parameter optional by adding `=` in type of the parameter or by putting param name in square brackets.
   
   For example, let us declare `Input1` as optional parameter:
    * `@param {type=} Input1`
    * `@param {type} [Input1]`

* **Return Type**
  Syntax: `@return {type}`
  Alternatively, you can use `@returns {type}`.
  Adds information about the function, such as its objective.
  {type} represents the return type of the function. Allowed return types are:

    1. string
    2. number
    3. boolean
    4. string[]
    5. number[]
    6. boolean[]
    7. date
    8. date[]
    9. array
    10. object

  All other return types are categorized under one of the above. None is not supported. Ensure that you select one of the types above. Return types are not case-sensitive.

**Adding a custom function**

For example, you want to add a custom function which calculates area of a square. Side length is the user input to the custom function, which is accepted using a numeric box in your form. The calculated output is displayed in another numeric box in your form. To add a custom function, you have to first create a client library, and then add it to the CRX repository.

To create a client library and add it in the CRX repository, perform the following steps:

1. Create a client library. For more information, see [Using Client-Side Libraries](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).
2. In CRXDE, add a property `categories`with string type value as `customfunction` to the `clientlib` folder.

   >[!NOTE]
   >
   >`customfunction`is an example category. You can choose any name for the category you create in the `clientlib`folder.

After you have added your client library in the CRX repository, use it in your Adaptive Form. It lets you use your custom function as a rule in your form. To add the client library in your Adaptive Form, perform the following steps:

1. Open your form in edit mode.
   To open a form in edit mode, select a form and select **[!UICONTROL Open]**.
1. In the edit mode, select a component, then select ![field-level](assets/select_parent_icon.svg) &gt; **[!UICONTROL Adaptive Form Container]**, and then select ![cmppr](assets/configure-icon.svg).
1. In the sidebar, under Name of Client Library, add your client library. ( `customfunction` in the example.)

   ![Adding the custom function client library](assets/clientlib.png)

1. Select the input numeric box, and select ![edit-rules](assets/edit-rules-icon.svg) to open the rule editor.
1. Select **[!UICONTROL Create Rule]**. Using options shown below, create a rule to save the squared value of the input in the Output field of your form.

   [![Using custom functions to create a rule](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)
  
1. Select **[!UICONTROL Done]**. Your custom function is added.

   >[!NOTE]
   >
   > To invoke a form data model from rule editor using custom functions, [see here](/help/forms/using-form-data-model.md#invoke-services-in-adaptive-forms-using-rules-invoke-services). 

#### Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>Ensure that you use `jsdoc` for every custom function. Although `jsdoc`comments are encouraged, include an empty `jsdoc`comment to mark your function as custom function. It enables default handling of your custom function.
-->

## 管理规则 {#manage-rules}

选择表单对象并选择![edit-rules1](assets/edit-rules-icon.svg)时，会列出该对象上的任何现有规则。 您可以查看标题并预览规则摘要。 此外，您还可以通过UI展开和查看完整的规则摘要、更改规则的顺序、编辑规则以及删除规则。

![列表规则](assets/list-rules-cc.png)

您可以对规则执行以下操作：

* **展开/折叠**：规则列表中的“内容”列显示规则内容。 如果整个规则内容在默认视图中不可见，请选择![expand-rule-content](assets/Smock_ChevronDown.svg)以展开它。

* **重新排序**：您创建的任何新规则都栈叠在规则列表的底部。 规则将从上到下执行。 顶部的规则先执行，然后是相同类型的其他规则。 例如，如果您分别将When、Show、Enable和When规则放在顶部的第一个、第二个、第三个和第四个位置，则顶部的何时规则会首先执行，然后是第四个位置的When规则。 然后，执行显示和启用规则。
您可以通过点按![排序规则](assets/sort-rules.svg)来更改规则的顺序，也可以将其拖放到列表中的所需顺序。

* **编辑**：要编辑规则，请选中规则标题旁边的复选框。 将显示用于编辑和删除规则的选项。 选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以在规则编辑器中打开选定的规则。

* **删除**：要删除规则，请选择该规则并选择&#x200B;**[!UICONTROL 删除]**。

* **启用/禁用**：当必须临时暂停使用规则时，您可以选择一个或多个规则，并在“操作”工具栏中选择&#x200B;**[!UICONTROL 禁用]**&#x200B;以禁用它们。 如果禁用某个规则，则它不会在运行时执行。 要启用已禁用的规则，可以选择该规则并选择操作工具栏中的启用。 规则的状态列显示规则是启用还是禁用。

![禁用规则](assets/disablerule-cc.png)

## 复制粘贴规则 {#copy-paste-rules}

您可以将规则从一个字段复制粘贴到其他类似字段，以节省时间。

要复制粘贴规则，请执行以下操作：

1. 选择要从中复制规则的表单对象，然后在组件工具栏中选择![编辑规则](assets/edit-rules-icon.svg)。 此时将显示规则编辑器用户界面，其中选定了表单对象，并显示现有规则。

   ![复制规则](assets/copyrule.png)

   有关管理现有规则的信息，请参阅[管理规则](rule-editor.md#p-manage-rules-p)。

1. 选中规则标题旁边的复选框，将显示用于管理规则的选项。 选择&#x200B;**[!UICONTROL 复制]**。

   ![复制规则2](assets/copyrule2.png)

1. 选择要将规则粘贴到的其他表单对象，然后选择&#x200B;**[!UICONTROL 粘贴]**。 此外，您可以编辑规则以对其进行更改。

   >[!NOTE]
   >
   >仅当表单对象支持复制的规则事件时，才能将规则粘贴到另一个表单对象。 例如，按钮支持click事件。 您可以将包含点击事件的规则粘贴到按钮，但不能粘贴到复选框。

1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存规则。

## 后续步骤

要了解自适应表单的规则编辑器中的各种运算符类型和事件，请参阅自适应表单的规则编辑器中的[可用运算符类型和事件](/help/forms/rule-editor-core-components-events-operators.md)一文。


## 另请参阅

{{see-also-rule-editor}}