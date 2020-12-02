---
title: 验证域
description: 验证域
translation-type: tm+mt
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# 验证域{#verify-domain-name}

DNS TXT记录授权在CDN服务中托管域。 客户必须在授权云管理器将CDN服务与自定义域部署并将其与后端服务关联的区域中创建DNS TXT记录。 此关联完全由客户控制，并强烈授权Cloud Manager将服务中的内容提供给域。 这项授权可以同时予以撤销。 TXT记录特定于域和云管理器环境。

1. 登录到域主机并访问DNS记录部分。
1. 复制并粘贴自定义域所在的DNS区域中的TXT项，与其显示完全一样。 如果您需要输入“name”，请为其指定`@`。

>[!NOTE]
>各种DNS查找工具（如[DNS查找工具](https://www.ultratools.com/tools/dnsLookup)、Google DoH）可用于查找TXT记录条目并识别TXT记录是缺失还是错误。
