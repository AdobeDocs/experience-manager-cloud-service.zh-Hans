---
title: 使用基于文档的创作为AEM Forms Edge Delivery服务创建表单
description: 制作完美的表单，快！ ⚡ AEM Forms Edge交付+基于文档的创作=超快的速度和SEO友好的表单，适合更开心的用户和搜索引擎。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f2752673dcaa0762bb55719cee23765aa8ecde96
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---


# 使用基于文档的创作为AEM Forms Edge Delivery服务创建表单

在当今的数字时代，创建用户友好的表单对于任何组织都至关重要。 AEM Forms Edge Delivery的基于文档的创作允许您使用熟悉的工具(如Word或Google文档)创建表单。这些表单将数据直接提交到Microsoft Excel或Google Sheets文件，使您能够使用生动的生态系统和强大的API(包括Google Sheets、Microsoft Excel和Microsoft Sharepoint)，轻松处理提交的数据或启动现有的业务工作流。

本指南将指导您完成以下步骤：

* 准备电子表格：了解如何设置Excel或Google工作表文件以进行数据收集并向其中添加表单字段。
* 将数据发送到工作表：了解如何使用POST请求将数据发送到工作表。
* 发布表单：将表单集成到AEM Sites页面或作为独立页面发布。

无论您是新手还是专业人士，本指南都使您能够构建用户喜欢的精美、功能化的表单。 让我们解锁高效的表单创建 — 立即行动！

## 开始之前

`WIP`

## 准备电子表格以接收数据

1. 在Microsoft OneDrive或Google驱动器上AEM Edge Delivery项目目录下的任意位置创建Microsoft Excel工作簿或Google工作表。 本文档使用名为的Google工作表 `contact-us.xlsx`，位于Adobe Experience Manager (AEM)项目的根目录。

1. 确保为项目配置的AEM用户(例如helix@adobe.com)具有工作表的编辑权限。

1. 打开您创建的工作簿，并将默认工作表的名称更改为“传入”。

   >[!NOTE]
   >
   > 如果“传入”工作表不存在，AEM将不会向此工作簿发送任何数据。

1. 在助手中预览工作表。

   >[!NOTE]
   >
   >即使您以前预览过工作表，也必须在首次创建“传入”工作表后再次预览它。

1. 通过添加与您输入的数据匹配的标头来准备工作表。 以下示例显示“contact-us”表单的字段：

   ![联系方式表单的字段](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   您可以手动执行此操作，也可以使用AEM管理服务中表单路由的POST请求执行此操作。 Admin服务将检查POST正文中的数据，并生成有效摄取数据并充分利用Forms服务所需的相应标题、表和工作表。

   要了解如何设置POST请求的格式以设置工作表，请参阅 [管理员API文档](https://www.hlx.live/docs/admin.html#tag/form). 此外，请查看以下提供的示例：

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

   您可以使用curl或Postman等工具来执行此POST请求，如下所示：

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

上述POST请求提供样本数据，包括表单字段及其各自样本值。 Admin服务使用此数据来设置表单。

虽然Admin服务建议配置您的工作表，但如果您希望手动创建标头，请参阅文档 [手动设置Forms工作表](https://www.hlx.live/docs/manual-forms-sheet-setup).

在将POST请求提交给Admin Service后，您将在工作簿中看到以下更改：

* 名为“shared-default”的新工作表将添加到Excel工作簿或Google工作表中。 在对工作表发出GET请求时，将检索“shared-default”工作表中存在的数据。 此工作表用作使用电子表格公式汇总传入数据的最佳位置，使其有利于在其他上下文中使用。

  在任何情况下，“shared-default”工作表都不应包含任何您不希望公开访问的个人身份信息或敏感数据。

* 名为“slack”的工作表将添加到Excel工作簿或Google工作表中。 在此工作表中，您可以在电子表格中摄取新数据时为指定的Slack渠道配置自动通知。 目前，AEM仅支持向AEM工程Slack组织和Adobe企业支持组织发送通知。

   1. 要设置Slack通知，请输入Slack工作区的“teamId”以及“渠道名称”或“ID”。 您还可以向slack-bot（使用调试命令）询问“teamId”和“渠道ID”。 最好使用“渠道ID”而不是“渠道名称”，因为它在渠道重命名之后仍然可用。

      >[!NOTE]
      >
      > 旧表单没有“teamId”列。 “teamId”包含在渠道列中，以“#”或“/”分隔。

   1. 输入所需的任何标题，并在字段下输入要在Slack通知中看到的字段名称。 每个标题应用逗号分隔（例如姓名、电子邮件）。

工作表现在设置为接收数据，您可以使用hlx.page、hlx.live或您的生产域直接向其发送POST请求。


## 将数据发送到工作表 {#send-data-to-your-sheet}

将工作表设置为接收数据后，您可以使用hlx.page、hlx.live或您的生产域直接向其发送POST请求以发送数据。

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL不应具有.json扩展名。 您必须发布工作表才能在.live或生产域上执行POST操作。

### 为EDS Forms格式化数据

可通过以下几种方式在POST正文中格式化表单数据。

* 名称：值对的数组：

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
  
* 具有键：值对的对象

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

* `x-www-form-urlencoded` 正文(`content-type` 标题必须设置为 `application/x-www-form-urlencoded`) &#39;firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



