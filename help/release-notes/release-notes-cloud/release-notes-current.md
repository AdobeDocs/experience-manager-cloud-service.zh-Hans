---
title: Adobe Experience Manager 云服务 2020.5.0 发行说明
description: Experience Manager 2020.5.0 发行说明
translation-type: tm+mt
source-git-commit: 8fe1f6f1c7c6a608ee1ca42836ee91e83487428d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 18%

---


# AEM 云服务 2020.5.0 发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.5.0 的常规发行说明。

## 发布日期 {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.5.0 is May 07, 2020.

## What&#39;s New in AEM Sites {#aem-sites}

可查看本节以了解AEM中AEM Sites作为云服务版本2020.5.0的新增功能和更新。

* 现在，在处理批量页面移动和作为异步作业进行转出后，可以获得详细的作业信息。
* 复制／粘贴页面树时，现在提供选择仅粘贴根页面或粘贴树的子页面。
* 导出到Adobe目标工作区的AEM体验片段现在显示为目标中唯一的优惠类型和优惠源。
* MSM —— 使 *用* publish触发器现在可成功为Live Copy源中的组件删除事件，即删除Live Copy源中已删除的组件。
* MSM - Live Copy组件现在从Live Copy源转 *出同一组件后* ，将重命名为_msm_moved。


## Cloud Manager 的新增功能 {#cloud-manager}

阅读本节内容，了解 AEM 云服务版本 2020.5.0 中 Cloud Manager 的新增功能和更新。

### 新增功能 {#what-is-new}

* 新增了六条代码质量规则，帮助客户在规划迁移到云服务时发现潜在问题。
* 新增了一 *个度量云服务兼容性* ，以总结与兼容性相关的问题数。
* 未能创建的环境现在将在创建失败后约24小时自动删除，除非已删除它们。
* 活动页面和管道执行列表API的性能已得到改进。
* 代码质量日志现在包含完整的堆栈跟踪以发现异常。

### 错误修复 {#bug-fixes}

* 在生产管道运行时，概述页面上会显示误导性信息卡。
* DontImplementOrExtendProviderTypesPomCheck代码质量 *规则有时可能* 会产生空指针异常。
* 概述页面中的某些文档链接无法正常工作。
* 创建环境对话框在Safari中无法正确呈现。
* 概述页面上的某些卡未正确显示实体名称。
* 在某些情况下，构建映像无法成功下载客户包。

