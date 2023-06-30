---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.7.0 的发行说明
description: 这些是 AEM as a Cloud Service 中 Cloud Manager 2023.7.0 的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 1b46f763903a1b103837ed7e8cc498ad08ce64f1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 35%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.7.0 的发行说明 {#release-notes}

本页记录了 AEM as a Cloud Service 中 Cloud Manager 2023.7.0 版本的发行说明。

>[!NOTE]
>
>参见 [此页面](/help/release-notes/release-notes-cloud/release-notes-current.md) 以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2023.7.0 版本的发布日期是 2023 年 6 月 29 日。下一个版本计划于 2023 年 8 月 10 日发布。

## 新增功能 {#what-is-new}

* Cloud Manager登陆页面上的信息卡现在指示是否 [增强的安全性](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) 为其项目启用。
* 如果开发 [管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 不包含测试步骤，用户现在可以选择在以下情况下包含测试步骤： [启动管道。](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)
   * 这将分阶段推出。
* 时间 [正在取消执行，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) 管道执行审批步骤现在要求用户提供取消的原因。
   * 这将分阶段推出。

## 错误修复 {#bug-fixes}

* 登录后，从Cloud Manager导航到创作UI再也无法重定向到Unified Shell。
* 现在，通过上线构件编辑上线日期将导航到 **上线** 制表符而不是 **增强的安全性** 选项卡。
* 在启动复制操作时，用户将无法再选择已调用复制操作的环境。
