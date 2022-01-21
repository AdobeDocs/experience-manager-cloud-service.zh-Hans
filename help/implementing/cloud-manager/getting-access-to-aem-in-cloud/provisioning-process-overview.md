---
title: 配置过程 — 概述
description: 配置过程 — 概述
source-git-commit: 2f40b11a20a4ebb3ff7d9d2835bbe56e91ddf96d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 8%

---


# AEMas a Cloud Service:入门和访问

本页列出了有关配置Experience Manageras a Cloud Service过程的自助资源。

## AEMas a Cloud Service配置过程概述

此部分涵盖有关以下内容的关键文章：

* 访问AEMas a Cloud Service
* Adobe Experience Manager as a Cloud Service载入和配置过程
* 帮助和资源


### 访问AEMas a Cloud Service

自动配置完成后：

* 已授予的访问权限 — Adobe将在AdobeIdentity Management系统(IMS)中创建组织
* 默认情况下，指定的管理员将拥有管理员权限
* 管理员可以通过Admin Console为其他团队成员添加用户和角色
* 在Cloud Manager中查看基于角色的权限，以确定权限分配

> ![processoverview.jpg](./assets/processOverview.jpg)


欲知更多信息，请访问 [在Experience League上Experience Manageras a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=en)

### 资源和链接

* [AEM as a Cloud Service 的 IMS 支持](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en)
* [Cloud Manager中基于角色的权限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html?lang=en#what-is-required)
* [访问 Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#getting-access)


## Adobe Experience Manager as a Cloud Service载入流程

### 1.采购订单触发器自动配置。

### 2.将组织载入Adobe Admin Console:

![processoverview2.jpg](./assets/processOverview2.jpg)

* 系统管理员:
   * 配置AEM程序和环境。
   * 导航到管理任务的Admin Console。
   * 声明域以确认各个域的所有权
   * 设置用户目录。
   * IDP配置。
* AEM 管理员:
   * 管理本地组、权限和权限。

### 3.载入用户并管理Admin Console中的访问：

![processoverview3.jpg](./assets/processOverview3.jpg)

根据用户大小和偏好，可使用三种载入用户的方法：
* 在Admin Console中手动创建用户
* 上载.csv文件
* 从企业Active Directory同步用户

### 4.管理员配置组织并授予用户和组对环境的访问权限

## 帮助和资源

* [首次登录 — Cloud Service](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)
* [配置对AEMas a Cloud Service的访问](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#accessing)
