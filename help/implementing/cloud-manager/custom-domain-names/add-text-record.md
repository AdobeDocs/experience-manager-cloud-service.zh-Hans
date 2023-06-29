---
title: 添加 TXT 记录
description: 了解如何在 Cloud Manager 中添加 TXT 记录以添加自定义域名。
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 96%

---

# 添加 TXT 记录 {#adding-txt}

DNS TXT 记录授权在 CDN 服务中托管的域。 您必须在授权 Cloud Manager 使用自定义域部署 CDN 服务并将其与后端服务关联的区域中，创建 DNS TXT 记录。 此关联完全由您控制，并授权 Cloud Manager 将服务中的内容提供给域。 此授权可授予并撤回。 TXT 记录特定于域和 Cloud Manager 环境。

在添加 TXT 记录之前，必须满足这些要求。

* 您必须能够修改组织域的 DNS 记录，或联系能够修改记录的适当人员。
* 如果您还不知道您的域主机或注册商，则必须确定其身份。

当您启动域验证时，Cloud Manager 会为您提供用于验证的名称和 TXT 值。 使用指定的名称和值将 TXT 记录添加到域的 DNS 服务器。

1. 登录到您的域主机并查找 DNS 记录部分。
1. 添加 `_aemverification.[yourdomainname]` 作为&#x200B;**名称**&#x200B;值，然后将 TXT 值与显示的值完全相加。

请参阅此表中的示例。

| 域 | 名称 | TXT 值 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | 复制 Cloud Manager UI 中显示的整个值。 该操作针对特定的域和环境。 例如：<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | 复制 Cloud Manager UI 中显示的整个值。 该操作针对特定的域和环境。 例如：<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

完成后，可以通过运行以下命令来验证结果

```shell
dig _aemverification.[yourdomainname] -t txt
```

预期结果应显示 Cloud Manager UI 中提供的 TXT 值。

例如，如果您的域是 `example.com`，然后运行：

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>有许多 [DNS 查找工具](https://www.ultratools.com/tools/dnsLookup)可用。 Google DoH 可用于查找 TXT 记录条目，并确定 TXT 纪录是否丢失或错误。
