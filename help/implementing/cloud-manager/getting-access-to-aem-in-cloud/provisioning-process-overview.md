---
title: 配置过程 – 概述
description: 配置过程 – 概述
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 95%

---


# AEM as a Cloud Service：登录和访问

此页面列出了有关 Experience Manager as a Cloud Service 的配置过程的自助资源。

## AEM as a Cloud Service 配置过程概述

此部分涵盖有关以下内容的关键文章：

* 访问 AEM as a Cloud Service
* Adobe Experience Manager as a Cloud Service 登录和配置过程
* 帮助及资源


### 访问 AEM as a Cloud Service

自动配置完成后：

* 授予访问权限 – Adobe 将在 Adobe Identity Management 系统 (IMS) 内创建一个组织
* 默认情况下，指定管理员将拥有管理员权限
* 管理员可以通过 Admin Console 为其他团队成员添加用户和角色
* 查看用户基于角色的权限，确定 Cloud Manager 中的权限分配

![processoverview.jpg](assets/processOverview.jpg)


有关更多信息，请参阅 [在Experience League上开始使用Experience Manageras a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=zh-Hans).

### 资源及链接

* [AEM as a Cloud Service 的 IMS 支持](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=zh-Hans)
* [Cloud Manager 中基于角色的权限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html?lang=zh-Hans#what-is-required)
* [访问 Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=zh-Hans#getting-access)


## Adobe Experience Manager as a Cloud Service 登录流程

### 1. 购买订单触发自动配置。

### 2. 将组织载入 Adobe Admin Console：

![processoverview2.jpg](assets/processOverview2.jpg)

* 系统管理员:
   * 配置 AEM 程序和环境。
   * 导航到 Admin Console 执行管理任务。
   * 索取域，确认各自域的所有权
   * 设置用户目录。
   * IDP 配置。
* AEM 管理员:
   * 管理本地组、权限和特权。

### 3. 将用户载入 Admin Console 并管理访问权限：

![processoverview3.jpg](assets/processOverview3.jpg)

根据大小和偏好，可以使用三种方法载入用户：
* 在 Admin Console 中手动创建用户
* 上载 .csv 文件
* 从企业活动同步用户
目录

### 4. 管理员配置组织并授予用户和组对环境的访问权限

## 帮助及资源

* [首次登录 – Cloud Service](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)
* [配置 AEM as a Cloud Service 的访问权限](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=zh-Hans#accessing)
