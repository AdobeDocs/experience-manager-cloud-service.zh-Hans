---
title: AEM 6.5 Forms与AEM云服务之间的更改内容
description: 您是Experience Manager Forms用户并且希望升级到Adobe Experience Manager Formsas a Cloud Service吗？ 了解在升级或迁移到Cloud Service之前最显着的更改。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 7c157cbeb530627c1b888379896ddffda3f3efb3
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 3%

---

# 对现有Adobe Experience Manager 6.5 Forms用户的显着更改  {#notable-changes-for-existing-AEM-Forms-users}

与Adobe Experience Manager Forms本地版和本地版相比，Adobe Experience Manager Forms as a Cloud Service对现有功能做出了一些显着更改 [!DNL Adobe-Managed Service] 环境。 主要区别如下：

| 功能 | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms |
|---|---|---|
| 云本机架构 | ✅ | ⛌ |
| 根据负载自动缩放 | ✅ | ⛌ |
| 升级无停机 | ✅ | ⛌ |
| 功能推出频率 | 敏捷* | 每季度 |
| 包含CDN（内容交付网络） | ✅ | ⛌ |
| 优化了拓扑以实现最大可复原性和效率 | ✅ | ⛌ |
| 云原生开发环境 | ✅ | ⛌ |
| 通过Cloud Manager提供自助服务 | ✅ | ⛌ |
| 通过连续集成和连续交付(CI/CD)实现自动升级 | ✅ | ⛌ |
| 与[!DNL Micosoft Power Automate] 集成  | ✅ | ⛌ |
| 与[!DNL DocuSign] 集成  | ✅ | ⛌ |
| 与Microsoft Dynamics和Salesforce轻松连接 | ✅ | ⛌ |
| 与Microsoft Azure数据存储轻松连接 | ✅ | ⛌ |
| 强化的规则编辑器 | ✅ | ⛌ |
| 表单创建向导 | ✅ | ⛌ |
| 对记录文档的自定义XCI支持 | ✅ | ⛌ |
| 自适应Forms <sup>1</sup> | ✅ | ✅ |
| 与多个数据源的数据集成 | ✅ | ✅ |
| 通信API（文档服务） <sup>2,3</sup> | ✅ | ✅ |
| automated forms conversion服务 <sup>4</sup> | ✅ | ✅ |
| 与[!DNL Adobe Sign] 集成  | ✅ | ✅ |
| 与[!DNL AEM Sites] 集成  | ✅ | ✅ |
| 与[!DNL Adobe Launch] 集成  | ✅ | ✅ |
| 与[!DNL Adobe Analytics] 集成  | ✅ | ✅ |
| Forms门户 <sup>5</sup> | ✅ | ✅ |
| AEM 工作流 | ✅ | ✅ |
| 记录文档 | ✅ | ✅ |
| 验证码不可见 | ✅ | ✅ |
| 可重用表单数据模型配置 | ✅ | ✅ |
| 基于Acroform的记录文档 | ✅ | ✅ |
| 针对启用了Adobe Sign的自适应Forms，基于政府ID的身份验证 | ✅ | ✅ |
| HTML5 <sup>6</sup> | ⛌ | ✅ |
| 文档安全 | ⛌ | ✅ |

在继续提供服务之前，请考虑以下特殊情况：

+++ 1.适应性Forms

* **基于XSD的自适应Forms:** 该服务不支持HTML5 Forms(Mobile Forms)。 如果您将基于XDP的表单渲染为HTML5 Forms，则可以继续在AEM 6.5 Forms上使用该功能。 可以使用XDP模板为“记录文档”设计模板。 该服务不支持基于XFA的自适应Forms
* **导入自适应表单模板：** 使用程序的构建管道和相应的Git存储库来导入现有的自适应表单模板。
* **规则编辑器：** AEM Formsas a Cloud Service提供了经过硬化 [规则编辑器](rule-editor.md#visual-rule-editor). 代码编辑器在Formsas a Cloud Service上不可用。 迁移实用程序可帮助您迁移具有自定义规则（在代码编辑器中创建）的表单。 该实用程序会将这些规则转换为Formsas a Cloud Service支持的自定义函数。 您可以将可重用函数与规则编辑器一起使用，以继续获取通过规则脚本获取的结果。 `onSubmitError` 或 `onSubmitSuccess` 函数现在可在规则编辑器中用作操作。
* **草稿和提交：** 该服务不会保留草稿和提交的自适应Forms的元数据。
* **预填充服务：** 默认情况下，预填充服务会在客户端将数据与自适应表单合并，而不是在AEM 6.5 Forms的服务器上合并数据。 该功能有助于缩短预填自适应表单所需的时间。 您始终可以配置为在Adobe Experience Manager Forms服务器上运行合并操作。
* **提交操作：** 的 **电子邮件作为PDF** 操作不可用。 的 **电子邮件** “提交”操作提供了发送附件和通过电子邮件附加记录文档(DoR)的选项。
* **组件**:该服务不支持表单签名体验，并且不包含自适应Forms的“摘要”和“验证”组件。



+++


+++ 2.文件服务：文档操作API（汇编程序服务）


该服务不支持依赖于其他服务或应用程序的操作：

* 不支持将非PDF格式的文档转换为PDF格式。 例如，不支持Microsoft Word到PDF、Microsoft Excel到PDF和HTML到PDF。 文档为非PDF格式。 在将这些文档与通信文档处理API结合使用之前，将这些文档转换为PDF格式。 例如，如果您的文档采用Microsoft Office、HTML、PostScript(PS)、XDP格式，请先将这些文档转换为PDF格式，然后再将这些文档与PDF文档一起使用。
* Adobe不支持基于Distiller的转化。 例如，将PostScript(PS)PDF
* Forms不支持基于服务的转化。 例如，将XDP转换为PDF forms。
* 该服务不支持将已签名PDF或透明PDF转换为其他PDF格式。
* 无法使用Reader扩展服务应用使用权限。
* 该服务无法将已签名或透明的PDF文档转换为PDF/A格式。

+++


+++ 3.文件服务：文档生成API（输出服务）

在单个API调用或批量处理中，您只能将一个模板与多个DATA XML文件一起使用。 不支持在单个API调用中使用多个模板和多个数据文件。

+++

+++ 4.Automated forms conversion服务

该服务不为Automated forms conversion服务提供元模型。 您可以 [从Automated forms conversion服务文档下载它](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

+++

+++ 5.Forms门户

无法开箱即用(OOTB)地支持匿名使用Forms门户。 您可以自定义表单门户，以便为未登录用户启用显示表单的功能。

+++


+++ 6.HTML5Forms(移动Forms)

* 该服务不支持HTML5 Forms(Mobile Forms)。 如果您将基于XDP的表单渲染为HTML5 Forms，则可以继续在AEM 6.5 Forms上使用该功能。

* 如果您有用于离线捕获数据并在下次联机时同步该数据，则可以继续使用 [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) 的AEM 6.5 Forms。

+++


+++ 7.表单数据模型

* Forms数据模型仅支持HTTP和HTTP端点提交数据。 该服务不支持REST连接器的互相SSL以及SOAP数据源的基于x509证书的身份验证。

* Formsas a Cloud Service允许将Microsoft Azure Blob、Microsoft Sharepoint、Microsoft OneDrive和支持常规CRUD（创建、读取、更新和删除）操作的服务用作数据存储，同时支持Open API规范2.0和Open API规范。 该服务还支持JDBC连接器。

+++


+++ 8.开发人员环境

* 云原生环境没有Web控制台（配置管理器）。 您可以使用 [[!DNL AEM Forms] as a Cloud ServiceSDK生成配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) 和CI/CD管线到 [部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) 到Cloud Service实例。
* 默认情况下，电子邮件仅支持HTTP和HTTP协议。 [联系支持团队](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 启用用于发送电子邮件的端口，并为环境启用SMTP协议。
* 该服务不支持将已签名PDF或透明PDF转换为其他PDF格式。 在将客户包与Forms as a Cloud Service一起使用之前，请使用本地化的Adaptive Forms的最新版adobe-aemfd-docmanager* URL约定重新编译您的自定义代码。现在，支持在URL中指定区域设置。 新的URL约定允许在调度程序或CDN上缓存本地化的表单。 在Cloud Service环境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 请求自适应表单的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe建议使用Dispatcher或CDN缓存。 这有助于提高预填充表单的渲染速度
* Adobe Experience Manager Forms as a Cloud Service为您的AEM项目提供了许多新功能和可能性。 但是，Adobe Experience Manager Maven项目需要进行一些更改才能与AEM Cloud Service兼容。 在高级别上，AEM要求将内容和代码分离为离散的子包，以便遵循可变内容和不可变内容之间的拆分。 使用 [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) 用于通过将内容和代码分离为离散包来重构现有项目包的工具，以与为Adobe Experience Manager as a Cloud Service定义的项目结构兼容。


+++

<!-- 

### HTML5 Forms (Mobile Forms)

The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms.

### Adaptive Forms 

* **XSD-Based Adaptive Forms:** The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. You can use XDP-template to design a template for Document for Record. The service does not support XFA based Adaptive Forms  
* **Importing Adaptive Form templates:** Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. 
*  **Rule editor:** AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor.  
* **Drafts and submissions:** The service does not retain metadata for drafts and submitted Adaptive Forms.  
* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. 
* **Submit actions:** The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. 
* **Components**:  The service does not support in-form signing experience and does not include the Summary and Verify components for Adaptive Forms.  
* **Forms portal**: Support for anonymous use of Forms portal is not available out of the box (OOTB). You can customize the forms portal to enable displaying forms for non-logged in users.

### Form Data Model

* Forms data model supports only HTTP and HTTPs endpoints to submit data. The service does not support Mutual SSL for REST connector and x509 certificate-based authentication for SOAP data sources. * Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores, both Open API specification 2.0 and Open API specification are supported. The service also provides support for JDBC connector.


### Automated Forms Conversion Service     

The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).


### Configurations

* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.  
* If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service. 


### Document Services: Document Manipulation APIs (Assembler Service)

The service does not support operations dependent on other services or applications:  

* Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported. If your documents are in a non-PDF format. Convert such documents to PDF format before using those with Communications Document Manipulation APIs. For example, if your documents are in Microsoft Office, HTML, PostScript (PS), XDP format, convert these documents to PDF format before using those with PDF documents. 
* Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF
* Forms Service-based conversions are not supported. For example, XDP to PDF Forms.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.
* Applying usage rights using Reader Extensions Service is not available. 
* The service does not provide the ability to convert signed or transparent PDF Documents to PDF/A format. 

### Document Services: Document Generation APIs (Output Service)

* In a single API call or batch, you can use one template with multiple DATA XML files. Using mutiple templates with multiple data files in a single API call is not supported. 

### Other differences

* A cloud-native environment does not have web console (configuration manager). You can use [[!DNL AEM Forms] as a Cloud Service SDK to generate configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) and CI/CD pipeline to [deploy the configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) to your Cloud Service instance.
* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.* Before using your customer bundles with Forms as a Cloud Service, recompile your custom code with the latest version of adobe-aemfd-docmanager* URL convention of localized Adaptive Forms now supports specifying a locale in the URL. New URL convention enables caching localized forms on a Dispatcher or CDN. On Cloud Service environment, use the URL format `http://host:port/content/forms/af/<afName>.<locale>.html` to request a localized version of an Adaptive Form instead of `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recommends using Dispatcher or CDN caching. It helps improve rendering speed of prefilled forms 
* Adobe Experience Manager Forms as a Cloud Service brings many new features and possibilities into your AEM Projects. However, there are some changes required to Adobe Experience Manager Maven projects to be compatible with AEM Cloud Service. At a high-level, AEM requires a separation of content and code into discrete subpackages to respect the split between mutable and immutable content. Use the [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) tool to restructure existing project packages by separating content and code into discrete packages to be compatible with the project structure defined for Adobe Experience Manager as a Cloud Service.
-->




