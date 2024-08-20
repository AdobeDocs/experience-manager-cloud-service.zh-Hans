---
title: IP 允许列表简介
description: 了解IP允许列表如何限制用户可以从哪些地址访问AEM as a Cloud Service中的域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 20%

---


# IP 允许列表简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理 IP 允许列表"
>abstract="AEM as a Cloud Service可通过Internet访问，并通过用户身份验证和授权进行保护。 Cloud Manager的IP允许列表可用于限制和控制对受信任IP地址的访问。 具有适当权限的 Cloud Manager 用户可创建受信任的 IP 地址的允许列表，其站点的用户可从这些地址访问其 AEM 域。"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="添加 IP 允许列表"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="查看和更新IP允许列表"

默认情况下，可通过Internet访问AEM as a cloud service。 虽然安全性是通过用户身份验证和授权来处理的，但 IP 允许列表是一种限制仅访问受信任的 IP 地址的方法。

Cloud Manager的IP允许列表可用于限制和控制对这些受信任IP地址的访问。 具有适当权限的Cloud Manager用户可以[创建受信任IP地址的IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)，其网站的用户可以从这些地址访问其AEM域。

添加后，可以将[IP允许列表作为一个单元或实体多次应用于或取消应用于环境中的作者服务或发布者服务，或同时应用于两者。](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)

>[!NOTE]
>
>如果未应用任何IP允许列表，则默认情况下允许所有IP地址。 应用IP允许列表时，除IP允许列表上的地址外，不允许使用任何IP地址。

## 限制 {#limitations}

请记住IP允许列表有几个限制。

* 最多可以在程序中添加50个IP允许列表。
* 每个IP允许列表最多可以添加50个IP/CIDR地址。
* Cloud Manager中支持IP允许列表名用于环境中的创作服务和/或发布服务。
