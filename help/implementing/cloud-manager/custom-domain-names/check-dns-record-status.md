---
title: 检查 DNS 记录状态
description: 检查 DNS 记录状态
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 5%

---

# 检查 DNS 记录状态 {#check-dns-record-status}

您可以通过从“域设置”页面的“环境”表中单击DNS记录的状态图标，来确定您的域名是否正确解析到AEMas a Cloud Service网站。

当您的自定义域名首次成功验证和部署后，Cloud Manager将自动触发DNS查找。 要进行后续尝试，您必须主动选择 **再次解决** 图标。

Cloud Manager会对您的域名执行DNS查找，并显示以下状态消息之一：

* **未检测到DNS状态**
在成功验证和部署您的自定义域名后，才会检测到DNS状态。 当您的自定义域名正在删除过程中时，也会观察到此状态。

* **DNS解析不正确**
这表示DNS记录配置尚未解析/指向，或错误。

   >[!NOTE]
   >您必须配置 `CNAME` 或 `A-record` 按照相应的说明操作。 请参阅配置DNS设置，以了解更多信息。 准备就绪后，必须选择 **再次解决** 图标。

* **正在解析DNS**
正在进行解决。 此状态通常在您选择状态旁边的“再次解析”图标后才会显示。

* **DNS解析正确**
您的DNS设置已正确配置。 您的网站为访客提供服务。
