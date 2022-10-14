---
title: IP 允许列表简介
description: 了解 IP 允许列表如何限制用户可以从哪些地址访问 AEM as a Cloud Service 域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 8d1680fa8dbaaefa297cf8c6698097b3c7acc48d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 100%

---


# IP 允许列表简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理 IP 允许列表"
>abstract="AEM as a cloud service 可通过互联网访问，并通过用户身份验证和授权进行保护。 Cloud Manager 的 IP 允许列表可用于仅限制和控制对受信任 IP 地址的访问。 具有适当权限的 Cloud Manager 用户可以创建受信任 IP 地址的允许列表，其站点的用户可以从中访问其 AEM 域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="添加 IP 允许列表"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="查看和更新 IP 允许列表"

AEM as a cloud service 可通过互联网访问，并通过用户身份验证和授权进行保护。 Cloud Manager 的 IP 允许列表可用于仅限制和控制对受信任 IP 地址的访问。 具有适当权限的 Cloud Manager 用户可以创建受信任 IP 地址的允许列表，其站点的用户可以从中访问其 AEM 域。

IP 允许列表可以作为一个单元或实体添加一次，并多次应用/取消应用到环境中的作者和/或发布者服务。

## 限制 {#limitations}

请记住 IP 允许列表有很多限制。

* 最多可以在程序中添加 50 个 IP 允许列表
* 每个 IP 允许列表最多可以添加 50 个 IP/CIDR 地址。
* 对于环境中的作者和/或发布服务，Cloud Manager 支持 IP 允许列表名称。
