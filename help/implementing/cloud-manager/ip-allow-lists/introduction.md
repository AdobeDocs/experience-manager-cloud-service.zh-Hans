---
title: 简介 — Cloud Manager中的IP允许列表
description: 简介 — Cloud Manager中的IP允许列表
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 简介 {#introduction}

AEM as a cloud service对internet开放，安全性通过用户身份验证和授权来处理。 IP允许列表是Cloud Manager中的一项功能，用于限制和控制仅对受信任用户的访问。 此功能允许具有权限的用户创建受信任IP地址的允许列表，其站点用户可以从中访问其AEM域。

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
