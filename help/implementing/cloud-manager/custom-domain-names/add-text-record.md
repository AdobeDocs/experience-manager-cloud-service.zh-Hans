---
title: 添加 TXT 记录
description: 了解如何添加TXT记录以在Cloud Manager中添加自定义域名。
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 491e710223c5878bfa81c4b0a57d18ec0ec29479
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 4%

---

# 添加 TXT 记录 {#adding-txt}

DNS TXT记录可授权域在CDN服务中托管。 您必须在区域中创建DNS TXT记录，以授权Cloud Manager将CDN服务与自定义域进行部署，并将其与后端服务相关联。 此关联完全由您控制，并授权Cloud Manager将服务中的内容提供到域。 此授权可以授予，也可以撤回。 TXT记录特定于域和Cloud Manager环境。

在添加TXT记录之前，必须满足这些要求。

* 您必须能够修改贵组织域的DNS记录，或联系可以的相应人员。
* 如果您还不知道域主机或注册机构，则必须确定该域主机或注册机构。

启动域验证时，Cloud Manager会为您提供用于验证的名称和TXT值。 使用指定的名称和值将TXT记录添加到域的DNS服务器。

1. 登录到域主机并找到DNS记录部分。
1. 添加 `_aemverification.[yourdomainname]` 作为 **名称** 值，并完全按照显示的方式添加TXT值。

请参阅此表中的示例。

| 域 | 名称 | TXT值 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | 复制Cloud Manager UI中显示的整个值。 这特定于域和环境。 例如：<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | 复制Cloud Manager UI中显示的整个值。 这特定于域和环境。 例如：<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

完成后，可以运行以下命令来验证结果

```shell
dig _aemverification.[yourdomainname] -t txt
```

预期结果应显示Cloud Manager UI中提供的TXT值。

例如，如果您的域为 `example.com`，然后运行：

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>有许多 [DNS查找工具](https://www.ultratools.com/tools/dnsLookup) 可用。 Google DoH可用于查找TXT记录条目，并识别TXT记录是否缺失或错误。
