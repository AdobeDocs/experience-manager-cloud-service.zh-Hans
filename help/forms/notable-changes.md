---
title: AEM 6.5 Forms与AEM Cloud Services之间的差异
description: 您是否是Experience Manager Forms用户，并且希望升级到Adobe Experience Manager Formsas a Cloud Service？ 在升级或迁移到Cloud Service之前，比较AEM 6.5 Forms和AEM Cloud Services并了解最显着的更改。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 2%

---

# 对现有Adobe Experience Manager 6.5 Forms用户的显着更改  {#notable-changes-for-existing-AEM-Forms-users}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html) |
| AEM as a Cloud Service | 本文 |


与Adobe Experience Manager Forms On-Premise和相比，Adobe Experience Manager Formsas a Cloud Service对现有功能进行了一些显着更改 [!DNL Adobe-Managed Service] 环境。 主要差异列示如下：

## 云原生功能

* 该服务具有云原生架构，允许根据负载自动缩放，升级时无需停机，频繁推出新功能和更新后也无需停机，拓扑优化以实现最大的弹性和效率。

* 该服务不包含将数据存储到Adobe Experience ManagerCloud Service实例的提交操作，因此超级安全。 通过表单捕获的数据将直接发送到配置的数据存储区。

* 此外，还包括一个免费的CDN（内容交付网络），可帮助您更快地交付和渲染表单。


## 更新了开发流

* 该服务提供了一个SDK，用于在将自定义代码部署到Cloud Service之前，在本地环境（本地计算机）中开发和测试该代码。 开发人员在其本地计算机上使用SDK开发和测试自定义组件、主题、工作流应用程序、配置、模板等。 在本地开发环境中测试自定义代码后，他们将自定义代码部署到 [Forms CS环境开发或暂存环境](/help/implementing/cloud-manager/deploy-code.md) ，以供在将它升级到生产环境之前进行进一步测试。

* 开发人员维护通用的Cloud Service和本地开发环境的代码 [git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). 在创建AEMas a Cloud Service程序时，会自动创建基于AEM原型的Git存储库。

  ![在AEM as a cloud service程序上自动创建git存储库](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Formsas a Cloud Service的开发流程与AEM Cloud Service的AEM Archetype保持一致。 但是，需要对Adobe Experience Manager Maven项目进行一些更改才能与AEM Cloud Service兼容。 从较高层面来看，AEM需要将内容和代码分离为离散的子包，以遵循可变内容和不可变内容之间的拆分。 使用 [Repository Modernizer工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) 通过将内容和代码分隔到单独的软件包来重构现有项目软件包，使其与为Adobe Experience Manager as a Cloud Service定义的项目结构兼容。

* 在将客户捆绑包与Formsas a Cloud Service结合使用之前，请使用最新版本的adobe-aemfd-docmanager重新编译自定义代码。

* 使用 [AEM Formsas a Cloud Service迁移实用程序](/help/forms/migrate-to-forms-as-a-cloud-service.md) 准备和迁移自适应Forms、主题、模板和云配置，从 <!-- AEM 6.3 Forms--> OSGi上的AEM 6.4 Forms和OSGi上的AEM 6.5 Forms [!DNL AEM] as a Cloud Service。 使用 [项目的Git存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 以导入现有的自适应表单模板。

* 默认情况下，电子邮件仅支持HTTP和HTTP协议。 [联系支持团队](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 启用发送电子邮件的端口并为环境启用SMTP协议。

## 本地化

* 本地化自适应Forms的URL约定现在支持在URL中指定区域设置。 新的URL约定支持在Dispatcher或CDN上缓存本地化的表单。 在Cloud Service环境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 请求自适应表单的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe建议使用Dispatcher或CDN缓存。 它有助于提高预填充表单的渲染速度。


## 自适应表单

* **规则编辑器：** AEM Formsas a Cloud Service提供强化的功能 [规则编辑器](rule-editor.md#visual-rule-editor). 代码编辑器在Formsas a Cloud Service上不可用。

  此 [迁移实用程序](/help/forms/migrate-to-forms-as-a-cloud-service.md) 帮助您迁移具有自定义规则（在代码编辑器中创建）的表单。 该实用程序会将此类规则转换为Formsas a Cloud Service上支持的自定义函数。 您可以将可重用的函数与 规则编辑器结合使用，以继续获取通过规则脚本获取的结果。此 `onSubmitError` 或 `onSubmitSuccess` 函数现在可用作规则编辑器中的操作。

* **预填充服务：** 默认情况下，预填充服务在客户端将数据与自适应表单合并，而不是在AEM 6.5 Forms中合并服务器上的数据。 该功能有助于缩短预填自适应表单所需的时间。 您始终可以配置以在Adobe Experience Manager Forms服务器上运行合并操作。

* **提交操作：** 此 **电子邮件** 提交操作提供了选项，用于发送附件和使用电子邮件附加记录文档(DoR)。 您可以使用它来代替 **作为PDF发送电子邮件** 可在AEM 6.5 Forms中执行的操作。

* **automated forms conversion服务**：服务不提供Automated forms conversion服务的元模型。 您可以 [从Automated forms conversion服务文档下载](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **基于XSD的自适应Forms：** 您可以使用XDP模板为记录文档设计模板。 该服务不支持基于XFA的自适应Forms

* **组件**：您可以使用 [自适应Forms核心组件](/help/forms/creating-adaptive-form-core-components.md) 来设计您的表单。 这些组件基于WCM核心组件，遵循BEM标准，并可轻松自定义。 该服务不支持表单内签名体验，也不包含自适应表单的“摘要”和“验证”组件

## Forms Portal

* 您可以使用Forms Portal的Search &amp; Lister、Drafts and Submission和Link组件列出登录用户的表单。 不支持开箱即用的Forms Portal匿名使用(OOTB)。 您可以自定义Forms Portal以启用为非登录用户显示表单。

* 该服务未保留草稿和已提交的自适应Forms的元数据。

## 文档服务:

Formsas a Cloud Service提供Document Generation和Document Manipulation RESTful API。 您可以使用这些API根据需要或批量生成或处理文档：

* **文档服务：文档生成API（输出服务）**：在单个API调用或批处理中，您只能使用一个包含多个DATA XML文件的模板。 不支持在一个API调用中对多个数据文件使用多个模板。

* **文档操作API（汇编程序服务）**：

   * 依赖文档服务或应用程序的操作不可用。 例如，不支持Microsoft Word到PDF、Microsoft Excel到PDF、HTML到PDF、PostScript (PS)到PDF、XDP到PDF forms。 这些操作分别依赖于Microsoft Office、Adobe Acrobat、AdobeDistiller、Forms Document Service。

   * 在将非PDF格式的文档与Communications Document Manipulation API结合使用之前，请将它们转换为PDF格式。 例如，如果您的文档为Microsoft Office、HTML、PostScript (PS)、XDP格式，则在将这些文档与PDF文档一起使用之前，请将这些文档转换为PDF格式。 您可以使用 [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) 转换的服务。

* 您可以使用AEM 6.5 Forms环境进行数字签名、加密、Reader扩展、发送到打印机、转换PDF和条形码Forms服务。


## 数据集成（表单数据模型）

* 该服务还支持JDBC连接器、Microsoft Dynamics、SalesForce、基于SOAP的Web服务和支持OData的服务。

* 您还可以连接AEM用户配置文件以检索和更新用户信息。

* Forms数据模型仅支持HTTP和HTTPS端点提交数据。 此服务不支持REST连接器的双向SSL和SOAP数据源的基于x509证书的身份验证。

* Formsas a Cloud Service允许将Microsoft Azure Blob、Microsoft Sharepoint、Microsoft OneDrive以及支持常规CRUD（创建、读取、更新和删除）操作的服务用作数据存储，同时支持Open API规范2.0和Open API 3.0规范。


## 电子签名

* 该服务提供了与Adobe Sign的OOTB集成，并支持DocuSign进行电子签名。

* 该服务还支持Adobe Sign角色。 您可以在自适应Forms编辑器中为企业用户配置角色，以便轻松配置签名工作流。


## HTML5 表单

* 您可以使用AEM 6.5 Forms环境执行以下操作：

   * 将基于XDP的表单渲染为HTML5 Forms。 该服务不支持HTML5 Forms (Mobile Forms)。

   * 离线捕获数据，并在您下次重新联机时使用 [AEM Forms工作区](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) 应用程序。

## 交互式通信

* 您可以使用Communications API在Formsas a Cloud Service上按需或批量生成个性化文档。 您可以将AEM 6.5 Forms环境用于交互式通信和Agent UI用例。

## 查看下一个

* [从AEM Forms（内部部署和AMS环境）迁移到AEM Formsas a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [“在AEM Sites中添加或创建自适应Forms”页](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [创建自适应表单（核心组件）](/help/forms/creating-adaptive-form-core-components.md)

## 附加信息

* [AEM Formsas a Cloud Service简介](/help/forms/home.md)
* [设置本地开发环境和初始开发项目](/help/forms/setup-local-development-environment.md)
