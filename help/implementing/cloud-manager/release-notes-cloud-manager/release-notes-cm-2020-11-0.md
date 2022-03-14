---
title: AEMas a Cloud Service版本2020.11.0中的Cloud Manager发行说明
description: AEMas a Cloud Service版本2020.11.0中的Cloud Manager发行说明
feature: Release Information
exl-id: e2acf515-d339-4d2b-9b62-09c1dab1ffac
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 8%

---

# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2020.11.0 {#release-notes}

本页概述了AEM as a Cloud Service 2020.11.0中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEMas a Cloud Service中Cloud Manager的发行日期为2020.11.0 2020年11月12日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 新菜单选项 **本地登录** 现在，用户可以从“环境”卡和“环境摘要”页面上的环境菜单选项中访问。
有关更多详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md#login-locally)。

* 的 **学习** 选项卡，此选项卡已在UI中刷新为新图像。

### 错误修复 {#bug-fixes-cloud-manager}

* 需要下载Maven插件，才能加载执行生成之前完成的依赖项。
* 现在，Cloud Manager页脚中用于选择语言的链接将导航到正确的位置。
* 有时，在代码扫描期间，SonarQube进程不会启动。 现在将自动检测并尝试重新启动。
* 所有现有的生产管道都将通过体验审核步骤自动启用。
