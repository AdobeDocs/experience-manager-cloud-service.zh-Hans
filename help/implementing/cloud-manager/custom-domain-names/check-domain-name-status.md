---
title: 检查域名状态
description: 了解如何确定 Cloud Manager 是否已成功验证您的自定义域名。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0c9328dc5be8f0a5e0924d0fc2ec59c9fce4141b
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 64%

---


# 检查域名状态 {#check-status}

了解如何确定 Cloud Manager 是否已成功验证您的自定义域名。

## 要求 {#requirements}

在Cloud Manager中检查域名状态之前，您必须满足这些要求。

* 您必须首先为自定义域添加TXT记录，如[添加TXT记录文档中所述。](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)

## 如何检查自定义域名的状态 {#how-to}

您可以在 Cloud Manager 中确定自定义域名的状态。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 单击左侧导航面板中的&#x200B;**域设置**。

1. 单击域名的&#x200B;**状态**&#x200B;图标。

将显示状态详细信息。 当显示&#x200B;**域已验证和部署**&#x200B;状态时，您的自定义域即可使用。 有关不同状态及其含义的详细信息，请参阅[下一部分](#statuses)。

>[!NOTE]
>
>当您在&#x200B;**添加自定义域**&#x200B;向导的验证步骤中选择&#x200B;**创建**&#x200B;时，当[向Cloud Manager中添加新的自定义域名时，Cloud Manager将自动触发验证。](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)对于后续验证，您必须主动选择状态旁边的再次验证图标。

## 了解验证状态 {#statuses}

Cloud Manager将通过[TXT值](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)验证域所有权，并显示以下状态消息之一。

* **域验证失败** – TXT 值缺失或检测到错误。

   * 按照状态消息中提供的说明解决问题。
   * 准备就绪后，您必须选择状态旁边的&#x200B;**再次验证**&#x200B;图标。

* **域验证正在进行** – 验证正在进行中。

   * 通常，在您选择状态旁边的&#x200B;**再次验证**&#x200B;图标后，该状态会显示。
   * 由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。

* **已验证，部署失败** – 验证成功，但 CDN 部署失败。

   * 在这种情况下，请联系您的 Adobe 代表。

* **域已验证和部署** – 此状态表示您的自定义域名已准备好使用。

   * 此时，您的自定义域名已准备好进行测试并指向 Cloud Manager 域名。
   * 请参阅 [配置 DNS 设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)，了解详细信息。

* **删除中** – 正在删除自定义域名。

* **删除失败** – 删除自定义域名失败，必须重试。

   * 请参阅[管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)，了解更多信息。

## 域名错误 {#domain-error}

以下是一些常见的域名验证错误及其典型分辨率。

### 域未安装错误 {#domain-not-installed}

在 TXT 记录的域验证过程中可能会发生此错误，即使您已经检查过该记录是否已适当更新。

#### 错误原因 {#cause}

快速将域锁定到注册该域的初始帐户，任何其他帐户都不能在不请求权限的情况下注册子域。此外，Fastly 只允许您将一个 Apex 域和关联子域分配给一个 Fastly 服务和帐户。如果您现有的Fastly帐户链接了用于AEM Cloud Service域的相同顶点和子域，则会看到此错误。

#### 错误解决方案 {#resolution}

错误修复如下：

* 在 Cloud Manager 中安装域之前，请从现有帐户中移除 Apex 和子域。

* 使用此选项将 Apex 域和所有子域链接到 AEM as a Cloud Service Fastly 帐户。有关更多详细信息，请参阅[使用 Fastly 文档中的域](https://docs.fastly.com/en/guides/working-with-domains)。

* 如果您的 Apex 域有多个您想链接到不同 Fastly 帐户的 AEM as a Cloud Service 和非 AEM as a Cloud Service 站点的子域，那么请尝试在 Cloud Manager 中安装该域。如果域安装失败，请通过 Fastly 创建客户支持票证，以便 Adob&#x200B;&#x200B;e 可以代表您与 Fastly 跟进。

>[!TIP]
>
>使用 Fastly 解决域授权问题通常需要 1-2 个工作日。因此，强烈建议在上线日期之前安装好域。

>[!NOTE]
>
>如果域未成功安装，请不要将站点的 DNS 路由到 AEM as a Cloud Service IP 的 DNS。

## 自定义域名的现有 CDN 配置 {#pre-existing-cdn}

如果您的自定义域名已有CDN配置，则&#x200B;**自定义域名**&#x200B;和&#x200B;**环境**&#x200B;页面上将显示一条信息性消息，鼓励您通过UI添加这些配置，以便它们在Cloud Manager中可见和可配置。

使用 UI 迁移所有预先存在的环境配置后，消息将消失。消息可能需要 1 – 2 个工作日才能消失。

请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)，了解更多详细信息。

## 后续步骤 {#next-steps}

在Cloud Manager中验证域状态后，您需要通过添加指向AEM as a Cloud Service的DNS CNAME或APEX记录来配置DNS设置。 继续文档[配置DNS设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)以继续设置自定义域名。
