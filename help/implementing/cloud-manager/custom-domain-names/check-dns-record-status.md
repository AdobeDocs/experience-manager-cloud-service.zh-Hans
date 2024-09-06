---
title: 检查 DNS 记录状态
description: 了解如何使用 Cloud Manager 确定您的 DNS 设置是否正确解析。
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 60%

---


# 检查 DNS 记录状态 {#check-dns-record-status}

了解如何使用 Cloud Manager 确定您的 DNS 设置是否正确解析。

## DNS记录状态 {#status}

在DNS正确解析之前，自定义域名无法提供实时流量。 在 Cloud Manager 中，您可以确定您的域名是否正确解析为 AEM as a Cloud Service 网站。

## 要求 {#requirements}

在使用Cloud Manager检查DNS记录状态之前，您必须满足这些要求。

* 您必须已按照文档[配置DNS设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)中的说明为自定义域名配置了DNS设置。

## 如何检查DNS记录状态 {#how-to}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 单击左侧导航面板中的&#x200B;**域设置**。

1. 单击域名的&#x200B;**状态**&#x200B;图标。

Cloud Manager对您的域名执行DNS查找并显示其[当前状态](#statuses)。

当您的自定义域名首次成功验证和部署时，Cloud Manager 将自动触发 DNS 查找。 对于后续尝试，您必须主动选择状态旁边的&#x200B;**再次解析**&#x200B;图标。

## Cloud Manager中的DNS状态 {#statuses}

自定义域在Cloud Manager中可以具有以下状态之一。

* **未检测到 DNS 状态** – 在您的自定义域名成功验证和部署之前，将不会检测到 DNS 状态。

   * 当您的自定义域名正在删除过程中时，也会观察到此状态。

* **DNS 解析不正确** – 这表明 DNS 记录配置尚未解析或错误。

   * 请参阅[配置 DNS 设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)，了解详细信息。
   * 准备就绪后，您必须选择状态旁边的&#x200B;**再次解析**&#x200B;图标。

* **DNS 解析正在进行中** – 解析正在进行中。

   * 通常，在您选择状态旁边的&#x200B;**再次解析**&#x200B;图标后，该状态会显示。

* **DNS 解析正确** – 您的 DNS 设置已正确配置。

   * 您的网站正在为访问者提供服务。

## 后续步骤 {#next-steps}

恭喜！您已成功配置自定义域以用于Cloud Manager。 有关如何使用Cloud Manager管理自定义域名的详细信息，请参阅文档[管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)。
