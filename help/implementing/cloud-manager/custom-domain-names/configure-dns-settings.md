---
title: '配置 DNS 设置 '
description: 配置 DNS 设置
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 016954bc712a135886a6031deba05d92e7d5099c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 6%

---

# 配置 DNS 设置 {#configure-dns}

在成功验证和部署您的自定义域名后，您便可以使用DNS提供程序更新您的自定义域名的DNS记录。 这样，您的网站便能够为访客提供服务。 因此，此活动通常在上线之前完成。

>[!NOTE]
>您或贵组织中的相应个人必须能够登录或联系您的DNS提供商（您从中购买域的公司），并在DNS设置中进行更新。

为此，您必须确定是否必须将DNS设置配置为 `CNAME` 或将您的自定义域名指向Cloud Manager域名的Apex记录。 A `CNAME` 或者，一旦配置好，域的所有Internet流量都将路由到其所指向的位置。 如果该位置未配置为提供流量，则将发生中断。 如果尚未进行测试，则内容中可能会出现错误。 这就是为什么始终在测试完成后完成此步骤，并且客户已准备好开始使用的原因。

必须完成下列步骤，如下表所示：

| 步骤 |  | 责任 | 了解更多信息 |
|--- |--- |--- |---|
| 添加SSL证书 | 添加SSL证书 | 客户 | [添加 SSL 证书](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| 域验证 | 添加TXT记录 | 客户 | [添加 TXT 记录](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| 查看域验证状态 |  | 客户 |  |
|  | 状态：域验证失败 | 客户 | [正在检查域名状态](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | 状态：已验证，部署失败 | 联系Adobe代表 | [正在检查域名状态](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| 通过添加CNAME或APEX记录，添加指向AEMas a Cloud Service的DNS记录 | 配置DNS设置 | 客户 | [配置 DNS 设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| 检查DNS记录状态 |  | 客户 | [检查 DNS 记录状态](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 状态：未检测到DNS状态 | 客户 | [检查 DNS 记录状态](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 状态：DNS解析不正确 | 客户 |  |


## CNAME记录 {#cname-record}

以下部分将帮助您确定哪种类型的记录适合您的DNS配置。

规范名称或 `CNAME` 记录是一种将别名映射到真或规范域名的DNS记录类型。 CNAME记录通常用于映射子域，例如 `www.example.com`  到托管该子域内容的域。

登录到您的域名注册机构并创建一个CNAME记录，以将您的自定义域名指向目标，如下所示：

| CNAME | 自定义域名指向Target |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## APEX记录 {#apex-record}

Apex域是不包含子域（如example.com）的自定义域。 顶点域配置有 `A` , `ALIAS` 或 `ANAME` 通过DNS提供程序进行记录。 Apex域必须指向特定的IP地址。

通过域提供程序将以下所有A记录添加到域的DNS设置中：

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
