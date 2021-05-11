---
title: 添加TXT记录
description: 添加自定义域名
exl-id: d441de29-af41-4d3e-9155-531af9702841
translation-type: tm+mt
source-git-commit: 4903f97c1bf0e7c8e96d604feb005d9611a7d9bb
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 添加TXT记录{#adding-txt}

DNS TXT记录可授权域在CDN服务中托管。 客户必须在授权Cloud Manager将CDN服务与自定义域部署并将其与后端服务关联的区域中创建DNS TXT记录。 此关联完全由客户控制，并强烈授权Cloud Manager将服务中的内容提供到域。 这项授权既可以授予，也可以撤回。

在创建TXT记录之前，您可以按照以下步骤操作：

* 能够修改组织域的DNS记录，或与可以联系的相应人员联系。
* 如果您还不知道，请确定您的域主机或注册机。

启动域验证时，Cloud Manager会为您提供用于验证的名称和TXT值。 使用指定的名称和值向域的DNS服务器添加TXT记录。

1. 登录到您的域主机并访问DNS记录部分。
1. 添加`_aemverification.[yourdomainname]`作为名称，并完全按显示的方式添加TXT值。
请参阅下表中的示例。

| 域 | 名称 | TXT值 |
|--- |--- |---|
| `example.com` | `_aemverification` | 显示在云管理器用户界面中，且特定于域和云管理器环境 |
| `test.example.com` | `_aemverification` | 显示在云管理器用户界面中，且特定于域和云管理器环境 |

完成后，您可以通过运行以下命令来验证结果：`dig _aemverification.[yourdomainname] -t txt`。
预期结果应显示在云管理器用户界面中提供的TXT值。

例如，如果您的域为`example.com`，则运行：`dig TXT _aemverification.example.com -t txt`。

>[!NOTE]
>还有各种[ DNS查找工具](https://www.ultratools.com/tools/dnsLookup),Google DoH可用于查找TXT记录条目并标识TXT记录是缺失还是错误。
