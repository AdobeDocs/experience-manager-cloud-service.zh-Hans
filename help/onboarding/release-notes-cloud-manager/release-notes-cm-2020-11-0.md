---
title: AEM中Cloud Manager作为Cloud Service版本2020.11.0的发行说明
description: AEM中Cloud Manager作为Cloud Service版本2020.11.0的发行说明
feature: Release Information
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 5%

---


# Adobe Experience Manager中Cloud Manager作为Cloud Service2020.11.0 {#release-notes}的发行说明

本页概述了AEM中作为Cloud Service 2020.11.0的Cloud Manager发行说明。

## 发布日期 {#release-date}

AEM中Cloud Manager作为Cloud Service 2020.11.0的发布日期为2020年11月12日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 现在，用户可以从环境卡和环境摘要页面上的环境菜单选项中使用新的菜单选项&#x200B;**本地登录**。
有关详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md#login-locally)。

* Cloud Manager中的&#x200B;**学习**&#x200B;选项卡已使用UI中的新图像进行刷新。

### 错误修复 {#bug-fixes-cloud-manager}

* 需要下载Maven插件，才能加载执行构建之前完成的依赖项。
* 现在，Cloud Manager页脚中用于选择语言的链接将导航到正确的位置。
* 有时，在代码扫描过程中，SonarQube进程不会开始。 现在将自动检测并尝试重新启动。
* 所有现有生产管道将通过体验审核步骤自动启用。
