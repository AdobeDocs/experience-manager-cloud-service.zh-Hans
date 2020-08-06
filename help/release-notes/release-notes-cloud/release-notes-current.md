---
title: 作为Cloud Service的2020.8.0版本 [!DNL Adobe Experience Manager] 的发行说明。
description: '[!DNLAdobe Experience Manager]作为2020.8.0的Cloud Service发行说明。'
translation-type: tm+mt
source-git-commit: 7f089e15deff87706e0ed3c38630b52832b277d4
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 6%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.8.0 的常规发行说明。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### 新增功能 {#what-is-new-cloud-manager}

* 内容审核是在Cloud Manager Sites生产管道中启用的一项功能。 具有站点的项目的生产管道配置现在将包含名为“内容审核”的第三个选项卡。 每当运行生产管道时，在进行自定义功能测试后，管道中将包括新的内容审核步骤，该测试将根据包括性能、SEO（搜索引擎优化）、辅助功能、最佳实践和PWA（渐进式Web应用程序）在内的许多维度评估网站。环境页面已重新设计。

* 现在，资产项目中新创建的环境将自动配置智能内容服务。

* 休眠环境可以从云管理器概述页面中解除休眠。

* 现在支持身份验证绑定的私有Maven存储库。

### 错误修复 {#bug-fixes-cm}

* 正在执行一些不必要的和不需要的SonarQube插件，作为代码质量扫描的一部分。

* 在管道执行页面上，分支名称的格式不正确。

* 在某些情况下，已完成的管道执行未被成功记录为已完成，从而防止了管道的新执行。

* 管道执行偶尔会因内部通信问题而“卡住”。

* 在设置新组织时，某些除系统管理员以外具有管理角色的用户被错误地授予了对Cloud Manager的访问权限。

* 在某些情况下，更新索引作业多次并行启动，导致部署失败。

* 项目卡上的工具提示不一致正确。

* 在删除环境时，用户界面错误地允许尝试对其执行操作。

* 概述页面上的颜色不匹配。

### 已知问题 {#known-issues}

* 包含无效页面，使内容审核平均分数低于应有分数。

* “内容审核”选项卡使用作者域而非发布域错误地显示了基本URL。

* 要激活“内容审核”步骤，用户必须编辑管道，（可选）添加页面。 如果未添加任何页面，则将审核主页。

