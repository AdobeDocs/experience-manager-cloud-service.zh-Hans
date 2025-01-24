---
title: SSL 证书简介
description: 了解Cloud Manager为您提供的自助服务工具，用于安装和管理SSL证书。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3d9ad70351bfdedb6d81e90d9d193fac3088a3ec
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 19%

---


# SSL 证书简介{#introduction}

了解Cloud Manager为您提供的自助服务工具，用于安装和管理SSL（安全套接字层）证书。

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理 SSL 证书"
>abstract="了解 Cloud Manager 如何为您提供用于安装和管理 SSL 证书的自助工具以面对您的用户保护您的站点。Cloud Manager 使用平台 TLS 服务来管理客户拥有并从第三方认证机构获得的 SSL 证书和私钥。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="查看、更新和替换 SSL 证书"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="检查 SSL 证书的状态"

## 什么是SSL证书？ {#overview}

企业和组织使用SSL（安全套接字层）证书来保护其网站，并允许客户信任这些证书。 要使用SSL协议，Web服务器需要SSL证书。

当组织或企业之类的实体向证书颁发机构(CA)请求证书时，CA完成验证过程。 此流程的范围包括从验证域名控制到收集公司注册文件和订阅者协议。 在实体的信息被验证之后，CA使用CA的私钥对其公钥进行签名。 因为所有主要的证书颁发机构都在Web浏览器中有根证书，实体的证书通过&#x200B;*信任链*&#x200B;链接，并且Web浏览器将其识别为受信任的证书。

>[!IMPORTANT]
>
>Cloud Manager 不提供 SSL 证书或私钥。 这些部分必须从证书颁发机构（受信任的第三方组织）获得。 一些知名的证书颁发机构包括&#x200B;*DigiCert*、*Let&#39;s Encrypt*、*GlobalSign*、*Entrust*&#x200B;和&#x200B;*Verisign*。

## 使用Cloud Manager管理证书 {#cloud-manager}

Cloud Manager提供自助服务工具来安装和管理SSL证书，确保用户的站点安全。 Cloud Manager支持两种管理证书的模型。

| | 模型 | 描述 |
| --- | --- | --- |
| A | **[托管SSL证书(DV)Adobe](#adobe-managed)** | Cloud Manager允许用户配置Adobe为快速域设置提供的DV（域验证）证书。 |
| B | **[客户管理的SSL证书(OV/EV)](#customer-managed)** | Cloud Manager提供平台TLS（传输层安全性）服务，允许您管理您拥有的OV和EV SSL证书以及来自第三方证书颁发机构的私钥，例如&#x200B;*让我们加密*。 |

这两种模型都提供了以下用于管理证书的常规功能：

* 每个 Cloud Manager 环境都可以使用多个证书。
* 私钥可以颁发多个 SSL 证书。
* 平台 TLS 服务基于终止 SSL 证书和承载该域的 CDN 服务将请求路由到客户的 CDN 服务。

>[!IMPORTANT]
>
>[要添加自定义域并将其与环境](/help/implementing/cloud-manager/custom-domain-names/introduction.md)关联，您必须具有覆盖该域的有效SSL证书。

### Adobe托管(DV) SSL证书 {#adobe-managed}

DV证书是最基本级别的SSL证书，通常用于测试目的或用于通过基本加密保护网站。 DV证书在[生产程序和沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)中均可用。

创建DV证书后，除非将其删除，否则Adobe每三个月会自动更新一次。

### 客户管理的OV/EV SSL证书 {#customer-managed}

OV和EV证书提供CA验证的信息。 此类信息可帮助用户评估网站所有者、电子邮件发件人或代码或PDF文档的数字签名者是否可信。 DV 证书不允许进行此类所有权验证。

此外，OV和EV通过Cloud Manager中的DV证书提供这些功能。

* 多个环境可以使用OV/EV证书。 即，可以只添加一次，也可以多次使用。
* 每个OV/EV证书通常包含多个域。
* Cloud Manager接受域的通配符OV/EV证书。

>[!TIP]
>
>如果您有多个自定义域，则可能不希望每次添加新域时都上载证书。 在这种情况下，您可以从获取覆盖多个域的单个证书中获益。

#### 客户管理的OV/EV SSL证书要求 {#requirements}

如果您选择添加自己的客户管理的OV/EV SSL证书，它必须满足以下要求：

* 证书必须符合OV（组织验证）或EV（扩展验证）策略。
   * Cloud Manager不支持添加您自己的DV（域验证）证书。
* 不支持自签名证书。
* 任何证书都必须是来自受信任证书颁发机构的X.509 TLS证书，并具有匹配的2048位RSA私钥。

#### 证书管理最佳实践

* **避免证书重叠：**

   * 为了确保顺利的证书管理，请避免部署与同一域匹配的重叠证书。 例如，将通配符证书(*.example.com)与特定证书(dev.example.com)一起使用可能会导致混淆。
   * TLS层优先处理最具体和最近部署的证书。

  示例场景：

   * “开发证书”涵盖`dev.example.com`并部署为`dev.example.com`的域映射。
   * “暂存证书”涵盖`stage.example.com`并部署为`stage.example.com`的域映射。
   * 如果“暂存证书”在&#x200B;*“开发证书”之后部署/更新*，则它还会为`dev.example.com`提供请求。

     要避免此类冲突，请确保将证书的作用域仔细限定为其目标域。

* **通配符证书：**

  虽然支持通配符证书（例如`*.example.com`），但应仅在必要时使用。 在重叠的情况下，以更具体的证书为准。 例如，特定证书为`dev.example.com`提供服务，而不是通配符(`*.example.com`)。

* **验证和故障排除：**
在尝试使用Cloud Manager安装证书之前，Adobe建议您使用`openssl`等工具在本地验证证书的完整性。 例如，

  `openssl verify -untrusted intermediate.pem certificate.pem`


<!--
>[!NOTE]
>
>If two certificates cover the same domain are installed, the one that is more exact is applied.
>
>For example, if your domain is `dev.adobe.com` and you have one certificate for `*.adobe.com` and another for `dev.adobe.com`, the more specific one (`dev.adobe.com`) is used.
-->

#### 客户管理的证书的格式 {#certificate-format}

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

在任何给定时间，Cloud Manager最多支持50个已安装的证书。 这些证书可以与程序中的一个或多个环境相关联，并且还包括任何过期的证书。

如果您已达到限制，请检查您的证书并考虑删除任何过期的证书。 或者，在同一证书中对多个域进行分组，因为一个证书可以覆盖多个域（最多100个SAN）。

## 了解详情 {#learn-more}

具有必要权限的用户可以使用 Cloud Manager 管理程序的 SSL 证书。 有关使用这些功能的详细信息，请参阅以下文档。

* [添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [管理SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

