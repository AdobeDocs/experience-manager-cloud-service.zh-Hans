---
title: 正在检查DNS记录状态
description: 正在检查DNS记录状态
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 正在检查DNS记录状态 {#check-dns-record-status}

您可以通过从“域设置”页面的“环境”表中单击DNS记录的状态图标，来确定您的域名是否正确解析到AEMas a Cloud Service网站。

当您的自定义域名首次成功验证和部署后，Cloud Manager将自动触发DNS查找。 对于后续尝试，必须主动选择状态旁边的&#x200B;**再次解析**&#x200B;图标。

Cloud Manager会对您的域名执行DNS查找，并显示以下状态消息之一：

* **未检测到DNS**
状态直到您的自定义域名成功验证和部署后，才会检测到DNS状态。当您的自定义域名正在删除过程中时，也会观察到此状态。

* **DNS解析**
不正确这表示DNS记录配置尚未解析/指向，或错误。Adobe代表将自动收到通知。

   >[!NOTE]
   >您必须按照相应的说明配置`CNAME`或`A-record`。 请参阅配置DNS设置，以了解更多信息。 准备就绪后，必须再次选择状态旁边的&#x200B;**resolve**&#x200B;图标。

* **正在进行**
ProgressResolution的DNS解析。此状态通常在您选择状态旁边的“再次解析”图标后才会显示。

* **正确解析**
DNS您的DNS设置已正确配置。您的网站为访客提供服务。
