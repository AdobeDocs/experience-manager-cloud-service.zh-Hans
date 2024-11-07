---
title: 本文概述了基于核心组件的自适应表单中自定义函数的各种用例。
description: 本文概述了基于核心组件的自适应表单中自定义函数的各种用例。 自定义函数在规则编辑器中用于创建表单的自定义规则。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: df92b91e-f3b0-4a08-bd40-e99edc9a50a5
source-git-commit: 88b9686a1ceec6729d9657d4bb6f458d9c411065
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 0%

---

# 开发和使用自定义函数的示例

本文提供了基于核心组件的自适应表单的自定义函数的详细示例，提供了有关在各种场景中有效实施这些函数的宝贵见解。 自定义函数在AEM Forms的规则编辑器中使用，使开发人员能够定义和控制控制表单行为的逻辑。
本文探讨了自定义函数的不同实现，展示了如何使用它们来定制表单以满足特定要求并增强整体功能。

## 使用自定义函数填充下拉列表选项

核心组件中的规则编辑器不支持&#x200B;**Set Options**&#x200B;属性在运行时动态填充下拉列表选项。 但是，您可以使用自定义函数填充下拉列表选项，这允许您根据特定逻辑检索选项。 自定义函数在填充下拉列表选项的方式和时间方面提供了更大的灵活性和控制力，增强了用户体验。

要使用自定义函数填充下拉列表选项，请按照[create-custom-function](/help/forms/custom-function-core-component-create-function.md)部分中的说明添加以下代码：


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

在上述代码中，`setEnums`用于设置`enum`属性，`setEnumNames`用于设置下拉列表的`enumNames`属性。

让我们为`Next`按钮创建一个规则，该规则在用户单击`Next`按钮时设置下拉列表选项的值：

![下拉列表选项](/help/forms/assets/drop-down-list-options.png)

请参阅下图以演示单击“显示”按钮时下拉列表的选项设置位置：

![规则编辑器中的下拉选项](/help/forms/assets/drop-down-option-rule-editor.png)

## 使用`SetProperty`规则显示面板

让我们了解自定义函数如何在`Contact Us`表单的帮助下使用字段和全局对象。

![与我们联系表单](/help/forms/assets/contact-us-form.png)

将以下代码添加到[create-custom-function](/help/forms/custom-function-core-component-create-function.md)部分中说明的自定义函数中，以将表单字段设置为`Required`。

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
> * 您可以使用位于`[form-path]/jcr:content/guideContainer.model.json`中的可用属性配置字段属性。
> * 使用Globals对象的`setProperty`方法对该表单进行的修改是异步的，在执行自定义函数期间不会反映这些修改。

在此示例中，`personaldetails`面板的验证是在单击按钮时进行的。 如果在面板中未检测到错误，则单击按钮后，另一个面板（`feedback`面板）将变为可见。

让我们为`Next`按钮创建一个规则，该规则将验证`personaldetails`面板，并在用户单击`Next`按钮时使`feedback`面板可见。

![设置属性](/help/forms/assets/custom-function-set-property.png)

请参阅下图以演示单击`Next`按钮时验证`personaldetails`面板的位置。 如果`personaldetails`中的所有字段都已验证，`feedback`面板将变为可见。

![设置属性表单预览](/help/forms/assets/set-property-form-preview.png)

如果`personaldetails`面板的字段中存在错误，则单击`Next`按钮时会在字段级别显示这些错误，并且`feedback`面板将保持不可见。

![设置属性表单预览](/help/forms/assets/set-property-panel.png)

## 验证字段

让我们了解自定义函数如何在`Contact Us`表单的帮助下使用字段和全局对象来验证字段。

按照[create-custom-function](/help/forms/custom-function-core-component-create-function.md)部分中的说明，在自定义函数中添加以下代码以验证字段。

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
> 如果未在`validate()`函数中传递任何参数，它将验证表单。

在此示例中，自定义验证模式应用于`contact`字段。 用户需要输入以`10`开头后接`8`位数的电话号码。 如果用户输入的电话号码不以`10`开头或包含多或少`8`位数，则单击该按钮时将显示验证错误消息：

![电子邮件地址验证模式](/help/forms/assets/custom-function-validation-pattern.png)

现在，下一步是为`Next`按钮创建一个规则，以验证单击按钮时的`contact`字段。

![验证模式](/help/forms/assets/custom-function-validate.png)

请参阅下图以演示，如果用户输入的电话号码不是以`10`开头，则在字段级别将显示错误消息：

![电子邮件地址验证模式](/help/forms/assets/custom-function-validate-error-message.png)

如果用户输入有效的电话号码并且验证`personaldetails`面板中的所有字段，屏幕上会显示`feedback`面板：

![电子邮件地址验证模式](/help/forms/assets/validate-form-preview-form.png)

## 重置面板

让我们了解自定义函数如何在`Contact Us`表单的帮助下使用字段和全局对象重置字段。

按照[create-custom-function](/help/forms/custom-function-core-component-create-function.md)部分中的说明，在自定义函数中添加以下代码以重置面板。

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
> 如果未在`reset()`函数中传递任何参数，它将验证表单。

在此示例中，`personaldetails`面板在单击`Clear`按钮时重置。 下一步是为`Clear`按钮创建一个规则，该规则将在单击按钮时重置面板。

![清除按钮](/help/forms/assets/custom-function-reset-field.png)

请参阅下图以显示，如果用户单击`clear`按钮，`personaldetails`面板将重置：

![重置表单](/help/forms/assets/custom-function-reset-form.png)

## 在字段级别显示自定义消息并将字段标记为无效

让我们了解自定义函数如何在`Contact Us`表单的帮助下使用字段和全局对象在字段级别显示自定义消息并将字段标记为无效。

您可以使用`markFieldAsInvalid()`函数将字段定义为无效，并在字段级别设置自定义错误消息。 `fieldIdentifier`值可以是`fieldId`、`field qualifiedName`或`field dataRef`。 名为`option`的对象的值可以是`{useId: true}`、`{useQualifiedName: true}`或`{useDataRef: true}`。
用于将字段标记为无效并设置自定义消息的语法包括：

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

按照[create-custom-function](/help/forms/custom-function-core-component-create-function.md)部分中的说明，在自定义函数中添加以下代码，以在字段级别启用自定义消息。

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

下一步是为`comments`字段创建规则：

![将字段标记为无效](/help/forms/assets/custom-function-invalid-field.png)

请参阅下面的演示，说明在`comments`字段中输入负反馈会触发字段级别的自定义消息显示：

![将字段标记为无效的预览表单](/help/forms/assets/custom-function-invalidfield-form.png)

如果用户在“注释”文本框中输入的字符数超过15个，则会验证该字段并提交表单：

![将字段标记为有效的预览表单](/help/forms/assets/custom-function-validfield-form.png)

## 将更改的数据提交到服务器

让我们了解自定义函数如何在`Contact Us`表单的帮助下使用字段和全局对象在服务器上提交操作数据。

以下代码行：
`globals.functions.submitForm(globals.functions.exportData(), false);`用于在操作后提交表单数据。
* 第一个参数是要提交的数据。
* 第二个参数表示在提交之前是否验证表单。 它是`optional`，默认设置为`true`。
* 第三个参数是提交的`contentType`，该参数也是可选的，默认值是`multipart/form-data`。 其他值可以是`application/json`和`application/x-www-form-urlencoded`。

按照[create-custom-function](/help/forms/custom-function-core-component-create-function.md)部分中的说明，在自定义函数中添加以下代码，以在服务器上提交操作数据：

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

在此示例中，如果用户将`comments`文本框留空，则`NA`在提交表单时提交给服务器。

现在，为提交数据的`Submit`按钮创建一个规则：

![提交数据](/help/forms/assets/custom-function-submit-data.png)

请参阅以下`console window`的图示，以演示如果用户将`comments`文本框留空，则在服务器上提交值为`NA`：

![在控制台窗口提交数据](/help/forms/assets/custom-function-submit-data-form.png)

您还可以检查控制台窗口以查看提交到服务器的数据：

在控制台窗口![Inspect数据](/help/forms/assets/custom-function-submit-data-console-data.png)

## 覆盖表单提交成功和错误处理程序

让我们了解自定义函数如何在`Contact Us`表单的帮助下使用字段和全局对象覆盖提交处理程序。

添加下面一行代码（如[create-custom-functionas](/help/forms/custom-function-core-component-create-function.md)部分中所述），以自定义表单提交的提交或失败消息，并在模式框中显示表单提交消息：

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

在此示例中，当用户使用`customSubmitSuccessHandler`和`customSubmitErrorHandler`自定义函数时，成功和失败消息将以模式显示。 JavaScript函数`showModal(type, message)`用于在屏幕上动态创建和显示模式对话框。

现在，为成功的表单提交创建规则：

![表单提交成功](/help/forms/assets/form-submission-success.png)

请参阅下图以演示成功提交表单后，成功消息将以模式显示：

![表单提交成功消息](/help/forms/assets/form-submission-success-message.png)

同样，让我们为失败的表单提交创建规则：

![表单提交失败](/help/forms/assets/form-submission-fail.png)

请参阅下图以演示，当表单提交失败时，将以模式模式显示错误消息：

![表单提交失败消息](/help/forms/assets/form-submission-fail-message.png)

若要以默认方式显示表单提交成功和失败，`Default submit Form Success Handler`和`Default submit Form Error Handler`函数是现成可用的。

如果自定义提交处理程序无法按预期在现有AEM项目或表单中执行，请参阅[疑难解答](#troubleshooting)部分。

## 在可重复面板的特定实例中执行操作

使用可重复面板上的可视规则编辑器创建的规则将应用于可重复面板的最后一个实例。 要为可重复面板的特定实例编写规则，我们可以使用自定义函数。

让我们创建另一个表单作为`Booking Form`，以收集有关前往目的地的旅客的信息。 将旅客面板添加为可重复面板，用户可以在其中使用`Add Traveler`按钮添加5名旅客的详细信息。

![旅行者信息](/help/forms/assets/traveler-info-form.png)

添加下面一行代码（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)部分中所述），以在可重复面板的特定实例中执行操作，而不是最后一个实例：

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

在此示例中，`hidePanelInRepeatablePanel`自定义函数在可重复面板的特定实例中执行操作。 在上述代码中，`travelerinfo`表示可重复面板。 `repeatablePanel[1].traveler, {visible: false}`代码在可重复面板的第二个实例中隐藏面板。

让我们添加标记为`Hide`的按钮并添加规则以隐藏可重复面板的第二个实例。

![隐藏面板规则](/help/forms/assets/custom-function-hidepanel-rule.png)

请参阅以下视频，以演示单击`Hide`后，第二个可重复实例中的面板将隐藏：

>[!VIDEO](https://video.tv.adobe.com/v/3429554?quality=12&learn=on)

## 加载表单时使用值预填字段

让我们了解自定义函数如何在`Booking Form`的帮助下使用字段和全局对象预填充字段。

添加以下代码行（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)部分中所述），以在初始化表单时在字段中加载预填充值：

```javascript
/**
 * Tests import data
 * @name testImportData
 * @param {scope} globals
 */
function testImportData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount','10000']]));
} 
```

在上述代码中，`testImportData`函数在加载表单时预填充`Booking Amount`文本框字段。 假设预订表单要求最低预订金额为`10,000`。

让我们在表单初始化时创建一个规则，其中加载表单时`Booking Amount`文本框字段中的值预填充为指定的值：

![导入数据规则](/help/forms/assets/custom-function-import-data.png)

请参阅下面的屏幕快照，该屏幕快照演示了在加载表单时，`Booking Amount`文本框中的值预填充了指定的值：

![导入数据规则表单](/help/forms/assets/custom-function-prefill-form.png)

## 设置特定字段的焦点

让我们了解自定义函数如何在`Booking Form`的帮助下使用字段和全局对象来设置对特定字段的关注。

添加下面一行代码（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)部分中所述），以便在单击`Submit`按钮时将焦点置于指定字段：

```javascript
/**
 * @name testSetFocus
 * @param {object} emailField
 * @param {scope} globals
 */
    function testSetFocus(field, globals)
    {
        globals.functions.setFocus(field);
    }
```

让我们向`Submit`按钮添加一个规则，以设置单击时`Email ID`文本框字段的焦点：

![设置焦点规则](/help/forms/assets/custom-function-set-focus.png)

请参阅下面的屏幕截图，其中演示了单击`Submit`按钮时，焦点设置在`Email ID`字段上：

![设置焦点规则](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> 如果要重点关注相对于`email`字段的下一个或上一个字段，则可以使用可选的`$focusOption`参数。

## 使用`dispatchEvent`属性添加或删除可重复面板

让我们了解自定义函数如何在`Booking Form`的帮助下使用`dispatchEvent`属性使用字段和全局对象添加或删除可重复面板。

添加以下代码行（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)部分中所述），以便在使用`dispatchEvent`属性单击`Add Traveler`按钮时添加面板：

```javascript
/**
 * Tests add instance with dispatchEvent
 * @name testAddInstance
 * @param {scope} globals
 */
function testAddInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel,'addInstance');
}
```

让我们向`Add Traveler`按钮添加一个规则，以便在单击该按钮时添加可重复面板：

![添加面板规则](/help/forms/assets/custom-function-add-panel.png)

请参阅下面的gif，其中演示了单击`Add Traveler`按钮时，使用`dispatchEvent`属性添加面板：

![添加面板](/help/forms/assets/custom-function-add-panel.gif)

同样，添加以下代码行（如[create-custom-function](#create-custom-function)部分中所述），以便在使用`dispatchEvent`属性单击`Delete Traveler`按钮时删除面板：

```javascript
/**
 
 * @name testRemoveInstance
 * @param {scope} globals
 */
function testRemoveInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 
```

让我们向`Delete Traveler`按钮添加一个规则，以便在单击可重复面板时将其删除：

![删除面板规则](/help/forms/assets/custom-function-delete-panel.png)

请参阅下面的gif，其中演示了在单击`Delete Traveler`按钮时，使用`dispatchEvent`属性删除旅行者面板：

![删除面板](/help/forms/assets/custom-function-delete-panel.gif)


## 疑难解答

* 如果自定义提交处理程序无法按预期在现有AEM项目或表单中执行，请执行以下步骤：
   * 确保[核心组件版本已更新到3.0.18及更高版本](https://github.com/adobe/aem-core-forms-components)。 但是，对于现有AEM项目和表单，还需要执行其他步骤：

   * 对于AEM项目，用户应使用`submitForm()`替换`submitForm('custom:submitSuccess', 'custom:submitError')`的所有实例，并通过Cloud Manager管道部署该项目。

   * 对于现有表单，如果自定义提交处理程序无法正常运行，用户需要使用规则编辑器在&#x200B;**提交**&#x200B;按钮上打开并保存`submitForm`规则。 此操作将`submitForm('custom:submitSuccess', 'custom:submitError')`中的现有规则替换为表单中的`submitForm()`。

## 另请参阅

{{see-also-rule-editor}}
