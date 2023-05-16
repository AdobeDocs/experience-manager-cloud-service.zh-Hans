---
title: AEM 版本更新
description: 了解AEM as a Cloud Service如何使用持续集成和交付(CI/CD)来使您的项目保持在最新版本。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 59bc2b5af22ef23775195f098517cec40d98d66b
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 23%

---


# AEM 版本更新 {#aem-version-updates}

了解AEM as a Cloud Service如何使用持续集成和交付(CI/CD)来使您的项目保持在最新版本。

## CI/CD {#ci-cd}

AEM as a Cloud Service使用持续集成和持续交付(CI/CD)来确保您的项目处于最新的AEM版本。 这表示将生产实例和暂存实例更新到最新 AEM 版本而不中断用户的服务。

版本更新将仅自动应用于生产实例和暂存实例。 [AEM更新必须手动应用于所有其他实例。](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)

## 更新类型 {#update-types}

有两种类型的 AEM 版本更新：

* **AEM 维护更新**

   * 可以每日发布。
   * 主要是用于维护目的，包括最新的错误修复和安全更新。
   * 由于定期应用更改，因此产生的影响最小。

* **新增功能更新**

   * 在 [可预测，按月计划。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## 更新失败 {#update-failure}

AEM更新通过一个涉及多个步骤且完全自动化的产品验证管道，可确保生产中任何系统的服务不会中断。 运行状况检查用于监控应用程序的运行状况。 如果这些检查在AEMas a Cloud Service更新期间失败，则该版本将不继续，并且Adobe将调查更新为何会导致此意外行为。

[产品测试和客户功能测试，](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) 这样可以防止产品升级和客户代码推送破坏生产系统，也会在AEM版本更新期间进行验证。

如果未能更新生产环境，Cloud Manager 将自动回滚到暂存环境。此操作将自动完成，以确保在更新完成后，暂存环境和生产环境均采用同一个 AEM 版本。

>[!NOTE]
>
>如果将自定义代码推送到暂存环境，而不是生产环境，则下次AEM更新将删除这些更改，以反映上次成功将客户版本的git标记推送到生产环境。 因此，必须再次部署仅在暂存环境中可用的自定义代码。

## 复合节点存储 {#composite-node-store}

在大多数情况下，更新将导致零停机时间，包括对于创作实例（即节点群集）。 可以滚动更新，原因是 [Oak中的复合节点存储功能。](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

此功能允许AEM同时引用多个存储库。 滚动 [蓝绿色部署，](/help/implementing/deploying/overview.md#index-management-using-blue-green-deployments) 新的绿色AEM版本包含其自己的 `/libs` （基于TarMK的不可变存储库），与旧的蓝色AEM版本不同，不过这两个存储库都引用了一个基于DocumentMK的共享可变存储库，其中包含以下区域： `/content` , `/conf` , `/etc` 等等。

因为蓝色和绿色都有各自的版本 `/libs`，则它们在滚动更新期间均可处于活动状态，在蓝色完全替换为绿色之前都会占用流量。
