---
title: 简介- Could Manager中的IP允许列表
description: 简介- Could Manager中的IP允许列表
translation-type: tm+mt
source-git-commit: 4635cb6360707d12cf512b0ee21f05169a153114
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# 简介 {#introduction}

AEM作为云服务，是对internet开放的，安全性是通过用户身份验证和授权处理的。 “IP允许列表”是云管理器中的一项功能，用于限制和控制仅对受信任用户的访问。 此功能使具有权限的用户能够创建受信任IP地址的允许列表，其站点用户可以从中访问其AEM域。

IP允许列表可以添加一次，然后作为一个单位或实体多次应用／取消应用到环境中的作者和／或发布者服务。

>[!NOTE]
>Cloud Manager中的创作和／或发布服务支持IP允许列表名称。

使用云管理器UI IP允许列表页或环境详细信息页，具有权限的用户可以执行多个任务来管理您的环境的IP允许列表，包括：

* 添加IP允许列表
   >[!NOTE]
   > 您可以在项目中跨环境服务添加一次，然后重复使用或应用规则任意次数。
* 查看或更新IP允许列表
* 应用或取消应用IP允许列表
* 删除IP允许列表