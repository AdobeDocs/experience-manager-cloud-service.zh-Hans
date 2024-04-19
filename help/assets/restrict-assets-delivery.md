---
title: 限制Experience Manager中的资源投放
description: 了解如何在中限制资源交付 [!DNL Experience Manager].
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 限制对中的资源的访问 [!DNL Experience Manager] {#restrict-access-to-assets}

Experience Manager中的中央资产治理允许DAM管理员或品牌经理管理对资产的访问。 它们可以通过在创作端(特别是在AEMas a Cloud Service创作实例上)为批准的资源配置角色来限制访问。

用户 [搜索](search-assets-api.md) 或利用 [投放URL](deliver-assets-apis.md) 成功通过授权流程后，可以获得对受限制资产的访问权限。

![限制了对资源的访问](/help/assets/assets/restricted-access.png)

## 使用IMS令牌的受限制投放 {#restrict-delivery-ims-token}

在Experience Manager中，通过IMS进行的受限投放涉及两个关键阶段：

* 创作
* 交付

### 创作 {#authoring}

要限制资源的投放，必须为以下范围内的资源配置角色： [!DNL Experience Manager] 或 [!DNL Experience Manager Assets]. 在中配置角色 [!DNL Experience Manager]，请按照以下步骤操作：

1. 转到 [!DNL Experience Manager] 作为DAM管理员。
1. 选择需要为其配置角色的资源。
1. 导航到 **[!UICONTROL 属性]** > **[!UICONTROL 高级]**，并确保 **[!UICONTROL 角色]** 字段存在于中 [!UICONTROL 高级元数据] 选项卡。

   ![角色元数据](/help/assets/assets/roles_metadata.jpg)
如果该字段不可用，请使用以下步骤添加该字段：

   1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**.
   1. 选择元数据架构并单击 **[!UICONTROL 编辑 _(e)_]**.
   1. 添加 **[!UICONTROL 多值文本]** 中的字段 **[!UICONTROL 构建表单]** 区域到表单中的元数据区域的位置。
   1. 单击新添加的字段，然后在  **[!UICONTROL 设置]** 面板：
      1. 更改 **[!UICONTROL 字段标签]** 到 _角色_.
      1. 更新 **[!UICONTROL 映射到属性]** 到 _./jcr：content/metadata/dam：roles_.

1. 获取要添加到资源的角色元数据中的IMS组。 要获取IMS组，请执行以下步骤：
   1. 登录到https://adminconsole.adobe.com/。
   1. 转到您各自的组织，然后导航到 **[!UICONTROL 用户组]**.
   1. 选择 **[!UICONTROL 用户组]** 您需要添加并提取 **[!UICONTROL orgID]** 和 **[!UICONTROL 用户组ID]** 或使用您的组织ID，例如 `{orgID}@AdobeOrg:{usergroupID}`.

1. 将组ID添加到 **[!UICONTROL 角色]** 资产属性的字段。 <br>
中定义的组ID **[!UICONTROL 角色]** 字段是唯一可访问该资源的用户。 您还可以在中添加IMS客户端ID和IMS配置文件ID **[!UICONTROL 角色]** 字段。 例如：`{orgId}@AdobeOrg:{profileId}`。

   >[!NOTE]
   >
   >对于新的Assets视图，您只能将访问权限授予文件夹级别，并且只能授予组而非单个用户。 了解有关 [在Experience Manager Assets中管理权限](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

### 受限资产的交付 {#delivery-restricted-assets}

受限资产的交付基于访问资产的成功授权。 如果请求是从AEM创作实例或资产选择器发送的，则授权基于IMS令牌，或者如果您的发布或预览实例设置了自定义身份提供程序，授权则基于特殊Cookie。

#### AEM创作或资源选择器的投放 {#delivery-aem-author-asset-selector}

要在从AEM创作实例或资产选择器发送请求时启用受限资产的投放，有效的IMS令牌至关重要。 请按照以下步骤操作：

1. [生成访问令牌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * 登录到AEMas a Cloud Service环境的开发控制台。

   * 导航到 **[!UICONTROL 环境]** > **[!UICONTROL 集成]** > **[!UICONTROL 本地令牌]** > **[!UICONTROL 获取本地开发令牌]** > **[!UICONTROL 复制accessToken值]**. 了解有关 [如何访问令牌和相关方面](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. 将获得的访问令牌集成到 **[!UICONTROL 授权]** 标头，确保其值带有前缀 **[!UICONTROL 持有者]**.

1. 通过启动请求来验证访问令牌的功能。 如果没有IMS访问令牌，或提供的访问令牌缺少与资产元数据中添加的令牌相同的主体或组，则会产生404错误。

#### 自定义身份提供程序的投放 {#delivery-custom-identity-provider}

如果您的发布或预览实例设置了自定义身份提供程序，则可以提及必须有权访问中安全资产的组。 `groupMembership` 属性。 当您通过登录到自定义身份提供程序时 [SAML集成](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)， `groupMembership` 属性会被读取并用于构造Cookie，在所有身份验证请求中发送它，类似于IMS令牌(如果来自AEM创作或资产选择器的请求)。

当页面上有安全资产并且向投放URL发出呈现资产的请求时，AEM检查Cookie或IMS令牌中存在的角色，并将其与匹配 `dam:roles property` 在创作资产期间应用。 如果存在匹配项，则会显示资源。
