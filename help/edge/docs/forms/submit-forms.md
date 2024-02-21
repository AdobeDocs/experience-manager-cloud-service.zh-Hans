---
title: 从电子表格到Forms — 掌握表单块字段验证
description: 使用电子表格和表单块字段更快地制作功能强大的表单！ 本指南可帮助您为EDS Forms块字段构建自定义验证。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---


# 启用表单以发送数据

创建和预览表单后，启用相应的工作表以接受数据。 要开始接受数据，请将电子表格设置为包含与要收集的数据匹配的标头。 添加到“shared-default”工作表的所有标头还应该出现在表下的“incoming”工作表中。

以下示例显示“contact-us”表单的字段：

![联系方式表单的字段](/help/edge/assets/contact-us-form-excel-sheet-fields.png)


完成此设置后，您的表单即准备好接受提交。 您可以采用以下方法之一，使电子表格能够接受数据：

* [手动配置电子表格以接受数据](#manually-configure-a-spreadsheet-to-receive-data)

* [使用管理员API启用电子表格以接受数据](#use-admin-apis-to-enable-a-spreadsheet-to-receive-data-use-admin-apis-to-enable-a-spreadsheet-to-recieve-data)

## 手动配置电子表格以接受数据

要手动配置电子表格以接受数据，请执行以下操作：


1. 打开您创建的工作簿，并将默认工作表的名称更改为“传入”。

   >[!WARNING]
   >
   > 如果“传入”工作表不存在，AEM将不会向此工作簿发送任何数据。

1. 通过添加与您输入的数据匹配的标头来准备工作表。 以下示例显示“contact-us”表单的字段：

   ![联系方式表单的字段](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. 在助手中预览工作表。

   >[!NOTE]
   >
   >即使您以前预览过工作表，也必须在首次创建“传入”工作表后再次预览它。


## 使用管理员API启用电子表格以接受数据

您可以在AEM Admin服务内向表单路由发起POST请求。 在收到POST正文数据后，管理员服务对其进行分析并自主生成数据摄取所需的基本标题、表和工作表，从而优化表单服务的功能。

要使用管理员API启用电子表格来接受数据，请执行以下操作：


1. 打开您创建的工作簿，并将默认工作表的名称更改为“传入”。

   >[!WARNING]
   >
   > 如果“传入”工作表不存在，AEM将不会向此工作簿发送任何数据。

1. 在助手中预览工作表。

   >[!NOTE]
   >
   >即使您以前预览过工作表，也必须在首次创建“传入”工作表后再次预览它。

1. 通过添加与您输入的数据匹配的标头来准备工作表。

   为此，您可以向AEM Admin服务中的表单路由发送POST请求。 管理服务会检查POST正文中的数据，并生成有效摄取数据并充分利用Forms服务所需的相应标题、表和工作表。

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
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country",      "PreferredContactMethod","SubscribeToNewsletter"]}%
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

   前面提到的POST请求提供了示例数据，包括表单字段及其各自的示例值。 Admin服务使用此数据设置表单。

   将POST请求提交到Admin Service后，您会在工作簿中看到以下更改：

* 名为“shared-default”的新工作表将添加到Excel工作簿或Google工作表中。 在对工作表发出GET请求时，将检索“shared-default”工作表中存在的数据。 此工作表用作使用电子表格公式汇总传入数据的最佳位置，使其有利于在其他上下文中使用。

  “shared-default”工作表绝不应包含任何您不希望公开访问的个人身份信息或敏感数据。

* 名为“Slack”的工作表将添加到Excel工作簿或Google工作表中。 在此工作表中，您可以在电子表格中摄取新数据时为指定的Slack渠道配置自动通知。 目前，AEM仅支持向AEM工程Slack组织和Adobe企业支持组织发送通知。

   1. 要设置Slack通知，请输入Slack工作区的“teamId”以及“渠道名称”或“ID”。 您还可以向slack-bot（使用调试命令）询问“teamId”和“渠道ID”。 最好使用“渠道ID”而不是“渠道名称”，因为它在渠道重命名之后仍然可用。

      >[!NOTE]
      >
      > 旧表单没有“teamId”列。 “teamId”包含在渠道列中，以“#”或“/”分隔。

   1. 输入所需的任何标题，并在字段下输入要在Slack通知中看到的字段名称。 每个标题应用逗号分隔（例如姓名、电子邮件）。

工作表现在设置为接收数据，您可以 [使用表单块预览表单](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) 或 [使用POST请求](#use-admin-apis-to-send-data-to-your-sheet) 开始将数据发送到工作表。



## 将数据发送到工作表 {#send-data-to-your-sheet}

将工作表设置为接收数据后，您可以 [使用表单块预览表单](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) 或 [使用管理员API](#use-admin-apis-to-send-data-to-your-sheet) 开始将数据发送到工作表。

### 使用管理员API将数据发送到工作表

您可以使用hlx.page、hlx.live或生产域直接将POST请求发送到您的表单以发送数据。


```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL不应具有.json扩展名。 您必须发布工作表才能对其执行POST操作 `.live` 或在生产域中。

#### 格式化表单数据

可通过几种不同方式在POST正文中格式化表单数据。 您可以使用：

* 数组 `name:value` 对：

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



* 对象 `key:value` 对：

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

* URL已编码(`x-www-form-urlencoded`)正文(带 `content-type` 标题设置为 `application/x-www-form-urlencoded`)

  ```Shell
  'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'
  ```

  例如，

  ```Shell
  curl -s -i -X POST \
    -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
    https://main--portal--wkndforms.hlx.live/contact-us
  ```

接下来，您可以自定义感谢消息， [配置感谢页面](/help/edge/docs/forms/thank-you-page-form.md)，或 [设置重定向](/help/edge/docs/forms/thank-you-page-form.md).

## 查看更多

* [创建和预览表单](/help/edge/docs/forms/create-forms.md)
* [启用表单以发送数据](/help/edge/docs/forms/submit-forms.md)
* [将表单发布到站点页面](/help/edge/docs/forms/publish-eds-forms.md)
* [向表单字段添加验证](/help/edge/docs/forms/validate-forms.md)
* [更改表单的主题和样式](/help/edge/docs/forms/style-theme-forms.md)