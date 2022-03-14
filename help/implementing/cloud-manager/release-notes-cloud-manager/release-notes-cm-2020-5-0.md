---
title: AEM 2020.5.0版中Cloud Manager的发行说明
description: AEM 2020.5.0版中Cloud Manager的发行说明
feature: Release Information
exl-id: 9f534858-d18f-4224-8b94-9583a05aed95
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 71%

---

# Adobe Experience Manager as a Cloud Service 2020.5.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2020.5.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM 2020.5.0版中Cloud Manager的发布日期是2020年5月7日。

## 新增功能 {#whats-new-cloud-manager}

* 添加了六个其他代码质量规则，以帮助客户在计划迁移到云服务时发现潜在问题。
* 添加了一个新量度“云服务兼容性”**，以汇总与兼容性相关的问题数量。
* 现在，创建失败的环境将在创建失败后大约 24 小时自动删除，除非已删除这些环境。
* “活动”页面和管道执行列表 API 的性能已得到改进。
* 代码质量日志现在包含完整的异常堆栈追踪。

### 错误修复  {#bug-fixes}

* 生产管道运行时，概述页面上显示误导性信息卡。
* *DontImplementOrExtendProviderTypesPomCheck* 代码质量规则有时可能会产生“空指针异常”。
* 概述页面中的某些文档链接无法正常使用。
* “创建环境”对话框在 Safari 中无法正确呈现。
* 概述页面上的某些信息卡无法正确显示实体名称。
* 在某些情况下，“生成图像”可能无法成功下载客户包。
