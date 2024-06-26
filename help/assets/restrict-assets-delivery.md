---
title: 限制Experience Manager中的资源投放
description: 了解如何在中限制资源交付 [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# 限制对中的资源的访问 [!DNL Experience Manager] {#restrict-access-to-assets}

Experience Manager中的中央资产治理允许DAM管理员或品牌经理管理对资产的访问。 他们可以通过在创作端(特别是在AEM as a Cloud Service创作实例上)为批准的资源配置角色来限制访问。

用户 [搜索](search-assets-api.md) 或利用 [投放URL](deliver-assets-apis.md) 成功通过授权流程后，可以获得对受限制资产的访问权限。

![限制了对资源的访问](/help/assets/assets/restricted-access.png)

## 使用IMS令牌的受限制投放 {#restrict-delivery-ims-token}

在Experience Manager中，通过IMS进行的受限投放涉及两个关键阶段：

* 创作
* 交付

### 创作 {#authoring}

您可以限制以下范围内的资产交付 [!DNL Experience Manager] 基于角色。 要配置角色，请执行以下步骤：

1. 转到 [!DNL Experience Manager] 作为DAM管理员。
1. 选择需要为其配置角色的资源。
1. 导航到 **[!UICONTROL 属性]** > **[!UICONTROL 高级]**，并确保 **[!UICONTROL 角色]** 字段存在于中 [!UICONTROL 高级元数据] 选项卡。

   ![角色元数据](/help/assets/assets/roles_metadata.jpg)
如果该字段不可用，请使用以下步骤添加该字段：

   1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**.
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
   >对于新的Assets视图，您只能将访问权限仅授予文件夹级别，并仅授予组而非单个用户。 了解有关 [在Experience Manager Assets中管理权限](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### 使用开启和关闭日期和时间限制资源的交付 {#restrict-delivery-assets-date-time}

DAM作者还可以通过定义资产属性中可用的激活的开启或关闭时间来限制资产的交付。

如果您为资产的激活定义准时，则会在定义的时间为资产生成投放URL。 在定义的时间之前，资产保持不活动状态。 同样，如果您为资产定义关闭时间，则会在定义的时间停用资产，并且资产的投放URL停止显示资产。

执行以下步骤，设置资产的开启时间和关闭时间：

1. 选择资源并单击 **[!UICONTROL 属性]**.

1. 在 **[!UICONTROL 已计划（取消）激活]** 的部分 **[!UICONTROL 基本]** 选项卡，根据您的要求定义开始时间或结束时间。

同样，在Assets视图中，您可以选择资源并单击 **[!UICONTROL 详细信息]** 查看资源属性并定义开启时间和关闭时间。

该字段在默认元数据表单中可用。 如果您的资产不是基于默认元数据架构，并且资产属性中的开启时间和关闭时间字段不可用，请在管理员视图中执行以下步骤：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**.
1. 选择元数据架构并单击 **[!UICONTROL 编辑]**.
1. 添加 **[!UICONTROL 日期]** 中的字段 **[!UICONTROL 构建表单]** 区域到表单中的元数据区域的位置。
1. 单击新添加的字段，然后在  **[!UICONTROL 设置]** 面板：
   1. 更改 **[!UICONTROL 字段标签]** 到 **准时** 或 **关闭时间**.
   1. 更新 **[!UICONTROL 映射到属性]** 到 _./jcr：content/onTime_ 对象 **准时** 字段和 _./jcr：content/offTime_ 对象 **关闭时间** 字段。
1. 单击&#x200B;**[!UICONTROL 保存]**。

同样，对于Assets视图，如果您的资源不是基于默认元数据架构，并且资源属性中的开启时间和关闭时间字段不可用，请执行以下步骤：

1. 单击 **[!UICONTROL 元数据Forms]** 在 **[!UICONTROL 设置]** 部分。
1. 选择元数据表单并单击 **[!UICONTROL 编辑]**.
1. 添加 **[!UICONTROL 日期]** 中的字段 **[!UICONTROL 组件]** 部分添加到表单中。
1. 单击新添加的字段并更改 **[!UICONTROL 标签]** 到 **准时** 或 **关闭时间**.
1. 更新 **[!UICONTROL 元数据属性]** 到 _./jcr：content/onTime_ 对象 **准时** 字段和 _./jcr：content/offTime_ 对象 **关闭时间** 字段。
1. 单击&#x200B;**[!UICONTROL 保存]**。



### 受限资产的交付 {#delivery-restricted-assets}

受限资产的交付基于访问资产的成功授权。 如果请求是从AEM创作实例或资源选择器发送的，则授权基于IMS令牌，或者如果您Publish或预览实例上设置了自定义身份提供程序，授权则基于特殊Cookie。

#### AEM创作或资源选择器请求的投放 {#delivery-aem-author-asset-selector}

要在从AEM创作实例或资产选择器发送请求时启用受限资产的投放，有效的IMS令牌至关重要。 请按照以下步骤操作：

1. [生成访问令牌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * 登录到您的AEM as a Cloud Service环境的开发控制台。

   * 导航到 **[!UICONTROL 环境]** > **[!UICONTROL 集成]** > **[!UICONTROL 本地令牌]** > **[!UICONTROL 获取本地开发令牌]** > **[!UICONTROL 复制accessToken值]**. 了解有关 [如何访问令牌和相关方面](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. 将获得的访问令牌集成到 **[!UICONTROL 授权]** 标头，确保其值带有前缀 **[!UICONTROL 持有者]**.

1. 通过启动请求来验证访问令牌的功能。 如果没有IMS访问令牌，或提供的访问令牌缺少与资产元数据中添加的令牌相同的主体或组，则会产生404错误。

#### Publish实例上自定义身份提供程序的投放 {#delivery-custom-identity-provider}

如果您在Publish或预览实例上设置自定义身份提供程序，则可以提及必须有权访问中安全资产的组。 `groupMembership` 属性。 当您通过登录到自定义身份提供程序时 [SAML集成](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)， `groupMembership` 属性会被读取并用于构造Cookie，在所有身份验证请求中发送它，类似于IMS令牌(如果来自AEM创作或资产选择器的请求)。

当页面上有安全资产并且向投放URL发出呈现资产的请求时，AEM检查Cookie或IMS令牌中存在的角色，并将其与匹配 `dam:roles property` 在创作资产期间应用。 如果存在匹配项，则会显示资源。

>[!NOTE]
>
> 在 [用于激活具有OpenAPI功能的Dynamic Media的支持票证](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities)，在使用案例中提及受限投放。 Adobe工程部将帮助进行必要的澄清和/或为受限交付设置流程。
