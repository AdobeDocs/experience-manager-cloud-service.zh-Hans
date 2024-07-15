---
title: 如何从AEM 6.5 Forms迁移到AEM Formsas a Cloud Service？
description: AEM as a Cloud Service迁移历程快速入门 | Adobe Experience Manager。 从 [!DNL AEM Forms] （内部部署和AMS环境）迁移到 [!DNL AEM Forms] as a Cloud Service环境。
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, migrate 6.5 forms to CS, migrate 6.5 forms to cloud service, upgrade 6.5 forms to CS, move 6.5 forms to CS, upgrade AEM 6.5 to CS, AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Migration Journey to AEM as a Cloud Service | Adobe Experience Manager.
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 1%

---

# 从[!DNL AEM Forms]（内部部署和AMS环境）迁移到[!DNL AEM Forms]as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/upgrade.html) |
| AEM as a Cloud Service | 本文 |

您可以将自适应Forms、主题、模板和云配置从OSGi上的<!-- AEM 6.3 Forms AEM 6.4 Forms on OSGi and --> AEM 6.5 Forms迁移或升级到[!DNL AEM]as a Cloud Service。 在迁移这些资源之前，请使用迁移实用程序将早期版本中使用的格式转换为[!DNL AEM]as a Cloud Service中使用的格式。
让我们开始迁移到AEM as a Cloud Service的过程 | Adobe Experience Manager。 运行Migration Utility时，将更新以下资产：

* 自适应Forms的自定义组件
* 自适应Forms模板和主题
* 云配置
* 代码编辑器脚本转换为可重用的函数并应用于可视规则。

## 迁移到Formsas a Cloud Service的注意事项 {#consideration}

要从AEM 6.5 Forms迁移到AEM Cloud Service，请务必考虑以下几点：

* 该服务帮助仅从OSGi环境上的[!DNL AEM Forms]迁移内容。 不支持将内容从JEE上的[!DNL AEM Forms]迁移到Cloud Service环境。

* (仅适用于AEM 6.5 Forms之前的版本)基于AEM 6.3 Forms或先前版本中提供的现成模板和主题的自适应Forms在[!DNL AEM Forms]as a Cloud Service上不受支持。

* 与Adobe Experience Manager 6.5 Forms(内部部署和Adobe托管服务)环境相比，Adobe Experience Manager Formsas a Cloud Service对现有功能进行了一些显着更改。 在继续迁移到服务之前，[了解这些可注释的更改](notable-changes.md)和[功能级别差异](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report)，以决定根据组织所需的功能进行迁移。




<!-- 
## Difference with AEM 6.5 Forms 

| Feature         | Difference with AEM 6.5 Forms    |
|--------------|-----------|
| HTML5 Forms (Mobile Forms)     | The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. |
| Adaptive Forms     | <li><b>XSD-Based Adaptive Forms:</b> The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. </li> <li><b> Adaptive Form templates:</b> Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. </li><li><b>Rule editor:</b> AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor. </li> <li><b>Drafts and submissions:</b> The service does not retain metadata for drafts and submitted Adaptive Forms. </li> <li><b> Prefill Service:</b> By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. </li><li><b>Submit actions:</b> The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. </li>|
| Form Data Model | <li>Forms data model supports only HTTP and HTTPs endpoints to submit data. </li><li>Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores. The service does not support JDBC connector, Mutual SSL for Rest connector, and x509 certificate-based authentication for SOAP data sources. </li>|
| Automated Forms Conversion Service     | The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).|
|Configurations|<li>Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment. </li> <li>If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service.</li> |
| Document Manipulation APIs (Assembler Service)| The service does not support operations dependent on other services or applications: <li>Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported</li><li>Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF</li><li>Forms Service-based conversions are not supported. For example, XDP to PDF Forms.</li><li>The service does not support converting a Signed PDF or Transparent PDF to another PDF format.</li>| -->

## 先决条件 {#prerequisites}

要确保从AEM Forms 6.5顺利过渡到AEM as a Cloud Service环境，请务必考虑以下先决条件：

* 为您的FormsCloud Service程序启用[Forms — 数字注册](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program)选项，并[运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)。

  ![练习结果](assets/enable-add-on.png)

* 在Cloud Service环境中，迁移实用程序与“用户映射工具”和“内容传输工具”配合使用。 迁移实用程序使[!DNL AEM Forms]资源与Cloud Service兼容，内容传输工具将内容从[!DNL AEM Forms]环境迁移到[!DNL AEM]as a Cloud Service环境。 在使用迁移实用程序之前，请了解[移至AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html)的过程。 该过程有两个工具：
   * [用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration)：用户映射工具可帮助您将用户映射到相应的Adobe IMS用户帐户。
   * [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration)：内容传输工具可帮助您准备内容并将内容从现有环境传输到Cloud Service环境。 它有助于用户轻松从AEM Forms升级到云环境。
* 在[!DNL AEM Forms]as a Cloud Service和您的本地[!DNL AEM Forms]环境中具有管理员权限的帐户。
* 从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载并安装Best Practice Analyzer、内容传输工具和[!DNL AEM Forms]迁移实用程序。

* 运行[Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)工具并修复报告的问题。 有关从Adobe Experience Manager Forms迁移到Adobe Experience Manager Formsas a Cloud Service可能存在的问题，请参阅[适用于Forms的AEM模式检测as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report)。


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->




## 将[!DNL AEM 6.5 Forms]资源迁移到AEM Cloud Service {#use-the-migration-utility}

执行以下步骤以使您的[!DNL AEM Forms]资源与Cloud Service兼容并将它们传输到[!DNL AEM]as a Cloud Service环境。

1. 创建现有[!DNL AEM Forms]环境的[克隆](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487)。

   >[!NOTE]
   >
   > 从6.5迁移到云服务时，建议使用克隆的环境来运行内容传输工具和迁移实用程序。 内容传输工具和迁移实用程序对内容和资产进行了一些更改。 因此，请勿在生产环境中运行内容传输工具和迁移实用程序。

1. 使用管理权限登录到您的克隆环境。

1. 运行[用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration)以将您的用户映射到相应的Adobe IMS用户帐户。 您需要Adobe IMS用户帐户才能登录到[!DNL AEM Forms]as a Cloud Service实例。

1. 在克隆的环境中从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载并安装[内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration)和[!DNL AEM Forms]as a Cloud Service迁移实用程序。 可以使用AEM包管理器安装该工具和实用程序。

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 内容迁移]**。

1. 打开&#x200B;**[!UICONTROL 准备Forms以进行迁移]**&#x200B;信息卡。 浏览器显示五个选项：
   * **[!UICONTROL AEM Forms Assets迁移]**
   * **[!UICONTROL 自适应Forms自定义组件迁移]**
   * **[!UICONTROL 自适应Forms模板迁移]**
   * **[!UICONTROL AEM Forms云配置迁移]**
   * **[!UICONTROL 代码编辑器脚本迁移]**

1. 逐个使用选项以使您的[!DNL AEM Forms]资源与[!DNL AEM]as a Cloud Service兼容：

   1. 选择&#x200B;**[!UICONTROL AEM Forms Assets迁移]**，然后在下一个屏幕中选择&#x200B;**[!UICONTROL 开始迁移]**。 它使[!DNL AEM Forms]环境中的自适应Forms和主题与[!DNL AEM]as a Cloud Service兼容。

   1. 选择&#x200B;**[!UICONTROL 自适应Forms自定义组件迁移]**，然后在“自定义组件迁移”页面中选择&#x200B;**[!UICONTROL 开始迁移]**。 它使为自适应Forms开发的任何自定义组件以及[!DNL AEM Forms]环境中的组件叠加与[!DNL AEM]as a Cloud Service兼容。

   1. 选择&#x200B;**[!UICONTROL 自适应Forms模板迁移]**，然后在“自定义组件迁移”页面中选择&#x200B;**[!UICONTROL 开始迁移]**。 它使`/apps`或`/conf`处的自适应表单模板与使用AEM模板编辑器创建的[!DNL AEM]as a Cloud Service兼容。

   1. 选择&#x200B;**[!UICONTROL AEM Forms云配置迁移]**，然后在“配置迁移”页面上选择&#x200B;**[!UICONTROL 开始迁移]**。 它会更新并将以下Cloud Service移动到新位置：

      * 表单数据模型Cloud Service
      * Google reCAPTCHACloud Service
      * [!DNL Adobe Sign]Cloud Service
      * Adobe FontsCloud Service

   1. 选择&#x200B;**[!UICONTROL 代码编辑器脚本迁移]**，指定保存可重用函数的位置，然后选择**[!UICONTROL 开始迁移]。

   Cloud Service不支持规则编辑器脚本。 **[!UICONTROL 代码编辑器脚本迁移]**&#x200B;工具将环境中的所有规则脚本转换为可重用的函数，并将可重用的函数应用到适当位置的可视化编辑器。 这些可重用函数以客户端库形式保存，并帮助您保持现有功能不变。 该工具会自动将生成的可重用函数应用于相应的自适应Forms。

   AEM Form迁移到Cloud Service，请使用[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)将可重用的函数（客户端库）导出到包。

1. [将](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager)可重用的函数（客户端库）包、[自定义代码、组件、配置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager)以及特定于自定义区域设置的库部署到您的[!DNL AEM]as a Cloud Service环境。

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. 运行[内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration)。 在&#x200B;**[!UICONTROL 创建迁移集]**&#x200B;屏幕上指定参数时，请将自适应Forms、主题、模板、表单数据模型(FDM)、Cloud Service、自定义组件和其他特定于AEM Forms的资源路径指定为&#x200B;**[!UICONTROL 要包含的路径]**&#x200B;选项。 它将指定的[!DNL AEM Forms]资源添加到迁移集。

## 各种特定于AEM Forms的资源的路径

从AEM Forms 6.5迁移到云服务时，您可以在以下位置找到特定于AEM Forms的资源：

* **自适应Forms**：您可以在`/content/dam/formsanddocuments/`和`/content/forms/af`找到自适应表单。 例如，对于标题为WKND注册的自适应表单，请添加路径`/content/dam/formsanddocuments/wknd-registration`和`/content/forms/af/wknd-registration`。
* **表单数据模型**：您可以在`/content/dam/formsanddocuments-fdm`找到所有表单数据模型(FDM)。 例如：`/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`。

* **客户端库**：客户端库的默认路径为`/etc/clientlibs/fd/theme`。

* **自适应表单模板**：模板的默认路径为`/conf/<template folder>`。 例如，对于标题为基本添加路径`/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`的模板。

* **自适应表单主题和客户端库**：主题的默认路径为` /content/dam/formsanddocuments-themes/`，客户端库的默认路径为`/etc/clientlibs/fd/theme`。 例如，对于标题为WKND主题的模板，在`/etc/clientlibs/reference-themes/wkndtheme-3-0`处为主题添加路径` /content/dam/formsanddocuments-themes/wkndtheme`和客户端库。 您还可以在其他自定义路径拥有主题和客户端库。

* **云配置**：您可以在`/conf/`中找到云配置。 例如，表单数据模型(FDM)云配置位于`/conf/global/settings/cloudconfigs/fdm`。

* **工作流模型**：您可以在`/conf/global/settings/workflow/models/`找到AEM工作流模型。 例如，对于标题为WKND注册的工作流模型，请添加路径`/conf/global/settings/workflow/models/wknd-registration`

您可以添加下面列出的顶级文件夹路径或如下所述的特定文件夹路径。 它使您能够在从AEM forms 6.5升级到云服务时一次性迁移特定资源以及所有资源和表单。

* `/content/dam/formsanddocuments-fdm`
* `/content/dam/formsanddocuments/themes`
* `/content/forms/af`
* `/etc/clientlibs/fd/theme`

将AEM Workflow模型从AEM Forms 6.5迁移到Cloud Service时，请指定以下路径：

* `/conf/global/settings/workflow/models/`
* `/conf/global/settings/workflow/launcher`
* `/var/workflow/models`

## 查看下一个

* [对现有Adobe Experience Manager 6.5 Forms用户的重要更改](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/notable-changes.html)
* [载入AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service.html)
* [在Cloud Service上创建您的第一个自适应表单](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html)

## 附加信息

迁移实用程序可帮助您迁移基于基础组件的自适应Forms。 此外，Formsas a Cloud Service支持自适应Forms核心组件。 因此，您可以：

* [创建基于核心组件的独立自适应Forms](/help/forms/creating-adaptive-form-core-components.md)
* [直接在AEM Sites页面中创建基于核心组件的自适应表单](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

要了解有关AEM Formsas a Cloud Service的更多信息，请参阅：

* [AEM FormsCloud Service简介](/help/forms/home.md)
* [AEM FormsCloud Service中的创新](/help/forms/latest-innovations.md)