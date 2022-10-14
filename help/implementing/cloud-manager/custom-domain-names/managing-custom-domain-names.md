---
title: 管理自定义域名
description: 了解如何使用 Cloud Manager 查看、更新、替换和删除自定义域名。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
source-git-commit: 955f4bb55434eeb1a429a1972714b71c5370de1e
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 100%

---

# 管理自定义域名 {#managing-custom-domain-names}

Cloud Manager 允许您查看、更新、替换和删除自定义域名。

## 查看和更新 {#view-and-update}

使用&#x200B;**查看和更新**&#x200B;菜单查看任何自定义域名的详细信息。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 确定要查看或更新的自定义域名的行。

1. 单击行最右端的省略号按钮。

1. 选择&#x200B;**查看和更新**&#x200B;选项。

## 更新自定义域名的 SSL 证书 {#update-cert}

您可以按照[相同的步骤查看和更新自定义域名](#view-and-update)，从而更新自定义域名的 SSL 证书。

>[!NOTE]
>
>SSL 证书必须有效，[已配置](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)，并包含要更新的自定义域名。

## 删除自定义域名 {#deleting}

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以使用 Cloud Manager 删除自定义域名。

### 从所有关联环境中删除自定义域名 {#delete-cdn-all}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 从&#x200B;**环境**&#x200B;屏幕导航到&#x200B;**域设置**&#x200B;页面。

1. 确定要删除的自定义域名的行。

1. 单击行最右端的省略号按钮。

1. 选择&#x200B;**删除**。

   ![删除自定义域名](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. 确认您的提交。

### 从特定环境中删除自定义域名 {#delete-cdn-specific}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。
1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。
1. 从&#x200B;**环境**&#x200B;页面，导航到感兴趣环境的详细信息屏幕。
1. 从域名表，确定要删除的自定义域名的行。
1. 单击行最右端的省略号按钮。
1. 选择&#x200B;**删除**。
1. 确认您的提交。
