---
title: AEM Forms as a Cloud Service 常见问题
description: Forms as a Cloud Service 常见问题
contentOwner: khsingh
role: User
feature: Adaptive Forms
index: false
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
source-git-commit: 5ee37f59bb959e0549c0541c6568aa8c135c330e
workflow-type: ht
source-wordcount: '975'
ht-degree: 100%

---

# 常见问题 {#frequently-asked-questions}

* **能否使用代码编辑器创建规则？**
可使用 Visual Editor 创建规则。[!DNL Forms] as a Cloud Service 上无代码编辑器可用。如果自适应表单使用通过代码编辑器开发的规则脚本，请使用[迁移实用程序](migrate-to-forms-as-a-cloud-service.md)将代码脚本转换为自定义函数。您可以将自定义函数与 Visual Editor 结合使用，以继续获取通过代码编辑器获取的结果。

* **能否在 Cloud Service 实例上创建基于 XFA 的自适应表单？**
是，可以在 Cloud Service 实例上创建基于 XFA 的自适应表单。不过，对于 AEM Forms as a Cloud Service SDK（本地开发环境）不支持基于 XFA 的自适应表单。如果要将基于 XFA 的自适应表单与 AEM Forms as a Cloud Service SDK 结合使用，请联系 Adobe 支持部门并提供您的用例和具体要求的详细信息。

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **能否将内容从内部部署或 [!DNL Adobe-Managed Services] 环境迁移到 [!DNL Forms] as a Cloud Service 环境？**
是，可以将自定义代码、内容和资源从内部部署或 [!DNL Adobe-Managed Services] 环境迁移到 [!DNL Forms] as a Cloud Service 环境。有关详细说明，请参阅[迁移到 Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md)。

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **可从何处获取 AEM [!DNL Forms] as a Cloud Service [!DNL Java™] API 参考文档？**
可以从 [!DNL Maven Central Repository] 下载 Java™ API 参考文档。要进行下载，请执行以下操作：
   1. 转到 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api)。
   1. 找到并打开包含最新版本的 [!DNL Experience Manager Forms] SDK 的页面。
   1. 单击“查看全部”选项以查看所有文件。
   1. 下载 `aem-forms-sdk-api-<version>-javadocs` .jar 并解压缩。
   1. 打开 index.html 文件以查看 API 参考文档。

* **可从何处获取自适应表单的 [!DNL JavaScript™] API 参考？**
可从 [!DNL  Maven Central Repository] 下载 [!DNL JavaScript™] API 参考文档。要进行下载，请执行以下操作：
   1. 打开 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api)。
   1. 找到并打开包含最新版本的 [!DNL Experience Manager Forms] SDK 的页面。
   1. 单击“查看全部”选项以查看所有文件。
   1. 下载 `aem-forms-sdk-api-<version>-jsdoc.jar` 并解压缩。
   1. 打开 index.html 文件以查看 API 参考文档。

* **能否继续使用现有的主题和模板？**
是，在使用[迁移实用程序](migrate-to-forms-as-a-cloud-service.md)将通过 AEM 6.4 Forms 和 AEM 6.5 Forms 创建的主题迁移到 [!DNL AEM Forms] as a Cloud Service 后，可以继续使用这些主题。

  还可根据 [!DNL AEM Forms] as a Cloud Service [原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment)创建项目，并使用其中附带的主题和模板示例。

* **能否生成符合架构的数据？**
是，可创建自适应表单以生成符合架构的数据。

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **能否缓存受保护内容？**
默认情况下禁用缓存受保护内容功能。要启用该功能，可执行在[缓存受保护内容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-hans)中提供的指示。

* **本地化自适应表单不呈现本地化版本？导致这个问题的原因是什么，如何解决它？**

  本地化自适应表单的 URL 约定现在支持在 URL 中指定区域设置。通过新的 URL 约定，可在 Dispatcher 或 CDN 上缓存本地化表单。在 Cloud Service 环境上，使用 URL 格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>` 请求自适应表单的本地化版本。Adobe 建议使用 Dispatcher 或 CDN 缓存。这有助于加快预填充表单的呈现速度。

* **我更新了自适应表格；但客户无法使用更新后的版本？**
默认情况下，CDN 每 5 分钟刷新一次缓存，请等待 5 分钟，然后检查更新后的版本。

* **能否使用自适应表单中的签名步骤创建浏览器内签名体验？**
否，签名步骤不适用于 [!DNL Forms] as a Cloud Service。删除自适应表单中的签名步骤。请允许用户在提交后签署自适应表单而代替签名步骤。这有助于您继续提供浏览器内签名体验。

* **能否在自适应表单中使用验证步骤？**
否，验证步骤不适用于 [!DNL Forms] as a Cloud Service。从现有的自适应表单中删除验证步骤，然后再将此类表单迁移到 Cloud Service 环境。

* **能否将图表添加到自适应表单？**
是，可以将图表添加到自适应表单。自适应表单提供了一个图表组件。可使用它将图表添加到自适应表单。

* **能否将表单数据模型连接到关系数据库模型？**
您可以将表单数据模型作为数据源连接到 [!DNL RESTful web services]、[!DNL SOAP-based web services]、[!DNL OData services] 和 Experience Manager 用户轮廓。<!--Support to connect a Form Data Model with a relational database is not available.-->

* **能否将自定义证书与表单数据模型 (FDM) 结合使用进行身份验证？**
表单数据模型 (FDM) 不提供使用自定义证书进行身份验证的方法。因此，不支持 x509 和双向 SSL 等自定义证书。

* **能否将 Forms Portal 提交操作用于自适应表单？**

  您可以修改现有自适应表单，以进行[提交到 REST 端点](configuring-submit-actions.md#submit-to-rest-endpoint)、[发送电子邮件](configuring-submit-actions.md#send-email)、[使用表单数据模型 (FDM) 提交](configuring-submit-actions.md#submit-using-form-data-model)和[调用 AEM 工作流](configuring-submit-actions.md#invoke-an-aem-workflow)提交操作。Forms Portal 和 Forms Portal 提交操作尚不可用。请关注每月发行说明以了解这些功能的可用性。

* **能否将 [!DNL AEM Forms] 应用程序与 [!DNL AEM Forms] as a Cloud Service 结合使用？**

  自适应表单提供了响应式设计。这些表单会根据底层设备更改外观、设计和交互性。在关注每月发行说明以了解这些功能的可用性的同时，可继续在移动设备上使用自适应表单。

* **哪些功能未包含在初始 GA 版本中？**
Forms Portal、[!DNL AEM Forms] 应用程序、与 Adobe Analytics 的集成以及与 Adobe Target 的集成未包含在初始 GA 版本中。有关新功能的信息，请查看每月发行说明。

* **我设计了一个 [JSON 架构来创建自适应表单](adaptive-form-json-schema-form-model.md)。此 JSON 架构为自适应表单的某些组件定义事件。AEM Forms as a Cloud Service 是否支持事件？**
在 Experience Manager 6.5 Forms 环境中根据该 JSON 架构创建自适应表单，并使用[迁移实用程序](migrate-to-forms-as-a-cloud-service.md)将此类自适应表单迁移到 AEM Forms as a Cloud Service。该实用程序将此类事件转换为客户端库，您可以继续在 Cloud Service 环境中使用自适应表单与事件。

<!-- 

* **Is there any AEM Forms as a Cloud Service connector for Microsoft Power Automate?**

  Yes, Adobe provides an Adobe Experience Manager connector to access [Adobe Experience Manager Forms - Communication capabilities](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html) through Microsoft Power Automate. You can create a PDF document that is based on a form design and XML form data or create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) and other Printer Definition Language documents. 

  You can get started with Adobe Experience Manager easily with just a few steps:

  1. Generate the Service credentials: Use Adobe Experience Manager Developer Console to [generate](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?#generate-service-credentials) the service credentials.  
  
  1. Setup your connection: Add your service credentials to the Adobe Experience Manager Connector. You can get crdential from service credential JSON and copy these credential details to your one-time connection setup:

    * AEM Server
    * Organization ID 
    * Client ID
    * Client Secret
    * Technical Account ID
    * Meta Scopes
    * Private Key - base64 encoded keys are accepted
    * Adobe IMS Host URL

    <br> 
    
    ![Use your Service Credential JSON for credential details](assets/forms-aem-pa-connector-connection.png)

    A sample Service Credential JSON file fields mapped to Adobe Experience Manager connector for Microsoft Power Automate.

    -->
