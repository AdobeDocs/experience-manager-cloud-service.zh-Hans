---
title: AEM 6.5 Forms与AEM云服务之间的差异
description: 您是Experience Manager Forms用户并且希望升级到Adobe Experience Manager Formsas a Cloud Service吗？ 比较AEM 6.5 Forms和AEM云服务，并了解在升级或迁移到Cloud Service之前最显着的更改。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 54a1ae1cc030030e44612b502b70c9b567144538
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 2%

---

# 对现有Adobe Experience Manager 6.5 Forms用户的显着更改  {#notable-changes-for-existing-AEM-Forms-users}

与Adobe Experience Manager Forms本地版和本地版相比，Adobe Experience Manager Forms as a Cloud Service对现有功能做出了一些显着更改 [!DNL Adobe-Managed Service] 环境。 主要区别如下：

## 云本机功能

* 该服务具有云原生架构，允许根据负载进行自动扩展，升级无停机，频繁和推出新功能和更新后，以及为实现最大可复原性和效率而优化的拓扑。

* 该服务不包含可将数据存储到Adobe Experience ManagerCloud Service实例的提交操作，从而使其变得超级安全。 通过表单捕获的数据将直接发送到配置的数据存储。

* 此外，还提供免费的CDN（内容交付网络），以帮助您更快地交付和渲染表单。


## 开发流程更新

* 该服务提供了一个SDK，用于在本地环境（本地计算机）中开发和测试自定义代码，然后再将代码部署到Cloud Service。 开发人员在其本地计算机上使用SDK开发和测试自定义组件、主题、工作流应用程序、配置、模板等。 在其本地开发环境中测试自定义代码后，他们会将自定义代码部署到 [Forms CS环境开发或暂存环境](/help/implementing/cloud-manager/deploy-code.md) 以在将其提升到生产环境之前进行进一步测试。

* 开发人员在通用环境中维护Cloud Service和本地开发环境的代码 [git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). 创建AEMas a Cloud Service程序时，将自动创建基于AEM Archetype的Git存储库。

   ![](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Formsas a Cloud Service的开发流程与AEM Cloud Service的AEM Archetype保持一致。 但是，Adobe Experience Manager Maven项目需要进行一些更改才能与AEM Cloud Service兼容。 在高级别上，AEM要求将内容和代码分离为离散的子包，以便遵循可变内容和不可变内容之间的拆分。 使用 [Repository Modernizer工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) 通过将内容和代码分离为离散的包来重构现有项目包，以与为Adobe Experience Manager as a Cloud Service定义的项目结构兼容。

* 在将客户包与Forms as a Cloud Service一起使用之前，请使用最新版本的adobe-aemfd-docmanager重新编译您的自定义代码。

* 使用 [AEM Formsas a Cloud Service迁移实用程序](/help/forms/migrate-to-forms-as-a-cloud-service.md) 要准备和迁移自适应Forms、主题、模板和云配置，请从 <!-- AEM 6.3 Forms--> AEM 6.4 Forms on OSGi和AEM 6.5 Forms on OSGi to [!DNL AEM] as a Cloud Service。 使用 [程序的Git存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 导入现有自适应表单模板。

* 默认情况下，电子邮件仅支持HTTP和HTTPs协议。 [联系支持团队](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 启用用于发送电子邮件的端口，并为环境启用SMTP协议。

## 本地化

* 本地化的自适应Forms的URL约定现在支持在URL中指定区域设置。 新的URL约定允许在调度程序或CDN上缓存本地化的表单。 在Cloud Service环境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 请求自适应表单的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe建议使用Dispatcher或CDN缓存。 这有助于提高预填充表单的渲染速度。


## 自适应表单

* **规则编辑器：** AEM Formsas a Cloud Service提供了经过硬化 [规则编辑器](rule-editor.md#visual-rule-editor). 代码编辑器在Formsas a Cloud Service上不可用。

   的 [迁移实用程序](/help/forms/migrate-to-forms-as-a-cloud-service.md) 可帮助您迁移具有自定义规则的表单（在代码编辑器中创建）。 该实用程序会将这些规则转换为Formsas a Cloud Service支持的自定义函数。 您可以将可重用的函数与 规则编辑器结合使用，以继续获取通过规则脚本获取的结果。的 `onSubmitError` 或 `onSubmitSuccess` 函数现在可在规则编辑器中作为操作使用。

* **预填充服务：** 默认情况下，预填充服务会在客户端将数据与自适应表单合并，而不是在AEM 6.5 Forms的服务器上合并数据。 该功能有助于缩短预填自适应表单所需的时间。 您始终可以配置为在Adobe Experience Manager Forms服务器上运行合并操作。

* **提交操作：** 的 **电子邮件** “提交”操作提供了发送附件和通过电子邮件附加记录文档(DoR)的选项。 您可以使用它代替 **电子邮件作为PDF** 操作在AEM 6.5 Forms中可用。

* **automated forms conversion服务**:该服务不为Automated forms conversion服务提供元模型。 您可以 [从Automated forms conversion服务文档下载它](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **基于XSD的自适应Forms:** 可以使用XDP模板为“记录文档”设计模板。 该服务不支持基于XFA的自适应Forms

* **组件**:您可以使用 [自适应Forms核心组件](/help/forms/creating-adaptive-form-core-components.md) 来设计表单。 这些组件基于WCM核心组件，遵循BEM标准，并且可以轻松自定义。 该服务不支持表单内签名体验，并且不包含自适应表单的“摘要”和“验证”组件

## Forms Portal

* 您可以使用Forms Portal的搜索和制表人、草稿和提交以及链接组件来列出已登录用户的表单。 无法开箱即用(OOTB)地支持匿名使用Forms Portal。 您可以自定义Forms门户，以为未登录的用户启用显示表单的功能。

* 该服务不会保留草稿和提交的自适应Forms的元数据。

## 文档服务:

Formsas a Cloud Service提供文档生成和文档操作RESTful API。 您可以根据需要，使用这些API按需或批量生成或处理文档：

* **文档服务：文档生成API（输出服务）**:在单个API调用或批量处理中，您只能将一个模板与多个DATA XML文件一起使用。 不支持在单个API调用中使用多个模板和多个数据文件。

* **文档操作API（汇编程序服务）**:

   * 依赖文档服务或应用程序的操作不可用。 例如，不支持Microsoft Word到PDF、Microsoft Excel到PDF、HTML到PDF、PostScript(PS)到PDF、XDP到PDF forms。 这些操作分别依赖于Microsoft Office、Adobe Acrobat、AdobeDistiller、Forms文档服务。

   * 将非PDF格式的文档转换为PDF格式，然后再将这些文档与通信文档处理API结合使用。 例如，如果您的文档采用Microsoft Office、HTML、PostScript(PS)、XDP格式，请先将这些文档转换为PDF格式，然后再将这些文档与PDF文档一起使用。 您可以使用 [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) 用于此类转化的服务。

* 您可以使用AEM 6.5 Forms环境进行数字签名、加密、Reader扩展、发送到打印机、转换PDF和条形码Forms服务。


## 数据集成（表单数据模型）

* 该服务还支持JDBC连接器、Microsoft Dynamics、SalesForce、基于SOAP的Web服务以及支持OData的服务。

* 您还可以连接AEM用户配置文件以检索和更新用户信息。

* Forms数据模型仅支持HTTP和HTTPS端点提交数据。 该服务不支持REST连接器的互相SSL以及SOAP数据源的基于x509证书的身份验证。

* Formsas a Cloud Service允许将Microsoft Azure Blob、Microsoft Sharepoint、Microsoft OneDrive和支持常规CRUD（创建、读取、更新和删除）操作的服务用作数据存储，同时支持Open API规范2.0和Open API 3.0规范。


## 电子签名

* 该服务提供与Adobe Sign的OOTB集成，并支持DocuSign进行电子签名。

* 该服务还支持Adobe Sign角色。 您可以在自适应Forms编辑器中为业务用户配置角色，以轻松配置签名工作流。


## HTML5 表单

* 您可以使用AEM 6.5 Forms环境执行以下操作：

   * 将基于XDP的表单渲染为HTML5 Forms。 该服务不支持HTML5 Forms(Mobile Forms)。

   * 捕获数据离线，并在下次与 [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) 应用程序。

## 交互式通信

* 您可以使用通信API按需或在Formsas a Cloud Service上批量生成个性化文档。 您可以将AEM 6.5 Forms环境用于交互式通信和代理UI用例。


