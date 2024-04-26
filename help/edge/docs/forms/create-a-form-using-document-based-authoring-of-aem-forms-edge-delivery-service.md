---
title: 使用基于文档的创作为 AEM Forms Edge Delivery Service 创建表单
description: 快速制作完美的表单！⚡ AEM Forms Edge Delivery + 基于文档的创作 = 速度极快、SEO 友好的表单，让用户更加满意，搜索引擎更加优异。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: ht
source-wordcount: '889'
ht-degree: 100%

---


# 使用基于文档的创作为 AEM Forms Edge Delivery Service 创建表单

在当今的数字时代，创建用户友好的表单对于任何组织都至关重要。AEM Forms Edge Delivery 的基于文档的创作功能让您能够使用 Word 或 Google Docs 等熟悉的工具创建表单。这些表单可将数据直接提交到 Microsoft Excel 或 Google Sheets 文件，使您能够使用 Google Sheets、Microsoft Excel 和 Microsoft Sharepoint 充满活力的生态系统和强大的 API，轻松处理提交的数据，或启动现有的业务工作流程。

本指南将会引导您完成：

* 准备电子表格：了解如何设置 Excel 或 Google Sheets 文件以进行数据收集并向其中添加表单字段。
* 将数据发送到工作表：了解如何使用 POST 请求将数据发送到工作表。
* 发布表单：将表单集成到 AEM Sites 页面或将其发布为独立页面。

无论您是新手还是专业人士，本指南都可以帮助您构建用户喜爱的美观、实用的表单。让我们来解锁高效的表单创建方式 - 现在就开始吧！

## 开始之前

`WIP`

## 准备电子表格以接收数据

1. 在 Microsoft OneDrive 或 Google Drive 上的 AEM Edge Delivery 项目目录下的任意位置创建一份 Microsoft Excel 工作簿或 Google 工作表。本文档使用名为 `contact-us.xlsx` 的 Google 工作表，其位于 Adobe Experience Manager (AEM) 项目的根目录。

1. 确保为您的项目配置的 AEM 用户（例如 helix@adobe.com）具有编辑工作表的权限。

1. 打开您创建的工作簿并将默认工作表的名称更改为“传入”。

   >[!NOTE]
   >
   > 如果“传入”工作表不存在，AEM 不会向此工作簿发送任何数据。

1. 在 Sidekick 中预览工作表。

   >[!NOTE]
   >
   >即使您之前已经预览过该工作表，在第一次创建“传入”工作表后也必须再次预览它。

1. 准备工作表，添加与您要输入的数据相匹配的标题。以下示例显示“联系我们”表单的字段：

   ![联系我们表格的字段](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   您可以手动执行此操作，也可以使用 AEM 管理服务中的表单路由的 POST 请求来执行此操作。管理服务将会检查 POST 正文中的数据，并生成有效获取数据并充分利用表单服务所需的适当标题、表格和工作表。

   要了解如何设置用于设置工作表的 POST 请求的格式，请参阅 [Admin API 文档](https://www.hlx.live/docs/admin.html#tag/form)。此外，请看下面提供的示例：

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
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country","PreferredContactMethod","SubscribeToNewsletter"]}%
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

虽然管理服务建议对您的工作表进行配置，但如果您希望手动创建标题，请参阅标题为[手动设置表单工作表](https://www.hlx.live/docs/manual-forms-sheet-setup)的文档。

在向管理服务提交 POST 请求后，您会在工作簿中观察到以下更改：

* 一份名为“shared-default”的新工作表将会被添加到您的 Excel 工作簿或 Google 工作表中。在向工作表发出 GET 请求时，系统将会检索“shared-default”工作表中存在的数据。该表是使用电子表格公式总结传入数据的最佳位置，使其有利于在其他情况下使用。

  在任何情况下，“shared-default”表都不应包含您不愿意公开的任何个人身份信息或敏感数据。

* 一份名为“slack”的工作表将会被添加到您的 Excel 工作簿或 Google 工作表中。在此工作表中，您可以在电子表格中引入新数据时为指定的 Slack 渠道配置自动通知。目前，AEM 仅支持向 AEM Engineering Slack 组织和 Adobe Enterprise 支持组织发送通知。

   1. 要设置 Slack 通知，请输入 Slack 工作区的“teamId”和“频道名称”或“ID”。您还可以向 slack-bot（使用调试命令）询问“teamId”和“channel ID”。最好使用“频道 ID”而不是“频道名称”，因为它在频道重命名后仍然有效。

      >[!NOTE]
      >
      > 旧的表单没有“teamId”列。“teamId”包含在频道列中，以“#”或“/”分隔。

   1. 输入您想要的任何标题，然后在字段下输入您想要在 Slack 通知中看到的字段的名称。每个标题应以逗号分隔（例如姓名、电子邮件）。

工作表现在已设置为可以接收数据，您可以使用 hlx.page、hlx.live 或您的生产域直接向其发送 POST 请求。


## 将数据发送到您的工作表 {#send-data-to-your-sheet}

将工作表设置为接收数据后，您可以使用 hlx.page、hlx.live 或您的生产域直接向其发送 POST 请求以发送数据。

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL 不应具有 .json 扩展。只有在发布工作表后，POST 操作才能在 .live 或生产域上运行。

### EDS Forms 数据格式化

您可以使用几种不同的方法来格式化 POST 正文中的表单数据。

* name:value 对数组：

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
              { "name": "message", "value": "I have some questions about your products." },
              { "name": "phone", "value": "123-456-7890" },
              { "name": "company", "value": "Example Inc." },
              { "name": "country", "value": "United States" },
              { "name": "preferred_contact_method", "value": "Email" },
              { "name": "newsletter_subscribe", "value": true }
              ]
          }'
  
* 具有 key:value 的对象

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

* `x-www-form-urlencoded` 正文（`content-type` 标题必须设置为 `application/x-www-form-urlencoded`）
&#39;firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



