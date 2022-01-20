---
title: AEMas a Cloud Service版本2022.01.0中的Cloud Manager发行说明
description: 以下是AEMas a Cloud Service版本2022.01.0中Cloud Manager的发行说明。
feature: Release Information
source-git-commit: 8da3976250c94d5858d07a83b0eb395fab9a3eda
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 2%

---


# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2022.01.0 {#release-notes}

本页面概述了AEMas a Cloud Service中Cloud Manager的发行说明2022.01.0。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEM Manager在as a Cloud Service中的发布日期为2022.01.0 2022年1月20日。 下一版本计划于2022年2月10日发布。

## 新增功能 {#what-is-new}

* Cloud Manager将 [当检测到使用了相同的git提交时，请避免重建代码库](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 执行多个全栈管道。
* 访问AEM环境日志现在需要 **部署管理器** 产品配置文件。 没有此配置文件的用户将在用户界面中看到一个禁用的按钮。
* UI将不允许为未启用站点作为解决方案的程序配置前端管道。
* 生成git密码后，将显示过期日期。

## 错误修复 {#bug-fixes}

* 已更正某些前端管道部署遇到的空指针异常。
* 现在，当环境运行的AEM版本已过时时，可以添加、更新和删除环境变量。
* 对于在某些极少数情况下使用计划步骤的管道，构建图像步骤将不再被标记为“错误”。
* 对于仅具有一个存储库的程序，管道执行屏幕现在将显示存储库名称。
