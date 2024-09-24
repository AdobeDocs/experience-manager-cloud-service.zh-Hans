---
title: 管理自定义域名
description: 了解如何使用 Cloud Manager 查看、更新、替换和删除自定义域名。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2d1382c84d872719332986baa5829d1623d9d9a6
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 34%

---


# 管理自定义域名 {#managing-custom-domain-names}

Cloud Manager允许您编辑、更新、替换和删除自定义域名。

## 编辑自定义域名配置 {#view-and-update}

在AdobeCloud Manager中，您可能想要编辑自定义域名配置，原因如下：

* **切换环境**：根据您是向最终用户(Publish)还是内部用户（创作）提供内容，应用正确的配置。
* **安全更新**：升级到较新的SSL证书，以增强安全性或合规性。
* **更改部署策略**：确保将正确的SSL证书应用于特定环境，以便正确加密和访问站点。

**要编辑自定义域名配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 在页面的左上角，单击汉堡图标以显示左侧导航菜单。
1. 在&#x200B;**服务**&#x200B;标题下，单击&#x200B;**CDN配置**。
1. 在&#x200B;**CDN配置**&#x200B;页面上，单击要编辑其CDN的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 单击&#x200B;**编辑**。
1. 在&#x200B;**编辑CDN配置**&#x200B;对话框中，执行以下操作：
   * 在&#x200B;**层**&#x200B;下拉列表中，选择要使用的层(Publish或预览)。
   * 在&#x200B;**SSL证书**&#x200B;下拉列表中，选择要使用的SSL证书。
1. 单击&#x200B;**更新**。


## 更新自定义域名的SSL证书 {#update-cert}

您可以按照[相同的步骤查看和更新自定义域名](#view-and-update)，从而更新自定义域名的 SSL 证书。

>[!NOTE]
>
>SSL证书必须有效，[已配置](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)，并包含要更新的自定义域名。


## 删除自定义域名 {#deleting}

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以使用 Cloud Manager 删除自定义域名。

### 从所有关联的环境中删除自定义域名 {#delete-cdn-all}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**概述**&#x200B;屏幕导航到&#x200B;**域设置**&#x200B;页面。

1. 确定要删除的自定义域名的行。

1. 单击行最右端的省略号按钮。

1. 选择&#x200B;**删除**。

1. 确认您的提交。


### 从特定环境中删除自定义域名 {#delete-cdn-specific}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。
1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。
1. 从&#x200B;**环境**&#x200B;页面，导航到感兴趣环境的详细信息屏幕。
1. 从域名表中，标识要删除的自定义域名的行。
1. 单击行最右端的省略号按钮。
1. 选择&#x200B;**删除**。
1. 确认您的提交。
