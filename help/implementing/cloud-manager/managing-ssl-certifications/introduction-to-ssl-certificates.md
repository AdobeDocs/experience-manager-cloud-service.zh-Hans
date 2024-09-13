---
title: SSL证书简介
description: 了解 Cloud Manager 如何为您提供自助服务工具来安装 SSL 证书。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 34%

---


# SSL证书简介{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理 SSL 证书"
>abstract="了解 Cloud Manager 如何为您提供用于安装和管理 SSL 证书的自助工具以面对您的用户保护您的站点。Cloud Manager 使用平台 TLS 服务来管理客户拥有并从第三方认证机构获得的 SSL 证书和私钥。"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="查看、更新和替换 SSL 证书"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="检查 SSL 证书的状态"


Cloud Manager提供自助服务工具来安装和管理SSL（安全套接字层）证书，确保用户的站点安全。 支持以下两个用例：

<!-- CQDOC-21758, #1 -->

| | 用例 | 描述 |
| --- | --- | --- |
| 1 | **Adobe托管证书(DV)** | Cloud Manager允许用户配置来自Adobe的DV（域验证）证书，以进行快速域设置。 DV证书是最基本级别的SSL证书，通常用于测试目的或用于通过基本加密保护网站。 DV证书在[生产程序和沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)中均可用。 创建DV证书后，除非将其删除，否则Adobe每三个月会自动更新一次。 |
| 2 | **客户管理的证书(OV/EV)** | Cloud Manager使用平台TLS（传输层安全性）服务来管理客户拥有的SSL证书和来自第三方证书颁发机构的私钥，如&#x200B;*Let&#39;s Encrypt*。 |

>[!NOTE]
>
>不允许客户上传DV（域验证）证书。


## SSL证书简介 {#certificates}

企业和组织使用SSL证书来保护其网站，并允许客户信任这些证书。 若要使用 SSL 协议，Web 服务器需要使用 SSL 证书。

当组织或企业之类的实体向证书颁发机构(CA)请求证书时，CA完成验证过程。 此流程的范围包括从验证域名控制到收集公司注册文件和订阅者协议。 在实体的信息被验证之后，CA使用CA的私钥对其公钥进行签名。 因为所有主要的证书颁发机构都在Web浏览器中有根证书，实体的证书通过&#x200B;*信任链*&#x200B;链接，并且Web浏览器将其识别为受信任的证书。

>[!IMPORTANT]
>
>Cloud Manager 不提供 SSL 证书或私钥。 这些东西必须从证书颁发机构（受信任的第三方组织）获得。 一些知名的证书颁发机构包括&#x200B;*DigiCert*、*Let&#39;s Encrypt*、*GlobalSign*、*Entrust*&#x200B;和&#x200B;*Verisign*。

Cloud Manager 支持以下客户 SSL 证书使用选项。

* 多个环境可以使用一个SSL证书。 即，可以只添加一次，也可以多次使用。
* 每个 Cloud Manager 环境都可以使用多个证书。
* 私钥可以颁发多个 SSL 证书。
* 每个证书通常包含多个域。
* 平台 TLS 服务基于终止 SSL 证书和承载该域的 CDN 服务将请求路由到客户的 CDN 服务。
* AEM as a Cloud Service 接受域的通配符 SSL 证书。

AEM as a Cloud Service仅支持安全`https`站点。 具有多个自定义域的客户不希望每次添加域时都上传证书。 这样的客户可受益于获得一个具有多个域的证书。

## SSL证书要求 {#requirements}

* AEM as a Cloud Service接受符合OV（组织验证）、EV（扩展验证）或DV（域验证）策略的证书。<!-- CQDOC-21758, #2 -->
* 任何证书都必须是来自受信任证书颁发机构的X.509 TLS证书，并具有匹配的2048位RSA私钥。
* 不接受自签名证书。

OV和EV证书提供CA验证的信息。 此类信息可帮助用户评估网站所有者、电子邮件发件人或代码或PDF文档的数字签名者是否可信。 DV 证书不允许进行此类所有权验证。

### 客户管理的SSL证书格式 {#certificate-format}

<!-- CQDOC-21758, #3 -->

SSL 证书文件必须采用 PEM 格式才能与 Cloud Manager 一起安装。PEM格式的通用文件扩展名包括`.pem,`。 `crt`, `.cer`, 和 `.cert`.

以下 `openssl` 命令可用于转换非 PEM 证书。

* 将 PFX 转化为 PEM

  ```shell
  openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
  ```

* 将 P7B 转化为 PEM

  ```shell
  openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
  ```

* 将 DER 转化为 PEM

  ```shell
  openssl x509 -inform der -in certificate.cer -out certificate.pem
  ```

## 已安装SSL证书数量的限制 {#limitations}

在任何给定时间，Cloud Manager允许最多安装50个SSL证书。 这些证书可以与程序中的一个或多个环境相关联，并且还包括任何过期的证书。

如果您已达到限制，请检查您的证书并考虑删除任何过期的证书。 或者，在同一证书中对多个域进行分组，因为一个证书可以覆盖多个域（最多100个SAN）。

## 了解详情 {#learn-more}

具有必要权限的用户可以使用 Cloud Manager 管理程序的 SSL 证书。 有关使用这些功能的详细信息，请参阅以下文档。

* [添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [管理SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

