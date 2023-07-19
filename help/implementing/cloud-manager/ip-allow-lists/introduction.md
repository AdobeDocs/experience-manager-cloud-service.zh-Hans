---
title: IP 允许列表简介
description: 了解 IP 允许列表如何限制用户可以从哪些地址访问 AEM as a Cloud Service 上的域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: ht
source-wordcount: '306'
ht-degree: 100%

---


# IP 允许列表简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理 IP 允许列表"
>abstract="可通过 Internet 访问 AEM as a Cloud Service，并通过用户身份验证和授权保护它。Cloud Manager 的 IP 允许列表可用于仅限访问受信任的 IP 地址和控制此类访问。具有适当权限的 Cloud Manager 用户可创建受信任的 IP 地址的允许列表，其站点的用户可从这些地址访问其 AEM 域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=zh-Hans" text="添加 IP 允许列表"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html?lang=zh-Hans" text="查看和更新 IP 允许列表"

默认情况下，AEM as a Cloud Service 可通过网络访问。虽然安全性是通过用户身份验证和授权来处理的，但 IP 允许列表是一种限制仅访问受信任的 IP 地址的方法。

Cloud Manager 的 IP 允许列表可用于仅限访问此类受信任的 IP 地址和控制此类访问。具有适当权限的 Cloud Manager 用户可[创建受信任的 IP 地址的允许列表](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)，其站点的用户可从这些地址访问其 AEM 域。

添加后，[IP 允许列表可以作为一个单元或实体多次应用/取消应用到环境中的作者和/或发布者服务。](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)

>[!NOTE]
>
>如果未应用 IP 允许列表，则默认情况下允许所有 IP 地址。应用 IP 允许列表后，除 IP 允许列表上的地址外，不允许任何 IP 地址。

## 限制 {#limitations}

请注意 IP 允许列表有多种限制。

* 最多可以在程序中添加 50 个 IP 允许列表
* 每个 IP 允许列表最多可以添加 50 个 IP/CIDR 地址。
* 对于环境中的作者和/或发布服务，Cloud Manager 支持 IP 允许列表名称。
