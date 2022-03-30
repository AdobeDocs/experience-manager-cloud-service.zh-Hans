---
title: 检查 DNS 记录状态
description: 了解如何使用Cloud Manager确定DNS设置是否正确解析。
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 2278abcf0c34fd34a7730242ee27814d37b7d4d0
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---

# 检查 DNS 记录状态 {#check-dns-record-status}

在Cloud Manager中，您可以确定域名是否正确解析到AEMas a Cloud Service网站。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **环境** 屏幕 **概述** 页面。

1. 单击 **域设置** 中。

1. 单击 **状态** 图标。

Cloud Manager会对您的域名执行DNS查找，并显示以下状态消息之一。

* **未检测到DNS状态**  — 在成功验证和部署您的自定义域名后，才会检测到DNS状态。

   * 当您的自定义域名正在删除过程中时，也会观察到此状态。

* **DNS解析不正确**  — 这表示DNS记录配置未解析或错误。

   * 请参阅文档 [配置DNS设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) 以了解更多。
   * 准备就绪后，必须选择 **再次解决** 图标。

* **正在解析DNS**  — 决议正在进行中。

   * 此状态通常在您选择 **再次解决** 图标。

* **DNS解析正确**  — 您的DNS设置已正确配置。

   * 您的网站为访客提供服务。

当您的自定义域名首次成功验证和部署后，Cloud Manager将自动触发DNS查找。 要进行后续尝试，您必须主动选择 **再次解决** 图标。
