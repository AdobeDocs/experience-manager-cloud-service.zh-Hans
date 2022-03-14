---
title: 获取SSL证书 — 管理SSL证书
description: 获取SSL证书 — 管理SSL证书
exl-id: a3a247e5-164a-4c9c-aeed-bde882635e6f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# 获取 SSL 证书 {#getting-an-ssl-certificate}

企业使用SSL证书来保护其网站，并允许其客户信任它们。 要使用SSL协议，Web服务器需要使用SSL证书。 Cloud Manager不提供SSL证书或私钥。 必须从认证机构(CA)获取这些证书。

当实体从证书颁发机构请求证书时，CA将完成验证过程。 这可以包括验证域名控制，收集公司注册文档和订阅者协议。 实体信息验证后，CA将使用CA的私钥签署其公钥。 由于所有主要证书颁发机构在Web浏览器中都具有根证书，因此该实体的证书将通过 *信任链* Web浏览器会将其识别为受信任的证书。

>[!NOTE]
>AEMas a Cloud Service将仅接受OV（组织验证）或EV（扩展验证）证书。 DV（域验证）或自签名证书将不被接受。 OV和EV证书为用户提供额外的、经CA验证的信息，用户可以使用这些信息来确定网站所有者、电子邮件发送者或可执行代码或PDF文档的数字签字人是否可信。 DV证书是通用的，并且价格低廉。 但是，它们不允许进行所有权验证。
>此外，任何证书都必须是来自受信任的认证中心(CA)的X.509 TLS证书，且具有匹配的2048位RSA私钥。
