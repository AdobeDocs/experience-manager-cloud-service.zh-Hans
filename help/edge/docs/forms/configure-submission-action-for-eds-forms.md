---
title: 为集成 Edge Delivery Services 的 AEM Forms 配置提交操作
description: 了解如何在使用 Edge Delivery Services 的 AEM Forms 中配置提交操作。在 Forms Submission Service 与 AEM Publish Submit Action 之间进行选择，以安全高效地处理表单数据。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 75d8ea4f0913e690e3374d62c6e7dcc44ea74205
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 99%

---

# 配置表单提交：您的数据会去哪儿？

当用户点击表单上的&#x200B;**提交**&#x200B;后，您需要告诉 Edge Delivery Services 如何处理这些数据。您有两个主要选项：

## 方法 1：使用 AEM Forms Submission Service（简单）

该服务非常适合执行常见且简单的操作，例如将数据发送到电子表格或电子邮件。

**什么是 Forms Submission Service，它能为您带来哪些帮助？**

[Forms Submission Service](/help/forms/forms-submission-service.md) 是一个由 Adobe 托管的端点。当表单将数据提交至该服务后，它会接管并执行预先配置的操作。该服务旨在简化设置过程。您可以配置将数据提交至电子表格或电子邮件：

* **提交到电子表格：**&#x200B;自动将已提交的表单数据添加为 Google Sheets 或 Microsoft Excel 文件（存储于 OneDrive 或 SharePoint）中的新行。
* **发送电子邮件：**&#x200B;将包含表单数据的电子邮件发送到您指定的一个或多个电子邮件地址。

#### 重要提示：设置要求

* **电子表格访问权限：**&#x200B;若需将数据发送至存储在 OneDrive/SharePoint 上的 Google Sheets 或 Excel 文件，Adobe 服务账号（通常为 `forms@adobe.com`）通常需要对此电子表格具有&#x200B;**编辑权限**。
* **抢先体验计划：**&#x200B;该服务中的某些功能，尤其是与电子表格相关的功能，可能属于抢先体验计划的一部分。您可能需要通过发送邮件至 `aem-forms-ea@adobe.com` 或填写包含项目详细信息的专用 Adobe 表单来申请访问权限。请务必查看最新的 Adobe 文档。

**Forms Submission Service 流程图**
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
![Forms Submission](/help/forms/assets/eds-fss.png)

该流程图展示了 Forms Submission Service 如何接收已提交的数据，并将其发送到预设的电子表格或电子邮件地址。

## 方法 2：提交至您的 AEM Publish 实例（高级）

若有更复杂的需求，[表单（尤其是使用 Universal Editor 创建的表单）可将数据直接发送至您的 AEM as a Cloud Service Publish 实例](/help/forms/configure-submit-actions-core-components.md)。此方式可充分释放 AEM 的后端能力。

**何时需要提交至 AEM Publish 实例？**

* 提交后触发自定义 AEM 工作流。
* 使用 AEM 表单数据模型（FDM）与数据库或其他企业系统集成。
* 连接第三方服务，例如 Marketo、Microsoft Power Automate 或 Adobe Workfront Fusion。
* 将数据存储至特定位置，例如 Azure Blob Storage 或 SharePoint 列表/文档库（不仅限于简单的电子表格）。
* 当您在 AEM 中需要执行复杂的服务器端验证或数据处理逻辑时。

**可用的提交操作（适用于 AEM Publish Submissions）**

* [提交到 REST 端点](/help/forms/configure-submit-action-restpoint.md)
* [使用 AEM 邮件服务发送电子邮件](/help/forms/configure-submit-action-send-email.md)
* [使用表单数据模型（FDM）提交](/help/forms/configure-data-sources.md)
* [调用 AEM 工作流](/help/forms/aem-forms-workflow-step-reference.md)
* [提交至 SharePoint（作为列表项或文档）](/help/forms/configure-submit-action-sharepoint.md)
* [提交至 OneDrive（作为文档）](/help/forms/configure-submit-action-onedrive.md)
* [提交至 Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [提交至 Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [提交至 Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [提交到Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> 即使您希望从 AEM Publish 实例将数据提交到 Google Sheets/Excel，也需采用与直接使用 Forms Submission Service 不同的配置步骤。

**AEM 发布提交流程图**

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

![AEM 发布提交流程图](/help/forms/assets/eds-aem-publish.png)
该流程图展示了表单如何提交至 AEM Publish 实例，并由其处理复杂的后端任务。

### Forms Submission Service 与 AEM Publish Submissions 的对比

| 功能 | Forms Submission Service | AEM Publish Submissions |
| :- | :- | :-- |
| **最适合** | 简单地将数据收集至电子表格、电子邮件通知 | 复杂工作流、企业系统集成、自定义逻辑 |
| **表单编写** | 适用于基于文档的表单；对简单的 Universal Editor 表单也适用 | 最适合由 Universal Editor 创建的表单 |
| **设置难度** | 较低（通常为简单配置） | 较高（需要配置 AEM Publish、Dispatcher、OSGi 和 CDN） |
| **后端系统** | Adobe 托管服务 | 您的 AEM as a Cloud Service Publish 实例 |
| **灵活性** | 限于电子表格/邮件 | 非常灵活，支持完整的 AEM Forms 操作 |
| **示例** | 将联系表单数据发送至 Google Sheets | 通过贷款申请表单触发 AEM 审批工作流 |

## 跨站点或页面嵌入表单的方法

有时，您希望在一个中央“表单站点”中创建和管理表单，但将该表单展示在其他网站或页面上。

### 为什么要嵌入表单？

* 您有一个使用 Universal Editor 创建的标准“联系我们”表单，需要在多个通过文档式创作（Document-Based Authoring）构建的登陆页面中显示。
* 您的主要网站内容基于文档创作（DA），但需要嵌入一个专用表单。
* 您希望在多个不同的 EDS 项目中重复使用一个经过良好维护的统一表单。

### 表单嵌入的技术原理

在您希望表单显示的页面（下文称为“宿主页面”）中，通常会包含一段代码（通常是一个特殊区块或脚本）。当用户访问宿主页面时，该代码会向实际托管表单的 URL（下文称为“表单源”）发起请求。表单源随后会返回 HTML 内容，由宿主页面插入并呈现出来。

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
此架构图展示了宿主页面如何从表单源获取表单 HTML 并将其显示。表单的提交仍使用原始表单配置的提交端点。

## 为嵌入式表单设置 CORS

[CORS（跨源资源共享）](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)是浏览器的安全机制。如果您的宿主页面（如 `site-a.com`）尝试从不同域名（如 `forms-site-b.com`）获取表单，浏览器会阻止该请求，除非 `forms-site-b.com` 明确通过 CORS 响应头允许访问。

如果&#x200B;**表单源服务器**&#x200B;未正确设置 CORS 响应头，浏览器将阻止宿主页面加载表单，则嵌入式表单将无法显示。

### 如何为托管表单的站点配置 CORS？

您需要配置托管&#x200B;**表单源**&#x200B;的服务器，使其在响应中包含特定的 HTTP 响应头。具体方法依赖于您的 EDS 设置方式（例如，对于 Franklin 项目，通常是在 GitHub 存储库中的 `helix-config.yaml` 或类似配置文件中完成，该文件控制 CDN 行为或边缘计算逻辑）。
需添加至表单源响应中的关键响应头：

* `Access-Control-Allow-Origin: <URL_of_Host_Page>`（例如 `https://your-site.com`）。在测试环境中，您可以使用 `*`，但在生产环境中应指定确切的域名。
* `Access-Control-Allow-Methods: GET, OPTIONS`（如果表单提交本身也属于跨域请求，您可能还需要 `POST`。但通常，提交操作会指向另一个同源或已特别配置的端点。）
* `Access-Control-Allow-Headers: Content-Type`（以及您的表单请求可能使用的任何其他自定义请求头。）

**示例（用于配置文件的概念性说明）：**

```yaml
        # In the configuration for the site HOSTING THE FORM (Form Source)
        headers:
          # Apply to paths where your forms are served, e.g., /forms/**
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-page-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS
```

## 其他注意事项：CDN 和多个代码库（Helix 4）

* **CDN 规则：**&#x200B;您的 CDN 可能支持请求代理。例如，请求 `host-page.com/embedded-form` 可由 CDN 内部路由来获取 `form-source.com/actual-form` 的内容，这样浏览器会认为它们是同源的。设置这类代理可能较为复杂。
* **多个代码库（Helix 4）：**&#x200B;如果您的宿主页面和表单源分别在不同的 GitHub 存储库中（这是 Helix 4 配置中的常见情况），请确保宿主页面的代码库中包含用于渲染或管理表单所需的 JavaScript“Form block”，或者确保从表单源获取的表单 HTML 是完整的，并内嵌所有必要的 JavaScript。原始文档指出：“在 Helix 4 多代码库场景中，您需要在两个代码库中都添加 Form block。”

### 常见的架构设置和配置步骤

以下是几种常见的表单配置方式，结合了不同的创作方法与提交策略，并附带关键配置要点。

#### 基于文档的表单 + 电子表格/电子邮件提交

这是最简单的设置。您可在 Word 或 Google Docs 中创建表单，它会通过 Forms Submission Service 将数据提交到电子表格或发送电子邮件。

1. 使用指定的表格结构或表单区块，在 Word/Google Doc/Sheet 或表格中定义您的表单。
1. 在文档（或相关配置中），指定用于 Forms Submission Service 的目标电子表格 URL 或电子邮件地址。
1. 确保 `forms@adobe.com`（或相应的服务账号）对目标电子表格具有编辑权限。
1. 将您的文档发布到 Edge Delivery 站点。

**基于文档的表单 + Forms Submission Service 架构**
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

![基于文档的表单 + Forms Submission Service 架构](/help/forms/assets/eds-doc-fss.png)

#### 使用 Universal Editor 创建的表单 + 表格/邮件提交方式

您可以使用可视化的 Universal Editor 构建表单，同时仍通过简洁的 Forms Submission Service 捕获数据。

1. 使用 AEM 中的 Universal Editor 创建表单。
1. 在 Universal Editor 中配置表单的提交操作，选择“提交至 Forms Submission Service”选项。
1. 指定目标电子表格的 URL 或电子邮件地址。
1. 如果使用电子表格，请确保 `forms@adobe.com` 具有编辑权限。
1. 将包含该表单的页面从 AEM 发布至 Edge Delivery 站点。

   **Universal Editor  + Forms Submission Service 架构**

   ![ Universal Editor  + Forms Submission Service 架构](/help/forms/assets/eds-ue-fss.png)

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

#### 使用 Universal Editor 创建的表单 + AEM Publish 实例提交（高级）

此设置方式使用 Universal Editor 创建表单，并通过 AEM Publish 实例执行强大的后端处理程序（如工作流、FDM 等）。此方案需要更多配置。

1. **在 Universal Editor 中创建表单：**&#x200B;使用 Universal Editor 构建表单。将其提交操作配置为指向某个 AEM Forms 操作（例如：“调用 AEM 工作流”、“使用表单数据模型提交”）。
1. **AEM Dispatcher 配置（适用于 AEM Publish 层）：**
   * **禁止重定向：**&#x200B;确保 Dispatcher 规则&#x200B;*不会*&#x200B;对路径 `/adobe/forms/af/submit/...` 的请求执行重定向。
   * **允许提交：**&#x200B;修改 Dispatcher 过滤器（例如 `filters.any` 文件），明确 `allow` 来自 Edge Delivery 站点的域名或 IP 地址对 `/adobe/forms/af/submit/...` 发起的 POST 请求。
1. **AEM 中的 OSGi 反向链接过滤器（适用于 AEM Publish 层）：**
   * 在 AEM 的 OSGi 控制台（`/system/console/configMgr`）中，查找并配置 “Apache Sling Referrer Filter”。
   * 将您的 Edge Delivery 站点的域（例如， `https://your-eds-domain.hlx.page`、 `https://your-custom-eds-domain.com`）添加至“Allow Hosts” 或 “Allow Hosts RegExp” 列表中。这会告知 AEM 接受来自您的 EDS 站点的提交请求。
1. **CDN 重定向规则（适用于您的 Edge Delivery CDN）：**
   * 您的 Edge Delivery 站点（例如 `your-eds-domain.hlx.page`）需要能够正确地将提交请求路由到 AEM Publish 实例。
   * 当 EDS 页面上的表单提交时，可能会使用类似 `/adobe/forms/af/submit/...` 的相对路径。您需要在 Edge Delivery CDN（或 edge worker）中设置一条规则，例如：“如果请求路径为 `your-eds-domain.hlx.page/adobe/forms/af/submit/...`，则将其代理或重定向至 `your-aem-publish-instance.com/adobe/forms/af/submit/...`。”
   * 具体实现方式取决于您的 CDN 提供商（例如 Fastly VCL、Akamai Property Manager、Cloudflare Workers）。
1. **（可选）开发用 `constants.js`（在 EDS 项目的代码库中）：**
   * 在本地开发或当客户端表单脚本需要获知完整的 AEM Publish URL 时，您可以在 Edge Delivery 项目的 GitHub 存储库中，通过 `constants.js` 或类似配置文件进行设置。示例：

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **发布：**&#x200B;将您的表单页面从 AEM 发布到 EDS，并确保所有 AEM 配置已在 AEM Publish 实例中生效。

   **Universal Editor  + AEM Publish 架构**

![ Universal Editor  + AEM Publish 架构](/help/forms/assets/eds-aem-publish.png)

此流程展示如下操作路径：用户在 EDS 站点上提交表单，CDN 将请求路由至 AEM Dispatcher，随后由 AEM Publish 进行处理。

#### 将表单嵌入至文档创作（DA）页面

您的主网站内容是通过文档创作（DA）创建的。您可以使用文档式创作或 Universal Editor 单独创建表单，然后将其嵌入到 DA 页面中。

1. **创建并发布表单：**
   * 使用文档式创作或 Universal Editor 创建您的表单。
   * 配置表单的提交方式（提交至 Forms Submission Service 或 AEM Publish，依据设置方案 1、2 或 3）。
   * 将该表单发布为一个独立页面，并使其可通过 Edge Delivery URL 访问（例如 `.../forms/my-special-form`）。
1. **配置 CORS：**&#x200B;在承载该独立表单的 Edge Delivery 站点或项目中，确保已设置 CORS 响应头，以允许来自您的文档创作站点的域名获取该表单。
1. **在 DA 中创建页面：**&#x200B;在文档创作环境中创建或编辑页面。
1. **嵌入表单区块：**&#x200B;在文档创作中使用相应区块嵌入外部 URL。将该区块指向您独立发布的表单页面的 URL。
1. **发布 DA 页面：**&#x200B;发布您的 DA 页面。页面现在将自动获取并显示该表单。

   **嵌入 DA 的表单架构**

   ![嵌入 DA 的表单架构](/help/forms/assets/eds-forms-embedd-da.png)

   此图展示了 DA 页面如何从另一个 EDS 位置加载表单。嵌入的表单会自行处理其提交逻辑。

## 疑难解答

* **我的表单提交不起作用。**
   * **检查控制台错误：**&#x200B;打开浏览器的开发者控制台（通常按 F12），在网络（Network）或控制台（Console）标签页中查看提交时是否有错误。
   * **验证提交 URL：**&#x200B;表单是否尝试提交至正确的端点（即 Forms Submission Service 的 URL 或 AEM Publish 的提交路径）？
   * **Forms Submission Service：**&#x200B;如果提交目标是电子表格，是否已为 `forms@adobe.com` 授予编辑权限？电子表格的 URL 是否正确？
   * **AEM Publish Submissions:**
      * 您的 Dispatcher 是否允许向 `/adobe/forms/af/submit/...` 发起 POST 请求？
      * AEM Publish 实例中的 Sling Referrer Filter 是否已配置为允许来自您的 EDS 域的请求？
      * CDN 中关于 `/adobe/forms/af/submit/...` 的重定向规则是否正常工作？

* **我的嵌入表单未显示。**

   * **CORS！** 这是最常见的原因。请在浏览器控制台中检查是否存在 CORS 错误。确保&#x200B;*托管*&#x200B;表单的站点已正确设置 `Access-Control-Allow-Origin` 响应头。
   * **表单 URL 是否正确？**&#x200B;宿主页面中的嵌入代码是否指向该表单的有效线上 URL？
   * **JavaScript 区块：**&#x200B;如果表单依赖特定的 JavaScript “Form block” 进行渲染，宿主页面上是否引入了该区块代码？

* **提交至 AEM Publish 时出现 “403 Forbidden” 或 “401 Unauthorized”。**

   * 这通常是因为 AEM Publish 中的 Sling Referrer Filter 未允许来自 EDS 域的请求。请仔细检查相关配置。
   * 尽管标准表单提交通常是匿名的，但如果您的 AEM 提交端点启用了身份验证，也可能是身份验证/授权配置问题。

## 后续步骤

本指南概述了如何将表单与 AEM Edge Delivery Services 集成使用。如需更详细的配置步骤和说明，请参阅 Adobe Experience Manager 官方文档。

* [使用 Edge Delivery Services 表单进行文档式创作](/help/edge/docs/forms/tutorial.md)
* [使用 Universal Editor 与 Edge Delivery Services 表单](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [文档创作（DA）与内容嵌入](https://www.aem.live/developer/da-tutorial)
* [AEM Forms Submission Service](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
