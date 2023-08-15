---
title: 检查域名状态
description: 了解如何确定 Cloud Manager 是否已成功验证您的自定义域名。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 97%

---


# 检查域名状态 {#check-status}

您可以在 Cloud Manager 中确定自定义域名的状态。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 单击左侧导航面板中的&#x200B;**域设置**。

1. 单击域名的&#x200B;**状态**&#x200B;图标。

Cloud Manager 将通过 TXT 值验证域所有权，并显示以下状态消息之一。

* **域验证失败** – TXT 值缺失或检测到错误。

   * 按照提供的说明解决问题。
   * 准备就绪后，您必须选择状态旁边的&#x200B;**再次验证**&#x200B;图标。

* **域验证正在进行** – 验证正在进行中。

   * 通常，在您选择状态旁边的&#x200B;**再次验证**&#x200B;图标后，该状态会显示。

* **已验证，部署失败** – 验证成功，但 CDN 部署失败。

   * 在这种情况下，请联系您的 Adobe 代表。

* **域已验证和部署** – 此状态表示您的自定义域名已准备好使用。

   * 此时，您的自定义域名已准备好进行测试并指向 Cloud Manager 域名。
   * 请参阅 [配置 DNS 设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)，了解详细信息。

* **删除中** – 正在删除自定义域名。

* **删除失败** – 删除自定义域名失败，必须重试。

   * 请参阅[管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)，了解更多信息。

当您在&#x200B;**添加自定义域**&#x200B;向导的验证步骤中选择&#x200B;**保存**&#x200B;时，Cloud Manager 将自动触发 TXT 验证。 对于后续验证，必须主动选择状态旁边的再次验证图标。

## 域名错误 {#domain-error}

以下是一些常见的域名错误及其典型的解决方法。

### 域未安装错误 {#domain-not-installed}

在 TXT 记录的域验证过程中可能会发生此错误，即使您已经检查过该记录是否已适当更新。

#### 错误原因 {#cause}

快速将域锁定到注册该域的初始帐户，任何其他帐户都不能在不请求权限的情况下注册子域。此外，Fastly只允许您将一个Apex域和关联的子域分配给一个Fastly服务和帐户。 如果您现有的 Fastly 帐户链接了 AEM Cloud Service 域使用的相同 Apex 和子域，您将看到此错误。

#### 错误解决方案 {#resolution}

错误修复如下：

* 在 Cloud Manager 中安装域之前，请从现有帐户中移除 Apex 和子域。 

* 使用此选项将 Apex 域和所有子域链接到 AEM as a Cloud Service Fastly 帐户。 有关更多详细信息，请参阅[使用 Fastly 文档中的域](https://docs.fastly.com/en/guides/working-with-domains)。

* 如果您的 Apex 域有多个您想链接到不同 Fastly 帐户的 AEM as a Cloud Service 和非 AEM as a Cloud Service 站点的子域，那么请尝试在 Cloud Manager 中安装该域。如果域安装失败，请通过 Fastly 创建客户支持票证，以便 Adob&#x200B;&#x200B;e 可以代表您与 Fastly 跟进。

>[!TIP]
>
>使用 Fastly 解决域授权问题通常需要 1-2 个工作日。因此，强烈建议在上线日期之前安装好域。

>[!NOTE]
>
>如果域未成功安装，请不要将站点的 DNS 路由到 AEM as a Cloud Service IP 的 DNS。

## 自定义域名的现有 CDN 配置 {#pre-existing-cdn}

如果您的自定义域名已有预先存在的 CDN 配置，则&#x200B;**自定义域名**&#x200B;和&#x200B;**环境**&#x200B;页面上会有一条提示消息，鼓励您通过 UI 添加这些配置，使其在 Cloud Manager 中可见并可配置。

使用 UI 迁移所有预先存在的环境配置后，消息将消失。 消息可能需要 1 – 2 个工作日才能消失。

请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)，了解更多详细信息。
