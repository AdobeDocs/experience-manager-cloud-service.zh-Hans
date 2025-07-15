---
Title: How to use forms submission service for submitting forms?
Description: Learn how to use forms submission service for submitting forms.
Keywords: Use form submission service, Submit form using form submission service
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: 37b20a97942f381b46ce36a6a3f72ac019bba5b7
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 9%

---

# Forms提交服务与Edge Delivery Services Forms

<span class="preview"> 此功能通过早期访问计划提供。要请求获得访问权限，请通过您的官方地址向 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> 发送电子邮件，并附上您的 GitHub 组织名称和存储库名称。例如，如果存储库 URL 为 https://github.com/adobe/abc，则组织名称为 adobe，存储库名称为 abc。</span>

通过Forms提交服务，可将表单提交的数据存储为任意电子表格(如OneDrive、SharePoint或Google Sheets)，从而允许您在首选的电子表格平台中轻松访问和管理表单数据。

![Forms提交服务](/help/forms/assets/form-submission-service.png)

## 使用Forms提交服务的优势

将Forms提交服务与电子表格结合使用的一些优势包括：

* **直接集成**：您可以配置表单以将数据直接提交到指定的电子表格，而无需手动传输数据。
* **数据结构**：在设置提交时，可以将表单字段映射到相应的电子表格列，以便进行有条理的数据存储。
* **访问控制**：您可以利用现有权限来控制谁可以访问和修改提交的表单数据，具体取决于选择的电子表格服务。

## 先决条件

以下是使用Forms提交服务的先决条件：

* 确保您的AEM项目具有最新的自适应表单块。
* 确保将您的Git存储库添加到允许列表以使用Forms提交服务。 列入允许列表请将您的GitHub组织名称和存储库名称[mailto:aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)添加到中，以使用Forms提交服务。

## 配置Forms提交服务

创建配置有自适应AEM块的新Forms项目。 请参阅[快速入门 — 开发人员教程](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial)文章，了解如何创建新的AEM项目。 更新项目中的`fstab.yaml`文件。 将现有引用替换为您与`forms@adobe.com`共享的文件夹的路径。

您可以[手动配置Forms提交服务](#configuring-the-forms-submission-service-manually)或[使用API配置Forms提交服务](#configuring-the-forms-submission-service-using-api)。

### 手动配置Forms提交服务

表单提交服务的![工作流](/help/forms/assets/forms-submission-service-workflow.png)

#### 1.使用表单定义创建表单

使用Google Sheets或Microsoft Excel创作表单。 要了解如何使用Microsoft Excel或Google Sheets中的表单定义创建表单，请[单击此处](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)。

以下屏幕截图显示了用于创建表单的表单定义：

![表单定义](/help/forms/assets/form-submission-definition.png)

>[!IMPORTANT]
>
>**表单创作所在的工作表对其命名有限制。仅 `helix-default` 和 `shared-aem` 可用作工作表名称。**

#### 2.启用电子表格以接受数据。

创建并预览表单后，启用相应的电子表格以开始接收数据。 添加新工作表作为`incoming`。 您可以[手动启用电子表格以接受数据](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/submit-forms#manually-enable-the-spreadsheet-to-accept-data)。

![传入工作表](/help/forms/assets/form-submission-incoming-sheet.png)

>[!WARNING]
>
> 如果`incoming`工作表不存在，AEM将不会向此工作簿发送任何数据。

#### 3.共享电子表格并生成链接。

要将电子表格共享到`forms@adobe.com`帐户并生成链接，请执行以下步骤：

1. 在Excel或Google工作表中，单击右上角的&#x200B;**共享**&#x200B;按钮。
1. 添加`forms@adobe.com`帐户并
单击眼睛图标，选择**编辑**&#x200B;访问权限，然后单击&#x200B;**发送**。

   ![共享传入工作表](/help/forms/assets/form-submission-share-incoming.png)

1. 若要复制电子表格链接，请单击右上角的&#x200B;**共享**&#x200B;按钮，然后选择&#x200B;**复制链接**。

   ![复制传入工作表的链接](/help/forms/assets/form-submission-copy-link.png)

#### 4.在表单定义中链接电子表格

要使用Google Sheets或Microsoft Excel配置Forms提交服务，请执行以下步骤：

1. 打开包含表单定义的电子表格。
1. 在与&#x200B;**提交**&#x200B;字段对应的行中，将复制的电子表格链接粘贴到&#x200B;**操作**&#x200B;列。

   ![链接电子表格](/help/forms/assets/form-submission-sheet-linking.png)

1. 使用带有更新后的表单提交服务的[AEM Sidekick](https://www.aem.live/docs/sidekick)预览和发布工作表。

>[!NOTE]
>
> 您可以参考[电子表格](/help/forms/assets/spreadsheet.xlsx)以使用Forms提交服务。

### 使用API配置Forms提交服务

您还可以向表单发送&#x200B;**POST**&#x200B;请求，以使用数据更新`incoming`工作表。

>[!NOTE]
>
> * 如果`incoming`工作表不存在，AEM将不会向此工作簿发送任何数据。
> * 将`incoming`工作表与Adobe Experience Manager共享`forms@adobe.com`并授予编辑权限。
> * 在Sidekick中预览和发布`incoming`工作表。

要了解如何设置POST请求的格式以设置工作表，请参阅[API文档](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)。 您可以查看下面提供的示例：

您可以使用curl或Postman等工具来执行此POST请求，如下所示。

* **使用Postman**：

例如，在替换后在Postman中发送以下请求：
* `{id}`包含您的表单ID
* `site or repository`包含您的GitHub存储库或站点名称
* 使用您的GitHub用户名`organization`

  ```json
  POST 'https://forms.adobe.com/adobe/forms/af/submit/{id}' \
  --header 'Content-Type: application/json' \
  --header 'x-adobe-routing: tier=live,bucket=main--[site/repository]--[organization]' \
  --data '{
      "data": {
          "startDate": "2025-01-10",
          "endDate": "2025-01-25",
          "destination": "Australia",
          "class": "First Class",
          "budget": "2000",
          "amount": "1000000",
          "name": "Mary",
          "age": "35",
          "subscribe": null,
          "email": "mary@gmail.com"
              }
          }'
  ```

单击Postman中的&#x200B;**发送**&#x200B;按钮将返回`201 Created`响应，并且`incoming`工作表将更新所提交的数据。

![Postman屏幕](/help/forms/assets/postman-api.png)

* **使用Curl命令**：

例如，更换后，在终端或命令提示符下执行以下命令：
* `{id}`包含您的表单ID
* `site or repository`包含您的GitHub存储库或站点名称
* 使用您的GitHub用户名`organization`


>[!BEGINTABS]

>用于macOS的[!TAB ]

    ``json
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; \
     — header &quot;Content-Type： application/json&quot; \
     — header &quot;x-adobe-routing： tier=live，bucket=main—[site/repository]—[organization]&quot; \
     — data `{
    `data&quot;： {
    `startDate&quot;： &quot;2025-01-10&quot;，
    `endDate&quot;： &quot;25-25&quot;，
    `destination&quot;：澳大利亚”，
    “class”：“First Class”，
    “budget”：“2000”，
    “amount”：“1000000”，
    “name”：“Joe”，
    “age”：“35”，
    “subscribe”： null，
    “email”：“mary@gmail.com”
    }
    }&#39;
    
    ”&#39;

>用于Windows操作系统的[!TAB ]

    ``json
    
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; ^
     — 标头&quot;Content-Type： application/json&quot; ^
     — 标头&quot;x-adobe-routing： tier=live，bucket=main—[site/repository]—[organization]&quot; ^
     — 数据&quot;{\&quot;data\&quot;： {\&quot;startDate\&quot;： \&quot;2025-01-10\&quot;， \&quot;endDate\&quot;： \&quot;2025-01-25\&quot;： \&quot;Destination\&quot; australia\&quot;， \&quot;class\&quot;： \&quot;First Class\&quot;， \&quot;budget\&quot;： \&quot;2000\&quot;， \&quot;amount\&quot;： \&quot;1000000\&quot;， \&quot;name\&quot;： \&quot;Joe\&quot;， \&quot;age\&quot;： \&quot;35\&quot;， \&quot;subscribe\&quot;： null， \&quot;email\&quot;： \&quot;mary@gmail.com\&quot;}}&quot;
    
    &quot;&#39;

>[!ENDTABS]

上述POST请求使用以下响应更新`incoming`表：

```json
    < HTTP/1.1 201 Created
    < Connection: keep-alive
    < Content-Length: 0
    < X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
    < X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
    < Accept-Ranges: bytes
    < Date: Fri, 10 Jan 2025 13:06:10 GMT
    < Via: 1.1 varnish
    < Access-Control-Allow-Origin: *
    < X-Served-By: cache-del21750-DEL
    < X-Cache: MISS
    < X-Cache-Hits: 0
    < X-Timer: S1736514370.704084,VS0,VE1234
```

以下屏幕显示了使用API发送数据所更新的`incoming`工作表的屏幕截图：

![已更新工作表](/help/forms/assets/updated-sheet.png)

## 另请参阅

{{see-more-forms-eds}}