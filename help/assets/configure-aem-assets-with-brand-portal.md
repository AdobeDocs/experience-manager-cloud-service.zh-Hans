---
title: 使用 Brand Portal 配置 AEM Assets 云服务
description: 使用 Brand Portal 配置 AEM Assets 云服务。
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: f54f5bbd5de76c3507d86b92255f1d4713e717fc
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 26%

---


# 使用 Brand Portal 配置 AEM Assets {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager(AEM)资产通过Adobe开发人员控制台配置为品牌门户，该控制台为品牌门户租户购买IMS令牌以进行授权。

**配置如何工作？**

使用Brand Portal租户（组织）配置AEM Assets云实例需要在AEM Assets云实例和Adobe Developer Console中进行配置。

1. 在AEM Assets云实例中，创建IMS帐户并生成公共证书（公钥）。
1. 在Adobe开发人员控制台中，为您的Brand Portal租户（组织）创建一个项目。
1. 在项目下，使用公钥配置API以创建服务帐户(JWT)连接。
1. 获取服务帐户凭据和JWT有效负荷信息。
1. 在AEM Assets云实例中，使用服务帐户凭据和JWT有效负荷配置IMS帐户。
1. 在AEM Assets云实例中，使用IMS帐户和Brand Portal端点（组织URL）配置Brand Portal云服务。
1. 通过将资产从AEM Assets云实例发布到Brand Portal来测试配置。

>[!NOTE]
>
>Brand Portal租户只应配置一个AEM Assets云实例。
>
>请勿配置具有多个AEM资产云实例的Brand Portal租户。


## 前提条件 {#prerequisites}

您需要以下各项才能使用 Brand Portal 配置 AEM Assets：

* 已启动且正在运行的 AEM Assets 云实例。
* Brand Portal 租户 URL。
* 对 Brand Portal 租户的 IMS 组织具有系统管理员权限的用户。

**联系客户关怀** ，进一步了解查询。

## 创建配置 {#create-new-configuration}

按指定顺序执行以下步骤，在Brand Portal中配置AEM Assets云实例。

1. [获取公共证书](#public-certificate)
1. [创建服务帐户(JWT)连接](#createnewintegration)
1. [配置IMS帐户](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)
1. [测试配置](#test-configuration)

### 创建 IMS 配置 {#create-ims-configuration}

IMS配置使用AEM Assets云实例对您的Brand Portal租户进行身份验证。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [配置IMS帐户](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公共证书允许您在Adobe开发人员控制台上验证用户档案。

1. 登录AEM Assets云实例。

1. From the **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

   ![Adobe IMS 帐户配置 UI](assets/ims-configuration1.png)

1. 在Adobe IMS配置页面中，单击创 **[!UICONTROL 建]**。

1. 您将被重定向到“ **[!UICONTROL Adobe IMS技术帐户配置”页]** 。 By default, the **Certificate** tab opens.

   选择云解决方 **[!UICONTROL 案Adobe Brand Portal]**。

1. Mark the check box **[!UICONTROL Create new certificate]** and specify an **alias** for the certificate. 别名将用作对话框的名称。

1. 单击&#x200B;**[!UICONTROL 创建证书]**。然后，在对 **[!UICONTROL 话框]** 中单击“确定”以生成公共证书。

   ![创建证书](assets/ims-config2.png)

1. Click **[!UICONTROL Download Public Key]** and save the certificate (.crt) file on your machine.

   该证书文件将用于后续步骤，以在Adobe开发人员控制台中为Brand Portal租户配置API并生成服务帐户凭据。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在“帐 **户** ”选项卡中，您创建Adobe IMS帐户，但为此，您需要在Adobe开发人员控制台中生成服务帐户凭据。 暂时保持此页面打开。

   在Adobe Developer Console中打开一 [个新选项卡并创建一个服务帐户(JWT)连接](#createnewintegration) ，以获取用于配置IMS帐户的凭据和JWT有效负荷。

### 创建服务帐户(JWT)连接 {#createnewintegration}

在Adobe开发人员控制台中，项目和API在组织（Brand Portal租户）级别进行配置。 配置API可在Adobe开发人员控制台中创建服务帐户(JWT)连接。 可通过生成密钥对（私钥和公钥）或上传公钥来配置API的方法有两种。 要在Brand Portal中配置AEM Assets云实例，您必须在AEM Assets云实例中生成公共证书（公钥），并通过上传公钥在Adobe Developer Console中创建凭据。 此公钥用于为所选Brand Portal组织配置API，并为服务帐户生成凭据和JWT有效负荷。 这些凭据还用于在AEM Assets云实例中配置IMS帐户。 配置IMS帐户后，您可以在AEM Assets云实例中配置Brand Portal云服务。

执行以下步骤以生成服务帐户凭据和JWT有效负荷：

1. 以IMS组织（Brand Portal租户）的系统管理员权限登录到Adobe Developer Console。 默认URL为

   [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)


   >[!NOTE]
   >
   >确保您从右上角的下拉菜单(组织列表)中选择了正确的IMS组织（Brand Portal租户）。

1. Click **[!UICONTROL Create new project]**. 将为您的组织创建一个空白项目。

   单击 **[!UICONTROL “编辑]** ”项目以更新 **[!UICONTROL 项目标题]** 和 **[!UICONTROL 说明]**，然 **[!UICONTROL 后单击“]**&#x200B;保存”。

   ![创建项目](assets/service-account1.png)

1. 在“项目概述”选项卡中，单 **[!UICONTROL 击“添加API]**”。

   ![添加API](assets/service-account2.png)

1. 在添加API窗口中，选择 **[!UICONTROL AEM Brand Portal]** ，然后单击 **[!UICONTROL 下一步]**。

   确保您有权访问AEM Brand Portal服务。

1. 在“配置API”窗口中，单 **[!UICONTROL 击“上传公钥”]**。 然后，单 **[!UICONTROL 击“Select a File]** （选择文件）”并上传您在“Obtain public certificate（获取公共证书）”部分下 [载的公共证书](#public-certificate) （.crt文件）。

   单击&#x200B;**[!UICONTROL 下一步]**。

   ![上传公钥](assets/service-account3.png)

1. 验证公共证书，然后单击“ **[!UICONTROL 下一步]**”。

1. 选择默认的产品用户档案 **[!UICONTROL 资产品牌门户]** ，然后单 **[!UICONTROL 击保存配置]**。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![选择产品用户档案](assets/service-account4.png)

1. 配置API后，您将被重定向到API概述。 在左侧导航的“凭据 **[!UICONTROL ”下]**，单 **[!UICONTROL 击“服务帐户(JWT)]**”。

   >[!NOTE]
   >
   >您可以根据需要视图凭据并执行其他操作（生成JWT令牌、复制凭据详细信息、检索客户端机密等）。

1. 从“客 **[!UICONTROL 户端凭据]** ”选项卡中，复 **[!UICONTROL 制客户端ID]**。

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![服务帐户凭据](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]**.

您现在可以使用客户端ID（API密钥）、客户端机密和JWT负载 [在AEM资产云实例中](#create-ims-account-configuration) 配置IMS帐户。

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

请执行以下步骤来配置您在获取公共证书时创建 [的IMS帐户](#public-certificate)。

1. 打开IMS配置并导航到帐 **[!UICONTROL 户选]** 项卡。 您在获取公共证书时 [使页面保持打开状态](#public-certificate)。

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在&#x200B;**[!UICONTROL 授权服务器]**&#x200B;中，输入 URL：[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   将客户端ID粘贴到您在创建服务帐户(JWT)连接时复制的API密钥、 [客户端机密和JWT有效负荷中](#createnewintegration)。

   单击&#x200B;**[!UICONTROL 创建]**。

   已配置IMS帐户。

   ![IMS 帐户配置](assets/create-new-integration6.png)


1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   在对 **[!UICONTROL 话框]** 中单击“检查”。 成功配置时，将显示一条消息，告 *示标记已成功检索*。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一个IMS配置。 请勿创建多个 IMS 配置。
>
>确保IMS配置通过运行状况检查。 如果配置未通过运行状况检查，则无效。 您必须删除它并创建新的有效配置。



### 配置云服务 {#configure-the-cloud-service}

请执行以下步骤来配置Brand Portal云服务：

1. 登录AEM Assets云实例。

1. From the **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. 在Brand Portal的“配置”页中，单击“ **[!UICONTROL 创建]**”。

1. 指定配置的&#x200B;**[!UICONTROL 标题]**。

   选择配置IMS帐户时已 [创建的IMS配置](#create-ims-account-configuration)。

   In the **[!UICONTROL Service URL]**, enter your Brand Portal tenant (organization URL).

   ![](assets/create-cloud-service.png)

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**。将创建云配置。现在已为您的 AEM Assets 云实例配置了 Brand Portal 租户。

### 测试配置{#test-configuration}

请执行以下步骤以验证配置：

1. 登录AEM Assets云实例。

1. From the **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

   ![](assets/test-bpconfig1.png)

1. 在“分发”页面中，您可以看到已为发布到品牌门 `bpdistributionagent0` 户创建一 **[!UICONTROL 个品牌门户分发代理]**。

   单击&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >默认情况下，将为 Brand Portal 租户创建一个分发代理。

1. 在分发代理页面中，您可以在状态选项卡下看到分 **[!UICONTROL 发队列]** 。

   分发代理包含两个队列：
   * **processing-queue**: 用于将资产分发到Brand Portal。

   * **error-queue**: 对于分发失败的资产。
   >[!NOTE]
   >
   >建议定期检查故障并清 **除错误队列** 。

   ![](assets/test-bpconfig3.png)

1. 要验证 AEM Assets 与 Brand Portal 之间的连接，请单击&#x200B;**[!UICONTROL 测试连接]**。

   ![](assets/test-bpconfig4.png)

   页面底部会显示一条消息，表明测试包已成功交付。

   >[!NOTE]
   >
   >请避免禁用分发代理，因为这可能导致资产分发（在队列中运行）失败。


已成功为您的 AEM Assets 云实例配置了 Brand Portal，您现在可以：

* [将资产从 AEM Assets 发布到 Brand Portal](publish-to-brand-portal.md)
* [将文件夹从 AEM Assets 发布到 Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [将收藏集从 AEM Assets 发布到 Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)

除了上述功能，您还可以将元数据架构、图像预设、搜索 Facet 和标记从 AEM Assets 发布到 Brand Portal。

* [将预设、架构和 Facet 发布到 Brand Portal](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [将标记发布到 Brand Portal](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


有关详细信息，请参阅 [Brand Portal 文档](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/home.html)。


## 分发日志 {#distribution-logs}

您可以检查日志，以了解有关分发代理执行的操作的详细信息。

例如，我们已将资产从AEM资产发布到Brand Portal以验证配置。

1. Follow the steps (from 1 to 4) as shown in the [test connection](#test-configuration) section and navigate to the distribution agent page.

1. 单击&#x200B;**[!UICONTROL 日志]**&#x200B;以查看分发日志。您可以在此处查看处理日志和错误日志。

   ![](assets/test-bpconfig5.png)

分发代理生成日志如下：

* 信息： 这是系统生成的日志，在成功配置时触发，从而启用分发代理。
* DSTRQ1（请求1）: 测试连接时的触发器。

发布资产时，会生成以下请求和响应日志：

**分发代理请求**：
* DSTRQ2（请求 2）：触发资产发布请求。
* DSTRQ3（请求3）: 系统会触发另一个请求，以发布资产所在的文件夹，并在Brand Portal中复制该文件夹。

**分发代理响应**：
* queue-bpdistributionagent0(DSTRQ2)：将资产发布到 Brand Portal。
* queue-bpdistributionagent0(DSTRQ3)：系统会在 Brand Portal 中复制包含该资产的文件夹。

在上例中，将触发其他请求和响应。 系统无法在Brand Portal中找到父文件夹（即添加路径），因为资产是首次发布的，因此，系统会触发其他请求，在发布资产的Brand Portal中创建具有相同名称的父文件夹。

>[!NOTE]
>
>如果 Brand Portal 中（上述示例中）不存在父文件夹，或父文件夹在 AEM Assets 中已被修改，则会生成其他请求。



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
