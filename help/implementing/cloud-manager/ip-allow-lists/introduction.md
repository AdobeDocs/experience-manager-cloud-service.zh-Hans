---
title: IP 允许列表简介
description: 了解 IP 允许列表如何限制用户可以从哪些地址访问 AEM as a Cloud Service 域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 286bc8e206b7a54cc1869e3965e55852cf62946d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 56%

---


# IP 允许列表简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理 IP 允许列表"
>abstract="AEM as a cloud service 可通过互联网访问，并通过用户身份验证和授权进行保护。 Cloud Manager 的 IP 允许列表可用于仅限制和控制对受信任 IP 地址的访问。 具有适当权限的 Cloud Manager 用户可以创建受信任 IP 地址的允许列表，其站点的用户可以从中访问其 AEM 域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="添加 IP 允许列表"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="查看和更新 IP 允许列表"

AEM as a cloud service預設可透過網際網路存取。 雖然安全性是透過使用者驗證和授權來處理，但IP允許清單是一種將存取限製為僅受信任的IP位址的方法。

Cloud Manager的IP允許清單可用於限制和控制對此類受信任IP地址的訪問。 具有適當許可權的Cloud Manager使用者可以 [建立允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) 受信任的IP位址數量，其網站的使用者可以從這些位址存取其AEM網域。

新增後， [可以套用/取消套用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 以單位或實體的身分多次前往環境中的作者和/或發佈者服務。

>[!NOTE]
>
>如果未套用IP允許清單，預設會允許所有IP位址。 套用IP允許清單後，除IP允許清單上的位址外，不允許任何IP位址。

## 限制 {#limitations}

请记住 IP 允许列表有很多限制。

* 最多可以在程序中添加 50 个 IP 允许列表
* 每个 IP 允许列表最多可以添加 50 个 IP/CIDR 地址。
* 对于环境中的作者和/或发布服务，Cloud Manager 支持 IP 允许列表名称。
