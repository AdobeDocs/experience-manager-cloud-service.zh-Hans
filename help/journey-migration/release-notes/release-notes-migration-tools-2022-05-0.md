---
title: AEMas a Cloud Service2022.5.0版中迁移工具的发行说明
description: AEMas a Cloud Service2022.5.0版中迁移工具的发行说明
feature: Release Information
exl-id: 1aa49e85-1914-44d9-bcf7-0a1b03926df0
source-git-commit: 01c4a21b980918ba99ac174419d80b577bc96dda
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 15%

---

# AEMas a Cloud Service2022.5.0版中迁移工具的发行说明 {#release-notes}

此页概述了AEMas a Cloud Service2022.5.0中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.30的发布日期是2022年6月1日。

### 新增功能 {#what-is-new-bpa}

* 能够使用CoralUI和Classic对话框构件检测和报告自定义对话框构件的使用情况。 建议将自定义经典对话框构件从ExtJS转换为CoralUI。 自定义Coral对话框构件应更新为CoralUI3。
* 能够检测和报告Assets Share Commons的使用情况和版本。 AEMas a Cloud Service上不支持Asset Share Commons 1.x，必须将其升级到2.x。
* 能够检测和报告版本中的节点数量。
* 能够检测和报告自定义复制代理或已修改的现成复制代理。

### 错误修复 {#bug-fixes-bpa}

* BPA报告NCC（不兼容更改）、UMI（升级错误配置问题）和PCX（页面复杂性）调查结果误报。 这些已修复。
* 当任何节点名称长度超过150字节时，BPA会报告故障。 已修复此问题，以便仅在节点父路径等于或大于350字节时检测此类故障。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本2.0.10的发布日期是2022年6月2日。

### 新增功能 {#what-is-new-ctt}

* 内容传输工具(CTT)已经演变为与Cloud Acceleration Manager配合使用，以简化整个内容传输流程。 CTT现在侧重于执行内容提取。 CTT摄取服务现已集成到Cloud Acceleration Manager中。 通过这种演进带来的好处包括：
   * 一次性提取迁移集并将它并行摄取到多个环境中的自助方式.
   * 通过更好的加载状态、防护机制和错误处理改善用户体验.
   * 摄取日志将保留，并且始终可用于进行故障排除.

## Cloud Acceleration Manager {#cam-release}

### 发布日期 {#release-date-cam}

Cloud Acceleration Manager的发布日期是2022年6月2日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager现在允许用户启动和管理内容传输，以便在迁移项目中将内容从客户的AEM实例（内部部署或Adobe Managed Services）移动到AEMas a Cloud Service。 请参阅 [使用内容传输卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) 了解更多详细信息。
