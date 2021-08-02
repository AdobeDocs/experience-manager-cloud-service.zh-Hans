---
title: AEM as a Cloud Manager版本2020.11.0的发行说明
description: AEM as a Cloud Manager版本2020.11.0的发行说明
feature: 版本信息
exl-id: e2acf515-d339-4d2b-9b62-09c1dab1ffac
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Manager as a Cloud ManagerCloud Service的发行说明2020.11.0 {#release-notes}

本页面概述了AEM as a Cloud 2020.11.0中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud Manager的Cloud Service2020.11.0的发布日期是2020年11月12日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 现在，用户可以从“环境”卡和“环境摘要”页面上的“环境”菜单选项中使用新的菜单选项&#x200B;**本地登录**。
有关更多详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md#login-locally) 。

* Cloud Manager中的&#x200B;**Learn**&#x200B;选项卡已使用UI中的新图像刷新。

### 错误修复 {#bug-fixes-cloud-manager}

* 需要下载Maven插件，才能加载执行生成之前完成的依赖项。
* 现在，Cloud Manager页脚中用于选择语言的链接将导航到正确的位置。
* 有时，在代码扫描期间，SonarQube进程不会启动。 现在将自动检测并尝试重新启动。
* 所有现有的生产管道都将通过体验审核步骤自动启用。
