---
title: AEM 2020.8.0版中Cloud Manageras a Cloud Service的发行说明
description: AEM 2020.8.0版中Cloud Manageras a Cloud Service的发行说明
feature: Release Information
exl-id: 70674e16-f9ba-4777-98fe-34161e90a481
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud Service 2020.8.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2020.8.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM 2020.8.0版中Cloud Manager的发布日期是2020年8月6日。

## 新增功能 {#whats-new-cloud-manager}

* 内容审核是Cloud Manager Sites Production Pipelines中启用的一项功能。 现在，具有Sites的程序的生产管道配置包含一个名为 **内容审核**. 每当运行生产管道时，一个新的内容审核步骤将在自定义功能测试后包含在管道中，该步骤将根据多个维度(包括性能、SEO（搜索引擎优化）、辅助功能、最佳实践和PWA（渐进式Web应用程序）在内)来评估站点。


   >[!NOTE]
   >内容审核现已重命名为“体验审核”。

   请参阅 [体验审核测试](/help/implementing/cloud-manager/experience-audit-testing.md) 以了解更多详细信息。

* 现在， Assets项目中新建的环境将自动配置为智能内容服务。

* 可以在Cloud Manager的中解除休眠环境的休眠 **概述** 页面。

* 能够在页面上执行由Google Lighthouse提供支持的“体验检查”功能。 作为Cloud Manager管道的一部分，可通过体验KPI检查和验证多达25个页面，并在Cloud Manager UI中显示得分。

### 错误修复 {#bug-fixes-cm}

* 在代码质量扫描中，正在执行一些不必要的和不需要的SonarQube插件。

* 在管道执行页面上，分支名称的格式不正确。

* 在某些情况下，已完成的管道执行未被成功记录为已完成，从而阻止管道的新执行。

* 管道执行偶尔会收到 *卡住* 因内部通信问题。

* 在配置新组织时，系统管理员以外的一些具有管理角色的用户错误地获得了Cloud Manager的访问权限。

* 在某些情况下，更新索引作业并行多次启动，从而导致部署失败。

* 程序卡片上的工具提示并不一致。

* 用户界面错误地允许在删除环境时尝试在环境中执行操作。

* Cloud Manager的 **概述** 页面。

### 已知问题 {#known-issues-cm}

* 包含的页面无效，导致内容审核平均分数低于应有值。

* “内容审核”选项卡未正确显示使用创作域而非发布域的基本URL。

* 要激活“内容审核”步骤，用户必须编辑管道，并（可选）添加页面。 如果未添加页面，则会审核主页。
