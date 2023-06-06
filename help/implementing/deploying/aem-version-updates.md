---
title: AEM 版本更新
description: 了解AEMas a Cloud Service如何使用持续集成和交付(CI/CD)来将您的项目保持在最新版本。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: dd1560aa4d260320f565ad993a8b3650c3ee5288
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 23%

---


# AEM 版本更新 {#aem-version-updates}

了解AEMas a Cloud Service如何使用持续集成和交付(CI/CD)来将您的项目保持在最新版本。

## CI/CD {#ci-cd}

AEMas a Cloud Service使用持续集成和持续交付(CI/CD)来确保您的项目使用的是最新的AEM版本。 这表示将生产实例和暂存实例更新到最新 AEM 版本而不中断用户的服务。

版本更新仅自动应用于生产和暂存实例。 [必须手动将AEM更新应用于所有其他实例。](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)

## 更新类型 {#update-types}

有两种类型的 AEM 版本更新：

* **AEM 维护更新**

   * 可以每日发布。
   * 主要是用于维护目的，包括最新的错误修复和安全更新。
   * 由于定期应用更改，因此产生的影响最小。

* **新增功能更新**

   * 发布日期 [可预测、按月计划。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## 更新失败 {#update-failure}

AEM更新通过密集且完全自动化的产品验证管道，其中涉及多个步骤，确保不中断任何生产系统中的服务。 运行状况检查用于监视应用程序的运行状况。 如果这些检查在AEMas a Cloud Service更新期间失败，则发布将不会继续，并且Adobe将调查更新导致此意外行为的原因。

[产品测试和客户功能测试，](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) AEM版本更新期间还会验证用于防止产品升级和客户代码推送中断生产系统的功能。

如果未能更新生产环境，Cloud Manager 将自动回滚到暂存环境。此操作将自动完成，以确保在更新完成后，暂存环境和生产环境均采用同一个 AEM 版本。

>[!NOTE]
>
>如果将自定义代码推送到暂存环境而不是生产环境，则下次AEM更新将删除这些更改，以反映上次成功发布到生产环境的客户的Git标记。 因此，必须再次部署仅在暂存时可用的自定义代码。

## 复合节点存储 {#composite-node-store}

在大多数情况下，更新不会产生停机时间，包括创作实例（节点集群）。 滚动更新可能是由于 [Oak中的复合节点存储功能。](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

此功能允许AEM同时引用多个存储库。 在 [滚动部署，](/help/implementing/deploying/overview.md#how-rolling-deployments-work) 新的AEM版本包含它自己的 `/libs` （基于TarMK的不可变存储库），与较旧的AEM版本不同，不过两者都引用基于DocumentMK的共享可变存储库，该存储库包含以下区域 `/content` ， `/conf` ， `/etc` 和其他人。

因为旧版本和新版本都有各自版本的 `/libs`，它们都可以在滚动更新期间处于活动状态，并且都可承受流量，直到新完全替换旧流量为止。
