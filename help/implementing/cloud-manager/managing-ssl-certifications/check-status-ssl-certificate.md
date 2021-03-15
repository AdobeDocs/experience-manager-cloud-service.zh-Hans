---
title: 检查SSL证书的状态 — 管理SSL证书
description: 检查SSL证书的状态 — 管理SSL证书
translation-type: tm+mt
source-git-commit: 0b04d43c8b5bb28286e616f0bd902c05ec56ec05
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# 正在检查SSL证书{#checking-status-an-ssl-certificate}的状态

您的SSL证书状态可从SSL证书页面一览表了解。

您可以通过以下颜色方案标识SSL证书的状态：

* **绿**
色指示您的证书在将来至少60天内有效。

* **橙**
色指示您的证书将在60天内过期。是时候确保您有计划续订您的证书并通过Cloud Manager UI替换它，以避免可能的站点访问或中断。 Cloud Manager将在UI中发送定期通知，提醒您证书即将过期。

* **红色**
指示尽管有多个通知，您的SSL证书仍已过期。

## IP允许列表{#pre-existing-cdn}的预存CDN配置

环境包括IP允许列表、SSL证书或自定义域名的预先存在的CDN配置的客户将在&#x200B;**IP允许列表**&#x200B;和&#x200B;**环境**&#x200B;详细信息页中看到以下消息。 在客户通过UI完全迁移所有预先存在的环境配置后，UI上显示的消息将会消失，并且消息可能需要1-2个工作日才能消失。

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>要查看和管理预先存在的配置，必须通过UI添加这些配置，如下图所示。

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)