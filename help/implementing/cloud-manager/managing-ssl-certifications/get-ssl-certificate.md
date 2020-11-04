---
title: 获取SSL证书——管理SSL证书
description: 获取SSL证书——管理SSL证书
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# 获取SSL证书 {#getting-an-ssl-certificate}

企业使用SSL证书保护其网站，并允许其客户信任它们。 为了使用SSL协议，Web服务器需要使用SSL证书。 云管理器不提供SSL证书或私钥。 必须从认证中心(CA)获得这些证书。

当实体从证书颁发机构(CA)请求证书时，CA完成验证过程。 这可以包括验证域名控制到收集公司注册文档和订户协议。

一旦实体信息被验证，CA将使用CA的私钥签署其公钥。 由于所有主要证书颁发机构在Web浏览器中都有根证书，因此实体的证书将通过信任链 *进行链接* ，并且Web浏览器将将其识别为受信任的证书。

