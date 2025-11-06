---
title: 管理 [!DNL Adobe Stock] 中的 [!DNL Assets]资源。
description: 在 [!DNL Adobe Stock] 内搜索、获取、许可和管理 [!DNL Adobe Experience Manager]资源。 将许可资产用作任何其他数字资产。
contentOwner: Vishabh Gupta
feature: Adobe Stock
role: Admin, User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 5%

---

# 在[!DNL Adobe Stock]中使用[!DNL Adobe Experience Manager Assets]资源 {#use-adobe-stock-assets-in-aem-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/aem-assets-adobe-stock.html?lang=en) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Stock] 服务为设计师和企业提供数百万高质量、精选的免版税照片、矢量图、插图、视频、模板和 3D 资产，可满足各种创意项目需求。

默认情况下，企业产品的[!DNL Adobe Stock]包含跨组织的共享权限。 资产获得组织用户的许可后，组织的其他用户便可以识别、下载和使用此资产，而无需再次许可。 一旦您的组织对资产进行了许可，该资产的使用权即永久有效。

组织可以将其企业[!DNL Adobe Stock]计划与[!DNL Experience Manager Assets]集成，以确保许可资产可广泛用于其创意和营销项目，并具有[!DNL Experience Manager]的强大资产管理功能。 [!DNL Experience Manager]用户无需离开[!DNL Experience Manager]界面，即可快速查找、预览和许可[!DNL Experience Manager]中保存的Adobe Stock资源。

## 集成[!DNL Experience Manager]和[!DNL Adobe Stock]的先决条件 {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets]允许用户直接从[!DNL Adobe Stock]搜索、预览、保存和许可[!DNL Experience Manager]资源。

满足以下要求以启用此集成：

* 启动并作为[!DNL Experience Manager Assets]实例运行[!DNL Cloud Service]。
* 企业[!DNL Adobe Stock]计划。
* 在[!DNL Admin Console]中具有默认Stock产品配置文件权限的用户。
* 具有在[!DNL Developer Access profile]中创建集成的[!DNL Adobe Developer Console]权限的用户。

企业[!DNL Adobe Stock]计划，

* 提供[!DNL Adobe Stock]的产品权利(与Experience Manager连接的库存)。
* 为[!DNL Adobe Admin Console]购买的股票权利积分。
* 允许在[!DNL Adobe Admin Console]内全局管理信用和许可。

在权利中，[!DNL Adobe Stock]中存在[!DNL Admin Console]的默认产品配置文件。 可以创建多个配置文件，这些配置文件确定谁可以许可Stock资产。 直接访问产品配置文件的用户可以访问[https://stock.adobe.com/](https://stock.adobe.com/)并许可Stock资产。 而则可以使用开发人员访问权限创建集成(API)的其他方法。 此集成验证[!DNL Experience Manager Assets]与[!DNL Adobe Stock]之间的通信。

<!--
### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).
-->

<!-- 
TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in User Preferences panel. To access the panel from Experience Manager home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.
-->

## 集成[!DNL Experience Manager]和[!DNL Adobe Stock] {#integrate-adobe-stock-with-aem-assets}

作为开发人员，执行以下步骤以集成[!DNL Adobe Experience Manager]和[!DNL Adobe Stock]。

<!--
1. [Obtain public certificate](#public-certificate)
   
   In [!DNL Experience Manager], create an IMS account and generate a public certificate (public key).

1. [Create service account (JWT) connection](#createnewintegration) 
   
   In [!DNL Adobe Developer Console], create a project for your [!DNL Adobe Stock] organization. Under the project, configure an API using the public key to create a service account (JWT) connection. Get the service account credentials and JWT payload information.

1. [Configure IMS account](#create-ims-account-configuration)

   In [!DNL Experience Manager], configure the IMS account using the service account credentials and JWT payload.

1. [Configure cloud service](#configure-the-cloud-service)

   In [!DNL Experience Manager], configure an [!DNL Adobe Stock] cloud service using the IMS account.


### Create an IMS configuration {#create-an-ims-configuration}

The IMS configuration authenticates your [!DNL Experience Manager Assets] author instance with the [!DNL Adobe Stock] entitlement. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your product profile in Adobe Developer Console.

1. Log in to your [!DNL Experience Manager Assets] cloud instance.

1. From the **[!UICONTROL Tools]** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. The **[!UICONTROL Adobe IMS Technical Account Configuration]** page opens. 

1. In the **[!UICONTROL Certificate]** tab, select **[!UICONTROL Adobe Stock]** from the **[!UICONTROL Cloud Solution]** drop-down list.  

1. You can create a certificate or reuse an existing certificate for the configuration. 

   To create a certificate, select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 

1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine. The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.

   Click **[!UICONTROL Next]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. In the **Account** tab, Adobe IMS account is created which requires the service account credentials.

   Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration). 

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at organization level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. In this example, the service account credentials are generated by uploading the public key.

To generate the service account credentials and JWT payload:

1. Log in to Adobe Developer Console with system administrator privileges. The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Ensure that you have selected the correct IMS organization (Stock entitlement) from the drop-down (organization) list.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]**. Update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and then click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL Adobe Stock]**. Click **[!UICONTROL Next]**. 

1. In the **[!UICONTROL Configure API]** window, select **[!UICONTROL Service Account (JWT)]** authentication. Click **[!UICONTROL Next]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Click **[!UICONTROL Upload your public key]**. Click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. Click **[!UICONTROL Next]**.

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select the default **[!UICONTROL Adobe Stock]** product profile and click **[!UICONTROL Save configured API]**. 

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option. Here, you can view the credentials and perform actions such as generate JWT tokens, copy credential details, and retrieve client secret.

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### Configure IMS account {#create-ims-account-configuration}

You must have the [certificate](#public-certificate) and [service account (JWT) credentials](#createnewintegration) to configure the IMS account.

To configure the IMS account: 

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, enter the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).  

   Enter the client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

1. Click **[!UICONTROL Create]**. An IMS account configuration is created. 

   ![configure-ims-acount](assets/aem-stock-ims-config.png)
   
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![health-check](assets/aem-stock-healthcheck.png)
-->

1. [在 [!DNL Developer Console]中设置程序](#set-up-a-program-in-developer-console)
1. [在 [!DNL AEM] 创作实例中添加配置](#add-configuration-in-the-aem-author-instance)

### 在[!DNL Developer Console]中设置程序 {#set-up-a-program-in-developer-console}

执行以下步骤以在[!DNL Developer Console]中设置程序：

1. 导航到[[!DNL Adobe Developer Console]](https://developer.adobe.com/console/14431/user/servicesandapis)并登录您的组织。
1. 选择&#x200B;**[!UICONTROL 新建项目]**（可在&#x200B;**[!UICONTROL 项目]**仪表板上找到）。
   ![将aem资产与adobe stock集成](/help/assets/assets/create-new-project-in-adobe-dev-console.png)
1. 单击&#x200B;**[!UICONTROL 添加到项目]**&#x200B;并选择&#x200B;**[!UICONTROL API]**。
1. 选择&#x200B;**[!UICONTROL Adobe Stock]**&#x200B;并单击&#x200B;**[!UICONTROL 下一步]**。
1. 指定&#x200B;**[!UICONTROL 凭据名称]**&#x200B;并验证是否已选择&#x200B;**[!UICONTROL OAuth服务器到服务器]**，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择&#x200B;**[!UICONTROL AEM Assets]** **[!UICONTROL 产品配置文件]**，然后单击&#x200B;**[!UICONTROL 保存配置的API]**。 将显示一条成功消息，确认您在[!DNL Developer Console]中创建了项目。 您的项目仪表板打开，在顶部显示项目名称，**[!UICONTROL API]**&#x200B;下的&#x200B;**[!UICONTROL Adobe Stock]**&#x200B;和&#x200B;**[!UICONTROL 产品配置文件]**&#x200B;下的&#x200B;**[!UICONTROL AEM Assets]**&#x200B;以及&#x200B;**[!UICONTROL 连接的凭据]**&#x200B;下的&#x200B;**[!UICONTROL OAuth服务器到服务器]**&#x200B;凭据卡。

   ![集成aem assets和adobe stock](/help/assets/assets/adc-project-name.png)

1. 选择&#x200B;**[!UICONTROL OAuth服务器到服务器]**&#x200B;凭据卡片，此时将显示&#x200B;**[!UICONTROL 凭据详细信息]**。 使用项目的这些[!DNL OAuth Server-to-Server]凭据详细信息（如&#x200B;**[!UICONTROL 客户端ID]**、**[!UICONTROL 客户端密钥]**、**[!UICONTROL 作用域]**、**[!UICONTROL 凭据名称]**、**[!UICONTROL 技术帐户ID]**、**[!UICONTROL 组织ID]**）在AEM创作实例[中向](#add-configuration-in-the-aem-author-instance)添加配置。

   ![aem assets和adobe stock](/help/assets/assets/oauth-server-server-credentials-details-page.png)

### 在[!DNL AEM]创作实例中添加配置 {#add-configuration-in-the-aem-author-instance}

执行以下步骤以在[!DNL AEM]创作实例中添加配置：

1. [在您的 [!DNL Adobe Stock IMS configuration] 创作实例中设置新的 [!DNL AEM] ](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)
1. [添加云配置以连接到 [!DNL Adobe Stock]](#add-cloud-configuration-to-connect-adobe-stock)

#### 在您的[!DNL Adobe Stock IMS configuration]实例中设置新的[!DNL AEM author] {#set-up-adobe-stock-ims-configuration-in-aem-author-instance}

执行以下步骤，在您的[!DNL Adobe Stock IMS configuration]创作实例中设置新的[!DNL AEM]：

1. 导航到您的[!DNL AEM]创作实例。
1. 单击![aem assets和adobe stock](/help/assets/assets/Hammer.svg)，选择&#x200B;**[!UICONTROL 安全性]**，然后选择&#x200B;**[!UICONTROL Adobe IMS配置]**。
1. 单击&#x200B;**[!UICONTROL 创建]**&#x200B;以创建新的IMS配置。 **[!UICONTROL Adobe IMS技术帐户配置]**&#x200B;页面显示多个字段，如&#x200B;**[!UICONTROL 云解决方案]**、**[!UICONTROL 标题]**、**[!UICONTROL 授权服务器]**、**[!UICONTROL 客户端ID]**、**[!UICONTROL 客户端密钥]**、**[!UICONTROL 作用域]**&#x200B;和&#x200B;**[!UICONTROL 组织ID]**。 按照以下说明在这些字段中指定详细信息：

   * **[!UICONTROL 云解决方案]**：选择&#x200B;**[!UICONTROL Adobe Stock]**。
   * **[!UICONTROL 标题]**：指定此集成的名称。
   * **[!UICONTROL 授权服务器]**：添加[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)作为授权服务器。
   * **[!UICONTROL 客户端ID]**：导航到您的项目仪表板，单击左窗格中可用的&#x200B;**[!UICONTROL OAuth服务器到服务器]**&#x200B;选项，选择&#x200B;**[!UICONTROL 凭据详细信息]**，复制&#x200B;**[!UICONTROL 客户端ID]**&#x200B;并将其粘贴到此处（请参阅[步骤7](#set-up-a-program-in-developer-console)）。
   * **[!UICONTROL 客户端密钥]**：导航到您的项目仪表板，单击左窗格中可用的&#x200B;**[!UICONTROL OAuth服务器到服务器]**&#x200B;选项，选择&#x200B;**[!UICONTROL 凭据详细信息]**，单击&#x200B;**[!UICONTROL 检索客户端密钥]**，复制&#x200B;**[!UICONTROL 客户端密钥]**&#x200B;并将其粘贴到此处（请参阅[步骤7](#set-up-a-program-in-developer-console)）。
   * **[!UICONTROL 作用域]**：导航到您的项目仪表板，单击左窗格中可用的&#x200B;**[!UICONTROL OAuth服务器到服务器]**&#x200B;选项，选择&#x200B;**[!UICONTROL 凭据详细信息]**，复制&#x200B;**[!UICONTROL 作用域]**&#x200B;并将其粘贴到此处（请参阅[步骤7](#set-up-a-program-in-developer-console)）。
   * **[!UICONTROL 组织ID]**：导航到您的项目仪表板，单击左窗格中可用的&#x200B;**[!UICONTROL OAuth服务器到服务器]**&#x200B;选项，选择&#x200B;**[!UICONTROL 凭据详细信息]**，复制&#x200B;**[!UICONTROL 组织ID]**&#x200B;并将其粘贴到此处（请参阅[步骤7](#set-up-a-program-in-developer-console)）。

   ![aem assets和adobe stock](/help/assets/assets/adobe-ims-technical-account-configuration.png)

1. 单击&#x200B;**[!UICONTROL 创建]**，将打开&#x200B;**[!UICONTROL Adobe IMS配置]**&#x200B;页面并显示您创建的[!DNL Adobe Stock]集成。

#### 添加云配置以连接到[!DNL Adobe Stock] {#add-cloud-configuration-to-connect-adobe-stock}

执行以下步骤以添加要连接到[!DNL Adobe Stock]的云配置：

1. 导航到您的[!DNL AEM author]实例。
1. 单击![aem assets和adobe stock](/help/assets/assets/Hammer.svg)，选择&#x200B;**[!UICONTROL 云服务]**，浏览并选择&#x200B;**[!UICONTROL Adobe Stock]**。

   ![将adobe stock与aem](/help/assets/assets/adding-cloud-config-to-adobe-stock.png)一起使用

1. 单击“**[!UICONTROL 创建]**”，“**[!UICONTROL Adobe Stock配置]**”页将显示多个字段。 按照以下说明在这些字段中指定详细信息：

   * **[!UICONTROL 标题]**：导航到&#x200B;**[!UICONTROL Adobe IMS技术帐户配置]**&#x200B;页面（请参阅[步骤3](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)），复制标题并将其粘贴到此处。
   * **[!UICONTROL 关联的Adobe IMS配置]**：选择您创建的[!DNL Adobe Stock]集成。
   * **[!UICONTROL 区域设置]**：选择&#x200B;**[!UICONTROL 英语（美国）]**。

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。

   ![将adobe stock与aem](/help/assets/assets/adobe-stock-config-page.png)一起使用

<!--
### Configure cloud service {#configure-the-cloud-service}

To configure the [!DNL Adobe Stock] cloud service:

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. In the [!DNL Adobe Stock Configurations] page, click **[!UICONTROL Create]**.

1. Specify a **[!UICONTROL Title]** for the cloud configuration. 

   Select the IMS configuration that you have created while [configuring the IMS account](#create-ims-account-configuration).

   Select your locale from the drop-down list.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Click **[!UICONTROL Save & Close]**. 
-->

您的[!DNL Experience Manager Assets]创作实例现已与[!DNL Adobe Stock]集成。 您可以创建多个[!DNL Adobe Stock]配置（例如，基于区域设置的配置）。 您现在可以从[!DNL Adobe Stock]用户界面中访问、搜索和许可[!DNL Experience Manager]资源。

![search-stock-assets](assets/aem-stock-searchstocks.png)

>[!NOTE]
>
>在此集成阶段，只有管理员才能访问[!DNL Adobe Stock]资产、搜索Stock资产（使用Omnisearch）并许可[!DNL Adobe Stock]资产。
>
>管理员可以将用户或组进一步添加到[!DNL Adobe Stock]云服务，并在[!DNL Experience Manager]中授予这些非管理员用户访问Stock配置的权限。

1. 要添加用户或组，请选择[!DNL Adobe Stock]云配置并单击&#x200B;**[!UICONTROL 属性]**。

1. 搜索以添加您为其分配了访问Adobe Stock配置的权限的用户或组。 请参阅[向用户组](#assign-permissions-to-group)分配权限。


## 向用户组分配权限 {#assign-permissions-to-group}

管理员可以创建用户组，并为特定用户或组授予访问[!DNL Adobe Stock]云服务的权限。

以下是用户搜索和许可Adobe Stock资源所需的权限：

* 配置路径： `/conf/global/settings/stock`
* 权限： `jcr:read`
* 权限类型： `Allow`

您可以创建用户组或向现有用户组分配权限。 可从[!DNL Experience Manager Assets]界面或[!DNL User Admin]控制台分配权限。

**为来自[!DNL Experience Manager]的用户组提供访问权限：**

1. 在[!DNL Experience Manager]用户界面中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 组]**。 为[!DNL Adobe Stock]创建用户组。

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 权限]**。

1. 在左侧面板中搜索用户组，并为Adobe Stock添加新的&#x200B;**[!UICONTROL 访问控制条目(ACE)]**。

   * 配置路径： `/conf/global/settings/stock`
   * 权限： `jcr:read`
   * 权限类型： `Allow`

   单击&#x200B;**[!UICONTROL 添加]**。

   ![用户权限](assets/aem-stock-user-permissions.png)

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 云服务]** > **[!UICONTROL Adobe Stock]**。 选择[!DNL Adobe Stock]云配置并单击&#x200B;**[!UICONTROL 属性]**。

1. 将已创建的用户组添加到[!DNL Adobe Stock]配置。 单击&#x200B;**[!UICONTROL 保存并关闭]**。

   ![assign-user](assets/aem-stock-adduser.png)

**为来自[!DNL User Admin Console]的用户提供访问权限：**

1. 打开[!DNL Experience Manager]用户Admin Console。 默认 URL 为 `http://localhost:4502/userdamin`。

1. 在左侧面板中，通过输入`user_id`或`name`搜索用户。 双击以打开用户属性。

1. 导航到&#x200B;**[!UICONTROL 权限]**&#x200B;选项卡，并允许`read`云配置[!DNL Adobe Stock]的`/conf/global/settings/stock`权限。

   >[!CAUTION]
   >
   >如果不允许云配置，则用户只能在&#x200B;**[!UICONTROL 界面中访问]** Assets[!DNL Experience Manager]。
   >
   >要允许访问[!UICONTROL Assets]和[!DNL Adobe Stock]资源，请确保该用户允许云配置。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以更新权限。

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. 将用户或组添加到[!DNL Adobe Stock]云配置。


## 访问Adobe Stock资源 {#access-stock-assets}

具有[!DNL Adobe Stock]云配置权限的非管理员用户可从[!DNL Adobe Stock]界面搜索和许可[!DNL Experience Manager]资产。

用户在访问[!DNL Adobe Stock]资产之前，必须执行激活[!DNL Adobe Stock]云配置的额外步骤。 这是一次性活动。 如果用户被分配了多个[!DNL Adobe Stock]云配置的权限，则用户可以从&#x200B;**[!UICONTROL 用户首选项]**&#x200B;中选择所需的配置。

要激活[!DNL Adobe Stock]云配置，请执行以下操作：

1. 登录到[!DNL Experience Manager]。

1. 单击右上角的用户图标，然后单击&#x200B;**[!UICONTROL 我的首选项]**。 将打开&#x200B;**[!UICONTROL 用户首选项]**&#x200B;窗口。

1. 从下拉列表中选择所需的&#x200B;**[!UICONTROL Stock配置]**，然后单击&#x200B;**[!UICONTROL 接受]**&#x200B;以激活配置。

   ![用户首选项](assets/aem-stock-preferences.png)

1. 导航到&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**。 您现在可以查看、搜索和许可[!DNL Adobe Stock]资产。

下表说明了访问[!DNL Adobe Stock]资源时用户权限的工作方式：

| 用户 | 组 | 权限 | 在用户首选项中接受Stock配置 | 访问Assets | 访问Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| admin | 不适用 | 所有 | 不适用 | 是 | 是 |
| test-doc1 | DAM 用户 | /conf/global/settings/stock/cloud-config | 是 | 是 | 是 |
| test-doc1 | DAM 用户 | /conf/global/settings/stock/cloud-config | 否 | 错误：无法加载数据 | 否 |
| test-doc1 | DAM 用户 | **允许**： /conf/global/settings/stock **拒绝**： /cloud-config | Stock配置不可见 | 是 | 否 |

## 在[!DNL Adobe Stock]中使用和管理[!DNL Experience Manager]资源 {#usemanage}

使用此功能，组织可以允许其用户使用[!DNL Adobe Stock]中的[!DNL Experience Manager Assets]资源工作。 在[!DNL Experience Manager]用户界面中，用户可以搜索[!DNL Adobe Stock]资源并许可所需的资源。

在[!DNL Adobe Stock]中许可[!DNL Experience Manager]资源后，便可以像普通资源一样对其进行使用和管理。 在[!DNL Experience Manager]中，用户可以搜索和预览资产；复制和发布资产；在[!DNL Brand Portal]上共享资产；通过[!DNL Experience Manager]桌面应用程序访问和使用资产；等等。

![从您的[!DNL Adobe Stock]工作区中搜索[!DNL Adobe Experience Manager]资源并筛选结果](assets/adobe-stock-search-results-workspace.png)

**A.**&#x200B;搜索与提供[!DNL Adobe Stock] ID的资产类似的资产。 **B.** 搜索与您选择的形状或方向匹配的资产。**C.**&#x200B;搜索一种或多种受支持的资产类型&#x200B;**D.**&#x200B;打开或折叠筛选器窗格&#x200B;**E.**&#x200B;许可并将所选资产保存在[!DNL Experience Manager] **F.**&#x200B;使用水印[!DNL Experience Manager]G.**在**&#x200B;网站上浏览与所选资产[!DNL Adobe Stock]H.**在**&#x200B;网站[!DNL Adobe Stock]I.**上查看所选资产搜索结果中的所选资产数** I.**j.**&#x200B;在卡片视图和列表视图之间切换

### 查找资源 {#find-assets}

您的[!DNL Experience Manager]用户可以在[!DNL Experience Manager]和[!DNL Adobe Stock]中搜索资源。 当搜索位置不限于[!DNL Adobe Stock]时，将显示来自[!DNL Experience Manager]和[!DNL Adobe Stock]的搜索结果。

* 要搜索[!DNL Adobe Stock]资源，请单击&#x200B;**[!UICONTROL 导航]** > **[!UICONTROL Assets]** > **[!UICONTROL 搜索Adobe Stock]**。

* 要在[!DNL Adobe Stock]和[!DNL Experience Manager Assets]中搜索资产，请单击搜索![搜索](assets/do-not-localize/search_icon.png)。

或者，开始在搜索栏中键入`Location: Adobe Stock`以选择[!DNL Adobe Stock]资源。 [!DNL Experience Manager]对搜索到的资源提供高级筛选功能，允许用户使用筛选器快速聚焦于所需的资源，如支持的资源类型、图像方向和许可状态。

>[!NOTE]
>
>从[!DNL Adobe Stock]搜索的Assets显示在[!DNL Experience Manager]中。 只有在用户[!DNL Adobe Stock]保存资产[!DNL Experience Manager]或[许可证并保存资产](/help/assets/aem-assets-adobe-stock.md#saveassets)之后，才会获取[资产并将其存储在](/help/assets/aem-assets-adobe-stock.md#licenseassets)存储库中。 为便于引用和访问，将显示和高亮显示已存储在[!DNL Experience Manager]中的Assets。 此外，[!DNL Stock]资源与一些其他元数据一起保存，以将源指示为[!DNL Stock]。

![在[!DNL Experience Manager]中搜索筛选器并在搜索结果中突出显示[!DNL Adobe Stock]个资源](assets/aem-search-filters2.jpg)

### 保存并查看所需的资产 {#saveassets}

选择要保存在[!DNL Experience Manager]中的资源。 单击顶部工具栏中的[!UICONTROL 保存]，并提供资源的名称和位置。 未授权的资产将带有水印保存在本地。

下次搜索资源时，保存的资源将带徽章突出显示，以表示此类资源在[!DNL Experience Manager Assets]中可用。

>[!NOTE]
>
>最近添加的资产显示“新”徽章，而不是“已许可”徽章。

### 许可资产 {#licenseassets}

用户可以使用其[!DNL Adobe Stock]企业计划的配额来许可[!DNL Adobe Stock]资源。 当您许可某个资产时，该资产将无水印保存，并且可用于在[!DNL Experience Manager Assets]中搜索和使用。

![用于在[!DNL Adobe Stock]中许可和保存[!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)资源的对话框


### 访问元数据和资源属性 {#access-metadata-and-asset-properties}

用户可以访问和预览元数据，包括保存在[!DNL Adobe Stock]中的资源的[!DNL Experience Manager]元数据属性，并为资源添加&#x200B;**[!UICONTROL 许可证引用]**。 但是，许可证引用的更新未在[!DNL Experience Manager]和[!DNL Adobe Stock]网站之间同步。

用户可以查看已许可和未许可资产的属性。

![查看和访问已保存资产的元数据和许可证引用](assets/metadata_properties.jpg)


## 已知限制 {#known-limitations}

* **限制用户进行许可的功能无法正常工作**：允许所有对Stock配置具有`read`权限的用户搜索和许可[!DNL Adobe Stock]资产。

* **非管理员用户必须手动激活[!DNL Adobe Stock]云配置**：在&#x200B;**[!UICONTROL 用户首选项]**&#x200B;窗口中，**[!UICONTROL Stock配置]**&#x200B;将[!DNL Adobe Stock]云配置显示为已启用，但该配置不适用于非管理员用户。 用户必须单击&#x200B;**[!UICONTROL 接受]**&#x200B;按钮才能激活Stock配置。 如果没有此步骤，则系统在访问&#x200B;**[!UICONTROL Assets]**&#x200B;时反映错误消息。

* **不显示编辑图像警告**：在许可图像时，用户无法检查图像是否仅用于编辑。 为防止可能的滥用，管理员可以从Admin Console关闭对编辑资源的访问权限。

* **显示的许可证类型错误**：资产的[!DNL Experience Manager]中可能显示不正确的许可证类型。 用户可以登录[!DNL Adobe Stock]网站以查看许可证类型。

* **引用字段和元数据未同步**：当用户更新许可证引用字段时，将在[!DNL Experience Manager]中更新许可证引用信息，但不会在[!DNL Adobe Stock]网站上更新。 同样，如果用户更新[!DNL Adobe Stock]网站上的引用字段，则更新不会在[!DNL Experience Manager]中同步。

<!--
## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations users can work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.
-->

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

<!--
### Find assets {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* To search for assets across [!DNL Adobe Stock] and [!DNL Experience Manager Assets], click search ![search](assets/do-not-localize/search_icon.png).

Alternatively, start typing `Location: Adobe Stock` in the search bar to select [!DNL Adobe Stock] assets. [!DNL Experience Manager] offers advanced filtering capabilities on the searched assets, allowing users to quickly zero-in on the required assets using filters, such as types of supported assets, image orientation, and licensed state.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] assets are fetched and stored in [!DNL Experience Manager] repository only after a user either [saves an asset](/help/assets/aem-assets-adobe-stock.md#saveassets) or [licenses and saves an asset](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Search filters in Experience Manager and highlighted Adobe Stock assets in search results](assets/aem-search-filters2.jpg)

*Figure: Search filters in [!DNL Experience Manager] and highlighted [!DNL Adobe Stock] assets in search results.*

### Save and view the required assets {#saveassets}

Select an asset that you want to save in [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. The unlicensed assets are saved locally with a watermark.

Next time when you search for assets, the saved assets are highlighted with a badge, to indicate that such assets are available in [!DNL Experience Manager Assets].

>[!NOTE]
>
>The recently added assets display a New badge instead of Licensed badge.

### License assets {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. When you license an asset, it is saved without a watermark and is available for searching and using in [!DNL Experience Manager Assets].

![Dialog to license and save Adobe Stock assets in Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figure: Dialog to license and save [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets].*

### Access metadata and asset properties {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

Users can see the properties for both, licensed and unlicensed assets.

![View and access metadata and license references of saved assets](assets/metadata_properties.jpg)

*Figure: View and access metadata and license references of saved assets.*

## Known limitations {#known-limitations}

* **Editorial image warning is not displayed**: When licensing an image, users cannot check if an image is Editorial Use Only. To prevent possible misuse, the administrators can turn off the access to editorial assets from the Admin Console.

* **Wrong license type is displayed**: It is possible that an incorrect license type is displayed in [!DNL Experience Manager] for an asset. Users can log into the [!DNL Adobe Stock] website to see the license type.

* **Reference fields and metadata are not synced**: When a user updates a license reference field, the license reference information is updated in [!DNL Experience Manager] but not on the [!DNL Adobe Stock] website. Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].
-->

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [有关将Adobe Stock资源与Experience Manager Assets结合使用的视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Adobe Stock企业计划帮助](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock常见问题解答](https://helpx.adobe.com/stock/faq.html)
