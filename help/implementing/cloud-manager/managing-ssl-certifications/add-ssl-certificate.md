---
title: 添加SSL证书 — 管理SSL证书
description: 添加SSL证书 — 管理SSL证书
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# 添加SSL证书 {#adding-an-ssl-certificate}

>[!NOTE]
>AEM as a Cloud Service将仅接受符合OV（组织验证）或EV（扩展验证）策略的证书。 DV（域验证）策略将不被接受。 此外，任何证书都必须是来自受信任的认证中心(CA)的X.509 TLS证书，且具有匹配的2048位RSA私钥。 AEMas a Cloud Service将接受域的通配符SSL证书。

配置证书需要几天时间，建议仅提前几个月配置证书。 请参阅 [获取SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) 以了解更多详细信息。

## 证书格式 {#certificate-format}

SSL文件必须采用PEM格式，才能在Cloud Manager上安装。 PEM格式内的常见文件扩展名包括 `.pem,` .`crt`, `.cer`, 和 `.cert`.

请按照以下步骤将SSL文件的格式转换为PEM:

* 将PFX转换为PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* 将P7B转换为PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* 将DER转换为PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## 重要注意事项 {#important-considerations}

* 要在Cloud Manager中安装SSL证书，用户必须具有业务所有者或部署管理器角色。

* 在任何给定时间，Cloud Manager将允许最多10个SSL证书，这些证书可以与您计划中的一个或多个环境关联，即使证书已过期也是如此。 但是，在具有此约束的程序中，Cloud Manager UI将允许安装最多50个SSL证书。 通常，证书可以覆盖多个域（最多100个SAN），因此请考虑将同一证书中的多个域分组，以便保持在此限制范围内。


## 添加证书 {#adding-a-cert}

按照以下步骤添加证书：

1. 登录到Cloud Manager。
1. 导航到 **环境** 屏幕 **概述** 页面。
1. 单击 **SSL证书** 菜单中。 此屏幕上将显示包含任何现有SSL证书详细信息的表。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 单击 **添加SSL证书** 打开 **添加SSL证书** 对话框。

   * 在 **证书名称**. 这可以是帮助您轻松引用证书的任何名称。
   * 粘贴 **证书**, **私钥** 和 **证书链** 进入各自的领域。 使用输入框右侧的粘贴图标。
这三个字段都不是可选字段，必须包含在内。

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >将显示检测到的任何错误。 您必须先解决所有错误，然后才能保存您的证书。 请参阅 [证书错误](#certificate-errors) 以了解有关解决常见错误的更多信息。

1. 单击 **保存** 提交您的证书。 您将在表中看到它显示为新行。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## 证书错误 {#certificate-errors}

### 证书策略 {#certificate-policy}

如果您看到错误“证书策略必须符合EV或OV，而不是DV策略。”，请检查您证书的策略。

通常，证书类型由策略中嵌入的OID值标识。 这些OID是唯一的，因此将证书转换为文本形式，搜索OID将确认证书具有匹配项。

您可以按如下方式查看证书详细信息。

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

此表提供标识模式。

| 图案 | 证书类型 | 可接受 |
|---|---|---|
| `2.23.140.1.2.1` | DV | 否 |
| `2.23.140.1.2.2` | OV | 是 |
| `2.23.140.1.2.3` 和 `TLS Web Server Authentication` | 有权使用https的IV证书 | 是 |

`grep`对于模式，您可以确认证书类型。

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### 正确的证书顺序 {#correct-certificate-order}

证书部署失败的最常见原因是中间证书或链证书的顺序不正确。 具体而言，中间证书文件必须以最靠近根的根证书或证书结尾，并且以从 `main/server` 证书到根。

您可以使用以下命令确定中间文件的顺序：

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

您可以验证私钥和 `main/server` 证书匹配：

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>这两个命令的输出必须完全相同。 如果找不到与 `main/server` 证书中，您将需要通过生成新的CSR和/或从SSL供应商请求更新的证书来重新为证书加密密钥。

### 证书有效期 {#certificate-validity-dates}

Cloud Manager希望SSL证书在将来至少90天内有效。 您应该检查证书链的有效性。
