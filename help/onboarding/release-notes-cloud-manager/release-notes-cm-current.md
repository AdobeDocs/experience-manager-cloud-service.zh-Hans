---
title: AEM中Cloud Manager作为Cloud Service版本2020.11.0的发行说明
description: AEM中Cloud Manager作为Cloud Service版本2020.11.0的发行说明
translation-type: tm+mt
source-git-commit: 65752c7c51538de27aa2b21695e8eb6c6695a5f5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.11.0 {#release-notes}

本页概述了AEM中作为Cloud Service2020.11.0的Cloud Manager发行说明。

## 发布日期 {#release-date}

AEM中Cloud Manager作为Cloud Service2020.11.0的发布日期为2020年11月12日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 现在，用户可 **以从环境卡** 和环境摘要页面上的“本地登录”菜单选项中使用新的菜单选项。

* 云管 **理器** 中的“学习”选项卡已通过UI中的新图像刷新

### 错误修复 {#bug-fixes-cloud-manager}

* 需要下载Maven插件，才能加载执行构建之前完成的依赖项。
* 现在，从Cloud Manager页脚中选择语言的链接将导航到正确的位置。
* 有时，在代码扫描过程中，SonarQube进程不会开始。 现在将自动检测并尝试重新启动。
* 所有现有的生产管道都将通过体验审核步骤自动启用。