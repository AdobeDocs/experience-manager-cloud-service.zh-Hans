---
title: 正在检查DNS记录状态
description: 正在检查DNS记录状态
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 正在检查DNS记录状态{#check-dns-record-status}

您可以通过从域设置页的Cloud Service表中单击DNS记录的状态图标，确定您的域名是否正确解析到AEM作为环境网站。

>[!NOTE]
>在首次成功验证和部署自定义域名时，Cloud Manager将自动触发DNS查找。 对于后续尝试，必须主动选择状态旁边的&#x200B;**resolve again**&#x200B;图标。

Cloud Manager会为您的域名执行DNS查找并显示以下状态消息之一：

* **未检测到DNS**
状态直到您的自定义域名成功验证和部署后，才会检测到DNS状态。当您的自定义域名正在删除过程中时，也会观察到此状态。

* **DNS解析**
不正确这表示DNS记录配置尚未解析／指向或错误。将自动通知Adobe代表。

   >[!NOTE]
   >必须按照相应的说明配置`CNAME`或`A-record`。 请参阅配置DNS设置以了解更多信息。 准备就绪后，必须再次选择状态旁的&#x200B;**resolve**&#x200B;图标。

* **正在进行DNS**
解析正在进行。此状态通常在您选择状态旁的“再次解析”图标后显示。

* **DNS解析正**
确您的DNS设置已正确配置。您的站点为访客提供服务。
