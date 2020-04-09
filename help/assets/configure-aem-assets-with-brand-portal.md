---
title: 使用Brand Portal配置AEM Assets云服务
description: 使用Brand Portal配置AEM Assets云服务。
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 4677a8771c5891b8c9846e0adb58025304a71bdd

---


# 使用Brand Portal配置AEM资产 {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager(AEM)资产通过Adobe I/O配置了Brand Portal,Adobe I/O可获取IMS令牌以授权您的Brand Portal租户。

## 前提条件 {#prerequisites}

您需要以下各项才能在Brand Portal中配置AEM资产：

* 一个正在运行的AEM Assets云实例。
* Brand Portal租户URL。
* 对Brand Portal租户的IMS组织具有系统管理员权限的用户。

**联系支持** ，进一步查询。

## Create configuration {#create-new-configuration}

您可以在Adobe I/O上创建新配置，以通过Brand Portal配置AEM Assets云实例。

在列出的序列中执行以下步骤：
1. [获取公共证书](#public-certificate)
1. [创建Adobe I/O集成](#createnewintegration)
1. [创建IMS帐户配置](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)
1. [测试配置](#test-configuration)

### 创建IMS配置 {#create-ims-configuration}

IMS配置使用AEM Assets作者实例验证您的Brand Portal租户。

IMS配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [创建IMS帐户配置](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公共证书允许您在Adobe I/O上验证用户档案。

1. 登录AEM Assets云实例

1. 从“ **Security**![](assets/tools.png) Tools **[!UICONTROL ”面板中，导航到“]** Security **[!UICONTROL ”>“]** Adobe IMS配置”。

   ![Adobe IMS帐户配置UI](assets/ims-configuration1.png)

1. Adobe IMS配置页面打开。

   单击&#x200B;**[!UICONTROL 创建]**。

   此操作将转到 **[!UICONTROL Adobe IMS技术帐户配置页]** 。

1. 默认情况下，“证 **书** ”选项卡打开。

   在 **Cloud Solution**，选择 **[!UICONTROL Adobe Brand Portal]**。

1. 标记复选 **[!UICONTROL 框创建新证书]** ，并指定证 **书的别名** 。 别名用作对话框的名称。

1. 单击“ **[!UICONTROL 创建证书]**”。 将显示一个对话框。 单击 **[!UICONTROL 确定]** ，以生成公共证书。

   ![创建证书](assets/ims-config2.png)

1. 单 **[!UICONTROL 击“下载公钥]** ”，然后将 ** AEM-Adobe-IMS.crt证书文件保存到您的计算机上。 证书文件用于创 [建Adobe I/O集成](#createnewintegration)。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在“帐 **户** ”选项卡中，您创建Adobe IMS帐户，但为此您需要集成详细信息。 此页面暂时打开。

   打开新选项卡并 [创建Adobe I/O集成](#createnewintegration) ，获取IMS帐户配置的集成详细信息。

### 创建Adobe I/O集成 {#createnewintegration}

Adobe I/O集成生成API密钥、客户端机密和有效负荷(JWT)，这是设置IMS帐户配置所必需的。

1. 使用Brand Portal租户的IMS组织的系统管理员权限登录到Adobe I/O控制台。

   默认URL: [https://console.adobe.io/](https://console.adobe.io/)

1. 单击“ **[!UICONTROL 创建集成]**”。

1. 选择 **[!UICONTROL 访问API]**，然后单击 **[!UICONTROL 继续]**。

   ![创建新集成](assets/create-new-integration1.png)

1. 此时将打开新的集成页面。

   从下拉列表中选择您的组织。

   在 **[!UICONTROL Experience Cloud中]**，选择 **[!UICONTROL AEM Brand Portal]** ，然后单击 **[!UICONTROL 继续]**。

   如果您禁用了“品牌门户”选项，请确保您从 **[!UICONTROL Adobe Services选项上方的下拉框中选择了正确的组织]** 。 如果您不了解您的组织，请与管理员联系。

   ![创建集成](assets/create-new-integration2.png)

1. 指定集成的名称和说明。 单击 **[!UICONTROL 从计算机中选择文件]** ，然后上传在“获取公 `AEM-Adobe-IMS.crt` 共证书”部分下 [载的文件](#public-certificate) 。

1. 选择您的组织的用户档案。

   或者，选择默认的用户档案资 **[!UICONTROL 产Brand Portal]** ，然后单 **[!UICONTROL 击创建集成]**。 将创建集成。

1. 单击 **[!UICONTROL 继续以视图集成详细信息]** ，以便集成信息。

   复制 **[!UICONTROL API密钥]**

   单击 **[!UICONTROL “检索客户端机密]** ”并复制客户端机密密钥。

   ![集成的API密钥、客户端机密和有效负荷信息](assets/create-new-integration3.png)

1. 导航到 **[!UICONTROL JWT]** 选项卡，并复制 **[!UICONTROL JWT有效负荷]**。

   API密钥、客户端密钥和JWT有效负荷信息将用于创建IMS帐户配置。

### 创建IMS帐户配置 {#create-ims-account-configuration}

确保您已执行以下步骤：

* [获取公共证书](#public-certificate)
* [创建Adobe I/O集成](#createnewintegration)

**创建IMS帐户配置的步骤：**

1. 打开“IMS配置”页的“帐 **[!UICONTROL 户]** ”选项卡。 您在“获取公共证书”部分的结尾处保持 [该页面打开](#public-certificate)。

1. 为IMS **[!UICONTROL 帐户指定]** “标题”。

   在授 **[!UICONTROL 权服务器]**，输入URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   粘贴您在创建Adobe I/O集成结束时复制的API密钥、客户端机密和 [JWT有效负荷](#createnewintegration)。

   单击&#x200B;**[!UICONTROL 创建]**。

   将创建集成。

   ![IMS帐户配置](assets/create-new-integration6.png)


1. 选择IMS配置，然后单击“检 **[!UICONTROL 查运行状况”]**。 将显示一个对话框。

   单击 **[!UICONTROL 检查]**。 成功连接时，将显示 *已成功检索的令牌* 消息。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>仅创建一个有效的IMS配置。 请勿创建多个IMS配置。
>
> 确保配置正常。 如果配置不健康，请删除该配置并创建一个新的健康配置。


### 配置云服务 {#configure-the-cloud-service}

执行以下步骤以创建Brand Portal云服务配置：

1. 登录AEM Assets云实例

1. 从“工 **具**![”面板中，导航至“云服务”](assets/tools.png) >“AEM Brand **[!UICONTROL Portal工具]******”。

   Brand Portal配置页面打开。

1. 单击&#x200B;**[!UICONTROL 创建]**。

1. 指定配 **[!UICONTROL 置的]** “标题”。

   选择您在步骤中创建的IMS配置，创建 [IMS帐户配置](#create-ims-account-configuration)。

   在服 **[!UICONTROL 务URL中]**，输入您的Brand Portal租户URL。

   ![](assets/create-cloud-service.png)

1. Click **[!UICONTROL Save and Close]**. 云配置已创建。 您的AEM Assets云实例现在已配置Brand Portal租户。

### Test configuration {#test-configuration}

1. 登录AEM Assets云实例。

1. 从“工 **具**![”面板中，导航至“部署工](assets/tools.png) 具” **[!UICONTROL >“分]******&#x200B;发工具”。

   ![](assets/test-bpconfig1.png)

1. 此时将打开“分发”页面。

   将在发布到品牌门户下 `bpdistributionagent0` 创建Brand Portal **[!UICONTROL 分发代理]**。

   Click **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >默认情况下，将为Brand Portal租户创建一个分发代理。

1. 此时将打开分发代理页面。 默认情况下，“状 **[!UICONTROL 态]** ”选项卡会打开，其中填充了分发队列。

   分发代理包含两个队列：
   * 用于将资产分发到Brand Portal的处理队列。
   * 分发失败的资产的错误队列。
   ![](assets/test-bpconfig3.png)

1. 要验证AEM资产与Brand Portal之间的连接，请单击“测 **[!UICONTROL 试连接”]**。

   ![](assets/test-bpconfig4.png)

   页面底部会显示一条消息，表明测试包已成功交付。

   >[!NOTE]
   >
   >请避免禁用分发代理，因为这可能导致资产分发（在队列中运行）失败。


您的AEM Assets云实例已成功配置Brand Portal，您现在可以：

* [将资产从AEM资产发布到Brand Portal](publish-to-brand-portal.md)
* [将文件夹从AEM资产发布到Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [将集合从AEM资产发布到Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)

除了上述功能，您还可以将元数据模式、图像预设、搜索彩块化和标记从AEM资产发布到Brand Portal。

* [将预设、模式和彩块化发布到Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [将标记发布到 Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


有关详细 [信息，请参阅Brand Portal文档](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) 。


## 分发日志 {#distribution-logs}

您可以检查日志，以了解有关对分发代理执行的操作的详细信息。

例如，我们已将资产从AEM资产发布到Brand Portal以验证配置。

1. 按照测试连接中所示的步骤（第1步到第4步） **[!UICONTROL 操作]** ，然后导航到分发代理页面。

1. 单击 **[!UICONTROL 日志]** ，以视图分发日志。 您可以在此处查看处理和错误日志。

   ![](assets/test-bpconfig5.png)

分发代理生成以下日志：

* 信息：这是系统生成的日志，在成功配置时触发，用于启用分发代理。
* DSTRQ1（请求1）:在测试连接时触发。

发布资产时，会生成以下请求和响应日志：

**分发代理请求**:
* DSTRQ2（请求2）:资产发布请求会触发。
* DSTRQ3（请求3）:系统会触发另一个请求，以发布资产所在的文件夹，并在Brand Portal中复制该文件夹。

**分发代理响应**:
* queue-bpdistributionagent0(DSTRQ2):资产将发布到Brand Portal。
* queue-bpdistributionagent0(DSTRQ3):系统会在Brand Portal中复制包含资产的文件夹。

在上例中，将触发其他请求和响应。 系统无法在Brand Portal中找到父文件夹（例如，添加路径），因为资产是首次发布的，因此，系统会触发其他请求，在发布资产的Brand Portal中创建同名的父文件夹。

>[!NOTE]
>
>如果父级文件夹在Brand Portal中不存在（在上例中），或父级文件夹在AEM资产中已被修改，则会生成其他请求。


## 附加信息 {#additional-information}

转到以 `/system/console/slingmetrics` 了解与已分发内容相关的统计信息：

1. **计数器指标**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **时间指标**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
