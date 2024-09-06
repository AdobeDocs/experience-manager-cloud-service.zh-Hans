---
title: 添加 TXT 记录
description: 了解如何添加TXT记录以验证您对用于Cloud Manager的自定义域的所有权。
exl-id: d441de29-af41-4d3e-9155-531af9702841
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 28%

---


# 添加 TXT 记录 {#adding-txt}

了解如何添加TXT记录以验证您对用于Cloud Manager的自定义域的所有权。

## 什么是TXT记录？ {#what-is}

文本记录（也称为TXT记录）是域名系统(DNS)中的一种资源记录。 它提供将任意文本与主机名关联的功能，例如有关主机名的可读信息，如服务器或网络信息。

Cloud Manager使用特定的TXT记录来授权要在CDN服务中托管的域。 您必须在授权Cloud Manager使用自定义域部署CDN服务并将其与后端服务关联的区域中创建DNS TXT记录。 此关联完全由您控制，并授权 Cloud Manager 将服务中的内容提供给域。 此授权可授予并撤销。 TXT记录特定于域和Cloud Manager环境。

## 要求 {#requirements}

在添加 TXT 记录之前，必须满足这些要求。

* 如果您还不知道您的域主机或注册商，则必须确定其身份。
* 您必须能够编辑组织域的DNS记录，或联系能够编辑记录的适当人员。
* 必须首先添加自定义域名，如[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)文档中所述。

## 添加TXT记录以进行验证 {#verification}

在验证要与Cloud Manager一起使用的自定义域名时，会添加TXT记录。

1. 必须首先添加自定义域名，如[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)文档中所述。

1. 在&#x200B;**添加域名**&#x200B;对话框的&#x200B;**验证**&#x200B;选项卡上，Cloud Manager显示用于验证的名称和TXT值。 复制此值。

   ![域名验证](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

1. 登录到您的域主机并找到DNS记录部分。

1. 将`_aemverification.[yourdomainname]`添加为该值的&#x200B;**Name**，并添加该TXT值，它与&#x200B;**添加域名**&#x200B;对话框中显示的值完全相同。

   * 请参阅以下部分](#examples)中的[示例。

1. 将TXT记录保存到域主机。

## TXT记录示例 {#examples}

| 域 | 名称 | TXT 值 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | 复制 Cloud Manager UI 中显示的整个值。 该操作针对特定的域和环境。 例如：<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | 复制 Cloud Manager UI 中显示的整个值。 该操作针对特定的域和环境。 例如：<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

## 验证TXT记录 {#verify}

完成后，可以通过运行以下命令来验证结果。

```shell
dig _aemverification.[yourdomainname] -t txt
```

预期结果应显示Cloud Manager UI的&#x200B;**添加域名**&#x200B;对话框的&#x200B;**验证**&#x200B;选项卡上提供的TXT值。

例如，如果您的域是 `example.com`，然后运行：

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>有几个[DNS查找工具](https://www.ultratools.com/tools/dnsLookup)可用。 Google DoH 可用于查找 TXT 记录条目，并确定 TXT 纪录是否丢失或错误。

>[!NOTE]
>
>由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。
>
>Cloud Manager 将验证所有权并更新可在域设置表中看到的状态。 请参阅[检查自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)，了解更多详细信息。

## 后续步骤 {#next-steps}

现在您已创建TXT条目，可以验证域名状态了。 继续文档[检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)以继续设置自定义域名。

>[!TIP]
>
>TXT条目和CNAME或A记录可以同时设置在管理的DNS服务器上，从而节省时间。
>
>如果要执行此操作，请先查看设置自定义域名的整个过程（如[自定义域名简介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)文档中所述），特别注意文档[help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)，并相应地更新您的DNS设置。