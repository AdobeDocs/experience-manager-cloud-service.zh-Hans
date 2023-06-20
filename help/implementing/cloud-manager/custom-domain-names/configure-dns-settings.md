---
title: 配置 DNS 设置
description: 配置 DNS 设置
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 87%

---

# 配置 DNS 设置 {#configure-dns}

成功验证和部署自定义域名后，您可以向 DNS 提供商更新自定义域名的 DNS 记录。这样做可以使您的网站为访问者提供服务。 因此，这项活动通常在上线前完成。

## 什么是 DNS 设置？ {#dns-settings}

`CNAME` 或记录一旦配置，将把域的所有互联网流量路由到它指向的任何位置。 如果该位置未配置为服务流量，则会发生中断。 如果尚未测试，则内容可能有错误。 这就是为什么这个步骤总是在测试完成后完成，并且您已经准备好上线。

要配置这些设置，您需要确定 `CNAME` 或Apex记录必须配置为将您的自定义域名指向Cloud Manager域名。 以下部分将帮助您确定哪种类型的记录适合您的 DNS 配置。

>[!NOTE]
>
>您或您组织中的适当个人必须能够登录或联系您的 DNS 提供商（您购买域的公司），并更新您的 DNS 设置。

## CNAME 记录 {#cname-record}

规范名称或 CNAME 记录是一种将别名映射为真实或规范域名的 DNS 记录类型。 CNAME 记录通常用于映射子域，例如 `www.example.com` 到托管该子域内容的域。

登录到您的域名注册商并创建 `CNAME` 记录，将您的自定义域名指向目标，如下表所示。

| CNAME | 自定义域名指向目标 |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Apex 记录 {#apex-record}

Apex 域是不包含子域的自定义域，例如 `example.com`。通过您的 DNS 提供商，Apex 域配置有 `A`、`ALIAS` 或 `ANAME` 记录。Apex 域必须指向特定的IP地址。

通过域提供商将以下所有 `A` 记录添加到域的 DNS 设置中。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
