---
title: 正在检查域名状态
description: 正在检查域名状态
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# 正在检查域名状态{#check-status}

您可以通过单击“域设置”页环境上的表中域名的状态图标，确定您的域名是否已成功验证。

>[!NOTE]
>在添加自定义域向导的验证步骤中选择保存后，Cloud Manager将自动触发TXT验证。 对于后续验证，必须主动选择状态旁边的&#x200B;**verify again**&#x200B;图标。

Cloud Manager将通过TXT值验证域所有权并显示以下状态消息之一：

* **域验证**
FailedTXT值缺失或检测到有错误。请按照说明重试。 准备就绪后，必须选择状态旁的“再次验证”图标。

* **正在进行域**
验证正在验证。此状态通常在您选择状态旁的“再次验证”图标后显示。

* **已验证， Deployment**
FailedTXT验证成功。但是，CDN部署失败。 将自动通知Adobe代表。

* **域已验证和**
已部署此状态表示您的自定义域名已准备好使用。注意：此时，您的自定义域名已准备好进行测试，并将其指向Cloud Manager域名。 转到配置DNS设置，了解如何执行此操作。

* **正**
在删除自定义域名。

* **自定**
义域名的删除失败删除失败。必须重试。 转到“删除自定义域名”，进一步了解主题。

