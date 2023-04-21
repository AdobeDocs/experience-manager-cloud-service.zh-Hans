---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.4.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.4.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: be39b09b609cccff916db462af9a84149d23a698
workflow-type: ht
source-wordcount: '186'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.4.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.4.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 的当前发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2023.4.0 版本的发布日期是 2023 年 4 月 13 日。下一个版本计划于 2023 年 5 月 11 日发布。

## 新增功能 {#what-is-new}

* [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)已更新到版本 41。

## 错误修复 {#bug-fixes}

* 当某个[证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)到期时，将不再从 CDN 中删除与该证书关联的[域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)和 [IP 允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。在此类情况下，该站点可继续访问。
* Cloud Manager UI 将显示更多醒目的事先警告，强调 [SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)即将到期。
* 修复了客户无法创建新环境或删除环境的罕见情况。
