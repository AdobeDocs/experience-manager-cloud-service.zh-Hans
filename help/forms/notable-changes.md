---
title: AEM 6.5 Forms与AEMCloud Service之间有何区别？
description: 比较AEM 6.5 Forms和AEMCloud Services，并了解在升级或迁移到Cloud Service之前最显着的更改。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
role: Admin, Developer, User
feature: Adaptive Forms
contentOwner: khsingh
source-git-commit: a5179851af8ec88e23d79a74265b10cbce2d50f1
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 1%

---

# AEM 6.5 Forms （AMS和内部部署）与AEM Forms as a Cloud Service (AEM CS Forms)之间的区别 {#notable-changes-for-existing-AEM-Forms-users}

与Adobe Experience Manager Forms On-Premise和[!DNL Adobe-Managed Service]环境相比，Adobe Experience Manager Forms as a Cloud Service对现有功能进行了一些显着更改。 主要差异列示如下：

## 云原生功能

* 该服务具有云原生架构，允许根据负载自动扩展、升级时无需停机时间、频繁推出新功能和更新后以及优化拓扑以最大程度地提高弹性和效率。

* 该服务不包含将数据存储到Adobe Experience ManagerCloud Service实例的提交操作，使其超级安全。 通过表单捕获的数据将直接发送到配置的数据存储。

* 此外，还包括一个免费的CDN（内容分发网络），可帮助您更快地交付和渲染表单。


## 更新开发流

* 该服务提供了一个SDK，用于在将自定义代码部署到Cloud Service之前，在本地环境（本地计算机）中开发和测试该代码。 开发人员在其本地计算机上使用SDK开发和测试自定义组件、主题、工作流应用程序、配置、模板等。 在本地开发环境中测试自定义代码后，他们将自定义代码部署到[Forms CS环境开发或暂存环境](/help/implementing/cloud-manager/deploy-code.md)以进行进一步测试，然后再将其提升到生产环境。

* 开发人员在公共[Git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html)中维护Cloud Service和本地开发环境的代码。 在创建AEM as a Cloud Service程序时，会自动创建基于AEM原型的Git存储库。

  在AEM as a Cloud Service程序上![自动创建Git存储库](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Forms的开发流程与AEM Cloud Service的AEM Archetypeas a Cloud Service保持一致。 但是，需要对Adobe Experience Manager Maven项目进行一些更改才能与AEM Cloud Service兼容。 从较高层面来看，AEM需要将内容和代码分离为离散的子包，以遵循可变内容和不可变内容之间的拆分。 使用[Repository Modernizer工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html)通过将内容和代码分隔到独立包中来重构现有项目包，使其与为Adobe Experience Manager as a Cloud Service定义的项目结构兼容。

* 在将客户捆绑包与Formsas a Cloud Service结合使用之前，请使用最新版本的adobe-aemfd-docmanager重新编译自定义代码。

* 使用[AEM Formsas a Cloud Service迁移实用程序](/help/forms/migrate-to-forms-as-a-cloud-service.md)准备自适应Forms、主题、模板和云配置，并将其从OSGi上的<!-- AEM 6.3 Forms-->AEM 6.4 Forms和OSGi上的AEM 6.5 Forms迁移到[!DNL AEM]as a Cloud Service。 使用程序](/help/implementing/cloud-manager/managing-code/managing-repositories.md)的[Git存储库导入现有的自适应表单模板。

* 默认情况下，电子邮件仅支持HTTP和HTTP协议。 [请与支持团队联系](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email)以启用端口来发送电子邮件，并为您的环境启用SMTP协议。

## 本地化

* 本地化自适应Forms的URL约定现在支持在URL中指定区域设置。 新的URL约定支持在Dispatcher或CDN上缓存本地化的表单。 在Cloud Service环境中，使用URL格式`http://host:port/content/forms/af/<afName>.<locale>.html`请求自适应表单的本地化版本，而不是`http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`。

* Adobe 建议使用 Dispatcher 或 CDN 缓存。它有助于提高预填充表单的渲染速度。


## 自适应表单

* **规则编辑器：** AEM Forms as a Cloud Service提供了一个强化的规则编辑器[规则编辑器](rule-editor.md#visual-rule-editor)。 代码编辑器在Formsas a Cloud Service上不可用。

  [迁移实用程序](/help/forms/migrate-to-forms-as-a-cloud-service.md)可帮助您迁移具有自定义规则（在代码编辑器中创建）的表单。 该实用程序会将此类规则转换为Formsas a Cloud Service上支持的自定义函数。 您可以将可重用的函数与规则编辑器结合使用，以继续获取通过规则脚本获取的结果。 `onSubmitError`或`onSubmitSuccess`函数现在可用作规则编辑器中的操作。

<!--* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server.-->

* **预填充服务：**&#x200B;预填充服务从服务器获取数据，并合并以在客户端预填充您的自适应Forms。 此功能有助于缩短填写自适应表单所需的时间。 您始终可以将[预填充服务](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/prefill-service-adaptive-forms-article-use.html)配置为在Adobe Experience Manager Forms服务器上运行合并操作。

* **提交操作：** **电子邮件**&#x200B;提交操作提供了选项，用于发送附件和使用电子邮件附加记录文档(DoR)。 您可以用它代替AEM 6.5 Forms中可用的&#x200B;**Email作为PDF**&#x200B;操作。

* **Automated forms conversion服务**：该服务未提供Automated forms conversion服务的元模型。 您可以从Automated forms conversion服务文档](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model)中[下载它。

* **基于XSD的自适应Forms：**&#x200B;您可以使用XDP-template为记录文档设计模板。 该服务不支持基于XFA的自适应Forms

* **组件**：该服务不支持表单内签名体验，并且不包含自适应表单的“摘要”和“验证”组件。

* **向导界面：**&#x200B;您可以使用[向导界面](/help/forms/creating-adaptive-form-core-components.md)快速配置常用选项并轻松创建自适应表单。

## Forms门户

* 该服务未保留草稿和已提交的自适应Forms的元数据。

## 文档服务：

Formsas a Cloud Service提供Document Generation和Document Manipulation RESTful API。 您可以根据需要使用这些API来按要求或批量生成或处理文档：

* **Document Services： Document Generation API （输出服务）**：在单一API调用或批处理中，您只能使用一个包含多个DATA XML文件的模板。 不支持在一个API调用中对多个数据文件使用多个模板。

* **文档操作API（汇编程序服务）**：

   * 依赖文档服务或应用程序的操作不可用。 例如，不支持Microsoft®Word到PDF、Microsoft®Excel到PDF、HTML到PDF、PostScript (PS)到PDF、XDP到PDF forms。 这些操作分别依赖于Microsoft®Office、Adobe Acrobat、AdobeDistiller和Forms Document Service。

   * 在将非PDF格式的文档与Communications Document Manipulation API结合使用之前，请将它们转换为PDF格式。 例如，如果您的文档为Microsoft® Office、HTML、PostScript (PS)、XDP格式，则在将这些文档与PDF文档一起使用之前，请将这些文档转换为PDF格式。 您可以将[ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html)服务用于此类转换。

   * 您可以使用AEM 6.5 Forms环境进行数字签名、加密、Reader扩展、发送到打印机、转换PDF和条形码Forms服务。


## 数据集成（表单数据模型）

* 该服务还支持JDBC连接器、Microsoft®Dynamics、SalesForce、基于SOAP的Web服务和支持OData的服务。

* 您还可以连接AEM用户配置文件以检索和更新用户信息。

* Forms数据模型仅支持HTTP和HTTPS端点提交数据。 此服务不支持REST连接器的双向SSL和SOAP数据源的基于x509证书的身份验证。

* Formsas a Cloud Service允许将Microsoft®Azure Blob、Microsoft®Sharepoint、Microsoft®OneDrive以及支持常规CRUD（创建、读取、更新和删除）操作的服务用作数据存储，同时支持Open API规范2.0和Open API 3.0规范。


## 电子签名

* 该服务提供了与Adobe Sign的OOTB集成，并支持DocuSign进行电子签名。

* 该服务还支持Adobe Sign角色。 您可以在自适应Forms编辑器中为商业用户配置角色，以便轻松配置签名工作流。


## HTML5 表单

* 您可以使用AEM 6.5 Forms环境执行以下操作：

   * 将基于XDP的表单渲染为HTML5 Forms。 该服务不支持HTML5 Forms。

   * 脱机捕获数据，并在下次使用[AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html)应用程序重新联机时对其进行同步。

## 交互式通信

* 您可以使用Communications API在Formsas a Cloud Service上按需或批量生成个性化文档。 您可以在交互式通信用例和代理UI用例中使用AEM 6.5 Forms环境。

## 另请参阅

* [从AEM Forms（内部部署和AMS环境）迁移到AEM Formsas a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [在AEM Sites中添加或创建自适应Forms页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [创建自适应表单（核心组件）](/help/forms/creating-adaptive-form-core-components.md)
* [AEM Forms as a Cloud Service 简介](/help/forms/home.md)
* [设置本地开发环境和初始开发项目](/help/forms/setup-local-development-environment.md)


<!--

## Additional Information

* [Introduction to AEM Forms as a Cloud Service](/help/forms/home.md)
* [Set up a local development environment and initial development project](/help/forms/setup-local-development-environment.md)

-->
