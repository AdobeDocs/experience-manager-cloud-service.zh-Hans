---
title: AEM as a Cloud Service 2022.5.0版中的迁移工具发行说明
description: AEM as a Cloud Service 2022.5.0版中的迁移工具发行说明
feature: Release Information
exl-id: 1aa49e85-1914-44d9-bcf7-0a1b03926df0
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# AEM as a Cloud Service 2022.5.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2022.5.0中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.30的发布日期是2022年6月1日。

### 新增功能 {#what-is-new-bpa}

* 能够使用CoralUI和Classic对话框构件检测和报告自定义对话框构件的使用情况。 建议将自定义经典对话框构件从ExtJS转换为CoralUI。 自定义Coral对话框构件应更新为CoralUI3。
* 能够检测和报告Assets Share Commons的使用情况和版本。 AEM as a Cloud Service上不支持Asset Share Commons 1.x，必须将其升级到2.x。
* 能够检测和报告版本中的节点数。
* 能够检测和报告自定义复制代理或已修改的现成复制代理。

### 错误修复 {#bug-fixes-bpa}

* BPA报告了NCC（不兼容更改）、UMI（升级错误配置问题）和PCX（页面复杂性）误报结果。 这些已被修复。
* 当任何节点名称长度超过150字节时，BPA会报告故障。 已修复此错误，以便仅在节点父路径等于或大于350字节时检测此类故障。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本2.0.10的发布日期为2022年6月2日。

### 新增功能 {#what-is-new-ctt}

* 内容传输工具(CTT)已经过演变，可与Cloud Acceleration Manager配合使用以简化整个内容传输流程。 CTT现在侧重于执行内容提取。 CTT摄取服务现已集成到Cloud Acceleration Manager中。 通过这种演变提供的好处包括：
   * 以自助方式提取一次迁移集并将其并行摄取到多个环境中。
   * 通过更好的加载状态、护栏和错误处理，改进了用户体验。
   * 摄取日志将保留，并且始终可用于进行故障排除。

## Cloud Acceleration Manager {#cam-release}

### 发布日期 {#release-date-cam}

Cloud Acceleration Manager的发布日期是2022年6月2日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager现在为用户提供了启动和管理内容传输的功能，以便将内容从客户的AEM实例(内部部署或AdobeManaged Services)移动到AEM as a Cloud Service，作为迁移项目的一部分。 有关更多详细信息，请参阅[使用内容传输卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer)。
