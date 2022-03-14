---
title: AEMas a Cloud Service版本2022.02.0中的Cloud Manager发行说明
description: 以下是AEMas a Cloud Service版本2022.02.0中Cloud Manager的发行说明。
feature: Release Information
exl-id: da0643a0-78f8-4e9d-9cc9-a1a17067a08c
source-git-commit: 8162d1d6ddeff867507f749f223c0111b6856122
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2022.02.0 {#release-notes}

本页面概述了AEMas a Cloud Service中Cloud Manager的发行说明2022.02.0。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEM Manager在as a Cloud Service中的发布日期为2022.02.0 2022年2月10日。 下一版本计划于2022年3月10日发布。

## 新增功能 {#what-is-new}

* 新加速 [网层配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 已引入以专门部署HTTPD/调度程序配置。
   * 您必须使用AEM版本 `2021.12.6151.20211217T120950Z` 或较新和 [选择启用调度程序工具的灵活模式](/help/implementing/dispatcher/disp-overview.md#validation-debug) 以使用此功能。
   * 此功能将在2022.02.0版后的两周内分阶段推出。
* Cloud Manager登陆页面体验已刷新，以提供改进的导航、在网格/图块视图之间轻松切换，以及用于快速获取项目摘要的弹出窗口。
* 新的失败阈值(`< D`) [可靠性评级量度。](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * 存在严重质量问题且影响系统稳定性的客户（主要与无效索引和工作流程相关）在这些问题得到解决之前将无法部署。
* 的严重性 `BannedPath` [质量规则](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) 已从阻止程序更改为关键。
* 在配置 [网层配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 关联。

## 错误修复 {#bug-fixes}

* 现在，在生成新密码时，旧的Git存储库密码始终无效。
* 在极少数情况下，通过API更新环境变量不再会妨碍管道执行。
