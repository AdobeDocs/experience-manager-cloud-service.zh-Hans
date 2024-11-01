---
title: 管理自定义域名
description: 了解如何使用 Cloud Manager 查看、更新、替换和删除自定义域名。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f64a551bc18b53d0026736ece2a44e48cd0cfb4c
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 19%

---


# 管理自定义域名 {#managing-custom-domain-names}

Cloud Manager允许您编辑、更新、替换、验证和删除自定义域名。

## 编辑自定义域名配置 {#view-and-update}

在AdobeCloud Manager中，您可能想要编辑自定义域名配置，原因如下：

* **切换环境**：根据您是向最终用户(Publish)还是内部用户（创作）提供内容，应用正确的配置。
* **安全更新**：升级到较新的SSL证书，以增强安全性或合规性。
* **更改部署策略**：确保将正确的SSL证书应用于特定环境，以便进行正确的加密和站点访问。

**要编辑自定义域名配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 在页面的左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。

1. 在&#x200B;**服务**&#x200B;标题下，单击&#x200B;**CDN配置**。

1. 在&#x200B;**CDN配置**&#x200B;页面上，在要编辑其CDN的行末尾单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 单击&#x200B;**编辑**。

1. 在&#x200B;**编辑CDN配置**&#x200B;对话框中，执行以下操作：

   * 在&#x200B;**层**&#x200B;下拉列表中，选择要使用的层(Publish或预览)。
   * 在&#x200B;**SSL证书**&#x200B;下拉列表中，选择要使用的SSL证书。

1. 单击&#x200B;**更新**。


## 更新自定义域名的SSL证书 {#update-cert}

执行上述相同步骤以更新自定义域名的SSL证书。

>[!NOTE]
>
>SSL证书必须有效，[已配置](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)，并包含要更新的自定义域名。


## 验证自定义域名 {#verify-custom-domain-name}

另请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**概述**&#x200B;屏幕导航到&#x200B;**域设置**&#x200B;页面。

1. 标识要验证的自定义域名的行。

1. 单击行最右端的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在下拉菜单中，单击&#x200B;**验证**。

1. 在&#x200B;**验证域**&#x200B;对话框中，在&#x200B;**您计划用于此域的证书类型是什么？**&#x200B;下拉列表，选择以下选项之一：

   | 证书类型选项 | 描述 |
   | --- | --- |
   | Adobe托管(DV) SSL证书 | 如果要使用DV（域验证）证书，请选择此证书类型。 此选项适用于大多数情况，可提供基本的域验证。 Adobe会自动管理和更新证书。 |
   | 客户管理的(OV/EV) SSL证书 | 如果您打算使用EV/OV SSL证书来保护域，请选择此证书类型。 此选项通过OV（组织验证）或EV（扩展验证）提供增强的安全性。 如果需要对证书进行更严格的验证、更高的信任级别或自定义控制，请使用。 |

1. 在&#x200B;**验证域**&#x200B;对话框中，根据您选择的证书类型，执行以下操作之一：

   | 如果您选择了证书类型 | 描述 |
   | --- | ---  |
   | Adobe 管理的证书 | a.完成[Adobe托管证书步骤](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-steps)。 完成&#x200B;**验证域**&#x200B;对话框中的步骤后，单击&#x200B;**验证**。<ul><li>由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。</li><li>Cloud Manager最终验证域名所有权并更新&#x200B;**域设置**&#x200B;表中的状态。 有关详细信息，请参阅[检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。</li>![验证域状态](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b.您现在可以[添加Adobe托管(DV) SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert)。</li></ul> |
   | 客户管理的证书 | a.单击&#x200B;**确定**。<br>b。您现在可以[添加客户管理的(OV/EV) SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert)。<br>添加证书后，您的域名在&#x200B;**域设置**&#x200B;表中标记为已验证。 有关详细信息，请参阅[检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。</li></ul><br>![验证客户管理的 EV/OV 证书的域名](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |


## 从所有关联的环境中删除自定义域名 {#deleting}

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以使用 Cloud Manager 删除自定义域名。

### 从所有关联的环境中删除自定义域名 {#delete-cdn-all}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**概述**&#x200B;屏幕导航到&#x200B;**域设置**&#x200B;页面。

1. 确定要删除的自定义域名的行。

1. 单击行最右端的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 选择&#x200B;**删除**。

1. 确认您的提交。


### 从特定环境中删除自定义域名 {#delete-cdn-specific}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 从&#x200B;**环境**&#x200B;页面，导航到感兴趣环境的详细信息屏幕。

1. 从域名表中，标识要删除的自定义域名的行。

1. 单击行最右端的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 选择&#x200B;**删除**。

1. 确认您的提交。
