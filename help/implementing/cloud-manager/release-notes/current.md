---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.7.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.7.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 2721cb20083eeda7546513817f1ddfe12e9cb43a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 44%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.7.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.7.0 版本的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 当前的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2023.7.0 版本的发布日期是 2023 年 6 月 29 日。计划于 2023 年 8 月 10 日发布下一个版本。

## 新增功能 {#what-is-new}

* Cloud Manager 登陆页面上的卡片现在指示是否为其程序启用了[增强安全性](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。
* 如果开发 [管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 不包含测试步骤，用户现在可以选择在以下情况下包含测试步骤： [启动管道。](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)
   * 这将分阶段推出。
* 时间 [正在取消执行，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) 管道执行审批步骤现在要求用户提供取消的原因。
   * 这将分阶段推出。
* 用户现在可以访问 [复制内容过程中的日志。](/help/implementing/developing/tools/content-copy.md#accessing-logs)
   * 仅当源环境和目标环境均采用AEM版本时，此选项才可用 `2023.7.12549` 或更高。

## 错误修复 {#bug-fixes}

* 登录后，从Cloud Manager导航到创作UI再也无法重定向到Unified Shell。
* 现在，通过上线构件编辑上线日期将导航到 **上线** 制表符而不是 **增强的安全性** 选项卡。
* 在启动复制操作时，用户将无法再选择已调用复制操作的环境。
