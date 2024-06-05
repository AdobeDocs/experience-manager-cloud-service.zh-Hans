---
title: 应用和取消应用 IP 允许列表
description: 了解如何对环境应用和取消应用 IP 允许列表。
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 84%

---


# 应用和取消应用 IP 允许列表 {#apply-allow-list}

应用 IP 允许列表时，列表定义中包含的所有 IP 范围都与环境中的作者或发布服务相关联。 取消应用列表与此过程相反。

## 应用 IP 允许列表 {#applying}

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以按照这些步骤应用 IP 允许列表。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。
1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。
1. 在&#x200B;**环境**&#x200B;屏幕上导航到特定的环境详细信息页面，然后导航到 **IP 允许列表**。
1. 使用表顶部的输入字段，以便选择IP允许列表以及要应用它的创作或发布服务。
   * IP 允许列表必须存在于 Cloud Manager 中才能应用它。
1. 单击&#x200B;**应用**，并确认您的提交。

## 取消应用允许列表 {#un-applying}

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以按照这些步骤取消应用 IP 允许列表。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。
1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。
1. 在&#x200B;**环境**&#x200B;屏幕上导航到特定的环境详细信息页面，然后导航到 **IP 允许列表**。
1. 标识要取消应用的IP允许列表的行。
1. 选择行最右侧的省略号按钮。
1. 选择&#x200B;**取消应用**&#x200B;选项，并确认您的提交。
