---
title: 如何从AEM 6.5 Forms和AEM 6.4 Forms迁移到 [!DNL AEM Forms] as a Cloud Service环境？
description: 从 [!DNL AEM Forms] 内部部署环境 [!DNL AEM Forms] as a Cloud Service环境
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: 8e28cff5b964005278858b6c8dd8a0f5f8156eaa
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 3%

---

# 迁移到[!DNL AEM Forms]as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

您可以从以下位置迁移自适应Forms、主题、模板和云配置： <!-- AEM 6.3 Forms--> AEM 6.4 Forms on OSGi和AEM 6.5 Forms on OSGi to [!DNL AEM] as a Cloud Service。 在迁移这些资产之前，请使用迁移实用程序将早期版本中使用的格式转换为 [!DNL AEM] as a Cloud Service。 运行迁移实用程序时，将更新以下资产：

* 自适应Forms的自定义组件
* 自适应Forms模板和主题
* 云配置
* 代码编辑器脚本将转换为可重用函数并应用于可视化规则。

## 注意事项 {#consideration}

* 该服务仅帮助从 [!DNL AEM Forms] 在OSGi环境中。 将内容从 [!DNL AEM Forms] 不支持在JEE中Cloud Service环境。

* (仅适用于升级到AEM 6.4 Forms或AEM 6.5 Forms的AEM 6.3 Forms或以前版本环境)不支持基于现成模板和AEM 6.3 Forms或以前版本中提供的主题的自适应Forms [!DNL AEM Forms] as a Cloud Service。

## 前提条件 {#prerequisites}

* [启用Forms — 数字注册](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) 的选项，并且 [运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

   ![练习结果](assets/enable-add-on.png)

* 在Cloud Service环境中，迁移实用程序与用户映射工具和内容传输工具结合使用。 迁移实用程序将 [!DNL AEM Forms] 与Cloud Service兼容的资产和内容传输工具可将内容从 [!DNL AEM Forms] 环境 [!DNL AEM] as a Cloud Service环境。 在使用迁移实用程序之前，请了解 [移动到AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html). 该过程有两种工具：
   * [用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration):用户映射工具可帮助您将用户映射到相应的Adobe IMS用户帐户。
   * [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration):内容传输工具可帮助您准备内容并将内容从现有环境传输到Cloud Service环境。
* 具有管理员权限的帐户 [!DNL AEM Forms] as a Cloud Service和您的本地 [!DNL AEM Forms] 环境。
* 下载并安装最佳实践分析器、内容传输工具和 [!DNL AEM Forms] 从迁移实用程序 [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)

* 运行 [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) 工具和修复报告的问题。

<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->

## 迁移 [!DNL AEM Forms] 资产  {#use-the-migration-utility}

请执行以下步骤，以 [!DNL AEM Forms] 与Cloud Service兼容的资产，并将其传输到 [!DNL AEM] as a Cloud Service环境。

1. 创建 [克隆](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) 现有 [!DNL AEM Forms] 环境。

   始终使用克隆环境来运行内容传输工具和迁移实用程序。 内容传输工具和迁移实用程序对内容和资产进行了一些更改。 因此，请不要在生产环境中运行内容传输工具和迁移实用程序。

1. 使用管理权限登录到克隆的环境。

1. 运行 [用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) 以使用相应的Adobe IMS用户帐户来映射用户。 您需要Adobe IMS用户帐户才能登录 [!DNL AEM Forms] as a Cloud Service实例。

1. 下载并安装 [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) 和 [!DNL AEM Forms] as a Cloud Service迁移实用程序 [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 在克隆的环境中。 您可以使用AEM包管理器来安装该工具和实用程序。

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 内容迁移]**.

1. 打开 **[!UICONTROL 准备Forms以进行迁移]** 卡。 浏览器显示五个选项：
   * **[!UICONTROL AEM Forms 资产迁移]**
   * **[!UICONTROL 自适应Forms自定义组件迁移]**
   * **[!UICONTROL 自适应Forms模板迁移]**
   * **[!UICONTROL AEM Forms 云配置迁移]**
   * **[!UICONTROL 代码编辑器脚本迁移]**

1. 逐一使用选项，以 [!DNL AEM Forms] 与 [!DNL AEM] as a Cloud Service:

   1. 点按 **[!UICONTROL AEM Forms Assets迁移]**，然后在下一个屏幕中，点按 **[!UICONTROL 开始迁移]**. 它将制作自适应Forms和您 [!DNL AEM Forms] 与 [!DNL AEM] as a Cloud Service。

   1. 点按 **[!UICONTROL 自适应Forms自定义组件迁移]** 和在自定义组件迁移页面中，点按 **[!UICONTROL 开始迁移]**. 它可为您的自适应Forms开发任何自定义组件，并在 [!DNL AEM Forms] 与 [!DNL AEM] as a Cloud Service。

   1. 点按 **[!UICONTROL 自适应Forms模板迁移]** 和在自定义组件迁移页面中，点按 **[!UICONTROL 开始迁移]**. 它使/apps或/conf中的自适应表单模板(使用AEM模板编辑器创建)与 [!DNL AEM] as a Cloud Service。

   1. 点按 **[!UICONTROL AEM Forms云配置迁移]** 然后，在配置迁移页面上，点按 **[!UICONTROL 开始迁移]**. 它会更新以下Cloud Services并将其移动到新位置：

      * 表单数据模型Cloud Service
      * Google reCAPTCHACloud Service
      * [!DNL Adobe Sign] 云服务
      * Adobe FontsCloud Service
   1. 点按 **[!UICONTROL 代码编辑器脚本迁移]**，指定要保存可重用函数的位置，然后点按**[!UICONTROL 开始迁移].

   Cloud Service不支持规则编辑器脚本。 的 **[!UICONTROL 代码编辑器脚本迁移]** 该工具将您环境中的所有规则脚本转换为可重用函数，并将可重用函数应用到位于适当位置的可视化编辑器。 这些可重用函数以客户端库的形式保存，并帮助您保持现有功能完好无损。 该工具会自动将生成的可重用函数应用到相应的自适应Forms。

   使用 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) 将可重用函数（客户端库）导出到包。

1. [部署](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) 可重用函数（客户端库）包， [自定义代码，组件，配置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager)，自定义区域设置特定的库 [!DNL AEM] as a Cloud Service环境。

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. 运行 [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration). 在 **[!UICONTROL 创建迁移集]** ，可指定自适应Forms、主题、模板、表单数据模型、Cloud Services、自定义组件和其他特定于AEM Forms的资产的路径，以及 **[!UICONTROL 要包含的路径]** 选项。 它会添加指定的 [!DNL AEM Forms] 要迁移的资产。

## 各种特定于AEM Forms的资产的路径

* **自适应Forms**:您可以在 `/content/dam/formsanddocuments/`和/content/forms/af。 例如，对于标题为WKND Registration的自适应表单，添加路径 `/content/dam/formsanddocuments/wknd-registration` 和 `/content/forms/af/wknd-registration`.
* **表单数据模式**:您可以在 `/content/dam/formsanddocuments-fdm`. 例如：`/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`。

* **客户端库**:客户端库的默认路径为 `/etc/clientlibs/fd/theme`.

* **自适应表单模板**:模板的默认路径是 `/conf/<template folder>`. 例如，对于标题为“基本添加路径”的模板 `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **自适应表单主题和客户端库**:主题的默认路径是 ` /content/dam/formsanddocuments-themes/` 而客户端库的默认路径为 `/etc/clientlibs/fd/theme`. 例如，对于标题为WKND主题添加路径的模板 ` /content/dam/formsanddocuments-themes/wkndtheme` 和客户端库(位于 `/etc/clientlibs/reference-themes/wkndtheme-3-0`. 您还可以在其他自定义路径上具有主题和客户端库。

* **云配置**:您可以在 `/conf/`. 例如，表单数据模型云配置位于 `/conf/global/settings/cloudconfigs/fdm`.

* **工作流模型**:您可以在以下位置找到AEM工作流模型： `/conf/global/settings/workflow/models/`. 例如，对于标题为WKND注册添加路径的工作流模型 `/conf/global/settings/workflow/models/wknd-registration`

您可以添加下面列出的顶级文件夹路径，也可以添加下面描述的特定文件夹路径。 它允许您同时迁移特定资产以及所有资产和表单。

* /content/dam/formsanddocuments-fdm
* /content/dam/formsanddocuments/themes
* /content/forms/af
* /etc/clientlibs/fd/theme

要迁移AEM工作流模型，请指定以下路径：

* /conf/global/settings/workflow/models/
* /conf/global/settings/workflow/launcher
* /var/workflow/models
