---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.7.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.7.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 2721cb20083eeda7546513817f1ddfe12e9cb43a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.7.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.7.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2023.7.0 版本的发布日期是 2023 年 6 月 29 日。计划于 2023 年 8 月 10 日发布下一个版本。

## 新增功能 {#what-is-new}

* Cloud Manager 登陆页面上的卡片现在指示是否为其项目启用了[增强安全性](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。
* 如果开发[管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)不包含测试步骤，则用户现在可在其[启动该管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)时包括测试步骤。
   * 此功能将分阶段推出。
* 在[取消执行](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)时，管道执行审批步骤现在要求用户提供取消的原因。
   * 此功能将分阶段推出。
* 用户现在可以访问[复制内容过程中的日志](/help/implementing/developing/tools/content-copy.md#accessing-logs)。
   * 此选项仅在源环境和目标环境均采用 AEM 版本 `2023.7.12549` 或更高版本时可用。

## 错误修复 {#bug-fixes}

* 登录后从 Cloud Manager 导航到创作 UI 不再无法重定向到 Unified Shell。
* 通过上线构件编辑上线日期现在导航到&#x200B;**上线**&#x200B;选项卡而非&#x200B;**增强安全性**&#x200B;选项卡。
* 在开始复制操作时，用户将无法再选择已调用复制操作的环境。
