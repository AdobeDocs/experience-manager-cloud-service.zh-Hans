---
title: 在Adaptive Forms for AEM Adaptive Forms中添加自定义错误处理程序
seo-title: Error Handlers in Adaptive Forms for AEM Adaptive Forms
description: AEM Forms使用配置为调用外部服务的REST端点为表单提供开箱即用的成功和错误处理程序。 您可以在AEM自适应表单中添加默认错误处理程序以及自定义错误处理程序。
seo-description: Error handler function and Rule Editor in Adaptive Forms helps you to effectively manage and customize error handling. You can add a default error handler as well as custom error handler in an AEM Adaptive Form.
keywords: 添加自定义错误处理程序、添加默认错误处理程序、在表单中添加错误处理程序、使用规则编辑器的调用服务添加自定义错误处理程序、配置规则编辑器添加自定义错误处理程序、使用规则编辑器添加自定义错误处理程序
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms
source-git-commit: 09ed1ae61e7748da2cc182b005a9dd26853cb3f7
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 2%

---

# 自适应Forms中的错误处理程序 {#error-handlers-in-adaptive-form}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html) |
| AEM as a Cloud Service | 本文 |

AEM Forms为表单提交提供开箱即用的成功和错误处理程序。 它还提供自定义错误处理程序函数的功能。 例如，您可以在后端为特定的错误代码调用自定义工作流，或者通知客户服务已停止。处理程序是根据服务器响应执行的客户端功能。 当使用API调用外部服务时，数据将传输到服务器进行验证，服务器将响应返回到客户端，其中包含有关提交的成功或错误事件的信息。 信息作为参数传递给相关处理程序以执行函数。 错误处理程序有助于管理和显示遇到的错误或验证问题。

![错误处理程序工作流，用于了解如何在表单中添加自定义错误处理程序](/help/forms/assets/error-handler-workflow.png)

自适应表单根据预设验证条件验证您在字段中提供的输入，并检查由配置为调用外部服务的REST端点返回的各种错误。 您可以根据在自适应表单中使用的数据源设置验证条件。 例如，如果使用RESTful Web服务作为数据源，则可以在Swagger定义文件中定义验证条件。

如果输入值满足验证条件，则这些值将提交给数据源，否则，自适应表单将使用错误处理程序显示错误消息。 与这种方法类似，自适应Forms与自定义错误处理程序集成以执行数据验证。 如果输入值不符合验证条件，则错误消息会在自适应表单中的字段级别显示。 当服务器返回的验证错误消息为标准消息格式时，会发生这种情况。


## 错误处理程序的使用 {#uses-of-error-handler}

错误处理程序有多种用途。 下面列出了错误处理程序函数的一些用法：
* **执行验证**：错误处理从根据预定义的规则或标准验证用户输入开始。 当用户填写自适应表单时，错误处理程序会验证输入以确保它满足所需的格式、长度或任何其他限制。

* **提供实时反馈**：当检测到任何错误时，错误处理程序会立即向用户显示反馈，例如相应表单字段下的内联错误消息。 此反馈可帮助用户识别和更正错误，而无需提交表单并等待响应。


* **显示错误消息**：当自适应表单提交遇到任何验证错误时，错误处理程序显示相应的错误消息。 错误消息应简明扼要，并突出显示需要注意的特定字段。

* **突出显示错误的字段**：为了吸引用户注意特定的不正确字段，错误处理程序会突出显示或视觉上区分相应的字段。 此操作可通过更改背景颜色、添加图标或边框或任何有助于用户快速找到并解决错误的其他可视提示来执行。


## 失败/错误响应格式 {#failure-response-format}

如果服务器验证错误消息采用以下标准格式，则自适应表单会在字段级别显示错误。
以下代码说明了现有的故障响应结构：

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
}
```


其中：

* `errorCausedBy` 描述失败的原因。
* `errors` 提及未能通过验证标准的字段的SOM表达式以及验证错误消息。
* `originCode` 由AEM添加的字段，包含由外部服务返回的http状态代码。
* `originMessage` 由AEM添加的字段，其中包含外部服务返回的原始错误数据。

随着AEM Forms版本的功能改进及后续更新，在RFC7807的基础上将现有的故障响应结构改为新的格式，向后兼容现有的故障响应结构：

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<SOM expression of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * 确保错误响应结构包含 **fieldName** 或 **dataRef**.
> * 确保 **内容类型** 标头为 **application/problem+json**.

其中：
* `type (required)` 指定失败类型。 它可以是以下值之一：
   * `SERVER_SIDE_VALIDATION` 表示由于服务器端验证而失败。
   * `FORM_SUBMISSION` 指示表单提交过程中失败
   * `SERVICE_INVOCATION` 表示在第三方服务调用过程中出现故障。
   * `FAILURE` 表示一般故障。
   * `VALIDATION_ERROR` 表示由于验证错误而失败。

* `title (optional)` 提供失败的标题或简短描述。
* `detail (optional)` 提供了有关故障的其他详细信息（如有必要）。
* `instance (optional)` 表示与失败关联的实例或标识符，并有助于跟踪或识别失败的特定发生次数。
* `validationErrors (required)` 包含有关验证错误的信息。 包含以下字段：
   * `fieldname` 提及未能通过验证标准的字段的SOM表达式。
   * `dataRef` 表示验证失败的字段的JSON路径或XPath。
   * `details` 包含带有错误字段的验证错误消息。
* `originCode (optional)` 由AEM添加的字段，包含由外部服务返回的http状态代码
* `originMessage (optional)` 由AEM添加的字段，其中包含外部服务返回的原始错误数据。

### 示例错误响应格式 {#sample-error-response-format}

显示错误响应的一些选项包括：

+++  基于自适应表单fieldName属性


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

      ```javascript
      {
      &quot;type&quot;： &quot;VALIDATION_ERROR&quot;，
      &quot;validationErrors&quot;： [
      {
      &quot;fieldName&quot;： &quot;guide[0].guide1[0].guideRootPanel[0].textbox1686647736683[0]&quot;，
      &quot;dataRef&quot;： &quot;&quot;，
      &quot;details&quot;： [
      “提供的ID无效。 提供的值不正确！”
      ]
      }
      ]}
      ```
  
  您可以通过点按自适应表单中任何字段并选择 **[!UICONTROL 查看SOM表达式]**.

  ![在自定义错误处理程序中显示错误响应的自适应表单字段的SOM表达式](/help/forms/assets/custom-error-handler-somexpression.png)

+++


+++ 基于自适应表单dataRef属性

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
  {
      "type": "VALIDATION_ERROR",
      "validationErrors": [
      {
          "fieldName": "",
          "dataRef": "/Pet/id",
          "details": [
          "Invalid ID supplied. Provided value is not correct!"
          ]
          }
  ]}
  ```

  ![在自定义错误处理程序中显示错误响应的自适应表单字段的数据引用](/help/forms/assets/custom-errorhandler-dataref.png)

您可以查看 **[!UICONTROL 属性]** 窗体组件的窗口。

+++


## 使用规则编辑器添加错误处理程序 {#add-error-handler-using-rule-editor}

使用 [规则编辑器的调用服务](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 操作，则可根据在自适应表单中使用的数据源定义验证条件。 如果将RESTful Web服务用作数据源，则可以在Swagger定义文件中定义验证条件。 利用Adaptive Forms中的错误处理程序函数和规则编辑器，您可以有效地管理和自定义错误处理。 您可以使用规则编辑器定义条件，并配置在触发规则时要执行的所需操作。 自适应表单根据预设验证条件验证您在字段中输入的输入。 如果输入值不符合验证条件，则错误消息会在自适应表单的字段级别显示。

>[!NOTE]
>
> * 要将错误处理程序与规则编辑器的调用服务操作结合使用，请使用表单数据模型配置自适应Forms。
> * 默认情况下，如果错误响应在标准架构中，则会提供默认错误处理程序，以在字段上显示错误消息。 如果错误响应不符合标准架构，则默认错误处理程序也可以调用自定义错误处理程序。

<!-- 
Using Rule Editor, you can:
* [Add default error handler function](#add-default-errror-handler)
* [Add custom error handler function](#add-custom-errror-handler)


### Add default error handler function {#add-default-errror-handler}

A default error handler is supported by default to display error messages on fields if the error response is in standard schema or in server-side validation failure. 
To understand how to use a default error handler using the [Rule Editor's Invoke Service](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) action, take an example of a simple Adaptive Form with two fields, **Pet ID** and **Pet Name** and use a default error handler at the **Pet ID** field to check for various errors returned by the REST endpoint configured to invoke an external service, for example, `200 - OK`,`404 - Not Found`, `400 - Bad Request`. To add a default error handler using the Rule Editor's Invoke Service action, execute the following steps:

1. Open an Adaptive Form in authoring mode, select a form component and tap **[!UICONTROL Rule Editor]** to open the rule editor.
1. Tap **[!UICONTROL Create]**.
1. Create a condition in the **When** section of the rule. For example, **When[Name of Pet ID field]** is changed. Select is changed from the **Select State** drop-down list.
1. In the **Then** section, select **[!UICONTROL Invoke Service]** from the **Select Action** drop-down list.
1. Select a **Post service** and its corresponding data bindings from the **Input** section. For example, to validate **Pet ID**, select a **Post service** as **GET /pet/{petId}** and select **Pet ID** in the **Input** section.
1. Select the data bindings from the **Output** section. Select **Pet Name** in the **Output** section.
1. Select **[!UICONTROL Default Error Handler]** from the **Error Handler** section. 
1. Click **[!UICONTROL Done]**.

 ![add a default error handler for a field validation checks in a form](/help/forms/assets/default-error-handler.png)

As a result of this rule, the values you enter for **Pet ID** checks validation for **Pet Name** using external service invoked by REST endpoint. If the validation criteria based on the data source fail, the error messages are displayed at the field level.

 ![display the default error message when you add a default error handler in a form to handle error responses](/help/forms/assets/default-error-message.png)

-->

### 添加自定义错误处理程序函数 {#add-custom-errror-handler}

您可以添加自定义错误处理程序函数以执行某些操作，例如：
* 处理使用非标准或标准错误响应的错误响应。 请务必注意，这些非标准错误响应不符合 [错误响应的标准架构](#failure-response-format).
* 将analytics事件发送到任何analytics平台。 例如，Adobe Analytics.
* 显示带有错误消息的模式对话框。

除了上述操作之外，还可以使用自定义错误处理程序来执行符合特定用户要求的自定义函数。

自定义错误处理程序是一个函数（客户端库），用于响应外部服务返回的错误，并向最终用户提供自定义响应。 任何带注释的客户端库 `@errorHandler` 被视为自定义错误处理程序函数。 此注释有助于识别 `.js` 文件。
要了解如何使用创建和使用自定义错误处理程序 [规则编辑器的调用服务](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 操作，我们以带有两个字段的自适应表单为例， **宠物ID** 和 **宠物名称** 并在中使用自定义错误处理程序 **宠物ID** 用于检查配置为调用外部服务的REST端点返回的各种错误的字段，例如， `200 - OK`，`404 - Not Found`， `400 - Bad Request`.

要在自适应表单中添加和使用自定义错误处理程序，请执行以下步骤：
1. [创建自定义错误处理程序](#create-custom-error-message)
1. [使用规则编辑器配置自定义错误处理程序](#use-custom-error-handler)

#### 1.创建自定义错误处理程序 {#create-custom-error-message}

要创建自定义错误函数，请执行以下步骤：
1. [克隆您的 AEM Forms as a Cloud Service 存储库.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).
1. 导航到 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/`。
1. 创建名为的文件夹 `js`.
1. 导航到 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` 文件夹。
1. 添加JavaScript文件，例如 `function.js`. 该文件包含自定义错误处理程序的代码。
让我们将以下代码添加到JavaScript文件中，以在浏览器控制台中显示从REST服务端点收到的响应和标头。

       ```javascript
       /**
       *自定义错误处理程序
       * @name customErrorHandler自定义错误处理程序函数
       * @errorHandler
       */
       函数customErrorHandler(response， headers)
       {
       console.log（“自定义错误处理程序处理开始……”）；
       console.log(&quot;response：&quot;+JSON.stringify(response))；
       console.log(&quot;headers：&quot;+JSON.stringify(headers))；
       console.log（“自定义错误处理程序处理结束……”）；
       }
       ```
   
   <!--  To call the default error handler after the custom error handler, the following line of the sample code is used:
        `guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers) `-->
1. 保存 `function.js` 文件。
1. 导航到 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` 文件夹。
1. 将文本文件添加为 `js.txt`. 该文件包含：

   ```javascript
       #base=js
       functions.js
   ```

1. 保存 `js.txt` 文件。

   >[!NOTE]
   >
   > 要了解有关如何创建自定义函数的更多信息，请单击 [规则编辑器中的自定义函数](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#write-rules).

1. 使用以下命令添加、提交和推送存储库中的更改：

   ```javascript
       git add .
       git commit -a -m "Adding error handling files"
       git push
   ```

1. [运行管道.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline)

成功执行管道后，自定义错误处理程序将在自适应表单规则编辑器中变得可用。 现在，让我们了解如何使用AEM Forms中的规则编辑器的调用服务配置和使用自定义错误处理程序。

#### 2.使用规则编辑器配置自定义错误处理程序 {#use-custom-error-handler}

使用自定义错误处理程序 **[!UICONTROL 规则编辑器的调用服务]** 操作：

1. 在创作模式下打开自适应表单，选择表单组件并点按 **[!UICONTROL 规则编辑器]** 以打开规则编辑器。
1. 点按 **[!UICONTROL 创建]**.
1. 在中创建条件 **时间** 部分。 例如，当 **[宠物ID字段的名称]** 已更改，请选择 **已更改** 从 **选择状态** 下拉列表。
1. 在 **则** 部分，选择 **[!UICONTROL 调用服务]** 从 **选择操作** 下拉列表。
1. 选择 **邮政服务** 及其相应的数据绑定 **输入** 部分。 例如，验证 **宠物ID**，选择一个 **邮政服务** 作为 **GET/pet/{petId}** 并选择 **宠物ID** 在 **输入** 部分。
1. 从中选择数据绑定 **输出** 部分。 例如，选择 **宠物名称** 在 **输出** 部分。
1. 选择 **[!UICONTROL 自定义错误处理程序]** 从 **[!UICONTROL 错误处理程序]** 部分。
1. 单击&#x200B;**[!UICONTROL 完成]**。

![在表单中添加自定义错误处理程序以处理错误响应](/help/forms/assets/custom-error-handler.png)


作为此规则的结果，您输入的值 **宠物ID** 检查验证 **宠物名称** 使用REST端点调用的外部服务。 如果基于数据源的验证标准失败，则错误消息将在字段级别显示。


![在表单中添加自定义错误处理程序以处理错误响应](/help/forms/assets/custom-error-handler-message.png)

打开浏览器控制台，检查从REST服务端点收到的响应和标头，以查看验证错误消息。


自定义错误处理程序函数负责根据错误响应执行其他操作，如显示模式对话框或发送Analytics事件。 自定义错误处理程序函数灵活地根据特定用户要求定制错误处理。

<!-- 

## Configure Adaptive Form submission to add custom handlers {#configure-adaptive-form-submission}

If the server validation error message does not display in the standard format, you can enable asynchronous submission and add a custom error handler on Adaptive Form submission to convert the message into a standard format.

### Configure asynchronous Adaptive Form submission {#configure-asynchronous-adaptive-form-submission}

Before adding custom handler, you must configure the adaptive form for asynchronous submission. Execute the following steps:

1. In adaptive form authoring mode, select the Form Container object and tap ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST Service endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Tap ![Save](assets/save_icon.png) to save the properties.

### Add custom error handler on Adaptive Form submission {#add-custom-error-handler-af-submission}

AEM Forms provides out-of-the-box success and error handlers for form submissions. Handlers are client-side functions that execute based on the server response. When an Adaptive Form is submitted, the data is transmitted to the server for validation, which returns a response to the client with information about the success or error event for the submission. The information is passed as parameters to the relevant handler to execute the function.

Execute the following steps to add custom error handler on Adaptive Form submission:

1. Open an Adaptive Form in authoring mode, select any form object, and tap  to open the rule editor.
1. Select **[!UICONTROL Form]** in the Form Objects tree and tap **[!UICONTROL Create]**.
1. Select **[!UICONTROL Error in Submission]** from the Event drop-down list.
1. Write a rule to convert custom error structure to the standard error structure and tap **[!UICONTROL Done]** to save the rule.

The following is a sample code to convert a custom error structure to the standard error structure:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

The `var som_map` lists the SOM expression of the Adaptive Form fields that you want to transform into the standard format. You can view the SOM expression of any field in an adaptive form by tapping the field and selecting **[!UICONTROL View SOM Expression]**.

Using this custom error handler, the adaptive form converts the fields listed in `var som_map` to standard error message format. As a result, the validation error messages display at field-level in the adaptive form.

 -->