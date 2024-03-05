---
title: 准备电子表格以接受数据
description: 使用电子表格和自适应表单块字段更快地制作功能强大的表单！
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: fd2e5df72e965ea6f9ad09b37983f815954f915c
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 92%

---


# 准备电子表格以接受数据

![基于文档的创作生态系统](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)

在[创建并预览表单](/help/edge/docs/forms/create-forms.md)后，可以启用相应的电子表格以开始接收数据。

![基于文档的创作生态系统](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)

<!-- 
>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->

要启用电子表格，请执行以下操作：

1. 打开包含您的表单的电子表格并附加一个新工作表，并将其重命名为 `incoming`。

   >[!WARNING]
   >
   > 如果 `incoming` 工作表不存在，AEM 不会向电子表格发送任何数据。

1. 将表单字段名称、`shared-default` 工作表中的 `Name` 列的值镜像到 `incoming` 工作表中的标题。

   `shared-default` 工作表的 `Name` 列中的每个值（不包括提交按钮）均充当 `incoming` 工作表中的标题。例如，请考虑下图，其中说明了“contact-us”表单的标题：

   ![“contact-us”表单的字段](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. 使用 Sidekick 预览工作表。

   >[!NOTE]
   >
   >即使您之前已经预览过该工作表，在第一次创建 `incoming` 工作表后也必须再次预览它。


将字段名称添加到 `incoming` 工作表后，您的表单便能接受提交。您可以预览表单并使用它向工作表提交数据。



您还可以在电子表格中观察到以下变化：

一份名为“Slack”的工作表将会被添加到您的 Excel 工作簿或 Google 工作表中。在此工作表中，您可以在电子表格中引入新数据时为指定的 Slack 渠道配置自动通知。目前，AEM 仅支持向 AEM Engineering Slack 组织和 Adobe Enterprise 支持组织发送通知。

1. 要设置 Slack 通知，请输入 Slack 工作区的“teamId”和“频道名称”或“ID”。您还可以向 slack-bot（使用调试命令）询问“teamId”和“channel ID”。最好使用“频道 ID”而不是“频道名称”，因为它在频道重命名后仍然有效。

   >[!NOTE]
   >
   > 旧的表单没有“teamId”列。“teamId”包含在频道列中，以“#”或“/”分隔。

1. 输入您想要的任何标题，然后在字段下输入您想要在 Slack 通知中看到的字段的名称。每个标题应以逗号分隔（例如姓名、电子邮件）。

   >[!WARNING]
   >
   >  在任何情况下，“shared-default”工作表都不应包含您不愿意公开的任何个人身份信息或敏感数据。


## （可选）使用管理员 API 以使电子表格能够接受数据

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

一份名为“Slack”的工作表将会被添加到您的 Excel 工作簿或 Google 工作表中。在此工作表中，您可以在电子表格中引入新数据时为指定的 Slack 渠道配置自动通知。目前，AEM 仅支持向 AEM Engineering Slack 组织和 Adobe Enterprise 支持组织发送通知。

1. 要设置 Slack 通知，请输入 Slack 工作区的“teamId”和“频道名称”或“ID”。您还可以向 slack-bot（使用调试命令）询问“teamId”和“channel ID”。最好使用“频道 ID”而不是“频道名称”，因为它在频道重命名后仍然有效。

   >[!NOTE]
   >
   > 旧的表单没有“teamId”列。“teamId”包含在频道列中，以“#”或“/”分隔。

1. 输入您想要的任何标题，然后在字段下输入您想要在 Slack 通知中看到的字段的名称。每个标题应以逗号分隔（例如姓名、电子邮件）。


工作表现在设置为接收数据，您可以 [使用自适应表单块预览表单](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) 或 [使用POST请求](#use-admin-apis-to-send-data-to-your-sheet) 开始将数据发送到工作表。

>[!WARNING]
>
>  在任何情况下，“shared-default”工作表都不应包含您不愿意公开的任何个人身份信息或敏感数据。

## 将数据发送到您的工作表 {#send-data-to-your-sheet}

将工作表设置为接收数据后，您可以 [使用自适应表单块预览表单](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) 或 [使用管理员API](#use-admin-apis-to-send-data-to-your-sheet) 开始将数据发送到工作表。

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

接下来，您可以自定义感谢消息、[配置感谢页面](/help/edge/docs/forms/thank-you-page-form.md)或[设置重定向](/help/edge/docs/forms/thank-you-page-form.md)。

## 查看更多

* [创建并预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单，以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到 Sites 页面](/help/edge/docs/forms/publish-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [改变表单主题和样式](/help/edge/docs/forms/style-theme-forms.md)
