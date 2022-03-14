---
title: 'Formsas a Cloud Service常见问题解答 '
description: Formsas a Cloud Service常见问题解答
contentOwner: khsingh
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 2%

---

# 常见问题 {#frequently-asked-questions}

* **我能否使用代码编辑器创建规则？**
您可以使用可视化编辑器创建规则。 代码编辑器在上不可用 [!DNL Forms] as a Cloud Service。 如果您的自适应表单使用使用代码编辑器开发的规则脚本，请使用 [迁移实用程序](migrate-to-forms-as-a-cloud-service.md) 将代码脚本转换为自定义函数。 您可以将自定义函数与可视化编辑器一起使用，以继续获取使用代码编辑器获取的结果。

* **我是否可以在Cloud Service实例上创建基于XFA的自适应表单？**
是，您可以在Cloud Service实例上创建基于XFA的自适应表单。 但是，对于AEM Formsas a Cloud ServiceSDK（本地开发环境），不提供对基于XFA的自适应Forms的支持。 如果您打算将基于XFA的自适应Forms与AEM Formsas a Cloud ServiceSDK结合使用，请联系Adobe支持，以详细了解您的用例和特定要求。

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **我是否可以从内部部署迁移内容？ [!DNL Adobe-Managed Services] 环境 [!DNL Forms] as a Cloud Service环境？**
能，您可以从内部部署或 [!DNL Adobe-Managed Services] 环境 [!DNL Forms] as a Cloud Service环境。 有关详细说明，请参阅 [迁移到Formsas a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **从何处获取AEM [!DNL Forms] as a Cloud Service [!DNL Java™] API参考文档？**
您可以从下载Java™ API参考文档 [!DNL Maven Central Repository]. 要下载，请执行以下操作：
   1. 转到 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. 找到并打开包含最新版本的 [!DNL Experience Manager Forms] SDK。
   1. 单击“查看全部”(View All)选项以查看所有文件。
   1. 下载并提取 `aem-forms-sdk-api-<version>-javadocs`.jar。
   1. 打开index.html文件以查看API引用文档。

* **从哪里可以找到 [!DNL JavaScript™] 自适应Forms的API引用？**
您可以下载 [!DNL JavaScript™] 中的API参考文档[!DNL  Maven Central Repository]. 要下载，请执行以下操作：
   1. 打开 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. 找到并打开包含最新版本的 [!DNL Experience Manager Forms] SDK。
   1. 单击“查看全部”(View All)选项以查看所有文件。
   1. 下载并提取 `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. 打开index.html文件以查看API引用文档。

* **我能否继续使用现有的主题和模板？**
是，在使用 [迁移实用程序](migrate-to-forms-as-a-cloud-service.md) 将他们移到 [!DNL AEM Forms] as a Cloud Service。

   您还可以根据 [!DNL AEM Forms] as a Cloud Service [原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment) 和使用包含的示例主题和模板。

* **我是否可以生成符合架构的数据？**
是，您可以创建自适应Forms以生成符合模式的数据。

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **我能否缓存安全内容？**
默认情况下，缓存安全内容功能处于禁用状态。 要启用该功能，您可以执行 [缓存安全内容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html).

* **我有一个本地化的自适应表单；它未呈现本地化版本？ 原因何在，如何解决？**

   本地化的自适应Forms的URL约定现在支持在URL中指定区域设置。 新的URL约定允许在调度程序或CDN上缓存本地化的表单。 在Cloud Service环境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 请求自适应表单的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe建议使用Dispatcher或CDN缓存。 这有助于提高预填充表单的渲染速度。

* **我更新了自适应表单；更新版本不供客户使用？**
默认情况下，CDN每5分钟刷新一次缓存，等待5分钟，然后检查更新的版本。

* **我能否使用自适应表单中的签名步骤来创建浏览器内签名体验？**
否，签名步骤不适用于 [!DNL Forms] as a Cloud Service。 删除自适应Forms中的签名步骤。 允许用户在提交后对自适应表单进行签名，而不是“签名”步骤。 它可帮助您继续提供浏览器内的签名体验。

* **我能否在自适应表单中使用验证步骤？**
否，验证步骤不可用于 [!DNL Forms] as a Cloud Service。 在将此类表单移至Cloud Service环境之前，请从现有的自适应Forms中删除验证步骤。

* **我可以向自适应表单中添加图表吗？**
是，您可以向自适应Forms添加图表。 自适应Forms提供了一个图表组件。 您可以使用它将图表添加到自适应表单。

* **是否可以将表单数据模型连接到关系数据库模型？**
可以将表单数据模型连接到 [!DNL RESTful web services], [!DNL SOAP-based web services], [!DNL OData services]，并将用户配置文件Experience Manager为数据源。 不支持将表单数据模型与关系数据库连接。

* **能否将自定义证书与表单数据模型结合使用以进行身份验证？**
表单数据模型不提供使用自定义证书进行身份验证的方法。 因此，不支持自定义证书，如x509和双向SSL。

* **我能否使用Forms Portal提交操作自适应Forms?**

   您可以修改现有的自适应Forms以使用 [提交到REST端点](configuring-submit-actions.md#submit-to-rest-endpoint), [发送电子邮件](configuring-submit-actions.md#send-email), [使用表单数据模型提交](configuring-submit-actions.md#submit-using-form-data-model)和 [调用AEM工作流](configuring-submit-actions.md#invoke-an-aem-workflow) 提交操作。 Forms Portal和Forms Portal提交操作尚不可用。 请关注每月的发行说明，以了解这些功能的可用性。

* **我能用一下吗 [!DNL AEM Forms] 应用程序 [!DNL AEM Forms] as a Cloud Service?**

   自适应表单提供了响应式设计。这些表单会根据底层设备更改外观、设计和交互性。您可以在移动设备上继续使用自适应Forms，同时在每月的发行说明中关注这些功能的可用性。

* **哪些功能未包含在初始GA版本中？**
Forms门户网站， [!DNL AEM Forms] 应用程序、与Adobe Analytics集成以及与Adobe Target集成未包含在初始GA版本中。 有关新增功能的信息，请查看月度发行说明。
