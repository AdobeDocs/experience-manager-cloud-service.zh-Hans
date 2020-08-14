---
title: 增强型智能标记
description: 使用 Adobe Sensei 的 AI 和 ML 服务应用上下文和描述性业务标记，以提高资产发现和内容交付速度。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 33ce255e126f2a49f1c1a6e94955aade2ca0d240
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 97%

---


# 配置 Experience Manager 以智能标记资产 {#configure-aem-for-smart-tagging}

使用分类控制的词汇标记资产可确保通过基于标记的搜索轻松识别和检索资产。Adobe 提供了智能标记，该功能使用人工智能和机器学习算法来培训图像。智能标记使用 [Adobe Sensei](https://www.adobe.com/cn/sensei/experience-cloud-artificial-intelligence.html) 的人工智能框架，根据您的标记结构和业务分类培训其图像识别算法。

智能标记功能可作为 [!DNL Experience Manager] 的加载项进行购买。购买后，系统会向组织的管理员发送一封电子邮件，其中包含指向 Adobe 开发人员控制台的链接。管理员需访问该链接以使用 Adobe 开发人员控制台将智能标记与 [!DNL Experience Manager] 相集成。

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
-->

>[!IMPORTANT]
>
>默认情 [!DNL Experience Manager Assets] 况下，新部署 [!DNL Adobe Developer Console] 与集成。 它有助于更快地配置智能标记功能。 在现有部署中，管理员按照以下步骤进行配置。

## 使用 Adobe 开发人员控制台进行集成 {#aio-integration}

必须使用 Adobe 开发人员控制台将 [!DNL Adobe Experience Manager] 与智能标记服务相集成，然后才能使用 SCS 标记图像。在后端，[!DNL Experience Manager] 服务器会使用 Adobe 开发人员控制台网关验证您的服务凭证，然后将您的请求转发给该服务。

* 在 [!DNL Experience Manager] 中创建配置以生成公共密钥。为 OAuth 集成[获取公共证书](#obtain-public-certificate)。
* [在 Adobe 开发人员控制台中创建集成](#create-aio-integration)，并上传生成的公共密钥。
* 从 Adobe 开发人员控制台使用 API 密钥和其他凭证在 [!DNL Experience Manager] 实例中[配置智能标记](#configure-smart-content-service)。
* [测试配置](#validate-the-configuration)。
* [证书过期后重新配置](#certrenew)。

### Adobe 开发人员控制台集成的先决条件 {#prerequisite-for-aio-integration}

在使用智能标记之前，请确保满足以下条件，以便在 Adobe 开发人员控制台上创建集成：

* 具备拥有组织管理员权限的 Adobe ID 帐户。
* 为您的组织启用了智能标记。

### 获取公共证书 {#obtain-public-certificate}

公共证书允许您在 Adobe 开发人员控制台上验证配置文件。您可从 [!DNL Experience Manager] 中创建证书。

1. 在 [!DNL Experience Manager] 用户界面中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL Adobe IMS 配置]**。

1. 在“[!UICONTROL Adobe IMS 配置]”页面上，单击&#x200B;**[!UICONTROL 创建]**。从&#x200B;**[!UICONTROL 云解决方案]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 智能标记]**。

1. 选择&#x200B;**[!UICONTROL 创建新证书]**。提供名称，然后单击&#x200B;**[!UICONTROL 创建证书]**。单击&#x200B;**[!UICONTROL 确定]**。

1. 单击&#x200B;**[!UICONTROL 下载公共密钥]**。

   ![Experience Manager 智能标记创建公共密钥](assets/aem_smarttags-config1.png)

### 创建集成 {#create-aio-integration}

要使用智能标记，请在 Adobe 开发人员控制台中创建集成，以生成 API 密钥、技术帐户 ID、组织 ID 和客户端密钥。

1. 在浏览器中访问 [https://console.adobe.io](https://console.adobe.io/)。选择相应的帐户并验证关联的组织角色是否为系统管理员。
1. 创建具有任何所需名称的项目。单击&#x200B;**[!UICONTROL 添加 API]**。
1. 在&#x200B;**[!UICONTROL 添加 API]** 页面中，依次选择 **[!UICONTROL Experience Cloud]** 和&#x200B;**[!UICONTROL 智能内容]**。单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择&#x200B;**[!UICONTROL 上传您的公共密钥]**。提供从 [!DNL Experience Manager] 下载的证书文件。此时将显示“[!UICONTROL 公共密钥上传成功]”消息。单击&#x200B;**[!UICONTROL 下一步]**。
1. “[!UICONTROL 创建新的服务帐户 (JWT) 凭证]”页面将显示刚刚配置的服务帐户的公共密钥。单击&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 选择产品配置文件]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 智能内容服务]**。单击&#x200B;**[!UICONTROL 保存配置的 API]**。页面会显示有关配置的更多信息。在 [!DNL Experience Manager] 中进一步配置智能标记时，请保持此页面处于打开状态，以复制这些值，并将其添加到 Experience Manager 中。

   ![在“概述”选项卡中，您可以查看为集成提供的信息。](assets/integration_details.png)

### 配置智能标记 {#configure-smart-content-service}

要配置集成，请使用 Adobe 开发人员控制台集成中的有效负荷、客户端密钥、授权服务器和 API 密钥字段的值。

1. 在 [!DNL Experience Manager] 用户界面中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL Adobe IMS 配置]**。
1. 访问 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面，并提供所需的&#x200B;**[!UICONTROL 标题]**。
1. 在&#x200B;**[!UICONTROL 授权服务器]**&#x200B;字段中，提供 `https://ims-na1.adobelogin.com` URL。
1. 在 **[!UICONTROL API 密钥]**&#x200B;字段中，提供 [!DNL Adobe Developer Console] 中的&#x200B;**[!UICONTROL 客户端 ID]**。
1. 在&#x200B;**[!UICONTROL 客户端密钥]**&#x200B;字段中，提供 [!DNL Adobe Developer Console] 中的&#x200B;**[!UICONTROL 客户端密钥]**。单击&#x200B;**[!UICONTROL 检索客户端密钥]**&#x200B;选项可进行查看。
1. 在 [!DNL Adobe Developer Console] 的项目中，单击左边距中的&#x200B;**[!UICONTROL 服务帐户 (JWT)]**。单击&#x200B;**[!UICONTROL 生成 JWT]** 选项卡。单击&#x200B;**[!UICONTROL 复制]**，以复制显示的 **[!UICONTROL JWT 有效负荷]**。在 [!DNL Experience Manager] 的&#x200B;**[!UICONTROL 有效负荷]**&#x200B;字段中提供此值。单击&#x200B;**[!UICONTROL 创建]**。

### 验证配置 {#validate-the-configuration}

完成配置后，请按照以下步骤验证配置。

1. 在 [!DNL Experience Manager] 用户界面中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL Adobe IMS 配置]**。

1. 选择智能标记配置。单击工具栏中的&#x200B;**[!UICONTROL 检查运行状况]**。单击&#x200B;**[!UICONTROL 检查]**。显示“[!UICONTROL 配置正常]”消息的对话框确认配置可正常工作。

![验证智能标记配置](assets/smart-tag-config-validation.png)

### 证书过期后重新配置 {#certrenew}

证书过期后，将不再受信任。要添加新证书，请执行以下步骤。无法续订已过期的证书。

1. 以管理员身份登录 [!DNL Experience Manager] 部署。单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**。

1. 找到并单击 **[!UICONTROL dam-update-service]** 用户。单击 **[!UICONTROL KeyStore]** 选项卡。
1. 删除包含已过期证书的现有 **[!UICONTROL similaritysearch]** KeyStore。单击&#x200B;**[!UICONTROL 保存并关闭]**。

   ![删除 Keystore 中的现有 similaritysearch 条目以添加新的安全证书](assets/smarttags_delete_similaritysearch_keystore.png)

   *图：删除 Keystore 中的现有`similaritysearch`条目以添加新的安全证书。*

1. 在 [!DNL Experience Manager] 用户界面中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL Adobe IMS 配置]**。打开可用的智能标记配置。要下载公共证书，请单击&#x200B;**[!UICONTROL 下载公共证书]**。

1. 访问 [https://console.adobe.io](https://console.adobe.io)，然后导航到“项目”中的现有服务。上传新证书并进行配置。有关配置的详细信息，请参阅[创建 Adobe 开发人员控制台集成](#create-aio-integration)中的说明。

## 为新上传的资产启用智能标记（可选）{#enable-smart-tagging-for-uploaded-assets}

1. 在 [!DNL Experience Manager] 中，转到&#x200B;**[!UICONTROL 工具 > 工作流 > 模型]**。
1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面上，选择 **[!UICONTROL DAM 更新资产]**&#x200B;工作流模式。
1. 单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。
1. 展开侧面板以显示步骤。拖动 DAM 工作流部分中可用的&#x200B;**[!UICONTROL 智能标记资产]**&#x200B;步骤，并将其放在&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤之后。

   ![在 DAM 更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤](assets/chlimage_1-105.png)

   *图：在 DAM 更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤。*

1. 打开要配置的步骤。在&#x200B;**[!UICONTROL 高级设置]**&#x200B;下，确保选中&#x200B;**[!UICONTROL 处理程序前进]**&#x200B;选项。

   ![设置处理程序以前进到工作流中的下一步。](assets/smart-tags-workflow-handler-setting.png)

1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中，如果希望工作流在预测标记时忽略失败情况，请选择&#x200B;**[!UICONTROL 忽略错误]**。要在上传资产时标记资产，而不考虑是否对文件夹启用了智能标记，请选择&#x200B;**[!UICONTROL 忽略智能标记标志]**。

1. 单击&#x200B;**[!UICONTROL 确定]**，以关闭流程步骤，然后保存工作流。单击&#x200B;**[!UICONTROL 同步]**。

>[!MORELIKETHIS]
>
>* [使用智能服务标记资产](smart-tags.md)

