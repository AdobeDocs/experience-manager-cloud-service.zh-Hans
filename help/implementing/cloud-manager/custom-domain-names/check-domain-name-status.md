---
title: 正在检查域名状态
description: 正在检查域名状态
translation-type: tm+mt
source-git-commit: 0b04d43c8b5bb28286e616f0bd902c05ec56ec05
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# 正在检查域名状态{#check-status}

您可以通过单击“域设置”(Domain Settings)页面环境表中域名的状态图标，确定您的域名是否已成功验证。

>[!NOTE]
>在“添加自定义域”向导的验证步骤中选择“保存”时，Cloud Manager将自动触发TXT验证。 对于后续验证，必须主动选择状态旁边的&#x200B;**verify again**&#x200B;图标。

Cloud Manager将通过TXT值验证域所有权并显示以下状态消息之一：

* **域验**
证失败TXT值缺失或检测到有错误。请按照说明重试。 准备就绪后，必须选择 
*验* 证状态旁的“againicon”。

* **正在进行域**
验证正在验证。此状态通常在您选择 
*验* 证状态旁的“againicon”。

* **已验证， Deployment**
FailedTXT验证成功。但是，CDN部署失败。 Adobe代表将自动收到通知。

* **域已验证和**
已部署此状态指示您的自定义域名已准备好使用。
   >[!NOTE]
   >此时，您的自定义域名已准备好进行测试，并将其指向Cloud Manager域名。 请参阅[配置DNS设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)以了解更多信息。

* **正**
在删除自定义域名的删除。

* **删除**
失败删除自定义域名失败。必须重试。 请参阅[删除自定义域名](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)以了解更多信息。


## IP允许列表{#pre-existing-cdn}的预存CDN配置

环境包括IP允许列表、SSL证书或自定义域名的预先存在的CDN配置的客户将在&#x200B;**IP允许列表**&#x200B;和&#x200B;**环境**&#x200B;详细信息页中看到以下消息。 在客户通过UI完全迁移所有预先存在的环境配置后，UI上显示的消息将会消失，并且消息可能需要1-2个工作日才能消失。

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>要查看和管理预先存在的配置，必须通过UI添加这些配置，如下图所示。

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)
