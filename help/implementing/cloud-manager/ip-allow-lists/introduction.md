---
title: IP 允许列表简介
description: 了解IPas a Cloud Service如何限制IPAEM可以从哪些地址访问允许列表上的域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 7%

---


# IP 允许列表简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理IP允许列表"
>abstract="AEM as a cloud service可通过internet访问，并通过用户身份验证和授权进行保护。 Cloud Manager的IP允许列表可用于限制和控制对受信任IP地址的访问。 具有适当权限的Cloud Manager用户可以创建受信任IP地址的个允许列表，其网站的用户可以从这些地址访问其AEM域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="添加 IP 允许列表"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html" text="查看和更新 IP 允许列表"

默认情况下，可通过Internet访问AEM as a cloud service。 虽然安全性是通过用户身份验证和授权处理的，但IP允许列表是一种将访问限制为仅受信任的IP地址的方法。

Cloud Manager的IP允许列表可用于限制和控制对此类受信任IP地址的访问。 具有适当权限的Cloud Manager用户可以 [创建允许列表](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) 受信任的IP地址，站点的用户可以从中访问其AEM域。

添加后， [允许列表可以应用/取消应用IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 作为单元或实体多次访问环境中的作者和/或发布者服务。

>[!NOTE]
>
>如果未应用IP允许列表，则默认情况下允许所有IP地址。 应用IP 允许列表允许列表时，除IP上的地址外，不允许使用其他IP地址。

## 限制 {#limitations}

请记住IP允许列表有几个限制。

* 允许列表最多可以在程序中添加50个IP
* 允许列表每个IP最多可以添加50个IP/CIDR地址。
* Cloud Manager中支持IP允许列表名称用于环境中的作者或publish服务，或同时支持两者。
