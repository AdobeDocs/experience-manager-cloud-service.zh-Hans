---
title: 正在检查域名状态
description: 正在检查域名状态
translation-type: tm+mt
source-git-commit: f11cb3b56f51046779300626d1deb037dd687309
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# 正在检查域名状态{#check-status}

您可以通过单击“域设置”页环境上的表中域名的状态图标，确定您的域名是否已成功验证。

>[!NOTE]
>在添加自定义域向导的验证步骤中选择保存后，Cloud Manager将自动触发TXT验证。 对于后续验证，必须主动选择状态旁边的&#x200B;**verify again**&#x200B;图标。

Cloud Manager将通过TXT值验证域所有权并显示以下状态消息之一：

* **域验证**
FailedTXT值缺失或检测到有错误。请按照说明重试。 准备就绪后，必须选择 
*验* 证状态旁的重新图标。

* **正在进行域**
验证正在验证。此状态通常在您选择 
*验* 证状态旁的重新图标。

* **已验证， Deployment**
FailedTXT验证成功。但是，CDN部署失败。 将自动通知Adobe代表。

* **域已验证和**
已部署此状态表示您的自定义域名已准备好使用。
   >[!NOTE]
   >此时，您的自定义域名已准备好进行测试，并将其指向Cloud Manager域名。 请参阅[配置DNS设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)以了解更多信息。

* **正**
在删除自定义域名。

* **自定**
义域名的删除失败删除失败。必须重试。 请参阅[删除自定义域名](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)以了解更多信息。

