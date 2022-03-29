---
title: 管理SSL证书简介
description: 了解Cloud Manager如何为您提供安装SSL证书的自助工具。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: 898f7bc46a3f1b0ac93ee43fbf7b60a11682a073
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---


# 管理SSL证书简介{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理SSL证书"
>abstract="了解Cloud Manager如何为您提供自助工具来安装和管理SSL证书，以便为您的用户保护您的网站。 Cloud Manager使用平台TLS服务来管理客户拥有并从第三方认证机构获取的SSL证书和私钥。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="查看、更新和替换SSL证书"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="检查SSL证书的状态"

Cloud Manager为您提供了自助工具来安装和管理SSL证书，以便为用户保护您的网站。 Cloud Manager使用平台TLS服务来管理客户拥有的、从第三方认证机构（如Let&#39;s Encrypt）获取的SSL证书和私钥。

## 证书简介 {#certificates}

企业使用SSL证书来保护其网站，并允许其客户信任它们。 要使用SSL协议，Web服务器需要使用SSL证书。

当实体从证书颁发机构请求证书时，CA将完成验证过程。 这可以包括验证域名控制，收集公司注册文档和订阅者协议。 实体信息验证后，CA将使用CA的私钥签署其公钥。 由于所有主要证书颁发机构在Web浏览器中都具有根证书，因此该实体的证书将通过 *信任链* Web浏览器会将其识别为受信任的证书。

>[!IMPORTANT]
>
>Cloud Manager不提供SSL证书或私钥。 必须从认证机构(CA)获得这些证书。

## Cloud Manager SSL管理功能 {#features}

Cloud Manager支持以下客户SSL证书使用选项。

* SSL证书可供多个环境使用。 即可添加一次，并多次使用。
* 每个Cloud Manager环境都可以使用多个证书。
* 私钥可能会颁发多个SSL证书。
* 每个证书通常包含多个域。
* 平台TLS服务会根据用于终止的SSL证书和托管该域的CDN服务，将请求路由到客户的CDN服务。
* AEMas a Cloud Service接受域的通配符SSL证书。

## 推荐 {#recommendations}

AEMas a Cloud Service仅支持secure `https` 站点。

* 具有多个自定义域的客户在每次添加域时都不希望上传证书。
* 此类客户将通过获取一个具有多个域的证书而受益。

## 要求 {#requirements}

* AEM as a Cloud Service将仅接受符合OV（组织验证）或EV（扩展验证）策略的证书。
* 任何证书都必须是来自受信任认证机构(CA)的X.509 TLS证书，且具有匹配的2048位RSA私钥。
* DV（域验证）策略未被接受。
* 不接受自签名证书。

OV和EV证书为用户提供额外的、经CA验证的信息，这些信息可用于确定网站所有者、电子邮件发送者或可执行代码或PDF文档的数字签字人是否可信。 DV证书不允许进行此类所有权验证。

## 限制 {#limitations}

Cloud Manager在任何给定时间最多允许安装50个SSL证书。 这些证书可以与您项目中的一个或多个环境关联，并且还包含任何过期的证书。

如果您已达到限制，请查看您的证书并考虑：

* 删除任何过期的证书。
* 对同一证书中的多个域进行分组，因为一个证书可以涵盖多个域（最多100个SAN）。

## 了解更多信息 {#learn-more}

具有必要权限的用户可以使用Cloud Manager管理程序的SSL证书。 有关使用这些功能的更多详细信息，请参阅以下文档。

* [添加 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [查看、更新或替换SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [删除 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
