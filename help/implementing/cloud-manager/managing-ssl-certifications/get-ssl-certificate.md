---
title: 获取SSL证书——管理SSL证书
description: 获取SSL证书——管理SSL证书
translation-type: tm+mt
source-git-commit: fecbd0b4d5cfd8aa970c235c79158bea44403c09
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# 获取SSL证书{#getting-an-ssl-certificate}

企业使用SSL证书保护其网站，并允许其客户信任它们。 为了使用SSL协议，Web服务器需要使用SSL证书。 云管理器不提供SSL证书或私钥。 必须从认证中心(CA)获得这些证书。

当实体从证书颁发机构请求证书时，CA将完成验证过程。 这可以包括验证域名控制到收集公司注册文档和订户协议。 一旦实体信息被验证，CA将使用CA的私钥签署其公钥。 由于所有主要证书颁发机构在Web浏览器中都有根证书，因此实体的证书将通过&#x200B;*信任链*&#x200B;链接，并且Web浏览器将将其识别为受信任的证书。

>[!NOTE]
>AEM作为Cloud Service将仅接受OV（组织验证）或EV（扩展验证）证书。 不接受DV（域验证）或自签名证书。 OV和EV证书为用户提供额外的、经CA验证的信息，他们可以使用这些信息来确定网站所有者、电子邮件发件人或可执行代码或PDF文档的数字签字人是否可信。 DV证书是通用的，并且价格低廉。 但是，它们不允许所有权验证。

