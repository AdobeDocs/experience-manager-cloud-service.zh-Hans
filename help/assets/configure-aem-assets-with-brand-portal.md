---
title: '使用Brand Portal配置AEM Assets as a [!DNL Cloud Service] '
description: 了解如何使用Brand Portal配置AEM Assets。 利用配置，可将已批准的品牌资产从AEM实例发布到Brand Portal，并将其分发给Brand Portal用户。
contentOwner: AK
feature: Brand Portal, Asset Distribution, Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 9%

---

# 使用 Brand Portal 配置 Experience Manager Assets {#configure-aem-assets-with-brand-portal}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

通过配置Adobe Experience Manager Assets Brand Portal，您可以将批准的品牌资产作为[!DNL Cloud Service]实例从Adobe Experience Manager Assets发布到Brand Portal，并将其分发给Brand Portal用户。

## 使用Cloud Manager激活Brand Portal {#activate-brand-portal}

Cloud Manager用户为Experience Manager Assets as a [!DNL Cloud Service]实例激活Brand Portal。 激活工作流在后端创建所需的配置(授权令牌、IMS配置和Brand Portal云服务)，并反映Cloud Manager中Brand Portal租户的状态。 激活Brand Portal可让Experience Manager Assets用户将资源发布到Brand Portal，并将它们分发给Brand Portal用户。

**前提条件**

您需要以下各项才能在Experience Manager Assets上将Brand Portal激活为[!DNL Cloud Service]实例：

* 启动并运行的Experience Manager Assets作为[!DNL Cloud Service]实例。
* 有权访问Cloud Manager的用户，已分配给Cloud Manager产品的配置文件。 有关详细信息，请参阅[访问Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=zh-Hans#accessing-cloud-manager)。

>[!NOTE]
>
>Experience Manager Assets as a [!DNL Cloud Service]实例需要配置的生产环境才能连接到Brand Portal租户。

**激活Brand Portal的步骤**

您可以在将Brand Portal作为[!DNL Cloud Service]实例创建生产环境时激活Experience Manager Assets，也可以单独激活。 假设环境已创建，此时您需要激活Brand Portal。

1. 登录到Adobe Cloud Manager并导航到&#x200B;**[!UICONTROL 环境]**。

   **[!UICONTROL 环境]**&#x200B;页面显示所有现有环境的列表。

1. 从列表中选择环境（逐个）以查看环境详细信息。

   Brand Portal有权使用其中一个可用环境，并反映在&#x200B;**[!UICONTROL 环境信息]**&#x200B;下。

   找到与Brand Portal关联的环境后，单击&#x200B;**[!UICONTROL 激活Brand Portal]**&#x200B;按钮以开始激活工作流。

   ![激活Brand Portal](assets/create-environment4.png)

1. 激活Brand Portal租户需要几分钟时间，因为激活工作流会在后端创建所需的配置。 激活Brand Portal租户后，状态将更改为“已激活”。

   ![查看状态](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal必须作为[!DNL Cloud Service]实例在与Experience Manager Assets相同的IMS组织上激活。
>
>如果您为IMS组织(org1-existing)配置了现有Brand Portal云配置([使用Adobe Developer Console手动配置](#manual-configuration))，并且为另一个IMS组织(org2-new)配置了Experience Manager Assets as a [!DNL Cloud Service]实例，则从Cloud Manager激活Brand Portal会将Brand Portal IMS组织重置为`org2-new`。 尽管`org1-existing`上手动配置的云配置在Experience Manager Assets创作实例中可见，但在从Cloud Manager激活Brand Portal后将不再使用。
>
>如果现有Brand Portal云配置和Experience Manager Assets as a [!DNL Cloud Service]实例使用相同的IMS组织(org1)，则您只需从Cloud Manager激活Brand Portal即可。
>
>请勿修改任何自动生成的设置。

**另请参阅**：

* [在Experience Manager Assets as a Cloud Service中添加用户和角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=zh-Hans)

* [在Cloud Manager中管理环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=zh-Hans#adding-environments)


**登录到您的Brand Portal租户**：

在Cloud Manager中激活Brand Portal租户后，您可以从Admin Console或直接使用租户URL登录到Brand Portal。

您的Brand Portal租户的默认URL为： `https://<tenant-id>.brand-portal.adobe.com/`。

其中，租户ID是IMS组织。


如果您不确定Brand Portal URL，请执行以下步骤：

1. 登录到[Admin Console](https://adminconsole.adobe.com/)并导航到&#x200B;**[!UICONTROL 产品]**。
1. 从左侧面板中，选择&#x200B;**[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**。
1. 单击&#x200B;**[!UICONTROL 转到Brand Portal]**&#x200B;以在浏览器中直接打开Brand Portal。

   或者从&#x200B;**[!UICONTROL 转到Brand Portal]**&#x200B;链接复制Brand Portal租户URL并将其粘贴到您的浏览器中以打开Brand Portal界面。

   ![访问Brand Portal](assets/access-bp-on-cloud.png)


**测试连接**

执行以下步骤来验证Experience Manager Assets as a [!DNL Cloud Service]实例与Brand Portal租户之间的连接：

1. 登录Experience Manager Assets。

1. 从&#x200B;**工具**&#x200B;面板，导航到&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 分发]**。

   ![导航到分发选项](assets/test-bpconfig1.png)

   已在&#x200B;**[!UICONTROL 发布到Brand Portal]**&#x200B;下创建Brand Portal分发代理(**[!UICONTROL bpdistributionagent0]**)。

   ![创建分发代理](assets/test-bpconfig2.png)

1. 单击&#x200B;**[!UICONTROL 发布到Brand Portal]**&#x200B;以打开分发代理。

   您可以在&#x200B;**[!UICONTROL 状态]**&#x200B;选项卡下看到分发队列。

   分发代理包含两个队列：
   * **processing-queue**：用于将资源分发到Brand Portal。

   * **error-queue**：对于分发失败的资产。

   >[!NOTE]
   >
   >建议定期查看故障并清除&#x200B;**错误队列**。

   ![正在处理资产分发的队列](assets/test-bpconfig3.png)

1. 要验证Experience Manager Assets as a [!DNL Cloud Service]与Brand Portal之间的连接，请单击&#x200B;**[!UICONTROL 测试连接]**&#x200B;图标。

   ![验证AEM与Brand Portal之间的连接](assets/test-bpconfig4.png)

   出现一条消息，表明您的&#x200B;*测试包已成功交付*。

   >[!NOTE]
   >
   >请避免禁用分发代理，因为这可能导致资产分发（在队列中运行）失败。

要验证Experience Manager Assets as a [!DNL Cloud Service]实例与Brand Portal租户之间的连接，请将资源从Experience Manager Assets发布到Brand Portal。 如果连接成功，则发布的资源将在Brand Portal界面中可见。


您现在可以：

* [将资源从Experience Manager Assets发布到Brand Portal](publish-to-brand-portal.md)
* [将文件夹从Experience Manager Assets发布到Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [将收藏集从Experience Manager Assets发布到Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [将资源从Brand Portal发布到Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=zh-hans) - Brand Portal中的资源源
* [将预设、架构和 Facet 发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=zh-Hans)
* [将标记发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=zh-Hans)

有关详细信息，请参阅[Brand Portal文档](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=zh-Hans)。

**分发日志**

您可以监视资产发布工作流的分发代理日志。

现在，让我们将资源从Experience Manager Assets发布到Brand Portal并查看日志。

1. 按照&#x200B;**测试连接**&#x200B;部分中所示的步骤（从1到4）操作，然后导航到分发代理页面。
1. 单击&#x200B;**[!UICONTROL 日志]**&#x200B;以查看处理和错误日志。

   ![正在处理和错误日志](assets/test-bpconfig5.png)

分发代理已生成以下日志：

* 信息：这是系统生成的日志，在成功配置分发代理时触发。
* DSTRQ1（请求1）：测试连接时触发。

发布资产时，会生成以下请求和响应日志：

**分发代理请求**：

* DSTRQ2（请求 2）：触发资产发布请求。
* DSTRQ3（请求3）：系统会触发另一个请求，以发布Experience Manager Assets文件夹（资产位于该文件夹中），并复制Brand Portal中的文件夹。

**分发代理响应**：

* queue-bpdistributionagent0(DSTRQ2)：将资产发布到 Brand Portal。
* queue-bpdistributionagent0 (DSTRQ3)：系统会复制Brand Portal中的Experience Manager Assets文件夹（包含资产）。

在上述示例中，还会触发其他请求和响应。 由于资产是首次发布，系统在Brand Portal中找不到父文件夹（添加路径），因此，触发了一个额外的请求，即在Brand Portal中创建要将资产发布到的同名父文件夹。

>[!NOTE]
>
>如果父文件夹在Brand Portal中不存在或在Experience Manager Assets中被修改，则会生成其他请求。

除了在Experience Manager Assets as a [!DNL Cloud Service]上激活Brand Portal的自动化工作流之外，还有另一种方法可使用Adobe Developer Console在Brand Portal中手动配置Experience Manager Assets as a [!DNL Cloud Service]，现在不再建议这样做。

>[!NOTE]
>
>如果您在激活Brand Portal租户时遇到任何问题，请联系客户支持。

## 使用Adobe Developer Console手动配置 {#manual-configuration}

>[!NOTE]
>
> 从2024年6月起，您无法创建新的JWT凭据。 今后，仅创建OAuth凭据。
> 请参阅更多[创建OAuth配置](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration:~:text=For%20example%3A-,Creating%20an%20OAuth%20configuration,-To%20create%20a)。

以下部分介绍了如何使用Adobe Developer Console在Brand Portal中手动配置Experience Manager Assets as a [!DNL Cloud Service]。

以前，Experience Manager Assets as a [!DNL Cloud Service]是通过Adobe Developer Console使用Brand Portal手动配置的，这样可获取Adobe Identity Management Services (IMS)帐户令牌以授权Brand Portal租户。 它需要在Experience Manager Assets和Adobe Developer Console中进行配置。

<!--1. In Experience Manager Assets, create an IMS account and generate a public key (certificate).-->
<!--1. Under the project, configure an API using the public key to create a service account connection.
1. Get the service account credentials and JSON Web Token (JWT) payload information.
1. In Experience Manager Assets, configure the IMS account using the service account credentials and JWT payload.-->
1. 在Adobe Developer Console中，为您的Brand Portal租户（组织）创建一个项目。
1. 在Experience Manager Assets中，使用IMS帐户和Brand Portal端点（组织URL）配置Brand Portal云服务。
1. 通过将资源从Experience Manager Assets发布到Brand Portal来测试配置。

>[!NOTE]
>
>Experience Manager Assets as a [!DNL Cloud Service]实例只能配置一个Brand Portal租户。

**前提条件**

您需要以下各项才能使用Brand Portal配置Experience Manager Assets：

* 启动并运行的Experience Manager Assets作为[!DNL Cloud Service]实例
* Brand Portal租户URL
* 对Brand Portal租户的IMS组织具有系统管理员权限的用户

## 创建配置 {#create-new-configuration}

按照指定的顺序执行以下步骤，使用Brand Portal配置Experience Manager Assets。

1. [在Adobe Developer Console中配置OAuth凭据](#config-oauth)
1. [使用OAuth创建新的Adobe IMS集成](#create-ims-account-configuration)
1. [配置云服务](#configure-cloud-service)
   <!--1. [Obtain public certificate](#public-certificate)-->
<!--1. [Create service account (JWT) connection](#createnewintegration) 
1. [Configure IMS account](#create-ims-account-configuration)-->

<!--
### Create IMS configuration {#create-ims-configuration}

The IMS configuration authenticates your Experience Manager Assets as a [!DNL Cloud Service] instance with the Brand Portal tenant. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)
-->
<!--

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your profile on Adobe Developer Console.

1. Login to Experience Manager Assets.
1. From the **Tools** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.
1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. It will redirect to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. By default, the **Certificate** tab opens.
1. Select **[!UICONTROL Adobe Brand Portal]** in the **[!UICONTROL Cloud Solution]** drop-down list.  
1. Select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 
1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

   ![Create Certificate](assets/ims-config2.png)

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (CRT) file on your machine.

   The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.  

   ![Download Certificate](assets/ims-config3.png)

1. Click **[!UICONTROL Next]**.

    In the **Account** tab, Adobe IMS account is created which requires the service account credentials that are generated in Adobe Developer Console. Keep this page open for now.

    Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration) to get the credentials and JWT payload for configuring the IMS account. 
-->
<!--

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at Brand Portal tenant (organization) level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. To configure Experience Manager Assets with Brand Portal, you must generate a public key (certificate) in Experience Manager Assets and create credentials in Adobe Developer Console by uploading the public key. These credentials are required to configure the IMS account in Experience Manager Assets. Once the IMS account is configured, you can configure the Brand Portal cloud service in Experience Manager Assets.

Perform the following steps to generate the service account credentials and JWT payload:

1. Login to Adobe Developer Console with system administrator privileges on the IMS organization (Brand Portal tenant). The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Ensure that you have selected the correct IMS organization (Brand Portal tenant) from the drop-down (organization) list located at the upper-right corner.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]** to update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**. 

   Ensure that you have access to the Experience Manager Brand Portal service.

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Then, click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. 

   Click **[!UICONTROL Next]**.

   ![Upload Public Key](assets/service-account3.png)

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Assets Brand Portal]** as the default product profile and click **[!UICONTROL Save configured API]**. 

   ![Select Product Profile](assets/service-account4.png)

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option.

   >[!NOTE] 
   >
   >* You can view the credentials and perform actions such as generate JWT tokens, copy credential details, retrieve client secret, and so on.
   >* Currently, only the Adobe's Developer Console Service Account (JWT) credential type is supported. Do not use the `OAuth Server-to-Server` credential type until it is supported in mid-April. Read more at [JWT Credentials Deprecation in Adobe Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=zh-Hans).

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Service Account Credentials](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in Experience Manager Assets.
-->
<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create an integration page. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information is used to create IMS account configuration.

-->

### 在Adobe Developer Console中配置OAuth凭据 {#config-oauth}

[在Adobe Developer Console中配置OAuth凭据](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#credentials-in-the-developer-console)，然后选择Brand Portal API。

### 使用OAuth创建新的Adobe IMS集成 {#create-ims-account-configuration}

[使用OAuth创建新的Adobe IMS集成](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration)，然后从云解决方案下的下拉列表中选择Brand Portal 。

<!--
Ensure that you have performed the following steps:

* [Obtain public certificate](#public-certificate)
* [Create service account (JWT) connection](#createnewintegration)
-->

<!--1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. Keep the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)  
-->
<!--
1. Complete the configuration based on details from the [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). Click **[!UICONTROL Create]**.
-->
<!--Specify client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

   The IMS account is configured. 

   ![IMS Account configuration](assets/create-new-integration6.png)

 <!--  
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![Adobe IMS Configurations Check Health.](assets/create-new-integration5.png)
-->
<!--
>[!CAUTION]
>
>You must have only one IMS configuration.
>
>Ensure that the IMS configuration passes the health check. If the configuration does not pass the health check, it is invalid. You must delete it and create another valid configuration.
-->

### 配置云服务 {#configure-cloud-service}

执行以下步骤以配置Brand Portal云服务：

1. 登录Experience Manager Assets。

1. 从&#x200B;**工具**&#x200B;面板，导航到&#x200B;**[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**。

1. 在“Brand Portal配置”页面中，单击&#x200B;**[!UICONTROL 创建]**。

1. 指定配置的&#x200B;**[!UICONTROL 标题]**。

   选择您在[配置IMS帐户](#create-ims-account-configuration)时创建的IMS配置。

   在&#x200B;**[!UICONTROL 服务URL]**&#x200B;字段中，指定您的Brand Portal租户（组织）URL。

   ![Brand Portal配置对话框。](assets/create-cloud-service.png)

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。 将创建云配置。

   您的Experience Manager Assets as a [!DNL Cloud Service]实例现在已配置有Brand Portal租户。

您现在可以通过检查分发代理并将资产发布到Brand Portal来测试配置。

如果启用了安全预览，则&#x200B;**在SPS中允许列表出口IP**
如果将Dynamic Media-Scene7与为公司启用的[安全预览](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=zh-Hans)结合使用，则建议Scene7公司管理员使用SPS (Scene7 Publishing System) Flash UI [为各个区域允许列表公共出口IP](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=zh-Hans#testing-the-secure-testing-service)。
出口IP如下所示：

| **地区** | **出口IP** |
|--- |--- |
| NA | 130.248.160.68、20.94.203.130 |
| EMEA | 51.132.146.75，130.248.244.202，130.248.244.203，130.248.244.204，130.248.244.210，130.248.244.211，130.248.244.212 |
| 亚太地区 | 63.140.44.54 |

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Login to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![test-bpconfig1](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![test-bpconfig2](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![test-bpconfig3](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![test-bpconfig4](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=zh-Hans) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=zh-Hans)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=zh-Hans)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=zh-Hans) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![ctest-bpconfig4](assets/ctest-bpconfig4.png)

The distribution agent has generated the following logs:

* INFO: This is a system-generated log that triggers on successful configuration of the distribution agent. 
* DSTRQ1 (Request 1): Triggers on test connection.

On publishing the asset, the following request and response logs are generated:

**Distribution agent request**:

* DSTRQ2 (Request 2): The asset publishing request is triggered.
* DSTRQ3 (Request 3): The system triggers another request to publish the AEM Assets folder (in which the asset exists) and replicates the folder in Brand Portal.

**Distribution agent response**:

* queue-bpdistributionagent0 (DSTRQ2): The asset is published to Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): The system replicates the AEM Assets folder (containing the asset) in Brand Portal.

In the above example, an additional request and response is triggered. The system could not find the parent folder (Add Path) in Brand Portal because the asset was published for the first time, therefore, it triggered an additional request to create a parent folder with the same name in Brand Portal where the asset is published.  

>[!NOTE]
>
>Additional request is generated in case the parent folder does not exist in Brand Portal or has been modified in AEM Assets. 
-->

<!--

## Additional information {#additional-information}

Go to `/system/console/slingmetrics` for statistics related to the distributed content:

1. **Counter metrics**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Time metrics**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`

-->

<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
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
