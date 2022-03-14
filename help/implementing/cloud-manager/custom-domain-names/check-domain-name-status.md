---
title: 正在检查域名状态
description: 正在检查域名状态
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 4533cbc689d69cbe126791b4426123f890754507
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 正在检查域名状态 {#check-status}

您可以通过单击“域设置”页面上环境表中域名的状态图标，来确定您的域名是否已成功验证。

>[!NOTE]
>在“添加自定义域”向导的验证步骤中选择保存后，Cloud Manager将自动触发TXT验证。 对于后续的验证，您必须主动选择 **再次验证** 图标。

Cloud Manager将通过TXT值验证域所有权，并显示以下状态消息之一：

* **域验证失败**
TXT值缺失或检测到有错误。 请按照说明重试。 准备就绪后，必须选择 
*再次验证* 图标。

* **正在进行域验证**
正在验证。 此状态通常在您选择 
*再次验证* 图标。

* **已验证，部署失败**
TXT验证成功。 但是，CDN部署失败。 请联系您的Adobe代表。

* **域验证和部署**
此状态表示您的自定义域名已准备就绪，可供使用。
   >[!NOTE]
   >此时，您的自定义域名已准备就绪，可供测试，并将其指向Cloud Manager域名。 请参阅 [配置DNS设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) 以了解更多。

* **删除**
正在删除自定义域名。

* **删除失败**
删除自定义域名失败。 必须重试。 请参阅 [删除自定义域名](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) 以了解更多。


## 针对自定义域名的预先存在的CDN配置 {#pre-existing-cdn}

如果客户的环境包含针对IP允许列表、SSL证书或自定义域名的预先存在的CDN配置，则客户将在 **IP允许列表** 和 **环境** 详细信息页面。 客户通过UI完全迁移所有预先存在的环境配置后，UI中显示的消息将消失，并且消息可能需要1-2个工作日才能消失。

>[!NOTE]
>要查看和管理预先存在的配置，必须通过UI添加这些配置。 请参阅 [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) 以了解更多详细信息。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
