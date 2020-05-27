---
title: 使用 Brand Portal 配置 AEM Assets 云服务
description: 使用 Brand Portal 配置 AEM Assets 云服务。
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 00e37e9493bc3dde8a4d83c562a889a67587ada0
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 80%

---


# 使用 Brand Portal 配置 AEM Assets {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager (AEM) Assets 通过 Adobe I/O 使用 Brand Portal 进行了配置，从而可获取 IMS 令牌以授权您的 Brand Portal 租户。

## 前提条件 {#prerequisites}

您需要以下各项才能使用 Brand Portal 配置 AEM Assets：

* 已启动且正在运行的 AEM Assets 云实例。
* Brand Portal 租户 URL。
* 对 Brand Portal 租户的 IMS 组织具有系统管理员权限的用户。

**联系客户关怀** ，进一步了解查询。

## 创建配置 {#create-new-configuration}

您可以在Adobe I/O上创建配置，以通过Brand Portal配置AEM Assets云实例。

按照列出的顺序执行以下步骤：
1. [获取公共证书](#public-certificate)
1. [创建 Adobe I/O 集成](#createnewintegration)
1. [创建 IMS 帐户配置](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)
1. [测试配置](#test-configuration)

### 创建 IMS 配置 {#create-ims-configuration}

IMS 配置通过 AEM Assets 作者实例对您的 Brand Portal 租户进行身份验证。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [创建 IMS 帐户配置](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公共证书允许您在 Adobe I/O 上验证配置文件。

1. 登录 AEM Assets 云实例。

1. From **tool** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

   ![Adobe IMS 帐户配置 UI](assets/ims-configuration1.png)

1. 打开 Adobe IMS 配置页面。

   单击&#x200B;**[!UICONTROL 创建]**。

   It will take you to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page.

1. 默认情况下，将打开&#x200B;**证书**&#x200B;选项卡。

   在&#x200B;**云解决方案**&#x200B;中，选择 **[!UICONTROL Adobe Brand Portal]**。

1. Mark the check box **[!UICONTROL Create new certificate]** and specify an **alias** for the certificate. 别名将用作对话框的名称。

1. 单击&#x200B;**[!UICONTROL 创建证书]**。将显示一个对话框。单击&#x200B;**[!UICONTROL 确定]**&#x200B;以生成公共证书。

   ![创建证书](assets/ims-config2.png)

1. 单击&#x200B;**[!UICONTROL 下载公钥]**，然后将 *AEM-Adobe-IMS.crt* 证书文件保存到您的计算机上。该证书文件将用于[创建 Adobe I/O 集成](#createnewintegration)。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在&#x200B;**帐户**&#x200B;选项卡中，您可以创建 Adobe IMS 帐户，但您需要集成详细信息。暂时保持此页面打开。

   打开新选项卡并[创建 Adobe I/O 集成](#createnewintegration)，以获取 IMS 帐户配置的集成详细信息。

### 创建 Adobe I/O 集成 {#createnewintegration}

Adobe I/O 集成可生成 API 密钥、客户端密钥和有效负荷 (JWT)，这是设置 IMS 帐户配置所必需的。

1. 使用 Brand Portal 租户的 IMS 组织的系统管理员权限登录到 Adobe I/O 控制台。

   默认 URL：[https://console.adobe.io/](https://console.adobe.io/)

1. 单击&#x200B;**[!UICONTROL 创建集成]**。

1. 选择&#x200B;**[!UICONTROL 访问 API]**，然后单击&#x200B;**[!UICONTROL 继续]**。

   ![创建新集成](assets/create-new-integration1.png)

1. 此时将打开新的集成页面。

   从下拉列表中选择您的组织。

   在 **[!UICONTROL Experience Cloud]** 中，选择 **[!UICONTROL AEM Brand Portal]**，然后单击&#x200B;**[!UICONTROL 继续]**。

   如果您禁用了 Brand Portal 选项，请确保您从 **[!UICONTROL Adobe Services]** 选项上方的下拉框中选择了正确的组织。如果您不了解您的组织，请与管理员联系。

   ![创建集成](assets/create-new-integration2.png)

1. 指定集成的名称和描述。单击&#x200B;**[!UICONTROL 从计算机中选择文件]**，然后上传在[获取公共证书](#public-certificate)部分下载的 `AEM-Adobe-IMS.crt` 文件。

1. 选择您的组织的配置文件。

   或者，选择默认的配置文件 **[!UICONTROL Brand Portal]**，然后单击&#x200B;**[!UICONTROL 创建集成]**。将创建集成。

1. 单击&#x200B;**[!UICONTROL 继续查看集成详细信息]**，以查看集成信息。

   复制 **[!UICONTROL API 密钥]**

   单击&#x200B;**[!UICONTROL 检索客户端密钥]**，并复制客户端密钥。

   ![集成的 API 密钥、客户端密钥和有效负荷信息](assets/create-new-integration3.png)

1. 导航到 **[!UICONTROL JWT]** 选项卡，并复制 **[!UICONTROL JWT 有效负荷]**。

   API 密钥、客户端密钥和 JWT 有效负荷信息将用于创建 IMS 帐户配置。

### 创建 IMS 帐户配置 {#create-ims-account-configuration}

确保您已执行以下步骤：

* [获取公共证书](#public-certificate)
* [创建 Adobe I/O 集成](#createnewintegration)

**创建 IMS 帐户配置的步骤：**

1. 打开“IMS 配置”页面的&#x200B;**[!UICONTROL 帐户]**&#x200B;选项卡。保持打开该页面[获取公共证书](#public-certificate)的结尾部分。

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在&#x200B;**[!UICONTROL 授权服务器]**&#x200B;中，输入 URL：[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   粘贴您在[创建 Adobe I/O 集成](#createnewintegration)结束时复制的 API 密钥、客户端密钥和 JWT 有效负荷。

   单击&#x200B;**[!UICONTROL 创建]**。

   将创建集成。

   ![IMS 帐户配置](assets/create-new-integration6.png)


1. 选择 IMS 配置，然后单击&#x200B;**[!UICONTROL 检查运行状况]**。将显示一个对话框。

   单击&#x200B;**[!UICONTROL 检查]**。成功连接时，将显示&#x200B;*已成功检索令牌*&#x200B;消息。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一个IMS配置。 请勿创建多个 IMS 配置。
>
>确保IMS配置通过运行状况检查。 如果配置未通过运行状况检查，则无效。 您必须删除它并创建新的有效配置。



### 配置云服务 {#configure-the-cloud-service}

执行以下步骤以创建 Brand Portal 云服务配置：

1. 登录 AEM Assets 云实例。

1. From **tool** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

   此时将打开 Brand Portal 的“配置”页面。

1. 单击&#x200B;**[!UICONTROL 创建]**。

1. 指定配置的&#x200B;**[!UICONTROL 标题]**。

   选择您在[创建 IMS 帐户配置](#create-ims-account-configuration)步骤中创建的“IMS 配置”。

   在&#x200B;**[!UICONTROL 服务 URL]** 中，输入您的 Brand Portal 租户 URL。

   ![](assets/create-cloud-service.png)

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**。将创建云配置。现在已为您的 AEM Assets 云实例配置了 Brand Portal 租户。

### 测试配置{#test-configuration}

1. 登录 AEM Assets 云实例。

1. From **tool** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

   ![](assets/test-bpconfig1.png)

1. 此时将打开“分发”页面。

   将在&#x200B;**[!UICONTROL 发布到 Brand Portal]** 下创建 Brand Portal 分发代理 `bpdistributionagent0`。

   单击&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >默认情况下，将为 Brand Portal 租户创建一个分发代理。

1. 此时将打开分发代理页面。默认情况下，会打开填充了分发队列的&#x200B;**[!UICONTROL 状态]**&#x200B;选项卡。

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

您可以检查日志，以了解有关对分发代理执行的操作的详细信息。

例如，我们已将资产从 AEM Assets 发布到 Brand Portal 以验证配置。

1. Follow the steps (Step 1 - 4) as shown in **[!UICONTROL Test Connection]** and navigate to the distribution agent page.

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
