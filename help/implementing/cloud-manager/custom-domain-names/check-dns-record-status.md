---
title: 检查 DNS 记录状态
description: 了解如何使用 Cloud Manager 确定您的 DNS 设置是否正确解析。
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 96%

---

# 检查 DNS 记录状态 {#check-dns-record-status}

在 Cloud Manager 中，您可以确定您的域名是否正确解析为 AEM as a Cloud Service 网站。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 单击 **域设置** （在左侧导航面板中）。

1. 单击域名的&#x200B;**状态**&#x200B;图标。

Cloud Manager 对域名执行 DNS 查找，并显示以下状态消息之一。

* **未检测到 DNS 状态** – 在您的自定义域名成功验证和部署之前，将不会检测到 DNS 状态。

   * 当您的自定义域名正在删除过程中时，也会看到此状态。

* **DNS 解析不正确** – 这表明 DNS 记录配置尚未解析或错误。

   * 请参阅[配置 DNS 设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)，了解详细信息。
   * 准备就绪后，您必须选择状态旁边的&#x200B;**再次解析**&#x200B;图标。

* **DNS 解析正在进行中** – 解析正在进行中。

   * 通常，在您选择状态旁边的&#x200B;**再次解析**&#x200B;图标后，该状态会显示。

* **DNS 解析正确** – 您的 DNS 设置已正确配置。

   * 您的网站正在为访问者提供服务。

当您的自定义域名首次成功验证和部署时，Cloud Manager 将自动触发 DNS 查找。 对于后续尝试，您必须主动选择状态旁边的&#x200B;**再次解析**&#x200B;图标。
