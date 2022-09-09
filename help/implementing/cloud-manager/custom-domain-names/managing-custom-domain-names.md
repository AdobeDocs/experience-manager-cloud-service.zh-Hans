---
title: 管理自定义域名
description: 了解如何使用Cloud Manager查看、更新、替换和删除自定义域名。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
source-git-commit: 878381f9c5780864f218a00a272b1600d578dcca
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 5%

---

# 管理自定义域名 {#managing-custom-domain-names}

Cloud Manager允许您查看、更新、替换和删除自定义域名。

## 查看和更新 {#view-and-update}

使用 **查看和更新** 菜单，以查看任何自定义域名的详细信息。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **环境** 屏幕 **概述** 页面。

1. 识别您希望查看或更新的自定义域名的行。

1. 单击行最右端的省略号按钮。

1. 选择 **查看和更新** 选项。

## 更新自定义域名的SSL证书 {#update-cert}

您可以跟踪 [查看和更新自定义域名的相同步骤](#view-and-update) 更新自定义域名的SSL证书。

>[!NOTE]
>
>SSL证书必须有效， [已配置，](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 和包含您正在更新的自定义域名。

##  删除自定义域名 {#deleting}

具有 **业务所有者** 或 **部署管理器** 角色可以使用Cloud Manager删除自定义域名。

### 从所有关联的环境中删除自定义域名 {#delete-cdn-all}

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **环境** 屏幕 **概述** 页面。

1. 导航到 **域设置** 页面 **环境** 屏幕。

1. 确定要删除的自定义域名的行。

1. 单击行最右端的省略号按钮。

1. 选择 **删除**.

   ![删除自定义域名](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. 确认您的提交。

### 从特定环境中删除自定义域名 {#delete-cdn-specific}

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。
1. 导航到 **环境** 屏幕 **概述** 页面。
1. 从 **环境** 页面，导航到目标环境的详细信息屏幕。
1. 从域名表中，确定要删除的自定义域名的行。
1. 单击行最右端的省略号按钮。
1. 选择 **删除**.
1. 确认您的提交。
