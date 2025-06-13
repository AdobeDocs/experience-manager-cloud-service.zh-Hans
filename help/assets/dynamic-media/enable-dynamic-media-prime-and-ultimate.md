---
title: 启用 [!DNL Dynamic Media] Prime和Ultimate
description: 了解如何启用 [!DNL Dynamic Media] Prime和Ultimate产品/服务。
feature: Asset Management
role: User, Admin
exl-id: 0ee161f5-bf44-41f1-928e-c07574fd43cc
source-git-commit: 82a3016149645701abe829ad89c493f480956267
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 4%

---

# 启用[!DNL Dynamic Media]Prime和Ultimate {#enable-dynamic-media-prime-and-ultimate}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 和 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 与 Edge Delivery Services 集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 可扩展性</b></a>
        </td>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
    </tr>
    <tr>
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

通过[!DNL Adobe Experience Manager] as a Cloud Service，您可以访问[!DNL Dynamic Media] Prime和Ultimate产品，以简化您的数字工作流并优化内容管理。 请参阅[Dynamic Media Prime和Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md)，了解它们的好处以及它们之间的主要区别。

本文提供了一个端到端的工作流，用于启用[!DNL Dynamic Media]Prime和Ultimate产品。

## 启用[!DNL Dynamic Media]Ultimate {#enable-dynamic-media-ultimate}

要启用[!DNL Dynamic Media] Ultimate，请执行以下操作：

1. [激活 [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)
1. [配置 [!DNL Dynamic Media] 解决方案](#configure-dynamic-media-solutions)
1. [创建并列出 [!DNL Dynamic Media] 公司](#create-and-list-dynamic-media-companies)
1. [在交付层配置自定义域](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the [!DNL AEM] [!DNL Dynamic Media] API card](#onboarding-api-keys)
-->

如果需要启用[!DNL Dynamic Media Prime]，请参阅[启用 [!DNL Dynamic Media Prime]](#enable-dynamic-media-prime)中提供的快速链接。

### 激活 [!DNL Dynamic Media with OpenAPI] {#activate-dynamic-media-with-openapi}

具有OpenAPI功能的[!DNL Dynamic Media]将DAM置于灵活而高效的内容供应链生态系统的核心，以确保资产治理和交付。

启用[!DNL Dynamic Media] Ultimate过程中的第一步是使用OpenAPI[&#128279;](/help/assets/dynamic-media-open-apis-overview.md)为您的Cloud Service环境激活[!DNL Dynamic Media] 。

#### 准备开始使用 {#prerequisites}

在启动激活过程之前，请确保您满足以下要求：

1. [访问Cloud Manager](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。
1. [您的项目包括 [!DNL Dynamic Media] 解决方案](#configure-dynamic-media-solutions)。
1. 您有[!DNL Dynamic Media]个Prime或Ultimate许可证。

#### 在Cloud Service环境中启用[!DNL Dynamic Media with OpenAPI]功能 {#enable-dynamic-media-with-openapi-capabilites-in-your-CS-environment}

执行以下步骤可为云服务环境启用[!DNL Dynamic Media with OpenAPI]：

1. [导航到Cloud Manager UI](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。

1. [如果无法访问现有环境，请创建环境](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments)。

1. 在环境详细信息页面上的&#x200B;**[!UICONTROL 环境信息]**&#x200B;部分的&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;行中选择&#x200B;**[!UICONTROL 单击以激活]**。

   ![使用OpenAPI功能激活Dynamic Media](/help/assets/assets/activate-adv-capabiliites-of-dm-openAPI.png)

1. 在确认对话框中单击&#x200B;**[!UICONTROL 激活]**&#x200B;以开始[!DNL Dynamic Media with OpenAPI]激活过程。 成功激活后，Cloud Manager会显示以下状态更新：
   1. **[!UICONTROL 环境阶段]**： **[!UICONTROL 正在运行]**
   1. ![已激活DM](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media &#x200B;]**：**[!UICONTROL &#x200B;已激活OpenAPI功能&#x200B;]**

      ![激活成功](/help/assets/assets/activation-successful.png){width="700" align="left"}

#### 重试激活 {#retry-activation}

如果激活失败，Cloud Manager会显示以下状态更新：

* **[!UICONTROL 环境暂存]**：**[!UICONTROL OpenAPI的DM失败]**
* ![DM已激活](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media &#x200B;]**：**[!UICONTROL &#x200B; OpenAPI功能无法激活&#x200B;]**

  ![重试激活](/help/assets/assets/retry-dm-openapi-failed-activation.png){width="700" align="left"}

选择&#x200B;**[!UICONTROL 单击以重试]**&#x200B;以重新启动激活。

或者，执行这些步骤以重新启动激活过程：

1. 导航到列出所有环境的页面。

1. 单击环境行末尾的更多选项（![更多选项](/help/assets/assets/three-dots.svg)）。

1. 选择&#x200B;**[!UICONTROL 使用OpenAPI激活重试DM]**&#x200B;以重新启动激活。

   ![从环境详细信息页面重试激活](/help/assets/assets/restart-activation-process-from-list-environment-page.png)

### 配置[!DNL Dynamic Media]解决方案 {#configure-dynamic-media-solutions}

将[!UICONTROL Dynamic Media]解决方案配置为在Cloud Manager中可用的现有或新环境中使用[带有OpenAPI的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)的基本和高级功能。

#### 准备开始使用 {#prerequisites-to-configure-dynamic-media-solutions}

确保您具有以下功能来配置[!UICONTROL Dynamic Media]解决方案：

1. [访问Cloud Manager](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。
1. 您有[!DNL Dynamic Media]个Ultimate许可证。

#### 为资产投放配置[!DNL Dynamic Media]解决方案 {#configure-dynamic-media-solutions-for-asset-delivery}

执行以下步骤：

1. [创建新程序](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/create-program)或导航到现有程序，然后单击&#x200B;**[!UICONTROL 编辑]**。 **[!UICONTROL 为生产设置]**&#x200B;页面显示&#x200B;**[!UICONTROL 解决方案和加载项]**&#x200B;选项卡。

1. 选择&#x200B;**[!UICONTROL Assets]**、**[!UICONTROL Assets Prime]**、**[!UICONTROL Assets Ultimate]**&#x200B;或&#x200B;**[!UICONTROL 站点]**&#x200B;以将&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;解决方案添加到您的项目中。

1. 选择&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;解决方案并单击&#x200B;**[!UICONTROL 继续]**&#x200B;以将&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;解决方案添加到您的项目中。 此操作重新启动程序中的所有现有环境，并向其中添加[!DNL Dynamic Media]解决方案。 此外，您在项目下创建的任何新环境都会自动获取[!DNL Dynamic Media]。

   ![为生产设置](/help/assets/assets/set-up-for-prod.png){width="500" align="left"}

请参阅[激活 [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)以在您的环境中开始使用[!DNL Dynamic Media]的功能和OpenAPI功能。

### 创建和列出[!DNL Dynamic Media]公司 {#create-and-list-dynamic-media-companies}

在AEM Cloud Service环境中创建并列出[!DNL Dynamic Media]公司，以管理AEM环境中的配置。

#### 准备开始使用 {#prerequisites-to-create-and-list-dynamic-media-companies}

要查看现有公司（帐户）或在您的IMS组织中添加新的[!DNL Dynamic Media]公司（帐户），您必须具有：

1. [访问Cloud Manager](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。

1. 您有[!DNL Dynamic Media]个Ultimate许可证。

#### 在您的IMS组织中创建和列出[!DNL Dynamic Media]公司 {#create-and-list-dynamic-media-companies-in-your-ims-organisation}

执行以下步骤以创建并列出可在您的[!DNL AEM]环境中配置的新[!DNL Dynamic Media]公司（帐户）：

1. 导航到[Cloud Manager许可证页面](https://experience-stage.adobe.com/#/@ssahnichstage/cloud-manager/license)。

1. 单击&#x200B;**[!UICONTROL 添加公司]**，将显示&#x200B;**[!UICONTROL 创建Dynamic Media公司]**&#x200B;对话框。

1. 指定唯一的[!DNL Dynamic Media]公司名称，选择公司区域并添加以逗号分隔的公司管理员电子邮件ID列表。

   ![创建Dynamic Media公司](/help/assets/assets/create-dynamic-media-company.png){width="500" align="left"}

1. 单击&#x200B;**[!UICONTROL 创建]**&#x200B;开始创建您的公司。 此操作向&#x200B;**[!UICONTROL [!DNL Dynamic Media]公司]**&#x200B;分区添加一个新行并显示&#x200B;**[!UICONTROL 正在设置]**&#x200B;为公司的&#x200B;**[!UICONTROL 状态]**。

   ![已启动Dynamic Media公司创建](/help/assets/assets/dm-company-creation-initiated.png)

1. **可选：**&#x200B;单击![信息图标](/help/assets/assets/info-icon-solid-black.svg)查看公司的详细信息。 创建公司时，**[!UICONTROL 状态]**&#x200B;将更新为&#x200B;**[!UICONTROL 就绪]**。

   ![Dynamic Media公司信息](/help/assets/assets/dm-company-information.png)

1. 作为Dynamic Media管理员，请查看您的邮箱中的欢迎电子邮件，其中包含要在[!DNL AEM] Cloud Service环境中[配置 [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#architecture-diagram-of-dynamic-media)公司以开始使用的步骤列表。

   ![欢迎电子邮件](/help/assets/assets/welcome-email.png)

#### 重试公司创建 {#retry-company-creation}

如果[!DNL Dynamic Media]公司创建失败，请根据失败状态执行以下步骤：

1. 如果&#x200B;**[!UICONTROL 状态]**&#x200B;为“待处理”，则请向客户支持团队提出问题以供解决。


   ![待处理状态](/help/assets/assets/company-creation-pending-status.png){width="350" align="center"}



1. 如果&#x200B;**[!UICONTROL 状态]**&#x200B;失败，则根据失败原因重试。

   ![失败状态](/help/assets/assets/company-creation-failure-status.png){width="380" align="center"}

### 可选：在交付层配置自定义域 {#configure-custom-domain-in-delivery-tier}

虽然AEM as a Cloud Service附带默认域，但您可以根据需要对其进行自定义。 使用Cloud Manager将自定义域附加到交付层。

#### 准备开始使用 {#prerequisites-to-configure-custom-domain-in-delivery-tier}

在启动配置过程之前，请确保您满足以下要求：

1. [访问Cloud Manager](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)。
1. [已在您的环境中激活 [!DNL Dynamic Media with OpenAPI] ](#activate-dynamic-media-with-openapi)。
1. 已启用[!DNL Dynamic Media with OpenAPI]处于就绪状态。
1. 用于投放层的域的EV或OV类型证书。 有关详细信息，请参阅[SSL证书简介](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates)。

#### 使用Cloud Manager在交付层配置自定义域 {#configure-custom-domain-in-delivery-tier-using-cloud-manager}

在Cloud Manager中执行以下步骤，在交付层配置自定义域：

1. [添加客户管理的SSL证书](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert)。

1. [添加自定义域名](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings)。

1. 导航到环境详细信息页面并[添加CDN配置](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/domain-mappings/add-domain-mapping)。 添加配置时，在&#x200B;**[!UICONTROL 配置CDN]**&#x200B;对话框的&#x200B;**[!UICONTROL 层]**&#x200B;字段中选择&#x200B;**[!UICONTROL 投放]**。

   ![配置CDN](/help/assets/assets/select-delivery-tier-in-configure-cdn-form.png)

   添加配置后，**[!UICONTROL CDN配置]**&#x200B;的&#x200B;**[!UICONTROL 状态]**&#x200B;将更新为&#x200B;**[!UICONTROL 已应用]**。

   ![配置CDN部署状态](/help/assets/assets/cdn-configuration-deployment-status.png)

1. 单击更多选项（![更多选项](/help/assets/assets/three-dots.svg)）并选择&#x200B;**[!UICONTROL 上线准备工作]**&#x200B;以显示&#x200B;**[!UICONTROL 上线准备工作]**&#x200B;对话框。

   ![上线准备选项](/help/assets/assets/go-live-readiness-option.png)

1. 执行&#x200B;**[!UICONTROL 配置CNAME]**&#x200B;步骤以映射DNS服务提供者的DNS记录中的`cdn.adobeaemcloud.com` （CNAME记录）。 此映射可确保将在自定义域中收到的请求重定向到Adobe的CDN。

   ![上线就绪对话框](/help/assets/assets/go-live-readiness-dialogbox.png){width="500" align="left"}

1. 单击&#x200B;**[!UICONTROL 确定]**，**[!UICONTROL 状态]**&#x200B;更新为&#x200B;**[!UICONTROL 已验证]**。 自定义域已准备好在投放URL中使用。


   ![配置CDN](/help/assets/assets/cdn-configurations-varified.png)



<!--
### Onboard API keys {#onboarding-api-keys}

Create an API key to access [!DNL Dynamic Media] with OpenAPIs and the delivery tier backed Asset Selector.

#### Prepare yourself for API keys onboarding process {#prerequisites-for-onboarding-api-keys} 

To start the API keys onboarding process, ensure you have:

1. [Access to Cloud Manager](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Activated [!DNL Dynamic Media with OpenAPI] in your environment](#activate-dynamic-media-with-openapi).
1. [Access to the Adobe Developer Console](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis#create-adobe-developer-console-adc-project).

#### Onboard the API keys using [!DNL AEM Dynamic Media] API card {#onboarding-api-keys-using-aem-dynamic-media-api-card}

Use the [Adobe Developer Console](https://developer.adobe.com/developer-console/) to onboard the API keys to:

1. [Access Dynamic Media APIs](#access-dynamic-media-apis)
1. [Access Delivery tier backed Asset Selector](#access-delivery-tier-backed-asset-selector)

#### Create an API key to access [!DNL Dynamic Media] with OpenAPIs {#access-dynamic-media-apis}

Execute the following steps to create an API key to access [!DNL Dynamic Media] with OpenAPIs:

1. Navigate to the **[!UICONTROL Admin Console]**. The Admin Console displays the **[!UICONTROL author]**, **[!UICONTROL delivery]** and **[!UICONTROL publish]** instances.
![instances on admin console](/help/assets/assets/delivery-instance-admin-console.png)
1. Select the **[!UICONTROL delivery]** instance to display the product profile with **[!UICONTROL AEM Dynamic Media enable API Services]** enabled by default. The product profile looks like this: **[!UICONTROL AEM Assets DM OpenAPI Users - delivery  - Program [ID Number] - Environment [ID Number]]**. 

   ![product profile on admin console](/help/assets/assets/admin-console-product-profile.png)

   >[!NOTE]
   >
   >This delivery instance is common for [!DNL Content Hub] and [!DNL Dynamic Media] with OpenAPI capabilities.

1. Navigate to the [Adobe Developer console](https://developer.adobe.com/console) and [create a new project](https://developer.adobe.com/dep/guides/dev-console/create-project/). See [Invoke OpenAPI-based AEM APIs for server to server authentication](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) to learn about creating a new project.
1. Select **[!UICONTROL AEM Dynamic Media API]** to access to the [!DNL Dynamic Media with OpenAPI capabilities] and click **[!UICONTROL Next]**.
![adobe developer console](/help/assets/assets/adobe-developer-console.png)
1. Select **[!UICONTROL Server-to-Server Authentication]** and click **[!UICONTROL Next]**. See [Server to Server authentication](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) to learn more about this authentication type.
![server-to-server-authentication](/help/assets/assets/server-to-server-authentication.png)
1. Select **[!UICONTROL OAuth Server-to-Server]**, specify a unique **[!UICONTROL Credential name]** and click **[!UICONTROL Next]**.
![oauth server to server credential](/help/assets/assets/oauth-server-server-and-credential-name.png)
1. Select your product profile (mentioned in step 2) to access the APIs using the environment's delivery endpoint and click **[!UICONTROL Save configured API]**.
![select product profile](/help/assets/assets/select-product-profile.png)
1. Select **[!UICONTROL AEM Dynamic Media API]**. Use the **[!UICONTROL OAuth Server-to-Server]** to fetch the **X-API-key** and access the token for the **authorization** header. 
![oauth server to server](/help/assets/assets/oauth-server-to-server-credentials.png)
Execute the below steps to use [Dynamic Media with OpenAPIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) using the **[!UICONTROL OAuth Server-to-Server]** credentials. 
    1. Copy the **[!UICONTROL API KEY (Client ID)]** and replace the `X-Api-Key` in the cURL.
    1. Click **[!UICONTROL Generate access token]** to generate an access token and replace `YOUR_JWT_HERE` with the token in the cURL.

The cURL looks like this:
```
headers: {
    'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    `},
```
See [Search Assets API](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/search-assets-api#search-assets-api-header) for more information.

### Access Delivery tier backed Asset Selector {#access-delivery-tier-backed-asset-selector}

TBD: Wiki in progress..
-->

## 启用[!DNL Dynamic Media]Prime {#enable-dynamic-media-prime}

要启用[!DNL Dynamic Media] Prime，请执行以下操作：

1. [使用OpenAPI激活Dynamic Media](#activate-dynamic-media-with-openapi)
1. [可选：在交付层](#configure-custom-domain-in-delivery-tier)中配置自定义域

<!--
1. [Onboard API keys using the AEM Dynamic Media API card](#onboarding-api-keys)
-->
