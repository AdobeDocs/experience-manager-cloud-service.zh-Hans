---
title: Formsas a Cloud Service常见问题解答
description: Formsas a Cloud Service常见问题解答
contentOwner: khsingh
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
index: false
source-git-commit: 93e7c4b31ea3037c98b64790ffdee11f94cc6134
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 3%

---

# 常见问题 {#frequently-asked-questions}

* **我可以使用代码编辑器创建规则吗？**
您可以使用可视编辑器创建规则。 代码编辑器在 [!DNL Forms] as a Cloud Service。 如果您的自适应表单使用通过代码编辑器开发的规则脚本，请使用 [迁移实用程序](migrate-to-forms-as-a-cloud-service.md) 将代码脚本转换为自定义函数。 您可以将自定义函数与可视编辑器结合使用，以继续获取通过代码编辑器获取的结果。

* **我能否在Cloud Service实例上创建基于XFA的自适应表单？**
能，您可以在Cloud Service实例上创建基于XFA的自适应表单。 但是，AEM Formsas a Cloud ServiceSDK（本地开发环境）不支持基于XFA的自适应Forms。 如果您打算将基于XFA的自适应Forms与AEM Formsas a Cloud ServiceSDK结合使用，请联系Adobe支持部门并提供您的用例的详细信息和特定要求。

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **我是否可以从内部部署迁移内容或 [!DNL Adobe-Managed Services] 环境 [!DNL Forms] as a Cloud Service环境？**
可以，您可以从内部部署迁移自定义代码、内容和资产，或 [!DNL Adobe-Managed Services] 环境 [!DNL Forms] as a Cloud Service环境。 有关详细说明，请参阅 [迁移到Formsas a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **从哪里可以获取AEM [!DNL Forms] as a Cloud Service [!DNL Java™] API参考文档？**
您可以从以下位置下载Java™ API参考文档 [!DNL Maven Central Repository]. 要下载，请执行以下操作：
   1. 转到 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. 找到并打开包含最新版本的页面 [!DNL Experience Manager Forms] SDK。
   1. 单击“查看全部”选项可查看所有文件。
   1. 下载并解压缩 `aem-forms-sdk-api-<version>-javadocs`.jar.
   1. 打开index.html文件以查看API参考文档。

* **从哪里可以得到 [!DNL JavaScript™] 自适应Forms的API参考？**
您可以下载 [!DNL JavaScript™] 来自的API参考文档[!DNL  Maven Central Repository]. 要下载，请执行以下操作：
   1. 打开 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. 找到并打开包含最新版本的页面 [!DNL Experience Manager Forms] SDK。
   1. 单击“查看全部”选项可查看所有文件。
   1. 下载并解压缩 `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. 打开index.html文件以查看API参考文档。

* **我是否可以继续使用现有主题和模板？**
是，在使用AEM 6.4 Forms和AEM 6.5 Forms之后，您可以继续使用通过 [迁移实用程序](migrate-to-forms-as-a-cloud-service.md) 以将其移至 [!DNL AEM Forms] as a Cloud Service。

   您也可以基于以下内容创建项目： [!DNL AEM Forms] as a Cloud Service [原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment) 并使用包括的示例主题和模板。

* **我能否生成与架构兼容的数据？**
可以，您可以创建自适应Forms以生成与架构兼容的数据。

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **是否可以缓存受保护的内容？**
默认情况下，缓存受保护内容功能处于禁用状态。 要启用该功能，您可以执行提供的说明 [缓存受保护内容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hans).

* **我有一个本地化的自适应表单；它不是渲染本地化的版本吗？ 原因可能是什么？如何解决这个问题？**

   本地化自适应Forms的URL约定现在支持在URL中指定区域设置。 新的URL约定支持在Dispatcher或CDN上缓存本地化的表单。 在Cloud Service环境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 请求自适应表单的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe建议使用Dispatcher或CDN缓存。 它有助于提高预填充表单的渲染速度。

* **我更新了自适应表单；客户无法使用更新的版本？**
默认情况下，CDN每5分钟刷新一次缓存，等待5分钟，然后检查是否有更新的版本。

* **我能否在自适应表单中使用“签名”步骤来创建浏览器内签名体验？**
否，签名步骤不可用于 [!DNL Forms] as a Cloud Service。 删除自适应Forms中的签名步骤。 允许用户在提交后签名自适应表单，而不是签名步骤。 它可帮助您继续提供浏览器内签名体验。

* **我是否可以在自适应表单中使用验证步骤？**
否，验证步骤不可用于 [!DNL Forms] as a Cloud Service。 在将此类表单移动到Cloud Service环境之前，请从现有自适应Forms中删除验证步骤。

* **我是否可以将图表添加到自适应表单？**
可以，您可以将图表添加到自适应Forms。 自适应Forms提供图表组件。 您可以使用该插件将图表添加到自适应表单。

* **是否可以将表单数据模型连接到关系数据库模型？**
您可以将表单数据模型连接到 [!DNL RESTful web services]， [!DNL SOAP-based web services]， [!DNL OData services]，并将用户配置文件Experience Manager为数据源。 不支持将表单数据模型与关系数据库连接。

* **我能否将自定义证书与表单数据模型结合使用以进行身份验证？**
表单数据模型不提供使用自定义证书进行身份验证的方法。 因此，不支持x509和双向SSL等自定义证书。

* **我能否使用Forms Portal提交操作自适应Forms？**

   您可以修改现有的自适应Forms以使用 [提交到REST端点](configuring-submit-actions.md#submit-to-rest-endpoint)， [发送电子邮件](configuring-submit-actions.md#send-email)， [使用表单数据模型提交](configuring-submit-actions.md#submit-using-form-data-model)、和 [调用AEM Workflow](configuring-submit-actions.md#invoke-an-aem-workflow) 提交操作。 Forms Portal和Forms Portal提交操作尚不可用。 留意功能可用性的每月发行说明。

* **我可以使用吗 [!DNL AEM Forms] 应用程序与 [!DNL AEM Forms] as a Cloud Service？**

   自适应表单提供了响应式设计。这些表单会根据底层设备更改外观、设计和交互性。您可以继续在移动设备上使用自适应Forms，同时保留每月发行说明中的关注内容，以便了解这些功能的可用性。

* **初始GA版本中未包含哪些功能？**
Forms门户， [!DNL AEM Forms] 应用程序、与Adobe Analytics的集成以及与Adobe Target的集成不包含在初始GA版本中。 有关新功能的信息，请查看每月发行说明。

* **我设计了一个 [用于创建自适应表单的JSON架构](adaptive-form-json-schema-form-model.md). JSON架构为自适应表单的某些组件定义事件。 AEM Formsas a Cloud Service是否支持事件？**
在Experience Manager6.5 Forms环境中创建基于JSON架构的自适应表单，并使用 [迁移实用程序](migrate-to-forms-as-a-cloud-service.md) 将此类自适应Forms迁移到AEM Formsas a Cloud Service。 该实用程序将此类事件转换为客户端库，您可以继续将自适应Forms用于Cloud Service环境中的事件。

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


