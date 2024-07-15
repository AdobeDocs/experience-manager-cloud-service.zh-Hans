---
title: 如何为AEM Forms配置 [!DNL Microsoft Dynamics] OData？
description: 了解如何基于 [!DNL Microsoft Dynamics] 服务中定义的实体、属性和服务创建表单数据模型(FDM)。
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# [!DNL Microsoft Dynamics] OData配置 {#microsoft-dynamics-odata-configuration}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/ms-dynamics-odata-configuration.html) |
| AEM as a Cloud Service | 本文 |

![数据集成](assets/data-integeration.png)

[!DNL Microsoft Dynamics]是一个客户关系管理(CRM)和企业资源规划(ERP)软件，它提供用于创建和管理客户帐户、联系人、潜在客户、机会和案例的企业解决方案。 [[!DNL Experience Manager Forms] 数据集成](data-integration.md)提供OData云服务配置以将Forms与在线和本地[!DNL Microsoft Dynamics]服务器集成。 它使您能够根据在[!DNL Microsoft Dynamics]服务中定义的实体、属性和服务来创建表单数据模型(FDM)。 表单数据模型(FDM)可用于创建与[!DNL Microsoft Dynamics]服务器交互以启用业务工作流的自适应Forms。 例如：

* 查询[!DNL Microsoft Dynamics]服务器以获取数据并预填充Adaptive Forms
* 提交自适应表单时将数据写入[!DNL Microsoft Dynamics]
* 通过表单数据模型(FDM)中定义的自定义实体在[!DNL Microsoft Dynamics]中写入数据，反之亦然

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  MS Dynamics ODataCloud Service（OData服务）在所有运行模式下均可用。 有关为[!DNL Experience Manager]实例配置运行模式的详细信息，请参阅[运行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#runmodes)。

AEM as a Cloud Service提供了多种现成的提交操作来处理表单提交。 您可以在[自适应表单提交操作](/help/forms/configure-submit-actions-core-components.md)文章中了解有关这些选项的更多信息。


## 先决条件 {#prerequisites}

在开始设置和配置[!DNL Microsoft Dynamics]之前，请确保您具有：

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* 已联机配置[!DNL Microsoft Dynamics] 365，或已安装以下[!DNL Microsoft Dynamics]版本之一的实例：

   * [!DNL Microsoft Dynamics] 365内部部署
   * [!DNL Microsoft Dynamics] 2016年内部部署

* [已向 [!DNL Microsoft Azure] Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)注册 [!DNL Microsoft Dynamics] 联机服务的应用程序。 记下已注册服务的客户端ID（也称为应用程序ID）和客户端密钥的值。 在[为您的 [!DNL Microsoft Dynamics] 服务](#configure-cloud-service-for-your-microsoft-dynamics-service)配置云服务时，将使用这些值。

## 为注册的[!DNL Microsoft Dynamics]应用程序设置回复URL {#set-reply-url-for-registered-microsoft-dynamics-application}

执行以下操作以设置已注册的[!DNL Microsoft Dynamics]应用程序的回复URL：

>[!NOTE]
>
>仅在将[!DNL Experience Manager Forms]与行[!DNL Microsoft Dynamics]服务器集成时使用此过程。

1. 转到[!DNL Microsoft Azure] Active Directory帐户，并在注册应用程序的&#x200B;**[!UICONTROL 回复URL]**&#x200B;设置中添加以下云服务配置URL：

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目录](assets/azure_directory_new.png)

1. 保存配置。

## 为IFD配置[!DNL Microsoft Dynamics] {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics]使用基于声明的身份验证向外部用户提供对[!DNL Microsoft Dynamics] CRM服务器上数据的访问。 要启用此功能，请执行以下操作为面向Internet的部署(IFD)配置[!DNL Microsoft Dynamics]并配置声明设置。

>[!NOTE]
>
> 仅在将[!DNL Experience Manager Forms]与内部部署[!DNL Microsoft Dynamics]服务器集成时使用此过程。

1. 为IFD配置[!DNL Microsoft Dynamics]本地实例，如[为 [!DNL Microsoft Dynamics]配置IFD](https://technet.microsoft.com/en-us/library/dn609803.aspx)中所述。
1. 使用Windows PowerShell运行以下命令以在启用IFD的[!DNL Microsoft Dynamics]上配置声明设置：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   有关详细信息，请参阅[CRM内部部署(IFD)的应用程序注册](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd)。

## 在AD FS计算机上配置OAuth客户端 {#configure-oauth-client-on-ad-fs-machine}

执行以下操作以在Active Directory联合身份验证服务(AD FS)计算机上注册OAuth客户端并授予对AD FS计算机的访问权限：

>[!NOTE]
>
>仅在将[!DNL Experience Manager Forms]与内部部署[!DNL Microsoft Dynamics]服务器集成时使用此过程。

1. 运行以下命令：

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID`是使用任何GUID生成器生成的客户端ID。
   * `redirect-uri`是[!DNL Experience Manager Forms]上[!DNL Microsoft Dynamics] OData云服务的URL。 与[!DNL Experience Manager Forms]一起安装的默认云服务部署在以下URL上：
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 运行以下命令以授予AD FS计算机上的访问权限：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource`是[!DNL Microsoft Dynamics]组织URL。

1. [!DNL Microsoft Dynamics]使用HTTPS协议。 要从[!DNL Forms]服务器调用AD FS端点，请在运行[!DNL Experience Manager Forms]的计算机上使用`keytool`命令将[!DNL Microsoft Dynamics]站点证书安装到Java证书存储中。

## 为您的[!DNL Microsoft Dynamics]服务配置云服务 {#configure-cloud-service-for-your-microsoft-dynamics-service}

OData服务由其服务根URL标识。 要在[!DNL Experience Manager]as a Cloud Service中配置OData服务，请确保您拥有该服务的服务根URL，并执行以下操作：

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>有关配置[!DNL Microsoft Dynamics 365]（在线或本地）的分步指南，请参阅[[!DNL Microsoft Dynamics] OData配置](ms-dynamics-odata-configuration.md)。

1. 转到&#x200B;**[!UICONTROL 工具>Cloud Service>数据源]**。 选择以选择要创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置文件夹](#cloud-folder)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据Source配置向导]**。 指定配置的名称和标题，从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL OData服务]**，浏览并选择配置的缩略图图像，然后选择&#x200B;**[!UICONTROL 下一步]**。
在**[!UICONTROL 身份验证设置]**&#x200B;选项卡中：

   1. 输入&#x200B;**[!UICONTROL 服务根]**&#x200B;字段的值。 转到Dynamics实例并导航到&#x200B;**[!UICONTROL 开发人员资源]**，以查看服务根字段的值。 例如， https://&lt;tenant-name>/api/data/v9.1/

   1. 选择&#x200B;**[!UICONTROL OAuth 2.0]**&#x200B;作为身份验证类型。

   1. 将&#x200B;**[!UICONTROL 客户端ID]**（也称为&#x200B;**应用程序ID**）、**[!UICONTROL 客户端密钥]**、**[!UICONTROL OAuth URL]**、**[!UICONTROL 刷新令牌URL]**、**[!UICONTROL 访问令牌URL]**&#x200B;和&#x200B;**[!UICONTROL 资源]**&#x200B;字段中的默认值替换为[!DNL Microsoft Dynamics]服务配置中的值。 必须在&#x200B;**[!UICONTROL 资源]**&#x200B;字段中指定动态实例URL，以使用表单数据模型(FDM)配置[!DNL Microsoft Dynamics]。 使用服务根URL派生动态实例URL。 例如，[https://org.crm.dynamics.com](https://org.crm.dynamics.com/)。

   1. 在&#x200B;**[!UICONTROL 授权范围]**&#x200B;字段中为[!DNL Microsoft Dynamics]上的授权进程指定&#x200B;**[!UICONTROL openid]**。

      ![身份验证设置](assets/dynamics_authentication_settings_new.png)
表单数据模型(FDM)
1. 单击&#x200B;**[!UICONTROL 连接到OAuth]**。 您将被重定向到[!DNL Microsoft Dynamics]登录页面。
1. 使用您的[!DNL Microsoft Dynamics]凭据登录并接受以允许云服务配置连接到[!DNL Microsoft Dynamics]服务。 建立表单数据模型(FDM)是云服务和服务的一次性任务。

   您是云服务配置页面的表单数据模型，该页面显示一条消息，表明OData配置已成功保存。

MS Dynamics ODataCloud Service（OData服务）云服务已配置并与您的Dynamics服务连接。 表单数据模型(FDM)

## 创建表单数据模型(FDM) {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

配置MS Dynamics OData云服务后，您可以在创建表单数据模型(FDM)时使用该服务。 有关详细信息，请参阅[创建表单数据模型(FDM)](create-form-data-models.md)。

接下来，您可以创建基于自适应表单的表单数据模型(FDM)，并将其用于各种自适应表单用例，例如：

* 通过查询[!DNL Microsoft Dynamics]实体和服务中的信息来预填充自适应表单
* 使用自适应表单规则调用在表单数据模型(FDM)中定义的[!DNL Microsoft Dynamics]服务器操作
* 将提交的表单数据写入[!DNL Microsoft Dynamics]实体

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

您可以[为自适应表单](/help/forms/using-form-data-model.md)配置表单数据模型提交操作，以将数据发送到Microsoft Dynamics OData。

有关在业务工作流中创建和使用表单数据模型(FDM)的更多信息，请参阅[数据集成](data-integration.md)。

## 相关文章

{{af-submit-action}}
