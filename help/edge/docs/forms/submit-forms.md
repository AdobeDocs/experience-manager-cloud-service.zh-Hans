---
title: 准备电子表格以接受数据
description: 使用电子表格和 Adaptive Forms Block 字段更快地制作功能强大的表单！
feature: Edge Delivery Services
exl-id: 0643aee5-3a7f-449f-b086-ed637ae53b5a
source-git-commit: 5eee563a9a425ef187afed69a8159d8b1298dad7
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 98%

---

# 设置Google Sheets或Microsoft Excel文件以开始接受数据


在[创建并预览表单](/help/edge/docs/forms/create-forms.md)后，就可以启用相应的电子表格开始接收数据。您可以手动启用电子表格以接受数据，或使用 Admin API 启用电子表格以接受数据。

![基于文档的创作生态系统](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)

<!-- 
>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->


## 手动启用电子表格以接受数据

使电子表格能够接受数据

1. 打开包含您的表单的电子表格并附加一个新工作表，并将其重命名为 `incoming`。

   >[!WARNING]
   >
   > 如果 `incoming` 工作表不存在，AEM 不会向电子表格发送任何数据。

1. 在此工作表中，插入一个名为“intake_form”的表。选择与表单字段名称匹配所需的列数。然后，在工具栏中转到“插入”>“表格”并单击“确定”。

1. 将表的名称更改为“intake_form”。在 Microsoft Excel 中，要更改表的名称，请选择该表并单击“表设计”。

1. 接下来，添加表单字段名称作为表标题。为了确保字段完全相同，您可以从“shared-default”表中复制并粘贴它们。在“shared-default”工作表中，选择并复制“名称”列下列出的表单 ID（提交字段除外）。

1. 在“传入”工作表中，选择“选择性粘贴”>“将行转置为列”，将字段 ID 复制为该新工作表中的列标题。只保留需要捕获数据的字段，其他可以忽略。

   `shared-default`工作表的`Name`列中的每个值（不包括提交按钮）都可以用作`incoming`工作表中的标题。例如，请考虑下图，其中说明了“contact-us”表单的标题：

   ![“contact-us”表单的字段](/help/edge/assets/contact-us-form-excel-sheet-fields.png)



1. 使用 AEM Sidekick 扩展预览表单更新。您的工作表现已准备好接受传入的表单提交。

   >[!NOTE]
   >
   >即使您之前已经预览过该工作表，在第一次创建 `incoming` 工作表后也必须再次预览它。


将字段名称添加到 `incoming` 工作表后，您的表单便能接受提交。您可以预览表单并使用它向工作表提交数据。

将工作表设置为接收数据后，您可以[使用 Adaptive Forms Block 预览表单](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page)或[使用 POST 请求](#use-admin-apis-to-send-data-to-your-sheet)开始将数据发送到工作表。

>[!WARNING]
>
>  在任何情况下，“shared-default”工作表都不应包含您不愿意公开的任何个人身份信息或敏感数据。

### 使用管理 API 使电子表格能够接受数据

您还可以向表单发送 POST 请求，使其能够接受数据并配置 `incoming` 工作表的标头。收到 POST 请求后，该服务会分析请求正文并自动生成数据摄取所需的基本标头和工作表。

要使用管理员 API 以使电子表格能够接受数据，请执行以下操作：


1. 打开您创建的工作簿并将默认工作表的名称更改为 `incoming`。

   >[!WARNING]
   >
   > 如果 `incoming` 工作表不存在，AEM 不会向此工作簿发送任何数据。

1. 在 Sidekick 中预览工作表。

   >[!NOTE]
   >
   >即使您之前已经预览过该工作表，在第一次创建 `incoming` 工作表后也必须再次预览它。

1. 发送 POST 请求以在 `incoming` 工作表中生成适当的标头，并将 `shared-default` 工作表添加到电子表格（如果它尚不存在）。

   要了解如何设置用于设置工作表的 POST 请求的格式，请参阅[管理员 API 文档](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile)。您可以查看下面提供的示例：

   **请求**

   ```JSON
   POST 'https://admin.hlx.page/form/{owner}/{repo}/{branch}/contact-us.json' \
   --header 'Content-Type: application/json' \
   --data '{
       "data": {
           "Email": "john@wknd.com",
           "Name": "John",
           "Subject": "Regarding Product Inquiry",
           "Message": "I have some questions about your products.",
           "Phone": "123-456-7890",
           "Company": "Adobe Inc.",
           "Country": "United States",
           "PreferredContactMethod": "Email",
           "SubscribeToNewsletter": true
       }
   }'
   ```


   **响应**

   ```JSON
   HTTP/2 200 
   content-type: application/json
   x-invocation-id: 1b3bd30a-8cfb-4f85-a662-4b1f7cf367c5
   cache-control: no-store, private, must-revalidate
   accept-ranges: bytes
   date: Sat, 10 Feb 2024 09:26:48 GMT
   via: 1.1 varnish
   x-served-by: cache-del21736-DEL
   x-cache: MISS
   x-cache-hits: 0
   x-timer: S1707557205.094883,VS0,VE3799
   strict-transport-security: max-age=31557600
   content-length: 138
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country",      "PreferredContactMethod","SubscribeToNewsletter"]}%
   ```

   您可以使用 curl 或 Postman 等工具来执行此 POST 请求，如下所示：

   ```JSON
   curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
       --header 'Content-Type: application/json' \
       --data '{
           "data": {
               "Email": "john@wknd.com",
               "Name": "John",
               "Subject": "Regarding Product Inquiry",
               "Message": "I have some questions about your products.",
               "Phone": "123-456-7890",
               "Company": "Wknd Inc.",
               "Country": "United States",
               "PreferredContactMethod": "Email",
               "SubscribeToNewsletter": true
       }
   }'
   ```

   上述 POST 请求提供了示例数据，包括表单字段及其各自的示例值。管理服务会使用此数据来设置表单。

   您的表单现已能够接受数据。您还可以在电子表格中观察到以下变化：

## 一旦启用接受数据，就会自动更改工作表。

将工作表设置为接收数据后，您会在电子表格中观察到以下变化：

一份名为“Slack”的工作表将会被添加到您的 Excel 工作簿或 Google 工作表中。在此工作表中，您可以在电子表格中引入新数据时为指定的 Slack 渠道配置自动通知。目前，AEM 仅支持向 AEM Engineering Slack 组织和 Adobe Enterprise 支持组织发送通知。

1. 要设置 Slack 通知，请输入 Slack 工作区的“teamId”和“频道名称”或“ID”。您还可以向 slack-bot（使用调试命令）询问“teamId”和“channel ID”。最好使用“频道 ID”而不是“频道名称”，因为它在频道重命名后仍然有效。

   >[!NOTE]
   >
   > 旧的表单没有“teamId”列。“teamId”包含在频道列中，以“#”或“/”分隔。

1. 输入您想要的任何标题，然后在字段下输入您想要在 Slack 通知中看到的字段的名称。每个标题应以逗号分隔（例如姓名、电子邮件）。

   >[!WARNING]
   >
   >  在任何情况下，“shared-default”工作表都不应包含您不愿意公开的任何个人身份信息或敏感数据。


## 将数据发送到您的工作表 {#send-data-to-your-sheet}

将工作表设置为可接收数据后，您可以使用 Adaptive Forms Block [预览表单](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page)或[使用 Admin API](#use-admin-apis-to-send-data-to-your-sheet) 开始向该工作表传递数据。

### 使用管理 API 将数据发送到您的工作表

您可以使用 hlx.page、hlx.live 或您的生产域将 POST 请求直接发送到表单来发送数据。


```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL 不应具有 .json 扩展。只有在发布工作表后，POST 操作才能在 `.live` 或生产域上运行。

#### 格式化表单数据

您可以使用几种不同的方法来格式化 POST 正文中的表单数据。您可以使用：

*  `name:value` 对数组：

  ```JSON
  {
    "data": [
      { "name": "name", "value": "Clark Kent" },
      { "name": "email", "value": "superman@example.com" },
      { "name": "subject", "value": "Regarding Product Inquiry" },
      { "name": "message", "value": "I have some questions about your products." },
      { "name": "phone", "value": "123-456-7890" },
      { "name": "company", "value": "Example Inc." },
      { "name": "country", "value": "United States" },
      { "name": "preferred_contact_method", "value": "Email" },
      { "name": "newsletter_subscribe", "value": true }
    ]
  }
  ```

  例如

  ```JSON
  curl -s -i -X POST 'https://main--portal--wkndforms.hlx.page/contact-us' \
      --header 'Content-Type: application/json' \
      --data '{
      "data": [
          { "name": "name", "value": "Clark Kent" },
          { "name": "email", "value": "superman@example.com" },
          { "name": "subject", "value": "Regarding Product Inquiry" },
          { "name": "message", "value": "I have some questions about your        products." },
          { "name": "phone", "value": "123-456-7890" },
          { "name": "company", "value": "Example Inc." },
          { "name": "country", "value": "United States" },
          { "name": "preferred_contact_method", "value": "Email" },
          { "name": "newsletter_subscribe", "value": true }
      ]
  }'
  ```



* 具有 `key:value` 对的对象：

  ```JSON
      {
        "data": {
          "name": "Jessica Jones",
          "email": "jj@example.com",
          "subject": "Regarding Product Inquiry",
          "message": "I have some questions about your products.",
          "phone": "123-456-7890",
          "company": "Example Inc.",
          "country": "United States",
          "preferred_contact_method": "Email",
          "newsletter_subscribe": true
        }
      }
  ```

  例如，

  ```JSON
  curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
  --header 'Content-Type: application/json' \
  --data '{
      "data": {
          "Email": "khushwant@wknd.com",
          "Name": "khushwant",
          "Subject": "Regarding Product Inquiry",
          "Message": "I have some questions about your products.",
          "Phone": "123-456-7890",
          "Company": "Adobe Inc.",
          "Country": "United States",
          "PreferredContactMethod": "Email",
          "SubscribeToNewsletter": true
      }
  }'
  ```

* URL 编码 (`x-www-form-urlencoded`) 正文（`content-type` 标头设置为 `application/x-www-form-urlencoded`）

  ```Shell
  'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'
  ```

  例如，

  ```Shell
  curl -s -i -X POST \
    -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
    https://main--portal--wkndforms.hlx.live/contact-us
  ```

接下来，您可以[自定义感谢消息](/help/edge/docs/forms/thank-you-page-form.md)。

## 另请参阅

{{see-more-forms-eds}}
