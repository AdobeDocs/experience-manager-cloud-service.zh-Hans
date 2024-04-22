---
title: 自定义域名简介
description: Cloud Manager 的 UI 让您添加自定义域，以自助方式使用唯一的品牌名称标识您的站点。
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: d9cd10772252d80487f578ee73f40ec334600029
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 96%

---


# 自定义域名简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="管理自定义域名"
>abstract="Cloud Manager 的 UI 让您添加自定义域，以自助方式使用唯一的品牌名称标识您的站点。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="添加自定义域名"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="查看和更新自定义域名"

Cloud Manager 的 UI 让您添加自定义域，以自助方式使用唯一的品牌名称标识您的站点。Adobe Experience Manager as a Cloud Service 配置有默认域名，以 `*.adobeaemcloud.com` 结尾。即使您将自定义域名与网站相关联，此默认域名仍会保留。

## 什么是自定义域名？ {#what-are-custom-domain-names}

每个网站都有一个唯一的、机器可读的数字地址，例如 `184.33.123.64`。域名系统 (DNS) 让您将数字地址转换为令人印象深刻的地址，例如 `wknd.com`，从而将定制的品牌域名连接到网站。

为您的网站提供一个让客户印象深刻并能展示您品牌的域名是很好做法。

您可以从域名注册机构、管理和销售域名的公司或组织购买域名。域名注册商管理 DNS 服务器上的域名。

>[!IMPORTANT]
>
>Cloud Manager 不是域名注册商，不提供 DNS 服务。

## 自定义域名和 BYO CDN {#byo-cdn}

AEM as a Cloud Service 提供内置的内容分发网络 (CDN) 服务，但也让您自带 (BYO) CDN 以与 AEM 一起使用。自定义域可以安装在 AEM 管理的 CDN 或您管理的 CDN 中。

* 安装在 AEM 管理的 CDN 中的自定义域名（以及证书）通过 Cloud Manager 进行管理。
* 安装在您自己的 CDN 中的自定义域名（以及证书）在该特定的 CDN 中进行管理。

在您自己的 CDN 中管理的域不需要通过 Cloud Manager 安装。它们会通过 X-Forwarded-Host 提供给 AEM，并会匹配 Dispatcher 中定义的虚拟主机。请参阅[ CDN 文档](/help/implementing/dispatcher/cdn.md)。

在一个环境中，您可以有一个安装在 AEM 管理的 CDN 中的域和一个安装在您自己的 CDN 中的域。

## 工作流 {#workflow}

添加自定义域名需要 DNS 服务和云管理器之间的交互。因此，安装、配置和验证自定义域名需要执行多个步骤。 下表概述了所需的步骤，包括发生常见错误时的操作。

| 步骤 | 描述 | 责任 | 了解详细信息 |
|--- |--- |--- |---|
| 1 | 将 SSL 证书添加到 Cloud Manager | 客户 | [添加 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | 添加 TXT 记录验证域 | 客户 | [添加 TXT 记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | 查看域验证状态 | 客户 | [检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3a | 如果域验证失败，状态为 `Domain Verification Failure` | 客户 | [检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | 如果域验证失败，状态为 `Verified, Deployment Failed`，请联系 Adobe | Adobe 客户关怀部门 | [检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | 通过添加指向 AEM as a Cloud Service 的 DNS CNAME 或 APEX 记录来配置 DNS 设置 | 客户 | [配置 DNS 设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | 检查 DNS 记录状态 | 客户 | [检查 DNS 记录状态](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | 如果 DNS 记录状态失败 `DNS status not detected` | 客户 | [检查 DNS 记录状态](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | 如果 DNS 记录状态失败 `DNS resolves incorrectly` | 客户 | [检查 DNS 记录状态](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>一般而言，用 AEM as a Cloud Service 设置自定义域名是一个简单的过程。但是，有时域委派可能会发生问题，而解决此问题可能耗时 1 至 2 个工作日。因此，强烈建议在上线日期之前安装好域。有关详细信息，请参阅文档[检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。

## 限制 {#limitations}

在AEMaaCS中使用自定义域名有几项限制。

* Cloud Manager 支持为 Sites 程序提供发布和预览服务的自定义域名。不支持作者服务的自定义域。
* 每个 Cloud Manager 环境最多可以为每个环境托管 500 个自定义域。
* 如果有当前正在运行的管道连接到这些环境，则无法将域名添加到这些环境。
* 同一域名不能在多个环境中使用。
* 一次只能添加一个域名。
* AEM as a Cloud Service 不支持通配符，例如`*.example.com`。
* 在添加自定义域名之前，必须为程序安装包含自定义域名（通配符证书有效）的有效 SSL 证书。请参阅[添加 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)，以了解更多信息。
