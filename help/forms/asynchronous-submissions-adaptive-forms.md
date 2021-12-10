---
title: 如何为自适应Forms配置异步提交？
description: 了解如何为自适应Forms配置异步提交。 深入了解异步提交如何用于自适应Forms。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 026f4920-f8f9-4b08-b1b0-af50229633d7
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# 异步提交自适应Forms {#asynchronous-submission-of-adaptive-forms}

传统上，Web表单配置为同步提交。 在同步提交中，当用户提交表单时，会将用户重定向到确认页面、感谢页面，或者在提交失败时，会重定向到错误页面。 但是，诸如单页应用程序等现代Web体验越来越受欢迎，其中网页保持静态，而客户端 — 服务器交互在后台进行。 您可以配置异步提交，以便通过自适应Forms提供此体验。

在异步提交中，当用户提交表单时，表单开发人员会插入一个单独的体验，如重定向到其他表单或网站的单独部分。 作者还可以插入单独的服务，如将数据发送到其他数据存储或添加自定义分析引擎。 在异步提交时，自适应表单的行为与单页应用程序类似，因为在服务器上验证提交的表单数据后，表单不会重新加载或其URL不会更改。

请阅读有关自适应Forms中异步提交的详细信息。

## 配置异步提交 {#configure}

要配置自适应表单的异步提交，请执行以下操作：

1. 在自适应表单创作模式中，选择表单容器对象并点按 ![cmppr1](assets/configure-icon.svg) 以打开其资产。
1. 在 **[!UICONTROL 提交]** 属性部分，启用 **[!UICONTROL 使用异步提交]**.
1. 在 **[!UICONTROL 提交时]** 部分，选择以下选项之一以成功提交表单。

   * **[!UICONTROL 重定向到URL]**:在表单提交时重定向到指定的URL或页面。 您可以指定URL或浏览以在 **[!UICONTROL 重定向URL/路径]** 字段。
   * **[!UICONTROL 显示消息]**:在表单提交时显示消息。 您可以在 **[!UICONTROL 显示消息]** 选项。 文本字段支持富文本格式。

1. 点按 ![check-button1](assets/save_icon.svg) 以保存属性。

## 异步提交的工作原理 {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] 为表单提交提供开箱即用的成功和错误处理程序。 处理程序是基于服务器响应执行的客户端函数。 在提交表单时，数据被传输到服务器进行验证，服务器会向客户端返回响应，其中包含有关提交的成功或错误事件的信息。 该信息作为参数传递给相关处理程序以执行该函数。

此外，表单作者和开发人员可以在表单级别编写规则以覆盖默认处理程序。 有关更多信息，请参阅 [使用规则覆盖默认处理程序](#custom).

让我们首先查看服务器对成功事件和错误事件的响应。

### 提交成功事件的服务器响应 {#server-response-for-submission-success-event}

提交成功事件的服务器响应的结构如下：

```json
{oneOf: [
{  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouOption : {type : "string"}
   }},
  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouContent: {type: "string"}
   }
]

}
```

成功提交表单时的服务器响应包括：

* 表单数据格式类型：XML或JSON
* XML或JSON格式的表单数据
* 选择了重定向到页面或显示消息的选项，该选项在表单中进行了配置
* 表单中配置的页面URL或消息内容

成功处理程序读取服务器响应并相应地重定向到配置的页面URL或显示消息。

### 针对提交错误事件的服务器响应 {#server-response-for-submission-error-event}

服务器响应提交错误事件的结构如下：

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

表单提交出错时的服务器响应包括：

* 错误、CAPTCHA或服务器端验证失败的原因
* 错误对象列表，包括验证失败的字段的SOM表达式和相应的错误消息

错误处理程序读取服务器响应，并相应地在表单上显示错误消息。

## 使用规则覆盖默认处理程序 {#custom}

表单开发人员和作者可以在表单级别编写规则以覆盖默认处理程序。 成功事件和错误事件的服务器响应在表单级别显示，开发人员可以使用 `$event.data` 在规则中。

执行以下步骤以编写规则来处理成功事件和错误事件。

1. 在创作模式下打开自适应表单，选择任意表单对象，然后点按 ![edit-rules1](assets/edit-rules-icon.svg) 以打开规则编辑器。
1. 选择 **[!UICONTROL 表单]** 在表单对象树中，点按 **[!UICONTROL 创建]**.
1. 选择 **[!UICONTROL 已成功提交]** 或 **[!UICONTROL 提交失败]** 从 **[!UICONTROL 选择状态]** 下拉列表。
1. 定义 **[!UICONTROL 然后]** 操作。 例如，选择 **[!UICONTROL 导航到]** 然后键入或粘贴URL。 您还可以使用 **[!UICONTROL 函数]** 选项卡。

   ![成功提交处理程序](assets/form-submission-handler.png)

1. 点按 **[!UICONTROL 完成]** 来保存规则。
