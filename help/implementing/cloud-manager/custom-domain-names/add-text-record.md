---
title: 添加TXT记录
description: 添加自定义域名
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 4903f97c1bf0e7c8e96d604feb005d9611a7d9bb
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 添加TXT记录{#adding-txt}

DNS TXT记录可授权域在CDN服务中托管。 客户必须在区域中创建DNS TXT记录，以授权Cloud Manager将CDN服务与自定义域进行部署，并将其与后端服务相关联。 此关联完全由客户控制，并强烈授权Cloud Manager将服务中的内容提供到域。 该授权既可以授予，也可以撤回。

在创建TXT记录之前，可以按照以下步骤操作：

* 能够修改贵组织域的DNS记录，或联系可以的相应人员。
* 如果您还不知道域主机或注册机构，请确定该域主机或注册机构。

启动域验证时，Cloud Manager会为您提供用于验证的名称和TXT值。 使用指定的名称和值将TXT记录添加到域的DNS服务器。

1. 登录到您的域主机，然后访问DNS记录部分。
1. 将`_aemverification.[yourdomainname]`添加为名称，并完全按显示方式添加TXT值。
请参阅下表中的示例。

| 域 | 名称 | TXT值 |
|--- |--- |---|
| `example.com` | `_aemverification` | 显示在Cloud Manager UI中，且特定于域和Cloud Manager环境 |
| `test.example.com` | `_aemverification` | 显示在Cloud Manager UI中，且特定于域和Cloud Manager环境 |

完成后，您可以运行以验证结果：`dig _aemverification.[yourdomainname] -t txt`。
预期结果应显示Cloud Manager UI中提供的TXT值。

例如，如果您的域是`example.com`，则运行：`dig TXT _aemverification.example.com -t txt`。

>[!NOTE]
>还有各种[DNS查找工具](https://www.ultratools.com/tools/dnsLookup),Google DoH可用于查找TXT记录条目，并识别TXT记录是否缺失或错误。
