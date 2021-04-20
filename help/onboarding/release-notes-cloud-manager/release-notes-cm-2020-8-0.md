---
title: AEM中Cloud Manager作为Cloud Service版本2020.8.0的发行说明
description: AEM中Cloud Manager作为Cloud Service版本2020.8.0的发行说明
feature: Release Information
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---


# Adobe Experience Manager中Cloud Manager作为Cloud Service 2020.8.0 {#release-notes}的发行说明

本页概述了AEM中作为Cloud Service 2020.8.0的Cloud Manager发行说明。

## 发布日期 {#release-date}

AEM中Cloud Manager作为Cloud Service 2020.8.0的发布日期为2020年8月06日。

## 新增功能 {#whats-new-cloud-manager}

* 内容审核是在Cloud Manager Sites Production Pipelines中启用的一项功能。 具有站点的项目的生产管道配置现在包括名为&#x200B;**内容审核**&#x200B;的第三个选项卡。 每当生产管道运行时，在进行自定义功能测试后，该管道中将包括新的内容审核步骤，该测试将根据包括性能、SEO（搜索引擎优化）、辅助功能、最佳实践和PWA（渐进式Web应用程序）在内的许多维度评估站点。


   >[!NOTE]
   >内容审核现已更名为Experience Audit。

   有关更多详细信息，请参阅[Experience Audit Testing](/help/implementing/cloud-manager/experience-audit-testing.md)。

* 现在，资产项目中新创建的环境将自动配置智能内容服务。

* 在Cloud Manager的&#x200B;**概述**&#x200B;页面中，可以取消休眠环境。

* 能够在页面上执行体验检查，由Google Lighthouse提供支持。 作为Cloud Manager渠道的一部分，可以根据体验KPI检查和验证最多25个页面，并在Cloud Manager用户界面中显示分数。

### 错误修复 {#bug-fixes-cm}

* 正在执行一些不必要的和不需要的SonarQube插件，作为代码质量扫描的一部分。

* 在管道执行页面上，分支名称的格式不正确。

* 在某些情况下，已完成的管道执行没有被成功记录为已完成，从而防止管道的新执行。

* 由于内部通信问题，管道执行偶尔会遇到&#x200B;*卡住*。

* 在设置新组织时，某些除系统管理员之外具有管理角色的用户被错误地授予了对Cloud Manager的访问权限。

* 在某些情况下，更新索引作业多次并行启动，导致部署失败。

* 项目卡上的工具提示并不一致。

* 在删除环境时，用户界面错误地允许尝试对其执行操作。

* Cloud Manager的&#x200B;**概述**&#x200B;页面上存在颜色不匹配。

### 已知问题 {#known-issues-cm}

* 包含无效页面，使内容审核平均分数低于应有分数。

* “内容审核”选项卡使用作者域而非发布域错误地显示了基本URL。

* 要激活“内容审核”步骤，用户必须编辑管道，并（可选）添加页面。 如果未添加任何页面，将审核主页。