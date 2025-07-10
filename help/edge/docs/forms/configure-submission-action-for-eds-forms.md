---
title: 使用Edge Delivery Services为AEM Forms配置提交操作
description: 了解如何使用Edge Delivery Services在AEM Forms中配置提交操作。 在Forms提交服务和AEM发布提交操作之间进行选择，以安全高效地处理表单数据。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 75d8ea4f0913e690e3374d62c6e7dcc44ea74205
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---

# 配置表单提交：您的数据流向何处？

用户单击表单上的&#x200B;**提交**&#x200B;后，您需要告诉Edge Delivery Services如何处理该数据。 您有两个主要选项：

## 方法1：使用AEM Forms提交服务（简化）

此服务非常适用于常见的、简单的操作，例如将数据发送到电子表格或电子邮件。

**它有什么能帮到您？**

[Forms提交服务](/help/forms/forms-submission-service.md)是Adobe托管的端点。 当您的表单向其提交数据时，此服务会接管系统并执行预配置的操作。 它设计为易于设置。 您可以配置：提交到电子表格或电子邮件：

* **提交到电子表格：**&#x200B;自动将提交的表单数据作为新行添加到Google工作表或Microsoft Excel文件(存储在OneDrive或SharePoint上)中。
* **发送电子邮件：**&#x200B;将包含表单数据的电子邮件发送到您指定的一个或多个电子邮件地址。

#### 重要信息：设置要求

* **电子表格访问：**&#x200B;若要将数据发送到OneDrive/SharePoint上的Google工作表或Excel文件，Adobe服务帐户（通常为`forms@adobe.com`）通常需要对该特定电子表格具有&#x200B;**编辑权限**。
* **提前访问计划：**&#x200B;此服务的某些功能（特别是电子表格功能）可能包含在提前访问计划中。 您可能需要通过电子邮件发送`aem-forms-ea@adobe.com`或填写包含项目详细信息的特定Adobe表单来请求访问权限。 请始终查看最新的Adobe文档。

**Forms提交服务流程图**
<!--
```mermaid
    graph TD
    UserForm[User Submits Form on Your EDS Site] >|Data Sent| FormSubmissionService[AEM Forms Submission Service]
    FormSubmissionService -- "If configured for Google Sheets" > GoogleSheet[Data written to Google Sheet]
    FormSubmissionService -- "If configured for Excel (OneDrive or SharePoint)" > ExcelSheet[Data written to Excel]
    FormSubmissionService -- "If configured for Email" > Email[Email with data is sent]

    style UserForm fill:#ccf,stroke:#333
    style FormSubmissionService fill:#fca,stroke:#333
    style GoogleSheet fill:#90ee90,stroke:#333
    style ExcelSheet fill:#90ee90,stroke:#333
    style Email fill:#add8e6,stroke:#333
```-->

![Forms提交](/help/forms/assets/eds-fss.png)

此流程图显示Forms提交服务如何接收提交的数据并将其发送到配置的电子表格或电子邮件。

## 方法2：提交到您的AEM发布实例（高级）

对于更复杂的需求，[表单（尤其是使用通用编辑器创建的表单）可以直接将数据发送到您的AEM as a Cloud Service发布实例](/help/forms/configure-submit-actions-core-components.md)。 这将解锁AEM的全部后端功能。

**您何时需要提交到AEM Publish？**

* 在提交后触发自定义AEM工作流。
* 使用AEM表单数据模型(FDM)与数据库或其他企业系统集成。
* 连接到Marketo、Microsoft Power Automate或Adobe Workfront Fusion等第三方服务。
* 将数据存储在Azure Blob Storage或SharePoint列表/文档库等特定位置（不只是简单的电子表格）。
* 当您在AEM中进行复杂的服务器端验证或数据处理逻辑时。

**可用提交操作(AEM发布提交)**

* [提交到REST端点](/help/forms/configure-submit-action-restpoint.md)
* [发送电子邮件(使用AEM的邮件服务)](/help/forms/configure-submit-action-send-email.md)
* [使用表单数据模型(FDM)提交](/help/forms/configure-data-sources.md)
* [调用 AEM 工作流](/help/forms/aem-forms-workflow-step-reference.md)
* [提交到SharePoint（作为列表项或文档）](/help/forms/configure-submit-action-sharepoint.md)
* [提交到OneDrive（作为文档）](/help/forms/configure-submit-action-onedrive.md)
* [提交到 Azure Blob 存储](/help/forms/configure-submit-action-azure-blob-storage.md)
* [提交到Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [提交到Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [提交到Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> 即使从AEM Publish定位Google Sheet/Excel，它涉及的配置步骤与直接的Forms提交服务不同。

**AEM发布提交流程图**

<!--```mermaid
    graph TD
    UEForm[User Submits Universal Editor Form on EDS Site] >|Data sent to AEM Publish URL - example: /adobe/forms/af/submit/...| AEMPublish[AEM Publish Instance]
    AEMPublish -- Configured to run AEM Workflow > AEMWorkflow[AEM Workflow is Triggered]
    AEMPublish -- Configured to use Form Data Model > FDM[FDM updates Backend System or Database]
    AEMPublish -- Configured for Marketo > Marketo[Data sent to Marketo Engage]
    AEMPublish -- Other configured actions... > OtherIntegrations[...]

    style UEForm fill:#ccf,stroke:#333
    style AEMPublish fill:#fca,stroke:#333
    style AEMWorkflow fill:#add8e6,stroke:#333
    style FDM fill:#add8e6,stroke:#333
    style Marketo fill:#add8e6,stroke:#333
```-->

![AEM发布提交流程图](/help/forms/assets/eds-aem-publish.png)
此流程图显示了提交到AEM Publish的表单，然后该表单处理复杂的后端任务。

### Forms提交服务与AEM发布提交之比较

| 功能 | Forms提交服务 | AEM发布提交内容 |
| :- | :- | :-- |
| **最适合** | 简单的数据捕获到电子表格、电子邮件通知 | 复杂的工作流、企业集成、自定义逻辑 |
| **表单创作** | 适用于基于文档的；适用于简单的UE表单 | Best for Universal Editor创作表单 |
| **设置工作** | 低（通常为简单的配置） | 更高(需要AEM Publish、Dispatcher、OSGi、CDN设置) |
| **后端系统** | Adobe托管服务 | 您的AEM as a Cloud Service发布实例 |
| **灵活性** | 仅限于工作表/电子邮件 | 非常灵活的全套AEM Forms操作 |
| **示例** | 将表单数据联系到Google工作表 | 贷款申请触发AEM审批工作流 |

## 如何在不同网站或页面中嵌入Forms

有时，您会希望在其他网页或网站的一个位置（例如，集中式“表单站点”）显示创建并管理的表单。

### 为什么要嵌入表单？

* 您有一个使用通用编辑器创建的标准“联系我们”表单，该表单需要显示在使用基于文档的创作构建的多个登陆页面上。
* 您的主网站内容位于文档创作(DA)中，您需要包含专门的表单。
* 您想在多个不同的EDS项目中重复使用单个维护良好的表单。

### 从技术上讲表单嵌入的工作原理

您希望在其中显示表单的页面（我们将其称为“主机页面”）将包含一些代码（通常是特殊块或脚本）。 当用户访问主机页面时，此代码会对托管实际表单的URL发出请求(我们将其称为“表单Source”)。 表单Source然后发送回其HTML，主机页面将插入并显示该表单。

**嵌入式表单架构**

<!--```mermaid
   graph LR
    User[User] >|Visits| HostPage[Host Page - for example: your-site.com/landing-page]
    HostPage >|Contains code to embed form| FetchForm{Host Page Requests Form HTML}
    FetchForm >|HTTP GET request to the form URL| FormSource[Form Source - for example: forms-repo.hlx.page/my-form]
    FormSource >|Returns form HTML| FetchForm
    FetchForm >|Injects form HTML into page| HostPage
    HostPage >|Displays full page with embedded form| User

    subgraph Submission ["Form Submission from Host Page"]
        HostPage_Form[Embedded form on the host page] >|User submits| TargetEndpoint[Submission endpoint - FSS or AEM Publish]
    end

    style HostPage fill:#e6f3ff,stroke:#333
    style FormSource fill:#ffe6e6,stroke:#333
    style FetchForm fill:#fff2cc,stroke:#333
    style Submission fill:#f0fff0,stroke:#333
```-->

![嵌入式表单架构](/help/forms/assets/eds-embedded-form.png)
此图显示了从表单Source中提取表单HTML并显示该表单的主机页面。 提交使用原始表单配置的端点。

## 为嵌入式Forms设置CORS

[CORS（跨源资源共享）](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)是浏览器安全功能。 如果您的主机页面（如`site-a.com`）尝试从其他域（如`forms-site-b.com`）获取表单，则浏览器将阻止它，除非`forms-site-b.com`明确允许通过CORS标头获取表单。

如果&#x200B;**Form Source服务器**&#x200B;上没有正确的CORS标头，浏览器将阻止Host Page加载该表单，并且不会显示您嵌入的表单。

### 如何在提供表单的网站上配置CORS？

您需要将托管&#x200B;**表单Source**&#x200B;的服务器配置为在响应中发送特定的HTTP标头。 确切的方法取决于您的EDS设置（例如，对于Franklin项目，这通常在控制CDN行为或边缘工作器逻辑的GitHub存储库中的`helix-config.yaml`或类似配置文件中完成）。
要添加到表单Source响应的键标头：

* `Access-Control-Allow-Origin: <URL_of_Host_Page>` （例如，`https://your-site.com`）。 对于测试，您可以使用`*`，但对于生产，请指定确切的域。
* `Access-Control-Allow-Methods: GET, OPTIONS` （如果表单提交本身也是跨源的，但通常提交到单独的，通常是同源或专门配置的端点，则您可能需要`POST`）。
* `Access-Control-Allow-Headers: Content-Type` （以及您的表单提取可能使用的任何其他自定义标头）。

**示例（配置文件的概念）：**

```yaml
        # In the configuration for the site HOSTING THE FORM (Form Source)
        headers:
          # Apply to paths where your forms are served, e.g., /forms/**
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-page-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS
```

## 其他注意事项：CDN和多个代码库(Helix 4)

* **CDN规则：**&#x200B;您的CDN可能会提供代理请求的方法。 例如，对`host-page.com/embedded-form`的请求可以由CDN在内部路由以从`form-source.com/actual-form`获取内容，从而使它对于浏览器显示为相同来源。 设置过程可能比较复杂。
* **多个代码库(Helix 4)：**&#x200B;如果您的Host Page和Form Source位于不同的GitHub存储库中（Helix 4设置中很常见），请确保呈现或管理表单所需的任何JavaScript“表单块”在Host Page的代码库中可用，或者从Form Source中获取的表单HTML自包含及其所有必需的JavaScript。 原始文档提到，对于“具有不同代码库的helix4，则需要在这两个代码库上添加Form块。”

### 常见体系结构设置和配置步骤

以下是设置表单的一些常用方法，这些方法结合了创作方法和提交策略以及关键配置点。

#### 提交电子表格/电子邮件的基于文档的表单

这是最简单的设置。 您在Word/Google Docs中创建表单，并通过Forms提交服务将数据提交到电子表格或电子邮件。

1. 在Word/Google文档/工作表中使用指定的表结构或表单块定义表单。
1. 在文档（或相关配置）中，指定Forms提交服务的目标电子表格URL或电子邮件地址。
1. 确保`forms@adobe.com`（或相关的服务帐户）具有目标电子表格的编辑访问权限。
1. 将文档发布到Edge Delivery网站。

**基于Doc的+Forms提交服务架构**
<!--
```mermaid
    graph TD
        User[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User] >|Fills Out| EDS_Page_DocBased[EDS Page with Document-Based Form]
        EDS_Page_DocBased >|Submits Data| FSS[AEM Forms Submission Service]
        FSS > Target[<img src='https://img.icons8.com/color/48/000000/google-sheets.png' width='30' /> Data to Spreadsheet / <img src='https://img.icons8.com/color/48/000000/filled-sent.png' width='30' /> Email Notification]

        Authoring[Form defined in Google Doc/Sheet] >|EDS Syncs & Renders| EDS_Page_DocBased

        style EDS_Page_DocBased fill:#ccf,stroke:#333
        style FSS fill:#fca,stroke:#333
        style Target fill:#90ee90,stroke:#333
        style Authoring fill:#e6ffe6,stroke:#333
```-->

![基于Doc的+Forms提交服务架构](/help/forms/assets/eds-doc-fss.png)

#### 带有电子表格/电子邮件提交的通用编辑器表单

您可以使用可视通用编辑器来构建表单，但还是使用简单的Forms提交服务来捕获数据。

1. 使用AEM中的通用编辑器创建表单。
1. 在UE中配置表单的提交操作，以使用“提交到Forms提交服务”选项。
1. 指定目标电子表格URL或电子邮件地址。
1. 如果使用电子表格，请确保`forms@adobe.com`具有编辑权限。
1. 将包含表单的页面从AEM发布到Edge Delivery网站。

   **通用编辑器+ Forms提交服务架构**

   ![通用编辑器+ Forms提交服务架构](/help/forms/assets/eds-ue-fss.png)

   <!--```mermaid
    graph TD
    User[User] >|Fills Out| EDS_Page_UE[EDS Page with Universal Editor Form]
    EDS_Page_UE >|Submits Data| FSS[AEM Forms Submission Service]
    FSS > Target[Data sent to Google Sheet and Email Notification]
    AuthoringUE[Form built in Universal Editor - AEM] >|AEM Publishes to EDS| EDS_Page_UE
    style EDS_Page_UE fill:#ccf,stroke:#333
    style FSS fill:#fca,stroke:#333
    style Target fill:#90ee90,stroke:#333
    style AuthoringUE fill:#e6f3ff,stroke:#333
    ```
    -->

#### 具有AEM发布提交的通用编辑器表单（高级）

此设置使用通用编辑器创建表单，并使用AEM Publish实例进行强大的后端处理（工作流、FDM等）。 这需要更多的配置。

1. **在UE中创建表单：**&#x200B;在通用编辑器中构建您的表单。 配置其提交操作以指向AEM Forms操作(例如“调用AEM工作流”、“使用表单数据模型提交”)。
1. **AEM Dispatcher配置(在您的AEM发布层上)：**
   * **无重定向：**&#x200B;确保您的Dispatcher规则&#x200B;*不会*&#x200B;向`/adobe/forms/af/submit/...`路径发出的重定向请求。
   * **允许提交：**&#x200B;修改您的Dispatcher筛选器（例如，在`filters.any`中）以明确地将来自Edge Delivery网站的域或IP地址的`allow`个POST请求`/adobe/forms/af/submit/...`。
1. AEM中的&#x200B;**OSGi反向链接筛选器(在您的AEM发布层上)：**
   * 在AEM OSGi控制台(`/system/console/configMgr`)中，查找并配置“Apache Sling引用过滤器”。
   * 将Edge Delivery站点的域（例如`https://your-eds-domain.hlx.page`、`https://your-custom-eds-domain.com`）添加到“允许主机”或“允许主机正则表达式”列表。 这会告知AEM接受来自您的EDS网站的提交内容。
1. **CDN重定向规则(在您的Edge Delivery CDN上)：**
   * 您的Edge Delivery站点（例如，`your-eds-domain.hlx.page`）需要正确地将提交请求路由到您的AEM发布实例。
   * 当您EDS页面上的表单提交时，它可能会定向相对路径，如`/adobe/forms/af/submit/...`。 您的Edge Delivery CDN（或Edge Worker）上需要一条规则，其中显示：“如果请求到达`your-eds-domain.hlx.page/adobe/forms/af/submit/...`，请将其转发（代理或重定向）到`your-aem-publish-instance.com/adobe/forms/af/submit/...`。”
   * 确切的实施取决于您的CDN提供商（例如，Fastly VCL、Akamai属性管理器、Cloudflare工作程序）。
1. **（可选） `constants.js`用于开发（在您的EDS项目的代码库中）：**
   * 对于本地开发，或者如果您的客户端表单脚本需要知道完整的AEM发布URL，您可以在Edge Delivery项目的GitHub存储库中的`constants.js`或类似配置文件中配置此项。 示例：

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **发布：**&#x200B;将您的表单页面从AEM发布到EDS，并确保所有AEM配置在您的AEM发布实例上都处于活动状态。

   **通用编辑器+ AEM发布架构**

![通用编辑器+ AEM发布架构](/help/forms/assets/eds-aem-publish.png)

这显示了流程：用户在EDS网站上提交，CDN路由到AEM Dispatcher，然后AEM发布处理它。

#### 将表单嵌入文档创作(DA)页面

您的主网站内容是在文档创作(DA)中创建的。 您可以分别使用基于文档的创作或通用编辑器创建表单，然后将其嵌入到您的DA页面。

1. **创建并发布表单：**
   * 使用基于文档的创作或通用编辑器创建表单。
   * 配置其提交方法(根据设置1、2或3，提交到Forms提交服务或AEM Publish)。
   * 发布此表单，使其驻留在自己的Edge Delivery URL上（例如`.../forms/my-special-form`）。
1. **配置CORS：**&#x200B;在托管此独立表单的Edge Delivery站点/项目上，确保已将CORS标头设置为允许文档创作站点的域提取它。
1. **在DA中创作页面：**&#x200B;在文档创作中创建或编辑您的页面。
1. **嵌入表单块：**&#x200B;在DA中使用适当的块嵌入外部URL。 将此块指向独立发布表单的URL。
1. **发布DA页面：**&#x200B;发布您的DA页面。 现在将获取并显示表单。

   **Forms嵌入到DA架构中**

   ![Forms嵌入到DA架构中](/help/forms/assets/eds-forms-embedd-da.png)

   此图显示了从其他EDS位置提取表单的DA页面。 嵌入表单处理其自身的提交。

## 疑难解答

* **我的表单提交无法正常进行。**
   * **检查控制台错误：**&#x200B;打开浏览器的开发人员控制台（通常为F12），并在提交时在“网络”选项卡或“控制台”选项卡上查找错误。
   * **验证提交URL：**&#x200B;表单是否正在尝试提交到正确的端点(Forms提交服务URL或AEM发布路径)？
   * **Forms提交服务：**&#x200B;如果发送到电子表格，是否授予`forms@adobe.com`编辑权限？ 电子表格URL是否正确？
   * **AEM发布提交：**
      * 您的Dispatcher是否允许向`/adobe/forms/af/submit/...`发布帖子？
      * AEM发布上的Sling引用过滤器是否已配置为允许您的EDS域？
      * 您针对`/adobe/forms/af/submit/...`的CDN重定向规则是否正常工作？

* **我的嵌入表单未出现。**

   * **CORS！**&#x200B;这是最常见的原因。 检查浏览器控制台是否存在CORS错误。 确保托管&#x200B;*表单的网站*&#x200B;具有正确的`Access-Control-Allow-Origin`标头。
   * **表单URL是否正确？**&#x200B;主机页面上的嵌入代码是否指向表单的正确实时URL？
   * **JavaScript块：**&#x200B;如果表单依赖于特定的JavaScript“表单块”进行渲染，该块的代码是否可在主机页面上使用？

* **我在提交到AEM Publish时收到“403禁止访问”或“401未授权”。**

   * 这通常指向AEM发布上的Sling引用过滤器，不允许来自EDS域的请求。 仔细检查其配置。
   * 如果您的AEM提交端点需要身份验证/授权问题，尽管标准表单提交通常是匿名的。

## 后续步骤

本指南概述了如何将表单与AEM Edge Delivery Services结合使用。 有关特定配置的更多详细分步说明，请参阅Adobe Experience Manager官方文档：

* [使用Edge Delivery Services Forms进行基于文档的创作](/help/edge/docs/forms/tutorial.md)
* [带有Edge Delivery Services Forms的通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [文档创作(DA)和嵌入内容](https://www.aem.live/developer/da-tutorial)
* [AEM Forms提交服务](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
