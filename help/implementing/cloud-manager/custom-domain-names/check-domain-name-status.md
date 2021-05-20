---
title: 正在检查域名状态
description: 正在检查域名状态
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 正在检查域名状态{#check-status}

您可以通过单击“域设置”页面上环境表中域名的状态图标，来确定您的域名是否已成功验证。

>[!NOTE]
>在“添加自定义域”向导的验证步骤中选择保存后，Cloud Manager将自动触发TXT验证。 对于后续的验证，必须主动选择状态旁边的&#x200B;**revify anail**&#x200B;图标。

Cloud Manager将通过TXT值验证域所有权，并显示以下状态消息之一：

* **域验证**
FailedTXT值缺失或检测到有错误。请按照说明重试。 准备就绪后，必须选择 
*状* 态旁边再次验证图标。

* **正在进行域**
验证正在验证。此状态通常在您选择 
*状* 态旁边再次验证图标。

* **已验证，部署**
失败TXT验证成功。但是，CDN部署失败。 Adobe代表将自动收到通知。

* **域已验证和**
已部署此状态表示您的自定义域名已准备就绪，可供使用。
   >[!NOTE]
   >此时，您的自定义域名已准备就绪，可供测试，并将其指向Cloud Manager域名。 请参阅[配置DNS设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)以了解详情。

* ****
正在删除自定义域名的删除操作。

* **自定**
义域名的删除失败删除失败。必须重试。 请参阅[删除自定义域名](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)以了解更多信息。


## 用于IP允许列表的预先存在的CDN配置{#pre-existing-cdn}

如果客户的环境中包含针对IP允许列表、SSL证书或自定义域名的预先存在的CDN配置，则该客户将在&#x200B;**IP允许列表**&#x200B;和&#x200B;**环境**&#x200B;详细信息页面中看到以下消息。 客户通过UI完全迁移所有预先存在的环境配置后，UI中显示的消息将消失，并且消息可能需要1-2个工作日才能消失。

>[!NOTE]
>要查看和管理预先存在的配置，必须通过UI添加这些配置。 有关更多详细信息，请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) 。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
