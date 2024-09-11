---
title: 自定义域名简介
description: Cloud Manager 的 UI 让您添加自定义域，以自助方式使用唯一的品牌名称标识您的站点。
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8a10634e413ea5c66845dfffa7396a4554a5b3ca
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 47%

---


# 自定义域名简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="管理自定义域名"
>abstract="Cloud Manager 的 UI 让您添加自定义域，以自助方式使用唯一的品牌名称标识您的站点。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="添加自定义域名"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="查看和更新自定义域名"

Adobe Experience Manager as a Cloud Service 配置有默认域名，以 `*.adobeaemcloud.com` 结尾。使用Cloud Manager的UI，您可以添加自定义域，以自助方式使用唯一的品牌名称标识您的站点。 即使在您将自定义域名与网站关联后，默认`*.adobeaemcloud.com`域名仍会保留。

## 什么是自定义域名？ {#what-are-custom-domain-names}

每个网站都有一个唯一的、机器可读的数字地址，例如 `184.33.123.64`。域名系统 (DNS) 让您将数字地址转换为令人印象深刻的地址，例如 `wknd.com`，从而将定制的品牌域名连接到网站。

为您的网站提供一个让客户印象深刻并能反映您品牌的域名是一个很好的做法。

您可以从域名注册机构、管理和销售域名的公司或组织购买域名。域名注册商管理 DNS 服务器上的域名。

>[!IMPORTANT]
>
>Cloud Manager 不是域名注册商，不提供 DNS 服务。

## 自定义域名并自带CDN {#byo-cdn}

AEM as a Cloud Service提供了内置的CDN（内容分发网络）服务，还允许您通过BYO（自带）CDN来与AEM一起使用。 自定义域可以安装在 AEM 管理的 CDN 或您管理的 CDN 中。

* Cloud Manager可管理在AEM管理的CDN中安装的自定义域名和证书。
* BYO CDN中安装的自定义域名和证书将直接在该CDN中进行管理。

**在您自己的CDN中管理的域不需要通过Cloud Manager进行安装** — 这些域将通过X-Forwarded-Host提供给AEM，并且与Dispatcher中定义的vhost匹配。 请参阅[ CDN 文档](/help/implementing/dispatcher/cdn.md)。

在一个环境中，您可以将两个域安装在AEM管理的CDN中，也可以将两个域安装在BYO CDN中。

## 工作流 {#workflow}

添加自定义域名需要 DNS 服务和云管理器之间的交互。由于此工作流，安装、配置和验证自定义域名需要执行多个步骤。 下表概述了所需的步骤，包括指向完成这些步骤的文档资源的链接。

| 步骤 | 描述 | 文档 |
| --- | --- | --- |
| 1 | 将 SSL 证书添加到 Cloud Manager | [添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | 将自定义域添加到Cloud Manager | [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | 通过添加指向 AEM as a Cloud Service 的 DNS CNAME 或 APEX 记录来配置 DNS 设置 | [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 4 | 查看域验证状态 | [检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 5 | 检查 DNS 记录状态 | [检查DNS记录状态](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>一般而言，用 AEM as a Cloud Service 设置自定义域名是一个简单的过程。但是，有时可能会出现域委派问题，这可能需要1 - 2个工作日才能解决。 因此，强烈建议在上线日期之前安装好域。有关详细信息，请参阅文档[检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。

## 限制 {#limitations}

在AEMaaCS中使用自定义域名有几项限制。

* Cloud Manager仅支持Sites程序的发布和预览服务的自定义域名。
   * 不支持作者服务的自定义域。
* 每个 Cloud Manager 环境最多可以为每个环境托管 500 个自定义域。
* 如果有当前正在运行的管道连接到这些环境，则无法将域名添加到这些环境。
* 同一域名不能在多个环境中使用。
* 一次只能添加一个域名。
* AEM as a Cloud Service 不支持通配符，例如`*.example.com`。
* 在添加自定义域名之前，必须为程序安装包含自定义域名（通配符证书有效）的有效SSL证书。

## 开始使用 {#get-started}

* 通过添加[SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)，开始为项目配置新的自定义域名。
* 通过查看文档[管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)来管理现有域名。
