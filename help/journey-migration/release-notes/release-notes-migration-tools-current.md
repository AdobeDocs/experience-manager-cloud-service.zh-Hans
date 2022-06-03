---
title: AEMas a Cloud Service版本2022.6.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2022.6.0中迁移工具的发行说明
feature: Release Information
source-git-commit: 717b2c851a18ef5171d64a462509ce08fb87a59c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# AEMas a Cloud Service版本2022.6.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2022.6.0as a Cloud Service中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.30的发布日期是2022年6月1日。

### 新增功能 {#what-is-new-bpa}

* 能够使用CoralUI和经典对话框小组件检测并报告自定义对话框小组件的使用情况。 建议将自定义经典对话框小组件从ExtJS转换为CoralUI。 应将自定义Coral对话框小组件更新为CoralUI3。

* 能够检测并报告资产共享共用的使用情况和版本。 AEMas a Cloud Service不支持资产共享共用1.x，必须将其升级到2.x。

* 能够检测并报告来自版本的节点数。

* 能够检测和报告已修改的自定义复制代理或现成复制代理。

### 错误修复 {#bug-fixes-bpa}

* BPA报告的是误报的NCC（不兼容的更改）、UMI（升级配置错误问题）和PCX（页面复杂性）发现结果。 这些已修复。
* 当任何节点名称长度超过150字节时，BPA报告失败。 此问题已得到修复，以便仅在节点父路径等于或大于350字节时才检测此类故障。

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具v2.0.10的发布日期是2022年6月2日。

### 新增功能 {#what-is-new-ctt}

* 内容传输工具(CTT)已发展为可与Cloud Acceleration Manager配合使用，以简化整个内容传输流程。 CTT现在侧重于执行内容提取。 CTT摄取服务现已集成到Cloud Acceleration Manager中。 通过此演变提供的好处包括：
   * 一种自助方式，只需提取一次迁移集，然后将其并行摄取到多个环境中。
   * 通过更好的加载状态、护栏和错误处理，改善了用户体验。
   * 将保留摄取日志，并始终可用于疑难解答。

## Cloud Acceleration Manager {#cam-release}

### 发布日期 {#release-date-cam}

Cloud Acceleration Manager的发布日期是2022年6月2日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager现在为用户提供以下功能：启动和管理内容传输，以将内容从客户的AEM实例（内部部署或Adobe Managed Services）移动到AEMas a Cloud Service，作为迁移项目的一部分。 请参阅 [使用内容传输卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) 以了解更多详细信息。
