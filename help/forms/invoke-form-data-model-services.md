---
title: 如何使用API从自适应Forms调用表单数据模型(FDM)服务？
description: 说明可用于从自适应表单字段中调用在WSDL中编写的Web服务的invokeWebServices API。
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms, Form Data Model
role: User
hide: true
hidefromtoc: true
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# 用于从自适应Forms调用表单数据模型(FDM)服务的API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概述 {#overview}

[!DNL AEM Forms]使表单作者能够通过从自适应表单字段中调用在表单数据模型(FDM)中配置的服务来进一步简化和增强表单填写体验。 要调用数据模型服务，您可以在可视编辑器中创建规则，或在[规则编辑器](rule-editor.md)的代码编辑器中使用`guidelib.dataIntegrationUtils.executeOperation` API指定JavaScript。

本文档侧重于使用`guidelib.dataIntegrationUtils.executeOperation` API编写JavaScript以调用服务。

## 使用API {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API从自适应表单字段中调用服务。 API语法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

`guidelib.dataIntegrationUtils.executeOperation` API的结构指定了有关服务操作的详细信息。 此结构的语法如下。

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API结构指定了有关服务操作的以下详细信息。

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>用于指定表单数据模型标识符、操作标题和操作名称的结构</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>指定表单数据模型(FDM)的存储库路径，包括其名称</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>指定要执行的服务操作的名称</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>将一个或多个表单对象映射到服务操作的输入参数</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>将一个或多个表单对象映射到服务操作的输出值以填充表单字段<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>基于服务操作的输入参数返回值。 它是用作回调函数的可选参数。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>如果success回调函数无法根据输入参数显示输出值，则显示错误消息。 它是用作回调函数的可选参数。<br /> </td>
  </tr>
 </tbody>
</table>

## 用于调用服务的示例脚本 {#sample-script-to-invoke-a-service}

以下示例脚本使用`guidelib.dataIntegrationUtils.executeOperation` API调用在`employeeAccount`表单数据模型(FDM)中配置的`getAccountById`服务操作。

`getAccountById`操作将`employeeID`表单字段中的值作为`empId`参数的输入，并返回相应员工的员工姓名、帐号和帐户余额。 输出值会填充到指定的表单字段中。 例如，`name`参数中的值在`fullName`表单元素中填充，在`account`表单元素中为`accountNumber`参数填充值。

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## 将API与回调函数结合使用 {#using-the-api-callback}

您还可以使用带有回调函数的`guidelib.dataIntegrationUtils.executeOperation` API调用表单数据模型服务。 API语法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

回调函数可以有`success`和`failure`回调函数。

### 包含成功和失败回调函数的示例脚本 {#callback-function-success-failure}

以下示例脚本使用`guidelib.dataIntegrationUtils.executeOperation` API调用在`employeeOrder`表单数据模型(FDM)中配置的`GETOrder`服务操作。

`GETOrder`操作将`Order ID`表单字段中的值作为`orderId`参数的输入并返回`success`回调函数中的订货量值。  如果`success`回调函数未返回订单数量，`failure`回调函数将显示`Error occured`消息。

>[!NOTE]
>
> 如果使用`success`回调函数，则指定的表单字段中不会填充输出值。

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
