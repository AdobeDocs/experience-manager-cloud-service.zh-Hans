---
title: 如何从AEM 6.5 Forms和AEM 6.4 Forms迁移到 [!DNL AEM Forms] as a Cloud Service环境？
description: 从迁移 [!DNL AEM Forms] （内部部署和AMS环境）到 [!DNL AEM Forms] as a Cloud Service环境
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: d9c19d0b567a9a97973c4c4e25e64722da109dbb
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 5%

---

# 从迁移 [!DNL AEM Forms] （内部部署和AMS环境）到 [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

您可以从以下位置迁移自适应Forms、主题、模板和云配置： <!-- AEM 6.3 Forms--> OSGi上的AEM 6.4 Forms和OSGi上的AEM 6.5 Forms [!DNL AEM] as a Cloud Service。 在迁移这些资产之前，请使用迁移实用程序将早期版本中使用的格式转换为中使用的格式 [!DNL AEM] as a Cloud Service。 运行Migration Utility时，将更新以下资产：

* 自适应Forms的自定义组件
* 自适应Forms模板和主题
* 云配置
* 代码编辑器脚本转换为可重用的函数并应用于可视规则。

## 注意事项 {#consideration}

* 该服务仅帮助从迁移内容 [!DNL AEM Forms] 在OSGi环境中。 内容迁移自 [!DNL AEM Forms] 不支持JEE到Cloud Service环境。

* (仅适用于AEM 6.3 Forms或已升级到AEM 6.4 Forms或AEM 6.5 Forms的先前版本环境)不支持基于AEM 6.3 Forms或先前版本中提供的现成模板和主题的自适应Forms [!DNL AEM Forms] as a Cloud Service。

* 与Adobe Experience Manager 6.5 Forms(内部部署和Adobe托管服务)环境相比，Adobe Experience Manager Formsas a Cloud Service对现有功能进行了一些显着更改。 在继续迁移到服务之前， [了解这些值得注意的更改](notable-changes.md) 和 [功能级差异](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report) 以根据贵组织所需的功能决定迁移。




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

## 前提条件 {#prerequisites}

* [启用Forms — 数字注册](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) 选项，适用于您的FormsCloud Service计划和 [运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

   ![练习结果](assets/enable-add-on.png)

* 在Cloud Service环境中，迁移实用程序可与“用户映射工具”和“内容传输工具”配合使用。 迁移实用程序会生成 [!DNL AEM Forms] 与Cloud Service兼容的资源，并且内容传输工具会从您的存储库迁移内容， [!DNL AEM Forms] 环境到 [!DNL AEM] as a Cloud Service环境。 在使用迁移实用程序之前，请了解 [迁移到AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html). 该过程有两个工具：
   * [用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration)：用户映射工具可帮助您将用户映射到相应的Adobe IMS用户帐户。
   * [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration)：内容传输工具可帮助您准备内容并将内容从现有环境传输到Cloud Service环境。
* 拥有管理员权限的帐户 [!DNL AEM Forms] as a Cloud Service和您的本地 [!DNL AEM Forms] 环境。
* 下载并安装Best Practice Analyzer、内容传输工具和 [!DNL AEM Forms] 迁移实用程序 [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)

* 运行 [最佳实践分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) 并修复报告的问题。 有关从Adobe Experience Manager Forms迁移到Adobe Experience Manager Formsas a Cloud Service可能存在的问题，请参阅 [适用于Formsas a Cloud Service的AEM模式检测](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report).


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->

## 迁移 [!DNL AEM Forms] 资产  {#use-the-migration-utility}

执行以下步骤，使 [!DNL AEM Forms] 与Cloud Service兼容的资源，并将其传输到 [!DNL AEM] as a Cloud Service环境。

1. 创建 [克隆](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) ，共个项目 [!DNL AEM Forms] 环境。

   始终使用克隆的环境来运行内容传输工具和迁移实用程序。 内容传输工具和迁移实用程序对内容和资产进行了一些更改。 因此，请勿在生产环境中运行内容传输工具和迁移实用程序。

1. 使用管理权限登录到克隆的环境。

1. 运行 [用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) 以将您的用户映射到相应的Adobe IMS用户帐户。 您需要Adobe IMS用户帐户登录到 [!DNL AEM Forms] as a Cloud Service实例。

1. 下载并安装 [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) 和 [!DNL AEM Forms] as a Cloud Service迁移实用程序 [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 在克隆的环境中。 您可以使用AEM包管理器安装该工具和实用程序。

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 内容迁移]**.

1. 打开 **[!UICONTROL 准备Forms以进行迁移]** 信息卡。 浏览器显示五个选项：
   * **[!UICONTROL AEM Forms 资产迁移]**
   * **[!UICONTROL 自适应Forms自定义组件迁移]**
   * **[!UICONTROL 自适应Forms模板迁移]**
   * **[!UICONTROL AEM Forms 云配置迁移]**
   * **[!UICONTROL 代码编辑器脚本迁移]**

1. 逐一使用选项以使 [!DNL AEM Forms] 与兼容的资产 [!DNL AEM] as a Cloud Service：

   1. 点按 **[!UICONTROL AEM Forms Assets迁移]**，然后在下一个屏幕中，点按 **[!UICONTROL 开始迁移]**. 它使自适应Forms和主题成为您的 [!DNL AEM Forms] 环境兼容 [!DNL AEM] as a Cloud Service。

   1. 点按 **[!UICONTROL 自适应Forms自定义组件迁移]** 在“自定义组件迁移”页面中，点按 **[!UICONTROL 开始迁移]**. 它可以为自适应Forms开发任何自定义组件，并在您的页面上提供组件叠加 [!DNL AEM Forms] 环境兼容 [!DNL AEM] as a Cloud Service。

   1. 点按 **[!UICONTROL 自适应Forms模板迁移]** 在“自定义组件迁移”页面中，点按 **[!UICONTROL 开始迁移]**. 它使/apps或/conf位置并使用AEM模板编辑器创建的自适应表单模板与兼容 [!DNL AEM] as a Cloud Service。

   1. 点按 **[!UICONTROL AEM Forms云配置迁移]** 然后在“配置迁移”页面上，点按 **[!UICONTROL 开始迁移]**. 它会更新以下Cloud Services并将其移动到新位置：

      * 表单数据模型Cloud Service
      * Google reCAPTCHACloud Service
      * [!DNL Adobe Sign] 云服务
      * Adobe FontsCloud Service
   1. 点按 **[!UICONTROL 代码编辑器脚本迁移]**，指定保存可重用函数的位置，然后点按**[!UICONTROL 开始迁移].

   Cloud Service不支持规则编辑器脚本。 此 **[!UICONTROL 代码编辑器脚本迁移]** tool可将环境中的所有规则脚本转换为可重用的函数，并将可重用的函数应用于适当位置的可视化编辑器。 这些可重用的功能以客户端库的形式进行保存，并帮助您保持现有功能不变。 该工具会自动将生成的可重用函数应用于相应的自适应Forms。

   使用 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) 将可重用函数（客户端库）导出到资源包。

1. [部署](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) 可重用函数（客户端库）包， [自定义代码、组件、配置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager)，自定义特定于区域设置的库 [!DNL AEM] as a Cloud Service环境。

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. 运行 [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration). 在上指定参数时 **[!UICONTROL 创建迁移集]** 屏幕，指定自适应Forms、主题、模板、表单数据模型、Cloud Services、自定义组件和其他特定于AEM Forms的资源到 **[!UICONTROL 要包含的路径]** 选项。 它添加指定的 [!DNL AEM Forms] 资源到迁移集。

## 各种特定于AEM Forms的资源的路径

* **自适应Forms**：您可以在以下位置找到自适应表单： `/content/dam/formsanddocuments/`和/content/forms/af。 例如，对于名为WKND注册的自适应表单，请添加路径 `/content/dam/formsanddocuments/wknd-registration` 和 `/content/forms/af/wknd-registration`.
* **表单数据模式**：您可以在以下位置找到所有表单数据模型 `/content/dam/formsanddocuments-fdm`. 例如：`/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`。

* **客户端库**：客户端库的默认路径为 `/etc/clientlibs/fd/theme`.

* **自适应表单模板**：模板的默认路径为 `/conf/<template folder>`. 例如，对于标题为基本添加路径的模板 `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **自适应表单主题和客户端库**：主题的默认路径为 ` /content/dam/formsanddocuments-themes/` 客户端库的默认路径为 `/etc/clientlibs/fd/theme`. 例如，对于名为WKND主题的模板，添加路径 ` /content/dam/formsanddocuments-themes/wkndtheme` 主题和客户端库 `/etc/clientlibs/reference-themes/wkndtheme-3-0`. 您还可以在其他自定义路径中具有主题和客户端库。

* **云配置**：您可以在以下位置找到云配置： `/conf/`. 例如，表单数据模型云配置位于 `/conf/global/settings/cloudconfigs/fdm`.

* **工作流模型**：您可以在以下位置找到AEM工作流模型： `/conf/global/settings/workflow/models/`. 例如，对于名为WKND注册的工作流模型，添加路径 `/conf/global/settings/workflow/models/wknd-registration`

您可以添加下面列出的顶级文件夹路径或如下所述的特定文件夹路径。 它允许您同时迁移特定资源以及所有资源和表单。

* /content/dam/formsanddocuments-fdm
* /content/dam/formsanddocuments/themes
* /content/forms/af
* /etc/clientlibs/fd/theme

要迁移AEM Workflow模型，请指定以下路径：

* /conf/global/settings/workflow/models/
* /conf/global/settings/workflow/launcher
* /var/workflow/model
