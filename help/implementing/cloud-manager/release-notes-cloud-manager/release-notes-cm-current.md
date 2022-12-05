---
title: Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2022.12.0 发行说明
description: 这些是 AEM as a Cloud Service 中的 Cloud Manager 2022.12.0 发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: aa7f2175e2a43a318a6171e622d292ed3a8e958b
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 48%

---


# Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2022.12.0 发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2022.12.0 的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 的当前发行说明。

## 发布日期 {#release-date}

AEM Manager版本2022.12.0的发布日期是2022年11月29日。 下一个版本计划于 2023 年 1 月 19 日发布。

## 新增功能 {#what-is-new}

* 通知 [AEM维护更新](/help/overview/what-is-new-and-different.md#aem-updates) 将在Cloud Manager UI中显示。 此更改将在2022.12.0版本发布后的几周内分阶段实施。
* 通过 [内容传输工具(CTT)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md) 进行中，开发人员控制台和Cloud Manager中的环境状态将显示为 `Ingestion in Progress`.
* 提高了 [Cloud Manager 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)的可用性和可靠性。

## 错误修复 {#bug-fixes}

* 为防止 [前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 在同一环境中执行管道时从运行。
* 为防止 `PATCH /program//environment//variables` 对具有 `FAILED` 状态。
