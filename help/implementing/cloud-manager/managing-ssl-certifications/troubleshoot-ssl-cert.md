---
title: SSL证书问题疑难解答
description: 了解如何通过识别常见原因来解决SSL证书问题，以便维护安全连接。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1017f84564cedcef502b017915d370119cd5a241
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 37%

---


# SSL证书问题疑难解答 {#certificate-problems}

了解如何通过识别常见原因来解决SSL证书问题，以便维护安全连接。

+++**证书无效**

## 证书无效 {#invalid-certificate}

出现此错误是因为客户使用了加密的私钥并以DER格式提供了密钥。

+++

+++**私钥必须是PKCS 8格式**

## 私钥必须是PKCS 8格式 {#pkcs-8}

出现此错误是因为客户使用了加密的私钥并以DER格式提供了密钥。

+++

+++**正确的证书顺序**

## 正确的证书顺序 {#certificate-order}

证书部署失败的最常见原因是中间证书或链证书的顺序不正确。

中间证书文件必须以根证书或最接近根的证书结尾。它们必须从 `main/server` 证书降序到根目录。

可以使用以下命令确定中间文件的顺序。

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

您可以使用以下命令验证私钥和 `main/server` 证书是否匹配。

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>这两个命令的输出必须完全相同。如果您找不到 `main/server` 证书的匹配私钥，您需要通过生成新的 CSR 和/或向 SSL 供应商请求更新的证书来重新键入证书。

+++

+++**删除客户端证书**

## 删除客户端证书 {#client-certificates}

添加证书时，如果收到类似于以下内容的错误：

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

您可能已将客户端证书包含在证书链中。 请确保该链不包含客户端证书，然后重试。

+++

+++**证书策略**

## 证书策略 {#policy}

如果您看到以下错误，请检查证书的策略。

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

嵌入的OID值通常标识证书策略。 将证书输出到文本并搜索OID将显示证书的策略。

您可以使用以下示例作为指导，将证书详细信息输出为文本。

```text
openssl x509 -in 9178c0f58cb8fccc.pem -text
certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            91:78:c0:f5:8c:b8:fc:cc
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, ST = Arizona, L = Scottsdale, O = "GoDaddy.com, Inc.", OU = http://certs.godaddy.com/repository/, CN = Go Daddy Secure Certificate Authority - G2
        Validity
            Not Before: Nov 10 22:55:36 2021 GMT
            Not After : Dec  6 15:35:06 2022 GMT
        Subject: C = US, ST = Colorado, L = Denver, O = Alexandra Alwin, CN = adobedigitalimpact.com
        Subject Public Key Info:
...
```

文本中的 OID 模式定义证书的策略类型。

| 图案 | 策略 | 在 Cloud Manager 中可接受 |
|---|---|---|
| `2.23.140.1.1` | EV | 是 |
| `2.23.140.1.2.2` | OV | 是 |
| `2.23.140.1.2.1` | DV | 否 |

通过 `grep`ping 输出证书文本中的 OID 模式，您可以确认您的证书策略。

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```
+++

+++**证书有效期

## 证书有效期 {#validity}

Cloud Manager 希望 SSL 证书自当前日期起至少 90 天有效。检查证书链的有效性。

+++

+++**错误的SAN证书应用于我的域

## 对我的域应用了错误的SAN证书 {#wrong-san-cert}

假设您要将`dev.yoursite.com`和`stage.yoursite.com`链接到非生产环境，将`prod.yoursite.com`链接到生产环境。

为了配置这些域的CDN，您需要为每个域安装一个证书，因此您安装一个用于非生产域覆盖`*.yoursite.com`的证书，另一个用于生产域覆盖`*.yoursite.com`的证书。

此配置有效。 但是，当您更新其中一个证书时，因为两个证书都涵盖相同的SAN条目，所以CDN将在所有适用的域上安装最新的证书，这可能显示为意外情况。

尽管这可能意外，但这不是错误，并且是基础CDN的标准行为。 如果您有两个或更多SAN证书覆盖同一SAN域条目，如果该域由一个证书覆盖，而另一个证书已更新，则现在将为域安装后者。

+++
