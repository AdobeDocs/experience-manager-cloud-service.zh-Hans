---
title: 解决 SSL 证书错误
description: 了解如何通过识别常见原因来对SSL证书错误进行故障排除，以便维护安全连接。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b387fee62500094d712f5e1f6025233c9397f8ec
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 56%

---


# SSL证书错误疑难解答 {#certificate-errors}

如果证书安装不正确或不符合Cloud Manager的要求，则可能会出现某些错误。

+++**证书无效**

出现此错误是因为客户使用了加密的私钥并以DER格式提供了密钥。

+++

+++**私钥必须是PKCS 8格式**

出现此错误是因为客户使用了加密的私钥并以DER格式提供了密钥。

+++

+++**正确的证书顺序**

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

添加证书时，如果收到类似于以下内容的错误：

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

您可能已将客户端证书包含在证书链中。 请确保该链不包含客户端证书，然后重试。

+++

+++**证书策略**

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

+++**证书有效日期**

Cloud Manager 希望 SSL 证书自当前日期起至少 90 天有效。检查证书链的有效性。

+++