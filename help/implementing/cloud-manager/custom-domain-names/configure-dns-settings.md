---
title: '配置DNS设置 '
description: 配置DNS设置
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 配置DNS设置{#configure-dns}

在成功验证和部署您的自定义域名后，您便可以使用DNS提供程序更新您的自定义域名的DNS记录。 这样，您的网站便能够为访客提供服务。 因此，此活动通常在上线之前完成。

>[!NOTE]
>您或贵组织中的相应个人必须能够登录或联系您的DNS提供商（您从中购买域的公司），并在DNS设置中进行更新。

要实现此目的，您必须确定是否必须将DNS设置配置为`CNAME`或Apex记录，以将您的自定义域名指向Cloud Manager域名。 `CNAME`或A记录在进行配置后，会将域的所有Internet流量路由到其指向的任何位置。 如果该位置未配置为提供流量，则将发生中断。 如果尚未进行测试，则内容中可能会出现错误。 这就是为什么始终在测试完成后完成此步骤，并且客户已准备好开始使用的原因。

## CNAME记录{#cname-record}

以下部分将帮助您确定哪种类型的记录适合您的DNS配置。

规范名称或`CNAME`记录是一种DNS记录类型，可将别名映射到真或规范域名。 CNAME记录通常用于将子域（如`www.example.com`）映射到托管该子域内容的域。

登录到您的域名注册机构并创建一个CNAME记录，以将您的自定义域名指向目标，如下所示：

| CNAME | 自定义域名指向Target |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## APEX记录{#apex-record}

Apex域是不包含子域（如example.com）的自定义域。 Apex域通过您的DNS提供程序配置了`A` 、 `ALIAS`或`ANAME`记录。 Apex域必须指向特定的IP地址。

通过域提供程序将以下所有A记录添加到域的DNS设置中：

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
