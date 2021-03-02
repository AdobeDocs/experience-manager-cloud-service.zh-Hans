---
title: 将AEM Assets配置为 [!DNL Cloud Service] 和Brand Portal
description: 使用 Brand Portal 配置 AEM Assets.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: bafb952cd984885e0f309b8a78a96ae48320b7df
workflow-type: tm+mt
source-wordcount: '1651'
ht-degree: 15%

---


# 将AEM Assets配置为[!DNL Cloud Service]（带有Brand Portal {#configure-aem-assets-with-brand-portal}）

通过配置Adobe Experience Manager Assets Brand Portal，您可以将Adobe Experience Manager Assets中已批准的品牌资产作为[!DNL Cloud Service]实例发布到Brand Portal，然后将其分发到Brand Portal用户。

**配置工作流**

AEM Assets作为[!DNL Cloud Service]已通过Adobe Developer Console配置Brand Portal，后者为Brand Portal租户购买Adobe Identity Management Services(IMS)帐户令牌以进行授权。 它要求在AEM Assets和Adobe开发人员控制台中进行配置。

1. 在AEM Assets中，创建IMS帐户并生成公钥（证书）。
1. 在Adobe开发人员控制台中，为您的Brand Portal租户（组织）创建一个项目。
1. 在项目下，使用公钥配置API以创建服务帐户连接。
1. 获取服务帐户凭据和JSON Web Token(JWT)有效负荷信息。
1. 在AEM Assets中，使用服务帐户凭据和JWT负载配置IMS帐户。
1. 在AEM Assets中，使用IMS帐户和Brand Portal端点（组织URL）配置Brand Portal云服务。
1. 通过将资产从AEM Assets发布到Brand Portal来测试配置。

>[!NOTE]
>
>作为[!DNL Cloud Service]实例的AEM Assets只能配置一个Brand Portal租户。

## 前提条件 {#prerequisites}

您需要以下各项才能使用 Brand Portal 配置 AEM Assets：

* 作为[!DNL Cloud Service]实例启动并运行AEM Assets
* Brand Portal租户URL
* 对Brand Portal租户的IMS组织具有系统管理员权限的用户

## 创建配置 {#create-new-configuration}

在指定序列中执行以下步骤以配置带Brand Portal的AEM Assets。

1. [获取公共证书](#public-certificate)
1. [创建服务帐户(JWT)连接](#createnewintegration)
1. [配置IMS帐户](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)
1. [测试配置](#test-configuration)

### 创建 IMS 配置 {#create-ims-configuration}

IMS配置将AEM Assets作为[!DNL Cloud Service]实例与Brand Portal租户进行身份验证。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [配置IMS帐户](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公钥（证书）可在Adobe Developer控制台上验证您的用户档案。

1. 登录 AEM Assets。
1. 从&#x200B;**工具**&#x200B;面板，导航到&#x200B;**[!UICONTROL 安全]** > **[!UICONTROL AdobeIMS配置]**。
1. 在Adobe IMS配置页中，单击&#x200B;**[!UICONTROL 创建]**。 它将重定向到&#x200B;**[!UICONTROL AdobeIMS技术帐户配置]**&#x200B;页。 默认情况下，将打开&#x200B;**证书**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL 云解决方案]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Adobe品牌门户]**。
1. 选中&#x200B;**[!UICONTROL 创建新证书]**&#x200B;复选框，并为公钥指定&#x200B;**别名**。 别名用作公钥的名称。
1. 单击&#x200B;**[!UICONTROL 创建证书]**。然后，单击&#x200B;**[!UICONTROL 确定]**&#x200B;以生成公钥。

   ![创建证书](assets/ims-config2.png)

1. 单击&#x200B;**[!UICONTROL 下载公钥]**&#x200B;图标，并将公钥(CRT)文件保存到计算机上。

   公钥稍后将用于为您的Brand Portal租户配置API并在Adobe Developer Console中生成服务帐户凭据。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在&#x200B;**帐户**&#x200B;选项卡中，将创建Adobe IMS帐户，该帐户需要在Adobe开发人员控制台中生成的服务帐户凭据。 暂时保持此页面打开。

   在Adobe Developer Console](#createnewintegration)中打开新选项卡并创建服务帐户(JWT)连接，以获取用于配置IMS帐户的凭据和JWT负载。[

### 创建服务帐户(JWT)连接{#createnewintegration}

在Adobe开发人员控制台中，项目和API在Brand Portal租户（组织）级别进行配置。 配置API可创建服务帐户(JWT)连接。 可通过生成密钥对（私钥和公钥）或上传公钥来配置API有两种方法。 要通过Brand Portal配置AEM Assets，您必须在AEM Assets中生成公钥（证书），并通过上传公钥在Adobe Developer Console中创建凭据。 在AEM Assets中配置IMS帐户时需要这些凭据。 配置IMS帐户后，即可在AEM Assets中配置Brand Portal云服务。

执行以下步骤以生成服务帐户凭据和JWT负载：

1. 使用IMS组织（Brand Portal租户）的系统管理员权限登录到Adobe Developer Console。 默认URL为[https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)。


   >[!NOTE]
   >
   >确保您从右上角的下拉（组织）列表中选择了正确的IMS组织（Brand Portal租户）。

1. 单击&#x200B;**[!UICONTROL 新建项目]**。 系统会为您的组织创建一个具有系统生成名称的空白项目。

   单击&#x200B;**[!UICONTROL 编辑项目]**&#x200B;以更新&#x200B;**[!UICONTROL 项目标题]**&#x200B;和&#x200B;**[!UICONTROL 说明]**，然后单击&#x200B;**[!UICONTROL 保存]**。

1. 在&#x200B;**[!UICONTROL 项目概述]**&#x200B;选项卡中，单击&#x200B;**[!UICONTROL 添加API]**。

1. 在&#x200B;**[!UICONTROL 添加API窗口]**&#x200B;中，选择&#x200B;**[!UICONTROL AEM Brand Portal]**&#x200B;并单击&#x200B;**[!UICONTROL 下一步]**。

   确保您有权访问AEM Brand Portal服务。

1. 在&#x200B;**[!UICONTROL 配置API]**&#x200B;窗口中，单击&#x200B;**[!UICONTROL 上传公钥]**。 然后，单击&#x200B;**[!UICONTROL 选择文件]**&#x200B;并上传您在[获取公共证书](#public-certificate)部分下载的公钥（.crt文件）。

   单击&#x200B;**[!UICONTROL 下一步]**。

   ![上传公钥](assets/service-account3.png)

1. 验证公钥，然后单击&#x200B;**[!UICONTROL 下一步]**。

1. 选择&#x200B;**[!UICONTROL 资产品牌门户]**&#x200B;作为默认产品用户档案，然后单击&#x200B;**[!UICONTROL 保存配置的API]**。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![选择产品用户档案](assets/service-account4.png)

1. 配置API后，您将被重定向到API概述页。 在左侧导航下的&#x200B;**[!UICONTROL 凭据]**&#x200B;中，单击&#x200B;**[!UICONTROL 服务帐户(JWT)]**&#x200B;选项。

   >[!NOTE]
   >
   >您可以视图凭据并执行诸如生成JWT令牌、复制凭据详细信息、检索客户端机密等操作。

1. 从&#x200B;**[!UICONTROL 客户端凭据]**&#x200B;选项卡中，复制&#x200B;**[!UICONTROL 客户端ID]**。

   单击&#x200B;**[!UICONTROL 检索客户端机密]**&#x200B;并复制&#x200B;**[!UICONTROL 客户端机密]**。

   ![服务帐户凭据](assets/service-account5.png)

1. 导航到&#x200B;**[!UICONTROL 生成JWT]**&#x200B;选项卡并复制&#x200B;**[!UICONTROL JWT负载]**&#x200B;信息。

您现在可以使用客户端ID（API密钥）、客户端机密和JWT负载[在AEM Assets中配置IMS帐户](#create-ims-account-configuration)。

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

### 配置IMS帐户{#create-ims-account-configuration}

确保您已执行以下步骤：

* [获取公共证书](#public-certificate)
* [创建服务帐户(JWT)连接](#createnewintegration)

请执行以下步骤来配置IMS帐户。

1. 打开IMS配置并导航到&#x200B;**[!UICONTROL 帐户]**&#x200B;选项卡。 在[获取公共证书](#public-certificate)时，您保持页面打开。

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在&#x200B;**[!UICONTROL 授权服务器]**&#x200B;字段中，指定URL:[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   在[创建服务帐户(JWT)连接](#createnewintegration)时，在&#x200B;**[!UICONTROL API密钥]**&#x200B;字段、**[!UICONTROL 客户端密钥]**&#x200B;和&#x200B;**[!UICONTROL 负载]**（JWT负载）中指定您复制的客户端ID。

   单击&#x200B;**[!UICONTROL 创建]**。

   已配置IMS帐户。

   ![IMS 帐户配置](assets/create-new-integration6.png)


1. 选择IMS帐户配置，然后单击&#x200B;**[!UICONTROL 检查运行状况]**。

   单击对话框中的&#x200B;**[!UICONTROL 选中]**。 成功配置时，将显示一条消息，提示已成功检索&#x200B;*令牌*。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一个IMS配置。
>
>确保IMS配置通过运行状况检查。 如果配置未通过运行状况检查，则无效。 您必须删除它并创建新的有效配置。

### 配置云服务 {#configure-the-cloud-service}

请执行以下步骤来配置Brand Portal云服务：

1. 登录 AEM Assets。

1. 从&#x200B;**工具**&#x200B;面板，导航到&#x200B;**[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**。

1. 在“Brand Portal配置”页中，单击&#x200B;**[!UICONTROL 创建]**。

1. 指定配置的&#x200B;**[!UICONTROL 标题]**。

   选择在[配置IMS帐户](#create-ims-account-configuration)时创建的IMS配置。

   在&#x200B;**[!UICONTROL 服务URL]**&#x200B;字段中，指定您的Brand Portal租户（组织）URL。

   ![](assets/create-cloud-service.png)

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。将创建云配置。

   您的AEM Assets现在已配置为[!DNL Cloud Service]实例的Brand Portal租户。

### 测试配置{#test-configuration}

请执行以下步骤以验证配置：

1. 登录 AEM Assets。

1. 从&#x200B;**工具**&#x200B;面板，导航到&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 分发]**。

   ![](assets/test-bpconfig1.png)

   在&#x200B;**[!UICONTROL 发布到Brand Portal]**&#x200B;下创建Brand Portal分发代理(**[!UICONTROL bpdistributionagent0]**)。

   ![](assets/test-bpconfig2.png)


1. 单击&#x200B;**[!UICONTROL 发布到Brand Portal]**&#x200B;以打开分发代理。

   您可以在&#x200B;**[!UICONTROL 状态]**&#x200B;选项卡下看到分布队列。

   分发代理包含两个队列：
   * **processing-queue**:用于将资产分发到Brand Portal。

   * **error-queue**:对于分发失败的资产。
   >[!NOTE]
   >
   >建议定期查看故障并清除&#x200B;**error-queue**。

   ![](assets/test-bpconfig3.png)

1. 要验证作为[!DNL Cloud Service]的AEM Assets与Brand Portal之间的连接，请单击&#x200B;**[!UICONTROL 测试连接]**&#x200B;图标。

   ![](assets/test-bpconfig4.png)

   将显示一条消息，提示已成功传送&#x200B;*测试包*。

   >[!NOTE]
   >
   >请避免禁用分发代理，因为这可能导致资产分发（在队列中运行）失败。

您现在可以：

* [将资产从 AEM Assets 发布到 Brand Portal](publish-to-brand-portal.md)
* [将文件夹从 AEM Assets 发布到 Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [将收藏集从 AEM Assets 发布到 Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [将资产从Brand Portal发布到AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=en) - Brand Portal中的资产来源
* [将预设、架构和 Facet 发布到 Brand Portal](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [将标记发布到 Brand Portal](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

有关详细信息，请参阅[Brand Portal文档](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/home.html)。

## 分发日志 {#distribution-logs}

您可以监视资产发布工作流的分发代理日志。

例如，我们已将资产从AEM Assets发布到Brand Portal以验证配置。

1. 按照[测试配置](#test-configuration)部分中显示的步骤（从1到4）操作，并导航到Distribution Agent页。
1. 单击&#x200B;**[!UICONTROL 日志]**&#x200B;以视图处理日志和错误日志。

   ![](assets/test-bpconfig5.png)

分发代理已生成以下日志：

* 信息：这是系统生成的日志，在成功配置分发代理时触发。
* DSTRQ1（请求1）：测试连接时触发器。

发布资产时，会生成以下请求和响应日志：

**分发代理请求**：

* DSTRQ2（请求 2）：触发资产发布请求。
* DSTRQ3（请求3）：系统会触发另一个请求，以发布AEM Assets文件夹（资产所在的文件夹），并在Brand Portal中复制该文件夹。

**分发代理响应**：

* queue-bpdistributionagent0(DSTRQ2)：将资产发布到 Brand Portal。
* queue-bpdistributionagent0(DSTRQ3):系统将复制Brand Portal中的AEM Assets文件夹（包含资产）。

在上述示例中，还会触发其他请求和响应。系统无法在Brand Portal中找到父文件夹（添加路径），因为资产是首次发布的，因此系统会触发另一个请求，要求在发布资产的Brand Portal中创建同名的父文件夹。

>[!NOTE]
>
>如果父级文件夹在Brand Portal中不存在或在AEM Assets中已修改，则会生成其他请求。

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
