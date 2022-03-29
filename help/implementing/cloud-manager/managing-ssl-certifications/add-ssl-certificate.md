---
title: 添加 SSL 证书
description: 了解如何使用Cloud Manager的自助工具添加您自己的SSL证书。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 2c87d5fb33b83ca77b97391e4b0baaf38f8dd026
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 2%

---

# 添加 SSL 证书 {#adding-an-ssl-certificate}

了解如何使用Cloud Manager的自助工具添加您自己的SSL证书。

>[!TIP]
>
>配置证书可能需要几天时间。 因此，Adobe建议提前配置证书。

## 证书格式 {#certificate-format}

SSL证书文件必须采用PEM格式才能与Cloud Manager一起安装。 PEM格式的常见文件扩展名包括 `.pem,` .`crt`, `.cer`, 和 `.cert`.

以下 `openssl` 命令可用于转换非PEM证书。

* 将PFX转换为PEM

   ```shell
   openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
   ```

* 将P7B转换为PEM

   ```shell
   openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
   ```

* 将DER转换为PEM

   ```shell
   openssl x509 -inform der -in certificate.cer -out certificate.pem
   ```

## 添加证书 {#adding-a-cert}

按照以下步骤使用Cloud Manager添加证书。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **环境** 屏幕 **概述** 页面。

1. 单击 **SSL证书** 中。 主屏幕上将显示包含任何现有SSL证书详细信息的表。

   ![添加SSL证书](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 单击 **添加SSL证书** 打开 **添加SSL证书** 对话框。

   * 在 **证书名称**.
      * 此名称仅供参考，可以是帮助您轻松引用证书的任何名称。
   * 粘贴 **证书**, **私钥**&#x200B;和 **证书链** 值。
      * 您可以使用输入框右侧的粘贴图标。
      * 这三个字段都是必填字段。

   ![“添加SSL证书”对话框](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * 将显示检测到的任何错误。
      * 您必须先解决所有错误，然后才能保存您的证书。
      * 请参阅 [证书错误](#certificate-errors) 部分以了解有关解决常见错误的更多信息。


1. 单击 **保存** 来保存您的证书。

保存后，您将在表格中看到证书显示为新行。

![保存的SSL证书](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>用户必须是 **业务所有者** 或 **部署管理器** 角色，以便在Cloud Manager中安装SSL证书。

## 证书错误 {#certificate-errors}

如果证书安装不正确或满足Cloud Manager的要求，则可能会出现某些错误。

### 证书策略 {#certificate-policy}

如果您看到以下错误，请检查证书的策略。

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

通常，证书策略由嵌入的OID值标识。 将证书输出到文本并搜索OID将显示证书的策略。

您可以将证书详细信息输出为文本，参考以下示例。

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

文本中的OID模式定义证书的策略类型。

| 图案 | 策略 | 在Cloud Manager中可接受 |
|---|---|---|
| `2.23.140.1.1` | EV | 是 |
| `2.23.140.1.2.2` | OV | 是 |
| `2.23.140.1.2.1` | DV | 否 |

按 `grep`对于输出证书文本中的OID模式，您可以确认您的证书策略。

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### 正确的证书顺序 {#correct-certificate-order}

证书部署失败的最常见原因是中间证书或链证书的顺序不正确。

中间证书文件必须以根证书或最接近根的证书结尾。 它们必须按 `main/server` 证书到根。

您可以使用以下命令确定中间文件的顺序。

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

您可以验证私钥和 `main/server` 证书匹配。

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>这两个命令的输出必须完全相同。 如果找不到与 `main/server` 证书中，您将需要通过生成新的CSR和/或从SSL供应商请求更新的证书来重新为证书加密密钥。

### 证书有效期 {#certificate-validity-dates}

Cloud Manager希望SSL证书在当前日期起至少90天内有效。 您应该检查证书链的有效性。
