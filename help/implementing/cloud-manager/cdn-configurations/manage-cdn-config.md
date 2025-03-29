---
title: 管理域映射
description: 了解如何使用Cloud Manager编辑和更新，或删除Edge Delivery站点或Cloud Manager环境的CDN配置。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: 41155a724f48ad28a12aac615a3e9a13bb3afa26
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 8%

---

# 管理域映射 {#manage-cdn-configurations}

了解如何使用Cloud Manager编辑或删除Edge Delivery站点或Cloud Manager环境的CDN配置。

## 从域映射页面编辑CDN配置 {#edit-cdn}

在Adobe Cloud Manager中，出于多种原因，您可能希望编辑CDN（内容分发网络）配置，包括环境层（发布或预览）和SSL证书。

* **环境更改**：调整层有助于将CDN设置与正确的环境相匹配，无论是用于实时生产（发布）还是测试（预览）。
* **安全增强功能**：在更新证书或解决合规性和安全需求时，可能需要选择其他SSL证书。
* **优化性能**：编辑配置可以确保根据不断变化的操作需求交付内容的CDN设置正确无误。

您可以编辑配置，而无需完全删除现有配置。 更改适用于选定的环境（例如，暂存或生产），并可能会影响内容的交付和保护方式。

用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的成员才能完成此任务。

**若要从域映射页面编辑CDN配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。
1. 在左侧菜单的&#x200B;**服务**&#x200B;下，单击![社交网络图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **域映射**。
1. 在&#x200B;**域映射**&#x200B;表中，单击要更新其CDN配置的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 从下拉菜单中，单击&#x200B;**编辑**。

1. 在&#x200B;**编辑CDN配置**&#x200B;对话框中，在相应的下拉列表中设置一个或多个选项。

   对话框中显示的选项取决于您使用的是&#x200B;**Adobe托管的CDN**&#x200B;还是&#x200B;**其他CDN提供商** （客户托管的CDN）。

1. 单击&#x200B;**更新**。

   已编辑CDN的状态将在&#x200B;**域映射**&#x200B;表中更新，以反映您所做的更改。


## 从环境页面编辑CDN配置

从&#x200B;**环境**&#x200B;页面编辑CDN配置的步骤与从“域映射”页面](#edit-cdn)编辑CDN配置的步骤[几乎相同，但入口点不同。

**若要从环境页面编辑CDN配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 在左侧菜单中，单击![数据图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **环境**。

1. 在&#x200B;**环境**&#x200B;页面上，选择一个感兴趣的环境。

1. 在环境详细信息页面的域映射分组中，单击与要编辑的CDN配置相对应的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在弹出菜单中，单击&#x200B;**编辑**。

1. 在&#x200B;**编辑CDN配置**&#x200B;对话框中，在相应的下拉列表中设置一个或多个选项。

   对话框中显示的选项取决于您使用的是&#x200B;**Adobe托管的CDN**&#x200B;还是&#x200B;**其他CDN提供商** （客户托管的CDN）。

1. 单击&#x200B;**更新**。

<!-- 
## Go live readiness: Configure DNS settings for a custom domain {#go-live-readiness} 

Before a custom domain can serve traffic in Adobe Cloud Manager, you must complete DNS configuration with your DNS provider. After deploying a domain mapping and clicking **Go live**, Cloud Manager displays a dialog box that guides you through the DNS record setup process. You have the option to go live by adding either a CNAME record type or an A record type representing Fastly's IPs, simplifying domain routing. This ability eliminates the restriction of relying solely on CNAME records for domain setup with Fastly.

MAYBE There is support for A record types to improve Go Live readiness for domains using CDN configurations in AEM Cloud Manager. MAYBE

See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record).

**To configure Go live readiness:**

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate organization and program.

1. In the left side menu, under **Services**, click ![Social network icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Domain Mappings**.

1. In the Domain Mappings table, click **Go live** near the end of a row that corresponds to a CDN whose Go Live readiness you want to configure. 

1. In the Go live readiness dialog box, do one of the following:

    | Configure  | Steps |
    | --- | --- |
    | A RECORD | Recommended for root domains like `example.com`<br><ol><li>Log in to your DNS service provider's portal.<li>Go to the DNS Records section.<li>Create an A record to point to all the listed IP addresses.<li>In the Go live readiness dialog box, click **OK**.<li>In the Domain Mappings table, under the **Status** column, click ![Refresh icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg).<br>The status is updated to **Verified** when the resolution is complete.</li></ol> |
    | CNAME | Recommended for custom domains like `www.example.com`<br><ol><li>Log in to your DMS service provider's portal.<li>Go to the DNS Records section.<li>Map [cdn.adobeaemcloud.com](http://cdn.adobeaemcloud.com/) (CNAME record) in the DNS record of the DNS service provider (your custom domain). This mapping ensures that requests received at the custom domain are redirected to Adobe's CDN.<li>In the **Go live readiness** dialog box, click **OK** to save the record.<br>Wait for DNS propogation (may take several minutes to a few hours). When the **[!UICONTROL Status]** column in the Domamin Mappings table updates to **[!UICONTROL Verified]**, the custom domain is ready to use. You may need to click ![Refresh icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) to refresh the status.</li></ol> | 
    
-->

## 删除CDN配置 {#delete-cdn}

在Cloud Manager中删除Adobe托管或客户托管的CDN配置时，将删除关联的域的路由和SSL证书设置。 域不再使用CDN进行流量交付，并且CDN提供的任何安全或性能增强功能都会丢失。 在设置新配置之前，无论重新添加已删除的CDN还是添加新配置，您都可能会遇到服务中断问题。

用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的成员才能完成此任务。

**要删除CDN配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 在左侧菜单的&#x200B;**服务**&#x200B;下，单击![社交网络图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **域映射**。

1. 在域映射表中，单击与要删除的CDN对应的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后单击&#x200B;**删除**。

1. 在&#x200B;**删除CDN配置**&#x200B;对话框中，单击&#x200B;**删除**。

1. 再次单击&#x200B;**删除**&#x200B;以确认删除网站的CDN。


## 从环境页面删除CDN配置

从&#x200B;**环境**&#x200B;页面中删除CDN配置的步骤与从“域映射”页面](#edit-cdn)中删除CDN配置的步骤[几乎相同，但入口点不同。

**要从环境页面删除CDN配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 在左侧菜单中，单击![数据图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **环境**。

1. 在&#x200B;**环境**&#x200B;页面上，选择一个感兴趣的环境。

1. 在环境详细信息页面的&#x200B;**域映射**&#x200B;分组中，单击与要删除的CDN配置相对应的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后单击&#x200B;**删除**。

1. 在&#x200B;**删除CDN配置**&#x200B;对话框中，单击&#x200B;**删除**。

1. 再次单击&#x200B;**删除**&#x200B;以确认删除网站的CDN。
