---
title: 将AEM Assets配置为 [!DNL Cloud Service] 与Brand Portal
description: 使用 Brand Portal 配置 AEM Assets.
contentOwner: Vishabh Gupta
feature: Brand Portal,Asset Distribution,Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: f1c95dd27857085a0a95a896efd2f66af346b75a
workflow-type: tm+mt
source-wordcount: '2449'
ht-degree: 7%

---

# 使用 Brand Portal 配置 Experience Manager Assets {#configure-aem-assets-with-brand-portal}

通过配置Adobe Experience Manager Assets Brand Portal，您可以从Adobe Experience Manager Assets作为 [!DNL Cloud Service] 实例发布到Brand Portal，并分发给Brand Portal用户。

## 使用Cloud Manager激活Brand Portal {#activate-brand-portal}

Cloud Manager用户将Brand Portal激活为Experience Manager Assets as a [!DNL Cloud Service] 实例。 激活工作流会在后端创建所需的配置(授权令牌、IMS配置和Brand Portal云服务)，并反映Cloud Manager中Brand Portal租户的状态。 激活Brand Portal后，Experience Manager Assets用户可以将资产发布到Brand Portal，并将其分发给Brand Portal用户。

**前提条件**

您需要满足以下条件才能在Experience Manager Assets as a [!DNL Cloud Service] 实例：

* Mananger Assets as a [!DNL Cloud Service] 实例。
* 有权访问Cloud Manager的用户，已分配给Cloud Manager产品的配置文件。 请参阅 [访问Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager) 以了解更多信息。

>[!NOTE]
>
>体验管理资产作为 [!DNL Cloud Service] 实例只能与一个Brand Portal租户连接。 您可以为Experience Manager Assets(作为 [!DNL Cloud Service] 例如，其中Brand Portal在一个环境中激活。

**激活Brand Portal的步骤**

在为Experience Manager Assets as a [!DNL Cloud Service] 实例，或单独进行。 假设环境已创建，此时您需要激活Brand Portal。

1. 登录到AdobeCloud Manager，然后导航到 **[!UICONTROL 环境]**.

   的 **[!UICONTROL 环境]** 页面会显示所有现有环境的列表。

1. 从列表中选择环境（逐个）以查看环境详细信息。

   Brand Portal有权使用其中一个可用环境，并反映在 **[!UICONTROL 环境信息]**.

   找到与Brand Portal关联的环境后，单击 **[!UICONTROL 激活Brand Portal]** 按钮来启动激活工作流。

   ![激活Brand Portal](assets/create-environment4.png)

1. 激活Brand Portal租户需要几分钟时间，因为激活工作流会在后端创建所需的配置。 激活Brand Portal租户后，状态将变为“已激活”。

   ![查看状态](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal必须在与Experience Mananger Assets(作为 [!DNL Cloud Service] 实例。
>
>如果您现有的Brand Portal云配置([使用Adobe开发人员控制台手动配置](#manual-configuration))，并将您的Experience Mananger Assets作为 [!DNL Cloud Service] 已为其他IMS组织(org2-new)配置实例，从Cloud Manager激活Brand Portal会将Brand Portal IMS组织重置为 `org2-new`. 尽管在 `org1-existing` 将在Experience Manager Assets创作实例中可见，但从Cloud Manager激活Brand Portal后，将不再使用。
>
>如果现有的Brand Portal云配置和Experience Manager Assets as a [!DNL Cloud Service] 实例使用的是相同的IMS组织(org1)，您只需从Cloud Manager中激活Brand Portal即可。
>
>请勿修改任何自动生成的设置。

**另请参阅**:

* [在Experience Manager Assets中添加用户和角色as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)

* [在Cloud Manager中管理环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**登录到您的Brand Portal租户**:

在Cloud Manager中激活您的Brand Portal租户后，您可以从Admin Console或直接使用租户URL登录到Brand Portal。

您的Brand Portal租户的默认URL是： `https://<tenant-id>.brand-portal.adobe.com/`.

其中，租户ID为IMS组织。

如果您不确定Brand Portal URL，请执行以下步骤：

1. 登录到 [Admin Console](https://adminconsole.adobe.com/) 并导航到 **[!UICONTROL 产品]**.
1. 从左边栏中，选择 **[!UICONTROL Adobe Experience Manager Brand Portal -Brand Portal]**.
1. 单击 **[!UICONTROL 转到Brand Portal]** 可直接在浏览器中打开Brand Portal。

   或者，从 **[!UICONTROL 转到Brand Portal]** 链接并粘贴到浏览器中以打开Brand Portal界面。

   ![访问Brand Portal](assets/access-bp-on-cloud.png)


**测试连接**

执行以下步骤以验证Experience Manager Assets as a [!DNL Cloud Service] 实例和Brand Portal租户：

1. 登录到Experience Mananger Assets。

1. 从 **工具** 面板，导航到 **[!UICONTROL 部署]** > **[!UICONTROL 分发]**.

   ![](assets/test-bpconfig1.png)

   Brand Portal分发代理(**[!UICONTROL bpdistributionagent0]**)创建于 **[!UICONTROL 发布到Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. 单击 **[!UICONTROL 发布到Brand Portal]** 打开分发代理。

   您可以在 **[!UICONTROL 状态]** 选项卡。

   分发代理包含两个队列：
   * **处理队列**:分配给Brand Portal。

   * **error-queue**:，用于分发失败的资产。
   >[!NOTE]
   >
   >建议查看失败情况并清除 **error-queue** 定期。

   ![](assets/test-bpconfig3.png)

1. 验证Experience Mananger Assets作为 [!DNL Cloud Service] 和Brand Portal，单击 **[!UICONTROL 测试连接]** 图标。

   ![](assets/test-bpconfig4.png)

   此时会显示一条消息，显示您的 *测试包已成功交付*.

   >[!NOTE]
   >
   >请避免禁用分发代理，因为这可能导致资产分发（在队列中运行）失败。

验证Experience Mananger Assets作为 [!DNL Cloud Service] 实例和Brand Portal租户，将资产从Experience Manager Assets发布到Brand Portal。 如果连接成功，则发布的资产会显示在Brand Portal界面中。


您现在可以：

* [将资产从Experience Mananger Assets发布到Brand Portal](publish-to-brand-portal.md)
* [将文件夹从Experience Manager Assets发布到Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [将收藏集从Experience Manager Assets发布到Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [将资产从Brand Portal发布到Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) -Brand Portal中的资产源
* [将预设、架构和 Facet 发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [将标记发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

请参阅 [Brand Portal文档](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 以了解更多信息。

**分发日志**

您可以监控资产发布工作流的分发代理日志。

现在，让我们将资产从Experience Mananger Assets发布到Brand Portal并查看日志。

1. 按照 **测试连接** 部分，然后导航到分发代理页面。
1. 单击 **[!UICONTROL 日志]** 查看处理日志和错误日志。

   ![](assets/test-bpconfig5.png)

分发代理已生成以下日志：

* 信息：它是系统生成的日志，在成功配置分发代理时触发。
* DSTRQ1（请求1）：测试连接时触发。

发布资产时，会生成以下请求和响应日志：

**分发代理请求**：

* DSTRQ2（请求 2）：触发资产发布请求。
* DSTRQ3（请求3）：系统会触发另一个请求，以发布Experience Manager Assets文件夹（资产存在于该文件夹中），并在Brand Portal中复制该文件夹。

**分发代理响应**：

* queue-bpdistributionagent0(DSTRQ2)：将资产发布到 Brand Portal。
* queue-bpdistributionagent0(DSTRQ3):系统会在Brand Portal中复制Experience Manager Assets文件夹（包含资产）。

在上例中，会触发其他请求和响应。 由于资产是首次发布，系统在Brand Portal中找不到父文件夹（添加路径），因此，它触发了另一个请求，在Brand Portal中创建一个与资产发布位置同名的父文件夹。

>[!NOTE]
>
>如果父文件夹在Brand Portal中不存在或已在Experience Manager Assets中修改，则会生成其他请求。

与在Experience Mananger Assets as a [!DNL Cloud Service]，则还有一种方法可手动配置Experience Manager Assets作为 [!DNL Cloud Service] 使用Brand Portal开发人员控制台（不再推荐）。

>[!NOTE]
>
>如果您在激活Brand Portal租户时遇到任何问题，请联系客户支持。

## 使用Adobe开发人员控制台进行手动配置 {#manual-configuration}

以下部分介绍如何手动配置Experience Manager Assets作为 [!DNL Cloud Service] 使用Brand Portal开发人员控制台。

以前， Experience Mananger Assets as a [!DNL Cloud Service] 已通过Brand Portal开发人员控制台手动配置Adobe，该控制台可获取AdobeIdentity Management服务(IMS)帐户令牌以授权Brand Portal租户。 它需要在Experience Manager Assets和Adobe开发人员控制台中进行配置。

1. 在Experience Manager Assets中，创建IMS帐户并生成公钥（证书）。
1. 在Adobe开发人员控制台中，为Brand Portal租户（组织）创建一个项目。
1. 在项目下，使用公钥配置API以创建服务帐户连接。
1. 获取服务帐户凭据和JSON Web令牌(JWT)有效负载信息。
1. 在Experience Manager Assets中，使用服务帐户凭据和JWT有效负载配置IMS帐户。
1. 在Experience Manager Assets中，使用IMS帐户和Brand Portal端点（组织URL）配置Brand Portal云服务。
1. 通过将资产从Experience Manager Assets发布到Brand Portal来测试您的配置。

>[!NOTE]
>
>体验管理资产作为 [!DNL Cloud Service] 实例只应配置一个Brand Portal租户。

**前提条件**

要使用Brand Portal配置Experience Mananger Assets，您需要满足以下条件：

* Mananger Assets as a [!DNL Cloud Service] 实例
* Brand Portal租户URL
* 对Brand Portal租户的IMS组织具有系统管理员权限的用户

## 创建配置 {#create-new-configuration}

按照指定的顺序，执行以下步骤以使用Brand Portal配置Experience Manager Assets。

1. [获取公共证书](#public-certificate)
1. [创建服务帐户(JWT)连接](#createnewintegration)
1. [配置IMS帐户](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)

### 创建 IMS 配置 {#create-ims-configuration}

IMS配置将您的Experience Mananger资产验证为 [!DNL Cloud Service] 实例。Brand Portal租户。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [配置IMS帐户](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公钥（证书）在Adobe开发人员控制台上对您的配置文件进行身份验证。

1. 登录到Experience Mananger Assets。
1. 从 **工具** 面板，导航到 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS配置]**.
1. 在Adobe IMS配置页面中，单击 **[!UICONTROL 创建]**. 它将重定向到 **[!UICONTROL Adobe IMS技术帐户配置]** 页面。 默认情况下， **证书** 选项卡。
1. 选择 **[!UICONTROL AdobeBrand Portal]** 在 **[!UICONTROL 云解决方案]** 下拉列表。
1. 选择 **[!UICONTROL 创建新证书]** 复选框并指定 **别名** 公钥。 别名用作公钥的名称。
1. 单击&#x200B;**[!UICONTROL 创建证书]**。然后，单击 **[!UICONTROL 确定]** 以生成公钥。

   ![创建证书](assets/ims-config2.png)

1. 单击 **[!UICONTROL 下载公钥]** 图标，并将公钥(CRT)文件保存到您的计算机上。

   公共密钥稍后用于在Brand Portal开发人员控制台中为您的Adobe租户配置API并生成服务帐户凭据。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在 **帐户** 选项卡，Adobe IMS帐户创建时需要在Adobe开发人员控制台中生成的服务帐户凭据。 暂时保持此页面打开。

   打开新选项卡并 [在Adobe开发人员控制台中创建服务帐户(JWT)连接](#createnewintegration) 以获取用于配置IMS帐户的凭据和JWT有效负荷。

### 创建服务帐户(JWT)连接 {#createnewintegration}

在Adobe开发人员控制台中，项目和API是在Brand Portal租户（组织）级别配置的。 配置API会创建服务帐户(JWT)连接。 可通过以下两种方法配置API：生成密钥对（私钥和公钥），或上传公钥。 要使用Brand Portal配置Experience Manager Assets，您必须在Experience Manager Assets中生成公钥（证书），并通过上传公共密钥在Adobe开发人员控制台中创建凭据。 在Experience Manager Assets中配置IMS帐户时需要这些凭据。 配置IMS帐户后，您便可以在Experience Manager Assets中配置Brand Portal云服务。

执行以下步骤以生成服务帐户凭据和JWT有效负载：

1. 使用IMS组织(Brand Portal租户)的系统管理员权限登录到Adobe开发人员控制台。 默认URL为 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >确保您从右上角的下拉列表（组织）中选择了正确的IMS组织(Brand Portal租户)。

1. 单击 **[!UICONTROL 创建新项目]**. 系统会为您的组织创建一个名为的空白项目。

   单击 **[!UICONTROL 编辑项目]** 更新 **[!UICONTROL 项目标题]** 和 **[!UICONTROL 描述]**，然后单击 **[!UICONTROL 保存]**.

1. 在 **[!UICONTROL 项目概述]** ，单击 **[!UICONTROL 添加API]**.

1. 在 **[!UICONTROL 添加API窗口]**，选择 **[!UICONTROL AEM Brand Portal]** 单击 **[!UICONTROL 下一个]**.

   确保您有权访问Experience Mananger Brand Portal服务。

1. 在 **[!UICONTROL 配置API]** 窗口，单击 **[!UICONTROL 上传您的公钥]**. 然后，单击 **[!UICONTROL 选择文件]** 并上传您在 [获取公共证书](#public-certificate) 中。

   单击&#x200B;**[!UICONTROL 下一步]**。

   ![上传公共密钥](assets/service-account3.png)

1. 验证公钥并单击 **[!UICONTROL 下一个]**.

1. 选择 **[!UICONTROL Assets Brand Portal]** 作为默认的产品配置文件，然后单击 **[!UICONTROL 保存配置的API]**.

   ![选择产品配置文件](assets/service-account4.png)

1. 配置API后，您将被重定向到API概述页面。 从左侧导航下 **[!UICONTROL 凭据]**，请单击 **[!UICONTROL 服务帐户(JWT)]** 选项。

   >[!NOTE]
   >
   >您可以查看凭据并执行诸如生成JWT令牌、复制凭据详细信息、检索客户端密钥等操作。

1. 从 **[!UICONTROL 客户端凭据]** 选项卡，复制 **[!UICONTROL 客户端ID]**.

   单击 **[!UICONTROL 检索客户端密钥]** 并复制 **[!UICONTROL 客户端密码]**.

   ![服务帐户凭据](assets/service-account5.png)

1. 导航到 **[!UICONTROL 生成JWT]** ，并复制 **[!UICONTROL JWT有效负载]** 信息。

现在，您可以将客户端ID（API密钥）、客户端密钥和JWT有效负载用于 [配置IMS帐户](#create-ims-account-configuration) 在Experience Mananger Assets中。

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

1. 打开IMS配置，然后导航到 **[!UICONTROL 帐户]** 选项卡。 您在 [获取公共证书](#public-certificate).

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在 **[!UICONTROL 授权服务器]** 字段，请指定URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   在 **[!UICONTROL API密钥]** 字段， **[!UICONTROL 客户端密钥]**&#x200B;和 **[!UICONTROL 负载]** （JWT有效负载） [创建服务帐户(JWT)连接](#createnewintegration).

   单击&#x200B;**[!UICONTROL 创建]**。

   已配置IMS帐户。

   ![IMS 帐户配置](assets/create-new-integration6.png)


1. 选择IMS帐户配置并单击 **[!UICONTROL 检查运行状况]**.

   单击 **[!UICONTROL 检查]** 中。 成功配置后，将显示一条消息，显示 *已成功检索令牌*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一个IMS配置。
>
>确保IMS配置通过运行状况检查。 如果配置未通过运行状况检查，则无效。 您必须删除它，然后创建一个有效的新配置。

### 配置云服务 {#configure-the-cloud-service}

执行以下步骤以配置Brand Portal云服务：

1. 登录到Experience Mananger Assets。

1. 从 **工具** 面板，导航到 **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. 在Brand Portal配置页面中，单击 **[!UICONTROL 创建]**.

1. 指定配置的&#x200B;**[!UICONTROL 标题]**。

   选择您在 [配置IMS帐户](#create-ims-account-configuration).

   在 **[!UICONTROL 服务URL]** 字段中，指定您的Brand Portal租户（组织）URL。

   ![](assets/create-cloud-service.png)

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。将创建云配置。

   您的Mananger Assets as a [!DNL Cloud Service] 现在已使用Brand Portal租户配置实例。

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
