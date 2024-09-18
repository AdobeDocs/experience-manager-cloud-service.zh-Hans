---
title: 管理CDN配置
description: 了解如何使用Cloud Manager编辑和更新，或删除Edge Delivery站点或Cloud Manager环境的CDN配置。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8e2fc0d4ee82e79d1a822a528b1a46acce3c192a
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 6%

---


# 管理CDN配置 {#manage-cdn-configurations}

了解如何使用Cloud Manager编辑和更新，或删除Edge Delivery站点或Cloud Manager环境的CDN配置。

## 编辑CDN配置 {#edit-cdn}

在AdobeCloud Manager中，出于多种原因，您可能想要编辑CDN配置，包括环境层(Publish或预览)和SSL证书。

* **环境更改**：调整层有助于将CDN设置与正确的环境相匹配，无论是用于实时生产(Publish)还是测试（预览）。
* **安全增强功能**：在更新证书或解决合规性和安全需求时，可能需要选择其他SSL证书。
* **优化性能**：编辑配置可以确保根据不断变化的操作需求交付内容的CDN设置正确无误。

您可以编辑配置，而无需完全删除现有配置。 更改适用于选定的环境（例如，暂存或生产），并可能会影响内容的交付和保护方式。

用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的成员才能完成此任务。

**要编辑CDN配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。
1. 在左侧导航面板中的&#x200B;**服务**&#x200B;下，单击&#x200B;**CDN配置**。
1. 在&#x200B;**CDN配置**&#x200B;表中，单击要编辑其CDN配置的行末尾的省略号。

   ![编辑CDN配置](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. 单击&#x200B;**编辑**。
1. 在&#x200B;**编辑CDN配置**&#x200B;对话框中，在相应的下拉列表中设置一个或多个选项。

   根据您使用的是Adobe管理的CDN还是客户管理的CDN，您在对话框中看到的选项可能会有所不同。

1. 单击&#x200B;**更新**。

   已编辑CDN的状态将在&#x200B;**CDN配置**&#x200B;表中更新，以反映您所做的更改。

## 删除CDN配置 {#delete-cdn}

在AdobeCloud Manager中删除Adobe管理或客户管理的CDN配置时，将删除关联的域的路由和SSL证书设置。 域不再使用CDN进行流量交付，并且CDN提供的任何安全或性能增强功能都会丢失。 在设置新配置之前，无论重新添加已删除的CDN还是添加新配置，您都可能会遇到服务中断问题。

用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的成员才能完成此任务。

**要删除CDN配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 在左侧导航面板中的&#x200B;**服务**&#x200B;下，单击&#x200B;**CDN配置**。

1. 在CDN配置表中，单击要删除其CDN的行末尾的省略号。

   ![正在删除CDN配置](/help/implementing/cloud-manager/assets/cdn-config-delete.png)

1. 单击&#x200B;**删除**。
1. 再次单击&#x200B;**删除**&#x200B;以确认删除网站的CDN。


