---
title: IP允许列表简介
description: 了解IP允许列表如何限制用户可以从哪些地址访问AEMas a Cloud Service域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 8d1680fa8dbaaefa297cf8c6698097b3c7acc48d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# IP允许列表简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理IP允许列表"
>abstract="AEM as a cloud service可通过internet访问，并通过用户身份验证和授权进行保护。 Cloud Manager的IP允许列表可用于仅限制和控制对受信任IP地址的访问。 具有适当权限的Cloud Manager用户可以创建受信任IP地址的允许列表，其站点的用户可以从这些地址访问其AEM域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="添加IP允许列表"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="查看和更新IP允许列表"

AEM as a cloud service可通过internet访问，并通过用户身份验证和授权进行保护。 Cloud Manager的IP允许列表可用于仅限制和控制对受信任IP地址的访问。 具有适当权限的Cloud Manager用户可以创建受信任IP地址的允许列表，其站点的用户可以从这些地址访问其AEM域。

IP允许列表可添加一次，并作为单位或实体多次应用/取消应用到环境中的创作和/或发布者服务。

## 限制 {#limitations}

IP存在许多限制，允许列表记住这些限制。

* 您的程序中最多可添加50个IP允许列表
* 每个IP允许列表最多可添加50个IP/CIDR地址。
* Cloud Manager支持在环境中为创作和/或发布服务提供IP允许列表名称。
