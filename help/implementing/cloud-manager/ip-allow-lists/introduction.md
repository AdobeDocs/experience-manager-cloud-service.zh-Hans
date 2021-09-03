---
title: 简介 — Cloud Manager中的IP允许列表
description: 简介 — Cloud Manager中的IP允许列表
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 3f282169b9ac2e2cf3e58277fd0c32cd97003de2
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理IP允许列表"
>abstract="AEM as a cloud service对internet开放，安全性通过用户身份验证和授权来处理。 IP允许列表是Cloud Manager中的一项功能，用于限制和控制仅对受信任用户的访问。 此功能允许具有权限的用户创建受信任IP地址的允许列表，其站点用户可以从中访问其AEM域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="添加IP允许列表"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="查看和更新IP允许列表"

AEM as a cloud service对internet开放，安全性通过用户身份验证和授权来处理。 IP允许列表是Cloud Manager中的一项功能，用于限制和控制仅对受信任用户的访问。 此功能允许具有权限的用户创建受信任IP地址的允许列表，其站点用户可以从中访问其AEM域。

>[!NOTE]
>您的程序中最多可以添加10个IP允许列表，并且每个IP允许列表中最多可以添加50个IP/CIDR地址。

IP允许列表可添加一次，并作为单位或实体多次应用/取消应用到环境中的创作和/或发布者服务。

>[!NOTE]
>Cloud Manager支持环境中用于创作和/或发布服务的IP允许列表名称。

使用Cloud Manager UI IP允许列表页面或环境详细信息页面，具有权限的用户可以执行多项任务来管理环境的IP允许列表，包括：

* [添加IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
   >[!NOTE]
   > 您可以在项目中的跨环境服务添加一次并重复使用或应用规则任意次数。
* [查看或更新IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
* [应用或取消应用IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
* [删除IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)
