---
title: 验证域
description: 验证域
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# 验证域 {#verify-domain-name}

DNS TXT记录可授权域在CDN服务中托管。 客户必须在区域中创建DNS TXT记录，以授权Cloud Manager将CDN服务与自定义域进行部署，并将其与后端服务相关联。 此关联完全由客户控制，并强烈授权Cloud Manager将服务中的内容提供到域。 该授权既可以授予，也可以撤回。 TXT记录特定于域和Cloud Manager环境。

1. 登录到您的域主机，然后访问DNS记录部分。
1. 将TXT条目复制并粘贴到自定义域所在的DNS区域中，与显示的完全一样。 如果需要输入“name”，请提供 `@`.

>[!NOTE]
>各种DNS查找工具，如 [DNS查找工具](https://www.ultratools.com/tools/dnsLookup),Google DoH可用于查找TXT记录条目，并识别TXT记录是否缺失或错误。
