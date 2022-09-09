---
title: AEMas a Cloud Service版本2022.02.0中的Cloud Manager发行说明
description: 以下是AEMas a Cloud Service版本2022.02.0中Cloud Manager的发行说明。
feature: Release Information
exl-id: da0643a0-78f8-4e9d-9cc9-a1a17067a08c
source-git-commit: 0c4a42595800f7f1d0869bf647c3ec99023b12c5
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 67%

---

# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2022.02.0 {#release-notes}

本页面概述了AEMas a Cloud Service中Cloud Manager的发行说明2022.02.0。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEM Manager在as a Cloud Service中的发布日期为2022.02.0 2022年2月10日。 下一版本计划于2022年3月10日发布。

## 新增功能 {#what-is-new}

* 新加速的[ Web 层配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)已引入，专门部署 HTTPD/Dispatcher 配置。
   * 您必须使用 AEM 版本`2021.12.6151.20211217T120950Z`或更新版本，并[选择启用 Dispatcher 工具的灵活模式](/help/implementing/dispatcher/disp-overview.md#validation-debug)才能使用此功能。
   * 该功能将在 2022.02.0 版本发布后的两周内分阶段推出。
* Cloud Manager 登陆页面体验已刷新，以提供改进的导航、网格/平铺视图之间的轻松切换，以及快速程序摘要的弹出窗口。
* 新失败阈值 (`< D`) 已添加到[可靠性评级量度。](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * 有严重质量问题影响系统稳定性的客户（主要与无效索引和工作流程有关）将无法部署，直到这些问题得到解决。
* `BannedPath` [根据质量规则](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)，严重性已从 blocker 变为 critical。
* 管道向导将在配置与之关联的 [Web 层配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)之前通知用户可能需要进行 AEM 环境更新。

## 错误修复 {#bug-fixes}

* 当生成新密码时，旧的 Git 存储库密码无效。
* 在极少数情况下，通过 API 更新环境变量不再干扰管道执行。
