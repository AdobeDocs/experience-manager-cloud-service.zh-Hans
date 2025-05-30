---
title: 应用和取消应用 IP 允许列表
description: 了解如何对Cloud Manager环境应用和取消应用IP允许列表。
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: aa33f84e6b38019f41ea0a4db8f49ccc201869f7
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 14%

---


# 应用和取消应用IP允许列表 {#apply-allow-list}

应用IP允许列表时，列表定义中包含的所有IP范围都与环境中的创作或发布服务相关联。 取消应用列表与此过程相反。

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

## 应用IP允许列表 {#applying}

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以按照这些步骤应用IP允许列表。

**要应用IP允许列表：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager。
1. 选择相应的组织。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。
1. 从&#x200B;**概述**&#x200B;页面，导航到&#x200B;**环境**&#x200B;屏幕。
1. 在&#x200B;**环境**&#x200B;屏幕上，导航到特定环境详细信息页面。
1. 导航到&#x200B;**IP允许列表**&#x200B;表。
1. 使用表顶部的输入字段，以便选择IP允许列表以及要应用它的创作、发布或预览服务。
IP允许列表必须已存在于Cloud Manager中才能应用它。 请参阅[添加IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)。
1. 单击![添加图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **应用**&#x200B;并确认您的提交。

## 取消应用IP允许列表 {#un-applying}

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以按照这些步骤取消应用IP允许列表。

**要取消应用IP允许列表：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager。
1. 选择相应的组织。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。
1. 从&#x200B;**概述**&#x200B;页面，导航到&#x200B;**环境**&#x200B;页面。
1. 导航到特定环境详细信息页面。
1. 在“常规”选项卡中，滚动到&#x200B;**IP允许列表**&#x200B;表。
1. 标识要取消应用的IP允许列表的行。
1. 在已识别行的右侧，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 单击&#x200B;**取消应用**。
1. 在&#x200B;**取消应用IP允许列表**&#x200B;对话框中，单击&#x200B;**取消应用**。
