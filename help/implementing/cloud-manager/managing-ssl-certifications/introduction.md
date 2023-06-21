---
title: 管理 SSL 证书简介
description: 了解 Cloud Manager 如何为您提供自助服务工具来安装 SSL 证书。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 83%

---


# 管理 SSL 证书简介{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理 SSL 证书"
>abstract="了解 Cloud Manager 如何为您提供用于安装和管理 SSL 证书的自助工具以面对您的用户保护您的站点。Cloud Manager 使用平台 TLS 服务来管理客户拥有并从第三方认证机构获得的 SSL 证书和私钥。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="查看、更新和替换 SSL 证书"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="检查 SSL 证书的状态"

Cloud Manager为您提供自助服务工具来安装和管理SSL证书，以便您能够为用户保护您的站点。 Cloud Manager使用平台TLS服务来管理客户拥有并从第三方认证机构（如Let’s Encrypt）获得的SSL证书和私钥。

## 证书简介 {#certificates}

企业使用 SSL 证书来保护其网站，并允许客户信任这些证书。 要使用SSL协议，Web服务器需要使用SSL证书。

当实体从证书颁发机构 (CA) 请求证书时，CA 完成验证过程。 这可以从验证域名控制到收集公司注册文件和订阅者协议。 一旦实体的信息得到验证，CA 将使用 CA 的私钥对其公钥进行签名。 由于所有主要的证书颁发机构在Web浏览器中都拥有根证书，因此实体的证书通过 *信任链* 并且Web浏览器会将其识别为可信证书。

>[!IMPORTANT]
>
>Cloud Manager 不提供 SSL 证书或私钥。 这些必须从证书颁发机构 (CA) 处获得。

## Cloud Manager SSL 管理功能 {#features}

Cloud Manager 支持以下客户 SSL 证书使用选项。

* SSL 证书可以由多个环境使用。 即，可以仅添加一次，使用多次。
* 每个 Cloud Manager 环境都可以使用多个证书。
* 私钥可以颁发多个 SSL 证书。
* 每个证书通常包含多个域。
* 平台 TLS 服务基于终止 SSL 证书和承载该域的 CDN 服务将请求路由到客户的 CDN 服务。
* AEM as a Cloud Service 接受域的通配符 SSL 证书。

## 推荐 {#recommendations}

AEM as a Cloud Service 仅支持安全`https`站点。

* 具有多个自定义域的客户不希望每次添加域时都得上载证书。
* 此类客户将因获得一个具有多个域的证书而受益。

## 要求 {#requirements}

* AEM as a Cloud Service 将只接受符合 OV（组织验证）或 EV（扩展验证）策略的证书。
* 任何证书都必须是来自可信证书颁发机构 (CA) 的 X.509 TLS 证书，该证书具有匹配的 2048 位 RSA 私钥。
* 不接受 DV（域验证）策略。
* 不接受自签名证书。

OV 和 EV 证书为用户提供额外的 CA 验证信息，可用于确定网站所有者、电子邮件发件人或可执行代码或 PDF 文档的数字签名人是否可信。DV 证书不允许进行此类所有权验证。

## 限制 {#limitations}

在任何给定时间，Cloud Manager 将允许最多安装 50 个 SSL 证书。 这些证书可以与程序中的一个或多个环境相关联，还包括任何过期的证书。

如果您已达到限制，请检查您的证书并考虑：

* 正在删除任何过期的证书。
* 在同一证书中对多个域进行分组，因为一个证书可以覆盖多个域（最多 100 个 SAN）。

## 了解详情 {#learn-more}

具有必要权限的用户可以使用 Cloud Manager 管理程序的 SSL 证书。 有关使用这些功能的详细信息，请参阅以下文档。

* [添加 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [查看、更新或替换 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [删除 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
