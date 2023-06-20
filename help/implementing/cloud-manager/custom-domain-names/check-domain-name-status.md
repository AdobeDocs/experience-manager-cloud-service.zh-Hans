---
title: 检查域名状态
description: 了解如何确定 Cloud Manager 是否已成功验证您的自定义域名。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 67%

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
   * 请参阅[配置 DNS 设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)文档，了解更多信息。

* **删除中** – 正在删除自定义域名。

* **删除失败** – 删除自定义域名失败，必须重试。

   * 请参阅[管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)文档，了解更多信息。

当您在&#x200B;**添加自定义域**&#x200B;向导的验证步骤中选择&#x200B;**保存**&#x200B;时，Cloud Manager 将自动触发 TXT 验证。 对于后续验证，必须主动选择状态旁边的再次验证图标。

## 域名错误 {#domain-error}

以下是一些常见的域名错误及其典型分辨率。

### 域未安装错误 {#domain-not-installed}

此错误可能会在TXT记录的域验证期间发生，即使您检查过记录已正确更新。

#### 错误原因 {#cause}

Fastly会将域锁定到注册它的初始帐户，没有其他帐户可以在未经许可的情况下注册子域。 此外，Fastly 只允许您将一个 Apex 域和关联子域分配给一个 Fastly 服务和帐户。 如果您现有的 Fastly 帐户链接了 AEM Cloud Service 域使用的相同 Apex 和子域，您将看到此错误。

#### 错误解决 {#resolution}

错误修复如下：

* 在 Cloud Manager 中安装域之前，请从现有帐户中移除 Apex 和子域。 

* 使用此选项将 Apex 域和所有子域链接到 AEM as a Cloud Service Fastly 帐户。 有关更多详细信息，请参阅[使用 Fastly 文档中的域](https://docs.fastly.com/en/guides/working-with-domains)。

* 如果您的Apex域有多个子域用于AEMas a Cloud Service和非AEMas a Cloud Service的站点，并且您希望将其链接到不同的Fastly帐户，那么请尝试将该域安装在Cloud Manager中。 如果域安装失败，请使用Fastly创建客户支持工单，以便Adobe可以代表您跟进Fastly。

>[!TIP]
>
>与Fastly解决域委派问题通常需要1 - 2个工作日。 因此，强烈建议在上线日期之前安装好域。

>[!NOTE]
>
>如果域未成功安装，请勿将站点的DNS路由到AEMas a Cloud Service的IP。

## 自定义域名的预先存在CDN配置 {#pre-existing-cdn}

如果您的自定义域名已有CDN配置，则 **自定义域名** 和 **环境** 页面，鼓励您通过UI添加这些配置，以便它们在Cloud Manager中可见和可配置。

使用 UI 迁移所有预先存在的环境配置后，消息将消失。 消息可能需要 1-2 个工作日才能消失。

请参阅文档[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)，了解更多详细信息。
