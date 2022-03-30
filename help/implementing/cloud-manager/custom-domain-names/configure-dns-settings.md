---
title: '配置 DNS 设置 '
description: 配置 DNS 设置
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 60b496024b3d012033309632999851c08f43c5d7
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# 配置 DNS 设置 {#configure-dns}

在成功验证和部署您的自定义域名后，您便可以使用DNS提供程序更新您的自定义域名的DNS记录。 这样，您的网站便能够为访客提供服务。 因此，此活动通常在上线之前完成。

## 什么是DNS设置？ {#dns-settings}

A `CNAME` 或者，一旦配置好，域的所有Internet流量都将路由到其所指向的位置。 If that location is not provisioned to serve the traffic, there will be an outage. 如果尚未进行测试，则内容中可能会出现错误。 这就是为什么此步骤始终在测试完成后完成，并且您已准备好开始使用。

要配置这些设置，您需要确定 `CNAME` 或者，必须将Apex记录配置为将您的自定义域名指向Cloud Manager域名。 以下部分将帮助您确定哪种类型的记录适合您的DNS配置。

>[!NOTE]
>
>您或贵组织中的相应个人必须能够登录或联系您的DNS提供商（您购买域的公司），并在DNS设置中进行更新。

## CNAME记录 {#cname-record}

规范名称或CNAME记录是一种DNS记录类型，可将别名映射到真或规范域名。 CNAME记录通常用于映射子域，例如 `www.example.com` 到托管该子域内容的域。

登录到您的域注册机构并创建 `CNAME` 记录以将您的自定义域名指向目标，如下表中所示。

| CNAME | 自定义域名指向Target |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## APEX记录 {#apex-record}

Apex域是不包含子域的自定义域，例如 `example.com`. 顶点域配置有 `A` , `ALIAS` 或 `ANAME` 通过DNS提供程序进行记录。 Apex域必须指向特定的IP地址。

添加以下所有内容 `A` 记录到域的DNS设置中。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
