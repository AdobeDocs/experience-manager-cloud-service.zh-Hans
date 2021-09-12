---
title: '使用AEM Assets将Brand Portal配置为a [!DNL Cloud Service] '
description: 使用 Brand Portal 配置 AEM Assets.
contentOwner: Vishabh Gupta
feature: Brand Portal,Asset Distribution,Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '2396'
ht-degree: 8%

---

# 使用AEM Assets将Brand Portal配置为[!DNL Cloud Service] {#configure-aem-assets-with-brand-portal}

通过配置Adobe Experience Manager Assets Brand Portal，您可以将已批准的品牌资产作为[!DNL Cloud Service]实例从Adobe Experience Manager Assets发布到Brand Portal，并分发给Brand Portal用户。

## 使用Cloud Manager激活Brand Portal {#activate-brand-portal}

Cloud Manager用户将AEM Assets的Brand Portal激活为[!DNL Cloud Service]实例。 激活工作流会在后端创建所需的配置(授权令牌、IMS配置和Brand Portal云服务)，并反映Cloud Manager中Brand Portal租户的状态。 激活Brand Portal后，AEM Assets用户可以将资产发布到Brand Portal，并将其分发给Brand Portal用户。

**前提条件**

您需要以下条件才能将AEM Assets上的Brand Portal作为[!DNL Cloud Service]实例激活：

* 作为[!DNL Cloud Service]实例已启动且正在运行的AEM Assets。
* 有权访问Cloud Manager的用户，已分配给Cloud Manager产品的配置文件。 有关更多信息，请参阅[访问Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager)。

>[!NOTE]
>
>作为[!DNL Cloud Service]实例的AEM Assets只能与一个Brand Portal租户连接。 您可以将AEM Assets作为[!DNL Cloud Service]实例具有多个环境（开发、生产和暂存），其中Brand Portal在一个环境中激活。

**激活Brand Portal的步骤**

您可以在为AEM Assets创建[!DNL Cloud Service]实例环境时激活Brand Portal，也可以单独激活。 假设环境已创建，此时您需要激活Brand Portal。

1. 登录到AdobeCloud Manager，然后导航到&#x200B;**[!UICONTROL Environments]**。

   **[!UICONTROL Environments]**&#x200B;页面显示所有现有环境的列表。

1. 从列表中选择环境（逐个）以查看环境详细信息。

   Brand Portal有权访问其中一个可用的环境，并反映在&#x200B;**[!UICONTROL 环境信息]**&#x200B;下。

   找到与Brand Portal关联的环境后，单击&#x200B;**[!UICONTROL 激活Brand Portal]**&#x200B;按钮以开始激活工作流。

   ![激活Brand Portal](assets/create-environment4.png)

1. 激活Brand Portal租户需要几分钟时间，因为激活工作流会在后端创建所需的配置。 激活Brand Portal租户后，状态将变为“已激活”。

   ![查看状态](assets/create-environment5.png)


>[!NOTE]
>
>必须在与[!DNL Cloud Service]实例相同的AEM Assets IMS组织上激活Brand Portal。
>
>如果您为IMS组织(org1-existing)现有Brand Portal云配置([使用Adobe开发人员控制台](#manual-configuration)手动配置)，并且为其他IMS组织(org2-new)配置了AEM Assets作为[!DNL Cloud Service]实例，则从Cloud Manager激活Brand Portal会将Brand Portal IMS组织重置为`org2-new`。 尽管在`org1-existing`上手动配置的云配置将在AEM Assets创作实例中可见，但在从Cloud Manager激活Brand Portal后将不再使用。
>
>如果现有的Brand Portal云配置和作为[!DNL Cloud Service]实例的AEM Assets使用的是相同的IMS组织(org1)，则您只需从Cloud Manager中激活Brand Portal。

**另请参阅**:
* [在AEM Assets中添加用户和角色作为Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)

* [在Cloud Manager中管理环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**登录到您的Brand Portal租户**:

在Cloud Manager中激活您的Brand Portal租户后，您可以从Admin Console或直接使用租户URL登录到Brand Portal。

您的Brand Portal租户的默认URL是：`https://<tenant-id>.brand-portal.adobe.com/`。

其中，租户ID为IMS组织。

如果您不确定Brand Portal URL，请执行以下步骤：

1. 登录到[Admin Console](http://adminconsole.adobe.com/)，然后导航到&#x200B;**[!UICONTROL 产品]**。
1. 从左边栏中，选择&#x200B;**[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**。
1. 单击&#x200B;**[!UICONTROL 转到Brand Portal]**，以在浏览器中直接打开Brand Portal。

   或者，从&#x200B;**[!UICONTROL 转到Brand Portal]**&#x200B;链接中复制Brand Portal租户URL，并将其粘贴到浏览器中以打开Brand Portal界面。

   ![访问Brand Portal](assets/access-bp-on-cloud.png)


**测试连接**

执行以下步骤以验证[!DNL Cloud Service]实例的AEM Assets与Brand Portal租户之间的连接：

1. 登录 AEM Assets。

1. 从&#x200B;**工具**&#x200B;面板中，导航到&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 分发]**。

   ![](assets/test-bpconfig1.png)

   在&#x200B;**[!UICONTROL 发布到Brand Portal]**&#x200B;下创建Brand Portal分发代理(**[!UICONTROL bpdistributionagent0]**)。

   ![](assets/test-bpconfig2.png)


1. 单击&#x200B;**[!UICONTROL 发布到Brand Portal]**&#x200B;以打开分发代理。

   您可以在&#x200B;**[!UICONTROL Status]**&#x200B;选项卡下看到分发队列。

   分发代理包含两个队列：
   * **processing-queue**:分配给Brand Portal。

   * **error-queue**:，用于分发失败的资产。
   >[!NOTE]
   >
   >建议定期查看故障并清除&#x200B;**error-queue**。

   ![](assets/test-bpconfig3.png)

1. 要验证AEM Assets as a [!DNL Cloud Service]与Brand Portal之间的连接，请单击&#x200B;**[!UICONTROL 测试连接]**&#x200B;图标。

   ![](assets/test-bpconfig4.png)

   出现一条消息，显示&#x200B;*测试包已成功交付*。

   >[!NOTE]
   >
   >请避免禁用分发代理，因为这可能导致资产分发（在队列中运行）失败。

要验证[!DNL Cloud Service]实例的AEM Assets与Brand Portal租户之间的连接，请将资产从AEM Assets发布到Brand Portal。 如果连接成功，则发布的资产会显示在Brand Portal界面中。


您现在可以：

* [将资产从 AEM Assets 发布到 Brand Portal](publish-to-brand-portal.md)
* [将文件夹从 AEM Assets 发布到 Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [将收藏集从 AEM Assets 发布到 Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [将资产从Brand Portal发布到AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)  - Brand Portal中的资产源
* [将预设、架构和 Facet 发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [将标记发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

有关更多信息，请参阅[Brand Portal文档](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)。

**分发日志**

您可以监控资产发布工作流的分发代理日志。

现在，让我们将资产从AEM Assets发布到Brand Portal并查看日志。

1. 按照&#x200B;**测试连接**&#x200B;部分中所示的步骤（从1到4）操作，然后导航到分发代理页面。
1. 单击&#x200B;**[!UICONTROL 日志]**&#x200B;以查看处理日志和错误日志。

   ![](assets/test-bpconfig5.png)

分发代理已生成以下日志：

* 信息：它是系统生成的日志，在成功配置分发代理时触发。
* DSTRQ1（请求1）：测试连接时触发。

发布资产时，会生成以下请求和响应日志：

**分发代理请求**：

* DSTRQ2（请求 2）：触发资产发布请求。
* DSTRQ3（请求3）：系统会触发另一个请求，以发布AEM Assets文件夹（资产存在其中），并在Brand Portal中复制该文件夹。

**分发代理响应**：

* queue-bpdistributionagent0(DSTRQ2)：将资产发布到 Brand Portal。
* queue-bpdistributionagent0(DSTRQ3):系统会在Brand Portal中复制AEM Assets文件夹（包含资产）。

在上例中，会触发其他请求和响应。 由于资产是首次发布，系统在Brand Portal中找不到父文件夹（添加路径），因此，它触发了另一个请求，在Brand Portal中创建一个与资产发布位置同名的父文件夹。

>[!NOTE]
>
>如果父文件夹在Brand Portal中不存在或在AEM Assets中已修改，则会生成其他请求。

除了在AEM Assets上以[!DNL Cloud Service]形式激活Brand Portal的自动化工作流之外，还有一种方法可使用Adobe开发人员控制台将AEM Assets手动配置为[!DNL Cloud Service]和Brand Portal，这已不再推荐使用此方法。

>[!NOTE]
>
>如果您在激活Brand Portal租户时遇到任何问题，请联系Adobe支持。

## 使用Adobe开发人员控制台进行手动配置 {#manual-configuration}

以下部分介绍如何使用“Adobe开发人员控制台”，使用Brand Portal手动将AEM Assets配置为[!DNL Cloud Service]。

以前，使用Brand Portal通过Adobe开发人员控制台手动配置了AEM Assets as a [!DNL Cloud Service]，该控制台可获取AdobeIdentity Management服务(IMS)帐户令牌以授权Brand Portal租户。 它需要在AEM Assets和Adobe开发人员控制台中进行配置。

1. 在AEM Assets中，创建IMS帐户并生成公钥（证书）。
1. 在Adobe开发人员控制台中，为Brand Portal租户（组织）创建一个项目。
1. 在项目下，使用公钥配置API以创建服务帐户连接。
1. 获取服务帐户凭据和JSON Web令牌(JWT)有效负载信息。
1. 在AEM Assets中，使用服务帐户凭据和JWT有效负载配置IMS帐户。
1. 在AEM Assets中，使用IMS帐户和Brand Portal端点（组织URL）配置Brand Portal云服务。
1. 通过将资产从AEM Assets发布到Brand Portal来测试您的配置。

>[!NOTE]
>
>作为[!DNL Cloud Service]实例的AEM Assets只能配置一个Brand Portal租户。

**前提条件**

您需要以下各项才能使用 Brand Portal 配置 AEM Assets：

* 作为[!DNL Cloud Service]实例已启动且正在运行的AEM Assets
* Brand Portal租户URL
* 对Brand Portal租户的IMS组织具有系统管理员权限的用户

## 创建配置 {#create-new-configuration}

按照指定的顺序执行以下步骤，以使用Brand Portal配置AEM Assets。

1. [获取公共证书](#public-certificate)
1. [创建服务帐户(JWT)连接](#createnewintegration)
1. [配置IMS帐户](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)

### 创建 IMS 配置 {#create-ims-configuration}

IMS配置将您的AEM Assets作为[!DNL Cloud Service]实例与Brand Portal租户进行身份验证。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [配置IMS帐户](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公钥（证书）在Adobe开发人员控制台上对您的配置文件进行身份验证。

1. 登录 AEM Assets。
1. 从&#x200B;**工具**&#x200B;面板中，导航到&#x200B;**[!UICONTROL 安全]** > **[!UICONTROL AdobeIMS配置]**。
1. 在“AdobeIMS配置”页面中，单击&#x200B;**[!UICONTROL 创建]**。 它将重定向到&#x200B;**[!UICONTROL AdobeIMS技术帐户配置]**&#x200B;页面。 默认情况下，将打开&#x200B;**Certificate**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL 云解决方案]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL AdobeBrand Portal]**。
1. 选中&#x200B;**[!UICONTROL 创建新证书]**&#x200B;复选框，并为公钥指定&#x200B;**别名**。 别名用作公钥的名称。
1. 单击&#x200B;**[!UICONTROL 创建证书]**。然后，单击&#x200B;**[!UICONTROL OK]**&#x200B;以生成公共密钥。

   ![创建证书](assets/ims-config2.png)

1. 单击&#x200B;**[!UICONTROL 下载公钥]**&#x200B;图标，然后将公钥(CRT)文件保存到您的计算机上。

   公共密钥稍后用于在Brand Portal开发人员控制台中为您的Adobe租户配置API并生成服务帐户凭据。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在&#x200B;**帐户**&#x200B;选项卡中，将创建AdobeIMS帐户，该帐户需要在Adobe开发人员控制台中生成的服务帐户凭据。 暂时保持此页面打开。

   在Adobe开发人员控制台](#createnewintegration)中打开新选项卡并[创建服务帐户(JWT)连接，以获取用于配置IMS帐户的凭据和JWT有效负载。

### 创建服务帐户(JWT)连接 {#createnewintegration}

在Adobe开发人员控制台中，项目和API是在Brand Portal租户（组织）级别配置的。 配置API会创建服务帐户(JWT)连接。 可通过以下两种方法配置API：生成密钥对（私钥和公钥），或上传公钥。 要使用Brand Portal配置AEM Assets，您必须在AEM Assets中生成公钥（证书），并通过上传公钥在Adobe开发人员控制台中创建凭据。 在AEM Assets中配置IMS帐户时需要这些凭据。 配置IMS帐户后，您便可以在AEM Assets中配置Brand Portal云服务。

执行以下步骤以生成服务帐户凭据和JWT有效负载：

1. 使用IMS组织(Brand Portal租户)的系统管理员权限登录到Adobe开发人员控制台。 默认URL为[https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)。


   >[!NOTE]
   >
   >确保您从右上角的下拉列表（组织）中选择了正确的IMS组织(Brand Portal租户)。

1. 单击&#x200B;**[!UICONTROL 创建新项目]**。 系统会为您的组织创建一个名为的空白项目。

   单击&#x200B;**[!UICONTROL 编辑项目]**&#x200B;以更新&#x200B;**[!UICONTROL 项目标题]**&#x200B;和&#x200B;**[!UICONTROL 描述]**，然后单击&#x200B;**[!UICONTROL 保存]**。

1. 在&#x200B;**[!UICONTROL 项目概述]**&#x200B;选项卡中，单击&#x200B;**[!UICONTROL 添加API]**。

1. 在&#x200B;**[!UICONTROL 添加API窗口]**&#x200B;中，选择&#x200B;**[!UICONTROL AEM Brand Portal]**&#x200B;并单击&#x200B;**[!UICONTROL 下一步]**。

   确保您有权访问AEM Brand Portal服务。

1. 在&#x200B;**[!UICONTROL 配置API]**&#x200B;窗口中，单击&#x200B;**[!UICONTROL 上传公钥]**。 然后，单击&#x200B;**[!UICONTROL 选择文件]**&#x200B;并上传您在[获取公共证书](#public-certificate)部分中下载的公钥（.crt文件）。

   单击&#x200B;**[!UICONTROL 下一步]**。

   ![上传公共密钥](assets/service-account3.png)

1. 验证公钥，然后单击&#x200B;**[!UICONTROL Next]**。

1. 选择&#x200B;**[!UICONTROL Assets Brand Portal]**&#x200B;作为默认的产品配置文件，然后单击&#x200B;**[!UICONTROL 保存配置的API]**。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![选择产品配置文件](assets/service-account4.png)

1. 配置API后，您将被重定向到API概述页面。 在左侧导航中，在&#x200B;**[!UICONTROL Credentials]**&#x200B;下，单击&#x200B;**[!UICONTROL 服务帐户(JWT)]**&#x200B;选项。

   >[!NOTE]
   >
   >您可以查看凭据并执行诸如生成JWT令牌、复制凭据详细信息、检索客户端密钥等操作。

1. 从&#x200B;**[!UICONTROL Client Credentials]**&#x200B;选项卡中，复制&#x200B;**[!UICONTROL 客户端ID]**。

   单击&#x200B;**[!UICONTROL 检索客户端密钥]**&#x200B;并复制&#x200B;**[!UICONTROL 客户端密钥]**。

   ![服务帐户凭据](assets/service-account5.png)

1. 导航到&#x200B;**[!UICONTROL 生成JWT]**&#x200B;选项卡，并复制&#x200B;**[!UICONTROL JWT有效负荷]**&#x200B;信息。

现在，您可以使用客户端ID（API密钥）、客户端密钥和JWT有效负载在AEM Assets中[配置IMS帐户](#create-ims-account-configuration)。

<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
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

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.

-->

### 配置IMS帐户 {#create-ims-account-configuration}

确保您已执行以下步骤：

* [获取公共证书](#public-certificate)
* [创建服务帐户(JWT)连接](#createnewintegration)

执行以下步骤以配置IMS帐户。

1. 打开IMS配置，然后导航到&#x200B;**[!UICONTROL 帐户]**&#x200B;选项卡。 在[获取公共证书](#public-certificate)时，保持打开该页面。

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在&#x200B;**[!UICONTROL 授权服务器]**&#x200B;字段中，指定URL:[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   在[创建服务帐户(JWT)连接](#createnewintegration)时，在&#x200B;**[!UICONTROL API密钥]**&#x200B;字段、**[!UICONTROL 客户端密钥]**&#x200B;和&#x200B;**[!UICONTROL 负载]**（JWT有效负载）中指定您复制的客户端ID。

   单击&#x200B;**[!UICONTROL 创建]**。

   已配置IMS帐户。

   ![IMS 帐户配置](assets/create-new-integration6.png)


1. 选择IMS帐户配置，然后单击&#x200B;**[!UICONTROL 检查运行状况]**。

   单击对话框中的&#x200B;**[!UICONTROL Check]**。 成功配置后，将显示一条消息，显示&#x200B;*令牌已成功检索*。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一个IMS配置。
>
>确保IMS配置通过运行状况检查。 如果配置未通过运行状况检查，则无效。 您必须删除它，然后创建一个有效的新配置。

### 配置云服务 {#configure-the-cloud-service}

执行以下步骤以配置Brand Portal云服务：

1. 登录 AEM Assets。

1. 从&#x200B;**工具**&#x200B;面板中，导航到&#x200B;**[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**。

1. 在Brand Portal配置页面中，单击&#x200B;**[!UICONTROL 创建]**。

1. 指定配置的&#x200B;**[!UICONTROL 标题]**。

   选择在[配置IMS帐户](#create-ims-account-configuration)时创建的IMS配置。

   在&#x200B;**[!UICONTROL 服务URL]**&#x200B;字段中，指定您的Brand Portal租户（组织）URL。

   ![](assets/create-cloud-service.png)

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。将创建云配置。

   现在，您的AEM Assets作为[!DNL Cloud Service]实例已配置为Brand Portal租户。

您现在可以通过检查分发代理并将资产发布到Brand Portal来测试配置。

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Log in to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click on the **[!UICONTROL Test Connection]** icon.

   ![](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![](assets/test-bpconfig5.png)

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
