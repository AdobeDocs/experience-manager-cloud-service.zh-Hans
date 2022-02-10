---
title: AEMas a Cloud Service版本2022.01.0中的Cloud Manager发行说明
description: 以下是AEMas a Cloud Service版本2022.01.0中Cloud Manager的发行说明。
feature: Release Information
source-git-commit: 6b0fd14fb2038e09b59fa487427b3202d8f129dc
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 70%

---


# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2022.01.0 {#release-notes}

本页面概述了AEMas a Cloud Service中Cloud Manager的发行说明2022.01.0。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Service 2022.01.0 中的 Cloud Manager 的发布日期是 2022 年 1 月 20 日。下一个版本计划于 2022 年 2 月 10 日发布。

## 新增功能 {#what-is-new}

* 当检测到在多个全栈管道执行中使用了相同的 git commit 时，Cloud Manager 将[避免重建代码库](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)。
* 访问 AEM 环境日志现在需要 **Deployment Manager** 产品配置文件。没有此配置文件的用户将在用户界面中看到一个禁用的按钮。
* 对于未将 Sites 作为解决方案启用的程序，该 UI 不允许进行前端管道配置。
* 生成 git 密码时，将显示到期日期。

## 错误修复 {#bug-fixes}

* 某些前端管道部署遇到的空指针异常已得到纠正。
* 现在可以在环境运行过时版本的 AEM 时添加、更新和删除环境变量。
* 对于在某些极少数情况下使用计划步骤的管道，“构建映像”步骤不再被标记为错误。
* 对于只有一个存储库的程序，管道执行屏幕现在将显示存储库名称。
