---
title: Adobe Experience Manager as a Cloud Service中的Cloud Manager 2022.6.0发行说明
description: 以下是AEM as a Cloud Service中Cloud Manager 2022.6.0的发行说明。
feature: Release Information
source-git-commit: 5200ee315ad88dae4b52c0ea904489e73f62a8a0
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 1%

---


# Adobe Experience Manager as a Cloud Service中的Cloud Manager 2022.6.0发行说明 {#release-notes}

本页记录了AEMas a Cloud Service中Cloud Manager 2022.6.0的发行说明。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEMas a Cloud Service中Cloud Manager 2022.6.0版的发布日期是2022年6月9日。 下一版计划于2022年6月30日发布。

## 新增功能 {#what-is-new}

* Cloud Manager UI现在允许 [自助内容恢复](/help/operations/backup.md) 到AEM云环境的已知良好状态。
   * 此功能将在2022.06.0版后的几周内分阶段推出。
* Cloud Manager登录页面上新增的欢迎卡使用户能够快速访问与租户相关的入门教程和进度量度。
   * 此功能将在2022.06.0版后的一周内分阶段推出。
* 具有必需权限的用户可以访问 [许可证功能板](/help/implementing/cloud-manager/license-dashboard.md) ，以查看租户可用权限的详细信息。
   * AEM Sites是第一个通过云管理功能板提供可用性和使用使用情况的解决方案。
   * 此功能将在2022.06.0版后的几周内分阶段推出。
* [新旧账户子帐户和自助服务用户管理](/help/implementing/cloud-manager/user-access-new-relic.md) 现在可通过Cloud Manager UI使用。
   * 此功能将在2022.06.0版后的几周内分阶段推出。
* Cloud Service制作项目主页上新增的上线小组件现在提供指导，为成功上线体验做好准备。
* [现在可以重复使用生成工件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 使用git镜像时。

## API更改 {#api-changes}

* 的 [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API已弃用，并且 [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) 的值。
   * `List Programs` 仍然有效，但其使用情况将在日志中生成警告消息。
   * 三个月后将不再支持该选件。

