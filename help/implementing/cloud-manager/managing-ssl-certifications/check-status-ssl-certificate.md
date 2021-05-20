---
title: 检查SSL证书的状态 — 管理SSL证书
description: 检查SSL证书的状态 — 管理SSL证书
exl-id: 59d81356-2fa9-43db-bfa5-c2896c530eaa
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 检查SSL证书{#checking-status-an-ssl-certificate}的状态

可以从SSL证书页面一目了然地了解SSL证书的状态。

您可以通过以下颜色方案标识SSL证书的状态：

* ****
绿色表示您的证书在将来至少60天内有效。

* ****
橙色表示您的证书将在60天内过期。现在是时候确保您有计划通过Cloud Manager UI续订并替换您的证书，以避免可能的站点访问或中断。 Cloud Manager将在UI中发送常规通知，以提醒您证书即将过期。

* ****
红色指示尽管有多个通知，但您的SSL证书已过期。

## 用于IP允许列表的预先存在的CDN配置{#pre-existing-cdn}

如果客户的环境中包含针对IP允许列表、SSL证书或自定义域名的预先存在的CDN配置，则该客户将在&#x200B;**IP允许列表**&#x200B;和&#x200B;**环境**&#x200B;详细信息页面中看到以下消息。 客户通过UI完全迁移所有预先存在的环境配置后，UI中显示的消息将消失，并且消息可能需要1-2个工作日才能消失。

>[!NOTE]
>要查看和管理预先存在的配置，必须通过UI添加这些配置。 有关更多详细信息，请参阅[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
