---
title: AEM中Cloud Manager作为Cloud Service版本2020.8.0的发行说明
description: AEM中Cloud Manager作为Cloud Service版本2020.8.0的发行说明
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.8.0 {#release-notes}

本页概述了AEM中作为Cloud Service2020.8.0的Cloud Manager发行说明。

## 发布日期 {#release-date}

AEM中Cloud Manager作为Cloud Service2020.8.0的发布日期为2020年8月6日。

## 新增功能 {#whats-new-cloud-manager}

* 内容审核是在Cloud Manager Sites Production Pipelines中启用的一项功能。 具有站点的项目的生产管道配置现在包括名为内容审核的第三 **个选项卡**。 每当运行生产管道时，在进行自定义功能测试后，管道中将包括新的内容审核步骤，该测试将根据包括性能、SEO（搜索引擎优化）、辅助功能、最佳实践和PWA（渐进式Web应用程序）在内的多个维度评估站点。


   >[!NOTE]
   >内容审核现已更名为“体验审核”。

   有关更多 [详细信息，请参](/help/implementing/cloud-manager/experience-audit-testing.md) 阅体验审核测试。

* 现在，资产项目中新创建的环境将自动配置智能内容服务。

* 冬眠环境可以从云管理器的概述页面 **解除** 。

* 能够在页面上执行体验检查，这由Google Lighthouse提供支持。 作为Cloud Manager渠道的一部分，最多可以根据体验KPI检查和验证25个页面，并在Cloud Manager UI中显示分数。

### 错误修复 {#bug-fixes-cm}

* 正在执行一些不必要的和不需要的SonarQube插件，作为代码质量扫描的一部分。

* 在管道执行页面上，分支名称的格式不正确。

* 在某些情况下，已完成的管道执行未被成功记录为已完成，从而防止了管道的新执行。

* 管道执行偶尔会因 *内部* 通信问题而卡住。

* 在设置新组织时，某些除系统管理员以外具有管理角色的用户被错误地授予了对Cloud Manager的访问权限。

* 在某些情况下，更新索引作业多次并行启动，导致部署失败。

* 项目卡上的工具提示不一致正确。

* 在删除环境时，用户界面错误地允许尝试对其执行操作。

* Cloud Manager的“概述”页面上存在颜色不 **匹配** 。

### 已知问题 {#known-issues-cm}

* 包含无效页面，使内容审核平均分数低于应有分数。

* “内容审核”选项卡使用作者域而非发布域错误地显示了基本URL。

* 要激活“内容审核”步骤，用户必须编辑管道，（可选）添加页面。 如果未添加任何页面，则将审核主页。