---
title: 使用具有OpenAPI功能的Dynamic Media限制资源交付
description: 了解如何使用OpenAPI功能限制资源交付。
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 2%

---

# 使用具有OpenAPI功能的Dynamic Media限制资源交付 {#restrict-access-to-assets}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>Dynamic Media with OpenAPI功能指南现在以PDF格式提供。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE 具有OpenAPI功能的Dynamic Media指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Manager中的中央资产治理允许DAM管理员或品牌管理员通过OpenAPI功能管理对Dynamic Media可用资产的访问。 他们可以通过在Identity Management AEM as a Cloud Service System (IMS)Adobe服务上的资源上配置某些元数据，将已批准的资源（精确到单个资源）限制为选定的[元数据用户或组](https://helpx.adobe.com/in/enterprise/using/users.html#user-mgt-strategy)。

一旦通过具有OpenAPI的Dynamic Media限制资源，则只有有权访问所述资源的（已载入Adobe IMS）用户才被授予访问权限。 要访问该资源，用户必须使用Dynamic Media的OpenAPI的[搜索](search-assets-api.md)和[交付](deliver-assets-apis.md)功能。

![限制了对资源的访问](/help/assets/assets/restricted-access.png)

在Experience Manager Assets中，通过IMS进行的受限投放涉及两个关键阶段：

* 创作
* 交付

## 创作 {#authoring}

### 使用IMS持有者令牌的受限投放 {#restrict-delivery-ims-token}

您可以根据IMS用户和组身份限制[!DNL Experience Manager]内资源的投放。

>[!NOTE]
>
此功能当前不是自助服务。 要限制IMS [用户](https://helpx.adobe.com/in/enterprise/using/manage-directory-users.html)和[组](https://helpx.adobe.com/in/enterprise/using/user-groups.html)的资源投放，请联系您的企业支持团队，以获取有关如何检索限制访问[Adobe Admin Console](https://adminconsole.adobe.com/)门户所需的信息以及如何在AEM as a Cloud Service创作服务中配置访问权限的指导。

### 使用开启和关闭日期和时间限制资源的交付 {#restrict-delivery-assets-date-time}

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



## 受限资产的交付 {#delivery-restricted-assets}

受限资产的交付基于访问资产的成功授权。 授权是通过[IMS持有者令牌](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/IMS/)(用于从[AEM Asset Selector](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)启动的请求的应用程序)或安全Cookie(如果您在AEM Publish/Preview服务上设置了自定义身份提供程序，并在页面上设置了Cookie创建和包含)进行的。

### AEM创作或资源选择器请求的投放 {#delivery-aem-author-asset-selector}

要在从AEM创作服务或AEM Asset Selector发送请求时启用受限资源的投放，有效的IMS持有者令牌至关重要。\
在AEM Cloud Service创作服务和Asset Selector上，会自动生成IMS持有者令牌并在成功登录后用于请求。

>[!NOTE]
>
要详细了解如何在基于AEM Asset Selector的集成上启用IMS身份验证，请联系企业支持

1. 对于非基于资产选择器的体验，具有OpenAPI功能的AEM as a Cloud Service和Dynamic Media当前支持服务器端API集成，并可生成IMS持有者令牌。
   * 按照[此处](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#the-server-to-server-flow)的说明执行服务到服务器API集成，这些集成可以通过[AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console)检索IMS持有者令牌
   * 在有限持续时间内，本地开发人员访问（不适用于生产用例）可通过按照[此处](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#developer-flow)的说明生成[AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console)上身份验证的用户的短期IMS持有者令牌

1. 在发出[Search](search-assets-api.md)和[Delivery](deliver-assets-apis.md) API请求时，将获取的IMS持有者令牌添加到HTTP请求的&#x200B;**[!UICONTROL Authorization]**&#x200B;标头中（请确保其值带有&#x200B;**[!UICONTROL 持有者]**&#x200B;前缀）。

1. 要验证访问限制，请启动传递API请求，该请求带有或不带&#x200B;**[!UICONTROL Authorization]**&#x200B;标头。
   * 如果没有IMS持有者令牌，或提供的IMS持有者令牌不属于被授予资产访问权限（直接或通过组成员资格）的用户，响应将生成`404`错误状态代码。
   * 如果IMS持有者令牌是被授予资产访问权限的一个或多个用户组之一，则响应将为资产的二进制内容生成`200`成功状态代码。

### 在Publish服务上交付自定义身份提供程序 {#delivery-custom-identity-provider}

可将AEM Sites、AEM Assets和具有OpenAPI许可证的Dynamic Media结合使用，允许在托管在AEM Publish或预览服务上的网站上配置受限的资产交付。 安全交付流利用浏览器Cookie建立用户的访问权限，并具有作为发布域子域的交付层的自定义域，是实施此用例的先决条件。 如果AEM Sites的Publish和预览服务配置为使用[自定义身份提供程序(IdP)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)，则必须在发布域发布用户的身份验证上设置一个名为`delivery-token`的新Cookie，封装用户的组成员资格。 投放层从安全Cookie中提取授权材料并验证访问。 有关更多详细信息，请记录[企业支持票证](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities)。
