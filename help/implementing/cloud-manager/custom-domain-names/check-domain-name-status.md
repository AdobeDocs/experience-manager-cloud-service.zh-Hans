---
title: 正在检查域名状态
description: 正在检查域名状态
translation-type: tm+mt
source-git-commit: 5cd22d8af20bb947e4cdab448cf8f20c6596bb2e
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---


# 正在检查域名状态 {#check-status}

您可以通过单击“域设置”页环境上的表中域名的状态图标，确定您的域名是否已成功验证。

>[!NOTE]
>在添加自定义域向导的验证步骤中选择保存后，Cloud Manager将自动触发TXT验证。 对于后续验证，必须主动选择状态旁的“再次验证”图标。 插入图像

Cloud Manager将通过TXT值验证域所有权并显示以下状态消息之一：

* **域验证失**&#x200B;败TXT值缺失或检测到有错误。 请按照说明重试。 准备就绪后，必须选择状态旁的“再次验证”图标。

* **正在进行域**&#x200B;验证。 此状态通常在您选择状态旁的“再次验证”图标后显示。

* **已验证，部署失败** TXT验证成功。 但是，CDN部署失败。 将自动通知Adobe代表。

* **域已验证和部**&#x200B;署此状态表示您的自定义域名已准备好使用。 注意：此时，您的自定义域名已准备好进行测试，并将其指向Cloud Manager域名。 转到配置DNS设置插入链接，了解如何执行此操作。

* **正在**&#x200B;删除自定义域名。

* **删除失败**&#x200B;删除自定义域名失败。 必须重试。 转到“删除自定义域名”，进一步了解主题。


## 配置DNS设置 {#configure-dns}

在成功验证和部署您的自定义域名后，您便可以使用DNS提供程序更新自定义域名的DNS记录。 这样，您的网站便能为访客服务。 因此，此活动通常在上线前完成。

>[!NOTE]
>您或组织中的相应个人必须能够登录或联系您的DNS提供者(您从中购买域的公司)，并在DNS设置中进行更新。

为此，您必须确定是否必须将DNS设置配置为将您的自 `CNAME` 定义域名指向云管理器域名的Apex记录。 配置 `CNAME` 后的记录或A记录会将域的所有Internet通信路由到其指向的任何位置。 如果该位置未设置为提供流量，则将发生中断。 如果尚未测试，内容中可能有错误。 这就是测试完成后，客户始终可以开始上线的原因。

### CNAME记录 {#cname-record}

以下部分将帮助您确定适合您的DNS配置的记录类型。

规范名称 `CNAME` 或记录是一种DNS记录类型，它将别名映射到真的或规范的域名。 CNAME记录通常用于将子域（如）映 `www.example.com` 射到托管该子域内容的域。

登录到域注册机并创建CNAME记录，将自定义域名指向目标，如下所示：

| CNAME | 自定义域名指向目标 |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

### APEX记录 {#apex-record}

apex域是不包含子域（如example.com）的自定义域。 Apex域通过DNS提供 `A` 程序 `ALIAS` 配置 `ANAME` 了、或记录。 Apex域必须指向特定的IP地址。

通过域提供程序将以下所有A记录添加到域的DNS设置中：

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## 正在检查DNS记录状态 {#check-status-dns-record}

您可以通过从域设置页的Cloud Service表中单击DNS记录的状态图标，确定您的域名是否正确解析到AEM作为环境网站。 Cloud Manager会为您的域名执行DNS查找并显示以下状态消息之一：

>[!NOTE]
>在首次成功验证和部署自定义域名时，Cloud Manager将自动触发DNS查找。 对于后续尝试，您必须主动再次 **选择状态** 旁边的“解析”图标。 插入图像

* **未检测到DNS状**&#x200B;态直到您的自定义域名成功验证和部署后，才会检测到DNS状态。 当您的自定义域名正在删除过程中时，也会观察到此状态。

* **DNS解析错误**&#x200B;这表示DNS记录配置尚未解析／指向或错误。 将自动通知Adobe代表。

   >[!NOTE]
   >您必须按照相应的 `CNAME` 说明 `A-record` 配置或配置。 转到配置DNS设置插入链接，进一步了解主题。 准备就绪后，必须选择状态旁的“再次解析”图标。

* **正在进行DNS解**&#x200B;析正在进行。 此状态通常在您选择状态旁的“再次解析”图标后显示。

* **DNS解析正确**&#x200B;您的DNS设置已正确配置。 您的站点为访客提供服务。
