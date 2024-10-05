---
title: IP 允许列表简介
description: 了解IP允许列表如何限制用户可以从哪些地址访问AEM as a Cloud Service中的域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 25%

---


# IP 允许列表简介 {#introduction}

了解IP允许列表如何限制用户可以从哪些地址访问AEM as a Cloud Service中的域。

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理 IP 允许列表"
>abstract="可通过 Internet 访问 AEM as a Cloud Service，并通过用户身份验证和授权保护它。Cloud Manager 的 IP 允许列表可用于仅限制和控制对受信任 IP 地址的访问。 具有适当权限的 Cloud Manager 用户可创建受信任的 IP 地址的允许列表，其站点的用户可从这些地址访问其 AEM 域。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="添加 IP 允许列表"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="查看和更新 IP 允许列表"

## 概述 {#overview}

默认情况下，可通过Internet访问AEM as a cloud service。 虽然安全性是通过用户身份验证和授权来处理的，但 IP 允许列表是一种限制仅访问受信任的 IP 地址的方法。

Cloud Manager的IP允许列表可用于限制和控制对这些受信任IP地址的访问。 具有适当权限的Cloud Manager用户可以[创建和添加受信任IP地址的IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)，其网站的用户可以从这些地址访问其AEM域。

添加后，可以将[IP允许列表作为一个单元或实体多次应用于或取消应用于环境中的作者服务或发布者服务，或同时应用于两者。](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)

>[!NOTE]
>
>如果未应用任何IP允许列表，则默认情况下允许所有IP地址。 应用IP允许列表时，除IP允许列表上的地址外，不允许使用任何IP地址。

## 限制 {#limitations}

在使用IP允许列表之前，请了解其功能、使用和对其他功能的影响的以下限制。

### IP允许列表的一般限制 {#general}

* 最多可以将50个IP允许列表添加到您的项目中。
* 每个IP允许列表最多可以添加50个IP/CIDR地址。
* Cloud Manager中支持IP允许列表名用于环境中的创作服务和/或发布服务。

### 前端管道和IP允许列表 {#front-end-pipeline}

如果您使用或打算使用[前端管道来开发站点](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)，则必须预先添加以下Cloud Manager IP允许列表。

当您[添加IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md#add-cm-allowlist)时，将其命名为&#x200B;*`Cloud Manager`*，然后复制下面的地址列表并将它们粘贴到IP允许列表对话框中。

```text
52.254.106.192/28
20.186.185.181
52.254.106.240/28
52.254.107.128/28
52.254.105.192/28
52.254.106.176/28
20.186.185.227
52.254.106.144/28
52.254.107.64/28
20.186.185.239
20.22.83.112
52.254.107.80/28
52.254.107.144/28
52.254.106.224/28
20.14.241.153
52.254.107.0/28
52.254.107.32/28
52.254.106.208/28
40.70.154.136/29
52.254.106.160/28
52.254.107.16/28
52.254.106.0/28
4.152.211.251
```

为避免前端管道运行中断，请确保添加此Cloud Manager IP允许列表。 然后，在启用管道之前&#x200B;*将该列表应用于创作环境*。

有关详细信息，请参阅[应用IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)和[启用前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)。

### Universal Editor和IP允许列表 {#universal-editor}

{{ip-allow-lists-ue}}
