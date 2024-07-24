---
title: 配置 DNS 设置
description: 了解如何为自定义域名配置DNS设置，以使您的网站能够为访客提供服务。
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 06e961febd7cb2ea1d8fca00cb3dee7f7ca893c9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 49%

---


# 配置 DNS 设置 {#configure-dns}

在自定义域名成功[验证和部署后，](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)您就可以向DNS提供商更新自定义域名的DNS记录了。 这样做可以使您的网站为访问者提供服务。因此，这项活动通常在上线前完成。

## 什么是 DNS 设置？ {#dns-settings}

`CNAME`或记录一旦配置，将把域的所有互联网流量路由到它指向的任何位置。 如果该位置未配置为服务流量，则会出现停机。如果尚未测试，则内容可能有错误。这就是为什么这个步骤总是在测试完成后完成，并且您已经准备好上线。

要配置这些设置，您需要确定是否必须配置`CNAME`或Apex记录以将您的自定义域名指向Cloud Manager域名。 本文档的以下部分将帮助您确定哪种类型的记录适合您的DNS配置。

## 要求 {#requirements}

在配置DNS记录之前，必须满足这些要求。

* 如果您还不知道您的域主机或注册商，则必须确定其身份。
* 您必须能够编辑组织域的DNS记录，或联系能够编辑记录的适当人员。
* 您必须已按照文档[检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)中所述验证配置的自定义域名

## CNAME 记录 {#cname-record}

规范名称或 CNAME 记录是一种将别名映射为真实或规范域名的 DNS 记录类型。CNAME 记录通常用于映射子域，例如 `www.example.com` 到托管该子域内容的域。

登录到您的域名注册商并创建 `CNAME` 记录，将您的自定义域名指向目标，如下表所示。

| CNAME | 自定义域名指向目标 |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Apex 记录 {#apex-record}

Apex 域是不包含子域的自定义域，例如 `example.com`。通过您的 DNS 提供商，Apex 域配置有 `A`、`ALIAS` 或 `ANAME` 记录。Apex 域必须指向特定的IP地址。

通过域提供商将以下`A`记录添加到域的DNS设置中。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## 后续步骤 {#next-steps}

为自定义域名配置DNS记录后，您需要在Cloud Manager中验证这些设置。 继续文档[检查DNS记录状态](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md)以完成您的自定义域名。
