---
title: 管理域映射
description: 了解如何使用Cloud Manager编辑和更新，或删除Edge Delivery站点或Cloud Manager环境的CDN配置。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: a764a9d1e7d9fcd0be6abf9e2fb409346dc0f549
workflow-type: tm+mt
source-wordcount: '1073'
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

从&#x200B;**环境**&#x200B;页面编辑CDN配置的步骤与从“域映射”页面[&#128279;](#edit-cdn)编辑CDN配置的步骤几乎相同，但入口点不同。

**若要从环境页面编辑CDN配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 在左侧菜单中，单击![数据图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **环境**。

1. 在&#x200B;**环境**&#x200B;页面上，选择一个感兴趣的环境。

1. 在环境详细信息页面的域映射分组中，单击与要编辑的CDN配置相对应的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在弹出菜单中，单击&#x200B;**编辑**。

1. 在&#x200B;**编辑CDN配置**&#x200B;对话框中，在相应的下拉列表中设置一个或多个选项。

   对话框中显示的选项取决于您使用的是&#x200B;**Adobe托管的CDN**&#x200B;还是&#x200B;**其他CDN提供商** （客户托管的CDN）。

1. 单击&#x200B;**更新**。


## 上线准备：为自定义域配置DNS设置 {#go-live-readiness}

在自定义域可以提供流量之前，您必须先向DNS提供商完成DNS配置。 部署域映射并单击&#x200B;**上线**&#x200B;后，Cloud Manager会显示一个对话框，引导您完成DNS记录设置过程。 您可以通过添加CNAME记录类型或A记录类型来选择上线。

<!-- See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record). -->

**要配置上线准备工作：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。
1. 在左侧菜单的&#x200B;**服务**&#x200B;下，单击![社交网络图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **域映射**。
1. 在域映射表中，单击与要配置其上线就绪性的CDN对应的行末尾附近的&#x200B;**上线**。

   ![上线准备情况对话框](/help/implementing/cloud-manager/assets/domain-mappings-go-live-readiness.png)

1. 在&#x200B;**上线准备**&#x200B;对话框中，执行以下操作之一：

   | 选项 | 步骤 |
   | --- | --- |
   | 配置记录 | 建议对根域（如`example.com`<br>）使用<ol><li>登录到DNS服务提供商的门户。<li>转到DNS记录部分。<li>创建一个A记录以指向列出的所有IP地址。</li></ol> |
   | 配置 CNAME | 建议对自定义域（如`www.example.com`<br>）使用<ol><li>登录到DMS服务提供商的门户。<li>转到DNS记录部分。<li>在DNS服务提供商（您的自定义域）的DNS记录中映射`cdn.adobeaemcloud.com` （CNAME记录）。 此映射可确保将在自定义域中收到的请求重定向到Adobe的CDN。</li></ol> |

1. 在&#x200B;**上线准备工作**&#x200B;对话框中，单击&#x200B;**确定**&#x200B;保存记录。

   等待DNS传播；这可能需要几分钟到几小时。

   当域映射表中的&#x200B;**[!UICONTROL 状态]**&#x200B;列更新为&#x200B;**[!UICONTROL 已验证]**&#x200B;时，自定义域已准备就绪。 您可能需要单击![刷新图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg)来更新状态。

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

从&#x200B;**环境**&#x200B;页面中删除CDN配置的步骤与从“域映射”页面[&#128279;](#edit-cdn)中删除CDN配置的步骤几乎相同，但入口点不同。

**要从环境页面删除CDN配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 在左侧菜单中，单击![数据图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **环境**。

1. 在&#x200B;**环境**&#x200B;页面上，选择一个感兴趣的环境。

1. 在环境详细信息页面的&#x200B;**域映射**&#x200B;分组中，单击与要删除的CDN配置相对应的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后单击&#x200B;**删除**。

1. 在&#x200B;**删除CDN配置**&#x200B;对话框中，单击&#x200B;**删除**。

1. 再次单击&#x200B;**删除**&#x200B;以确认删除网站的CDN。
