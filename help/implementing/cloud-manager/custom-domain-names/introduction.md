---
title: 自定义域名简介
description: Cloud Manager的UI允许您添加自定义域，以便通过自助方式使用唯一的品牌名称来标识您的网站。
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: cc1b0d653706150c616ceafd002dc7594b6c7072
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 7%

---


# 自定义域名简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="管理自定义域名"
>abstract="Cloud Manager的UI允许您添加自定义域，以便通过自助方式使用唯一的品牌名称来标识您的网站。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html" text="添加自定义域名"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html" text="查看和更新自定义域名"

Cloud Manager的UI允许您添加自定义域，以便通过自助方式使用唯一的品牌名称来标识您的网站。 Adobe Experience Manager as a Cloud Service配置了默认域名，以 `*.adobeaemcloud.com`. 此默认域名会保留，即使在您将自定义域名关联到您的网站后也是如此。

## 什么是自定义域名？ {#what-are-custom-domain-names}

每个网站都具有与其关联的唯一、机器可读的数字地址，例如 `184.33.123.64`. 域名系统(DNS)允许您通过将数字地址转换为易记的地址(如 `wknd.com`.

为网站命名一个对客户来说容易记忆且能反映您品牌的域名，这是最佳做法。

您可以从域名注册机构、管理和销售域名的公司或组织处购买域名。 域名注册器管理DNS服务器上的域名。

>[!IMPORTANT]
>
>Cloud Manager不是域名注册机构，不提供DNS服务。

## 限制 {#limitations}

在AEMaaCS中使用自定义域名存在许多限制。

* Cloud Manager支持为站点程序发布和预览服务使用自定义域名。 不支持创作端的自定义域。
* 每个Cloud Manager环境最多可托管每个环境500个自定义域。
* AEMas a Cloud Service不支持通配符域。
* 在添加自定义域名之前，必须为您的程序安装包含自定义域名的有效SSL证书。 请参阅添加SSL证书以了解更多信息。
* 当当前正在运行的管道已附加到这些环境时，无法将域名添加到这些环境。
* 一次只能添加一个域名。
* 同一域名不能在多个环境中使用。

## 工作流 {#workflow}

添加自定义域名需要DNS服务与Cloud Manager之间进行交互。 因此，安装、配置和验证自定义域名需要执行许多步骤。 下表概述了所需的步骤，包括在发生常见错误时要执行的操作。

| 步骤 | 描述 | 责任 | 了解更多信息 |
|--- |--- |--- |---|
| 1 | 将SLL证书添加到Cloud Manager | 客户 | [添加 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | 添加TXT记录以验证域 | 客户 | [添加 TXT 记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | 查看域验证状态 | 客户 | [正在检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3a | 如果域验证失败，并且状态为 `Domain Verification Failure` | 客户 | [正在检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | 如果域验证失败，并且状态为 `Verified, Deployment Failed`，联系Adobe | Adobe客户关怀 | [正在检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | 通过添加指向AEMas a Cloud Service的DNS CNAME或APEX记录来配置DNS设置 | 客户 | [配置 DNS 设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | 检查DNS记录状态 | 客户 | [检查 DNS 记录状态](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | 如果DNS记录状态失败，则为 `DNS status not detected` | 客户 | [检查 DNS 记录状态](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | 如果DNS记录状态失败，则为 `DNS resolves incorrectly` | 客户 | [检查 DNS 记录状态](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
