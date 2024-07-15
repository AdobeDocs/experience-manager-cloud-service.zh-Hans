---
title: 限制Experience Manager中的资源投放
description: 了解如何在 [!DNL Experience Manager]中限制资源交付。
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# 限制对[!DNL Experience Manager]中资产的访问 {#restrict-access-to-assets}

Experience Manager中的中央资产治理允许DAM管理员或品牌经理管理对资产的访问。 他们可以通过在创作端(特别是在AEM as a Cloud Service创作实例上)为批准的资源配置角色来限制访问。

成功通过授权过程后，用户[搜索](search-assets-api.md)或利用[投放URL](deliver-assets-apis.md)可以获得对受限资产的访问权限。

![限制了对资源的访问](/help/assets/assets/restricted-access.png)

## 使用IMS令牌的受限制投放 {#restrict-delivery-ims-token}

在Experience Manager中，通过IMS进行的受限投放涉及两个关键阶段：

* 创作
* 交付

### 创作 {#authoring}

您可以根据角色限制[!DNL Experience Manager]内资源的投放。 要配置角色，请执行以下步骤：

1. 以DAM管理员身份转到[!DNL Experience Manager]。
1. 选择需要为其配置角色的资源。
1. 导航到&#x200B;**[!UICONTROL 属性]** > **[!UICONTROL 高级]**，并确保[!UICONTROL 高级元数据]选项卡中存在&#x200B;**[!UICONTROL 角色]**&#x200B;字段。

   ![角色元数据](/help/assets/assets/roles_metadata.jpg)
如果该字段不可用，请使用以下步骤添加该字段：

   1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。
   1. 选择元数据架构并单击&#x200B;**[!UICONTROL 编辑&#x200B;_(e)_]**。
   1. 从表单右侧的&#x200B;**[!UICONTROL 构建表单]**&#x200B;分区向元数据分区添加一个&#x200B;**[!UICONTROL 多值文本]**&#x200B;字段。
   1. 单击新添加的字段，然后在&#x200B;**[!UICONTROL 设置]**&#x200B;面板中进行以下更新：
      1. 将&#x200B;**[!UICONTROL 字段标签]**&#x200B;更改为&#x200B;_角色_。
      1. 将&#x200B;**[!UICONTROL 映射到属性]**&#x200B;的更新为&#x200B;_。/jcr：content/metadata/dam：roles_。

1. 获取要添加到资源的角色元数据中的IMS组。 要获取IMS组，请执行以下步骤：
   1. 登录到https://adminconsole.adobe.com/。
   1. 转到相应的组织并导航到&#x200B;**[!UICONTROL 用户组]**。
   1. 选择要添加的&#x200B;**[!UICONTROL 用户组]**，并从URL中提取&#x200B;**[!UICONTROL orgID]**&#x200B;和&#x200B;**[!UICONTROL userGroupID]**，或者使用您的组织ID，例如`{orgID}@AdobeOrg:{usergroupID}`。

1. 将组ID添加到资产属性的&#x200B;**[!UICONTROL 角色]**&#x200B;字段。 <br>
在**[!UICONTROL 角色]**&#x200B;字段中定义的组ID是唯一可访问该资源的用户。 您还可以在&#x200B;**[!UICONTROL 角色]**&#x200B;字段中添加IMS客户端ID和IMS配置文件ID。 例如：`{orgId}@AdobeOrg:{profileId}`。

   >[!NOTE]
   >
   >对于新的Assets视图，您只能将访问权限仅授予文件夹级别，并仅授予组而非单个用户。 了解有关[在Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions)中管理权限的详细信息。

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### 使用开启和关闭日期和时间限制资源的交付 {#restrict-delivery-assets-date-time}

DAM作者还可以通过定义资产属性中可用的激活的开启或关闭时间来限制资产的交付。

如果您为资产的激活定义准时，则会在定义的时间为资产生成投放URL。 在定义的时间之前，资产保持不活动状态。 同样，如果您为资产定义关闭时间，则会在定义的时间停用资产，并且资产的投放URL停止显示资产。

执行以下步骤，设置资产的开启时间和关闭时间：

1. 选择资产并单击&#x200B;**[!UICONTROL 属性]**。

1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡的&#x200B;**[!UICONTROL 计划（取消）激活]**&#x200B;部分中，根据您的要求定义开始时间或结束时间。

同样，在Assets视图中，您可以选择资源并单击&#x200B;**[!UICONTROL 详细信息]**&#x200B;以查看资源属性并定义开启时间和关闭时间。

该字段在默认元数据表单中可用。 如果您的资产不是基于默认元数据架构，并且资产属性中的开启时间和关闭时间字段不可用，请在管理员视图中执行以下步骤：

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。
1. 选择元数据架构并单击&#x200B;**[!UICONTROL 编辑]**。
1. 将右侧&#x200B;**[!UICONTROL 构建表单]**&#x200B;分区中的&#x200B;**[!UICONTROL Date]**&#x200B;字段添加到表单中的元数据分区。
1. 单击新添加的字段，然后在&#x200B;**[!UICONTROL 设置]**&#x200B;面板中进行以下更新：
   1. 将&#x200B;**[!UICONTROL 字段标签]**&#x200B;更改为&#x200B;**开始时间**&#x200B;或&#x200B;**结束时间**。
   1. 将&#x200B;**[!UICONTROL 映射到属性]**&#x200B;的更新为&#x200B;_。/jcr：content/onTime_&#x200B;用于&#x200B;**On Time**&#x200B;字段和&#x200B;_。/jcr：content/offTime_&#x200B;用于&#x200B;**关闭时间**&#x200B;字段。
1. 单击&#x200B;**[!UICONTROL 保存]**。

同样，对于Assets视图，如果您的资源不是基于默认元数据架构，并且资源属性中的开启时间和关闭时间字段不可用，请执行以下步骤：

1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;部分中单击&#x200B;**[!UICONTROL 元数据Forms]**。
1. 选择元数据表单，然后单击&#x200B;**[!UICONTROL 编辑]**。
1. 从左窗格中的&#x200B;**[!UICONTROL 组件]**&#x200B;部分添加一个&#x200B;**[!UICONTROL 日期]**&#x200B;字段到表单中。
1. 单击新添加的字段并将&#x200B;**[!UICONTROL 标签]**&#x200B;更改为&#x200B;**开始时间**&#x200B;或&#x200B;**结束时间**。
1. 将&#x200B;**[!UICONTROL 元数据属性]**&#x200B;更新为&#x200B;_。/jcr：content/onTime_&#x200B;用于&#x200B;**On Time**&#x200B;字段和&#x200B;_。/jcr：content/offTime_&#x200B;用于&#x200B;**关闭时间**&#x200B;字段。
1. 单击&#x200B;**[!UICONTROL 保存]**。



### 受限资产的交付 {#delivery-restricted-assets}

受限资产的交付基于访问资产的成功授权。 如果请求是从AEM创作实例或资源选择器发送的，则授权基于IMS令牌，或者如果您Publish或预览实例上设置了自定义身份提供程序，授权则基于特殊Cookie。

#### AEM创作或资源选择器请求的投放 {#delivery-aem-author-asset-selector}

要在从AEM创作实例或资产选择器发送请求时启用受限资产的投放，有效的IMS令牌至关重要。 请按照以下步骤操作：

1. [生成访问令牌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)。
   * 登录到您的AEM as a Cloud Service环境的开发控制台。

   * 导航到&#x200B;**[!UICONTROL 环境]** > **[!UICONTROL 集成]** > **[!UICONTROL 本地令牌]** > **[!UICONTROL 获取本地开发令牌]** > **[!UICONTROL 复制accessToken值]**。 了解有关[如何访问令牌和相关方面的更多信息](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. 将获得的访问令牌集成到&#x200B;**[!UICONTROL 授权]**&#x200B;标头，确保其值以&#x200B;**[!UICONTROL 持有者]**&#x200B;为前缀。

1. 通过启动请求来验证访问令牌的功能。 如果没有IMS访问令牌，或提供的访问令牌缺少与资产元数据中添加的令牌相同的主体或组，则会产生404错误。

#### Publish实例上自定义身份提供程序的投放 {#delivery-custom-identity-provider}

如果您在Publish或“预览”实例上设置自定义身份提供程序，则可以在设置过程中提及必须有权访问`groupMembership`属性内安全资产的组。 当您通过[SAML集成](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)登录到自定义身份提供程序时，将读取`groupMembership`属性并用于构造Cookie，在所有身份验证请求中都会发送该Cookie，类似于IMS令牌(如果来自AEM作者或资产选择器的请求)。

当页面上有安全资产并且向投放URL发出渲染资产的请求时，AEM检查Cookie或IMS令牌中存在的角色，并将其与资产创作期间应用的`dam:roles property`匹配。 如果存在匹配项，则会显示资源。

>[!NOTE]
>
> 在用于激活具有OpenAPI功能的Dynamic Media的[支持工单中](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities)，提及用例中的受限投放。 Adobe工程部将帮助进行必要的澄清和/或为受限交付设置流程。
