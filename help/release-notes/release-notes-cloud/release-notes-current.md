---
title: ' [!DNL Adobe Experience Manager]  云服务 2020.8.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] 云服务 2020.8.0 版的发行说明。'
translation-type: tm+mt
source-git-commit: dafdbffa96cd565379a700c696586222f43022c2
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 12%

---


# [!DNL Adobe Experience Manager] 云服务 2020.8.0 版的发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.8.0 版的常规发行说明。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品控制台功能现已可用。 这使AEM中的营销人员／作者能够视图和浏览存储在商务后端中的类别和产品。 还提供了产品控制台中目录和产品属性支持。

* 产品和类别选择器经过改进，可让营销人员通过SKU选择产品或通过类别ID选择类别。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### 新增功能 {#what-is-new-cloud-manager}

* 内容审核是在Cloud Manager Sites Production Pipelines中启用的一项功能。 具有站点的项目的生产管道配置现在包括名为内容审核的第三 **个选项卡**。 每当运行生产管道时，在进行自定义功能测试后，管道中将包括新的内容审核步骤，该测试将根据包括性能、SEO（搜索引擎优化）、辅助功能、最佳实践和PWA（渐进式Web应用程序）在内的多个维度评估站点。

   Refer to [Content Audit Testing](/help/implementing/developing/introduction/understand-test-results.md#content-audit-testing) for more details.

* 现在，资产项目中新创建的环境将自动配置智能内容服务。

* 冬眠环境可以从云管理器的概述页面 **解除** 。

* 现在支持身份验证绑定的私有Maven存储库。

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

## 内容传输工具 {#content-transfer-tool}

可查看本节以了解新增功能以及内容传输工具版本1.0.4的更新。

### 新增功能 {#what-is-new-ctt}

* 内容传输工具现在支持共享S3数据存储。

### 错误修复 {#ctt-bug-fixes}

* 为工具添加了更多超时以完成操作。

* 早期版本的UI有时显示成功的提取，即使日志显示错误。

