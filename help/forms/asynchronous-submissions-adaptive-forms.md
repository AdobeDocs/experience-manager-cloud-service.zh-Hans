---
title: 如何为自适应Forms配置异步提交？
description: 了解如何为自适应Forms配置异步提交。 深入了解异步提交如何适用于自适应Forms。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 026f4920-f8f9-4b08-b1b0-af50229633d7
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---

# 异步提交自适应Forms {#asynchronous-submission-of-adaptive-forms}


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/asynchronous-submissions-adaptive-forms.html) |
| AEM as a Cloud Service | 本文 |


传统上，Web窗体配置为同步提交。 在同步提交中，当用户提交表单时，会被重定向到确认页面、感谢页面，或者在提交失败的情况下被重定向到错误页面。 但是，像单页应用程序这样的现代Web体验正在变得流行起来，这是因为网页保持静态，而客户端 — 服务器交互发生在后台。 您可以配置异步提交以通过自适应Forms提供此体验。

在异步提交中，当用户提交表单时，表单开发人员会插入单独的体验，例如重定向到网站的其他表单或单独的部分。 作者还可以插入单独的服务（如将数据发送到其他数据存储）或添加自定义分析引擎。 在异步提交的情况下，自适应表单的行为类似于单页应用程序，这是因为在服务器上验证提交的表单数据时，表单不会重新加载或其URL不会更改。

有关自适应Forms中异步提交的详细信息，请阅读和。

## 配置异步提交 {#configure}

要为自适应表单配置异步提交，请执行以下操作：

1. 在自适应表单创作模式下，选择表单容器对象并点按 ![cmppr1](assets/configure-icon.svg) 以打开其属性。
1. 在 **[!UICONTROL 提交]** 属性部分，启用 **[!UICONTROL 使用异步提交]**.
1. 在 **[!UICONTROL 提交时]** 部分，选择以下选项之一以在成功提交表单时执行。

   * **[!UICONTROL 重定向到URL]**：在提交表单时重定向到指定的URL或页面。 您可以指定URL或浏览来选择 **[!UICONTROL 重定向URL/路径]** 字段。
   * **[!UICONTROL 显示消息]**：在表单提交时显示消息。 您可以在下面的文本字段中写入消息 **[!UICONTROL 显示消息]** 选项。 文本字段支持富文本格式。

1. 点按 ![check-button1](assets/save_icon.svg) 以保存属性。

## 异步提交的工作方式 {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] 为表单提交提供开箱即用的成功和错误处理程序。 处理程序是根据服务器响应执行的客户端功能。 当提交表单时，数据被传输到服务器进行验证，服务器将响应返回到客户端，其中包含有关提交的成功或错误事件的信息。 信息作为参数传递给相关处理程序以执行函数。

此外，表单作者和开发人员可以在表单级别编写规则以覆盖默认处理程序。 有关更多信息，请参阅 [使用规则覆盖默认处理程序](#custom).

让我们首先查看服务器响应中的成功和错误事件。

### 提交成功事件的服务器响应 {#server-response-for-submission-success-event}

提交成功事件的服务器响应结构如下：

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
* 已选择选项，用于重定向到页面或显示表单中配置的消息
* 页面URL或消息内容，如表单中所配置

成功处理程序读取服务器响应，并相应地重定向到配置的页面URL或显示消息。

### 提交错误事件的服务器响应 {#server-response-for-submission-error-event}

提交错误事件的服务器响应结构如下：

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

在提交表单时出现错误时，服务器响应包括：

* 错误原因，验证码或服务器端验证失败
* 错误对象列表，其中包括验证失败的字段的SOM表达式和相应的错误消息

错误处理程序会读取服务器响应，并在表单上显示相应的错误消息。

## 使用规则覆盖默认处理程序 {#custom}

表单开发人员和作者可以在表单级别编写规则以覆盖默认处理程序。 成功和错误事件的服务器响应在表单级别公开，开发人员可以使用进行访问 `$event.data` 在规则中。

执行以下步骤来编写规则以处理成功和错误事件。

1. 在创作模式下打开自适应表单，选择任意表单对象，然后点按 ![edit-rules1](assets/edit-rules-icon.svg) 以打开规则编辑器。
1. 选择 **[!UICONTROL 表单]** 在表单对象树中，然后点按 **[!UICONTROL 创建]**.
1. 选择 **[!UICONTROL 已成功提交]** 或 **[!UICONTROL 提交失败]** 从 **[!UICONTROL 选择状态]** 下拉列表。
1. 定义 **[!UICONTROL 则]** 操作。 例如，选择 **[!UICONTROL 导航到]** 然后键入或粘贴URL。 您还可以使用拖动任何函数 **[!UICONTROL 函数]** 选项卡。

   ![提交处理程序成功](assets/form-submission-handler.png)

1. 点按 **[!UICONTROL 完成]** 以保存规则。
