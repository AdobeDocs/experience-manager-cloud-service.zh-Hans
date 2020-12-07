---
title: '配置DNS设置 '
description: 配置DNS设置
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# 配置DNS设置{#configure-dns}

在成功验证和部署您的自定义域名后，您便可以使用DNS提供程序更新自定义域名的DNS记录。 这样，您的网站便能为访客服务。 因此，此活动通常在上线前完成。

>[!NOTE]
>您或组织中的相应个人必须能够登录或联系您的DNS提供者(您从中购买域的公司)，并在DNS设置中进行更新。

为此，您必须确定是否必须将DNS设置配置为`CNAME`或Apex记录，将您的自定义域名指向Cloud Manager域名。 设置`CNAME`或A记录后，会将域的所有Internet通信路由到其指向的任何位置。 如果该位置未设置为提供流量，则将发生中断。 如果尚未测试，内容中可能有错误。 这就是测试完成后，客户始终可以开始上线的原因。

## CNAME记录{#cname-record}

以下部分将帮助您确定适合您的DNS配置的记录类型。

规范名称或`CNAME`记录是一种DNS记录类型，将别名映射到真的或规范域名。 CNAME记录通常用于将子域（如`www.example.com`）映射到承载该子域内容的域。

登录到域注册机并创建CNAME记录，将自定义域名指向目标，如下所示：

| CNAME | 自定义域名指向目标 |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## APEX记录{#apex-record}

apex域是不包含子域（如example.com）的自定义域。 Apex域通过DNS提供程序配置了`A` 、 `ALIAS`或`ANAME`记录。 Apex域必须指向特定的IP地址。

通过域提供程序将以下所有A记录添加到域的DNS设置中：

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
