---
title: AEM 版本更新
description: 了解AEMas a Cloud Service如何使用持续集成和交付(CI/CD)将您的项目保持在最新版本上。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: dd567c484d71e25de1808f784c455cfb9b124fbf
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 11%

---


# AEM 版本更新 {#aem-version-updates}

了解AEMas a Cloud Service如何使用持续集成和交付(CI/CD)将您的项目保持在最新版本上。

## CI/CD {#ci-cd}

AEMas a Cloud Service使用持续集成和持续交付(CI/CD)，以确保您的项目使用的是最新的AEM版本。 此过程可无缝更新您的生产、暂存和开发实例，而不会造成任何用户中断。

在自动更新实例之前，新的AEM维护版本会提前3-5天发布。 在此期间，您可以选择执行以下操作
[触发开发实例的手动更新](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment).
此时间过后，版本更新会首先自动应用于您的开发环境。 如果更新成功，则更新流程将继续到暂存和生产实例。 开发和暂存实例充当自动质量关口，在生产环境中应用更新之前，将在其中执行自定义编写的测试。

>[!NOTE]
>
> 注意：开发环境的自动更新将于2023年逐步为所有客户启用。 如果您的开发环境未自动更新，则可以使用手动更新来使其与暂存环境和生产环境保持同步。


## 更新类型 {#update-types}

有两种类型的 AEM 版本更新：

* **AEM 维护更新**

   * 可以每日发布。
   * 主要是用于维护目的，包括最新的错误修复和安全更新。
   * 由于定期应用更改，因此产生的影响最小。

* **新增功能更新**

   * 发布日期 [可预测，按月计划。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## 更新失败 {#update-failure}

AEM更新需要执行大量且完全自动化的产品验证管道，该管道包含多个步骤，可确保生产中的任何系统都不会出现服务中断。
运行状况检查用于监视应用程序的运行状况。
如果这些检查在AEMas a Cloud Service更新期间失败，则发布将不会继续，并且Adobe将调查更新导致此意外行为的原因。

当您在环境中部署新版本的自定义代码时，
[产品和自定义功能测试](/help/implementing/cloud-manager/overview-test-results.md#functional-testing)
在确保生产系统在应用更改后仍保持稳定和功能方面发挥着关键作用。 AEM版本更新过程中也利用这些测试。

如果未能更新生产环境，Cloud Manager 将自动回滚到暂存环境。此操作将自动完成，以确保在更新完成后，暂存环境和生产环境均采用同一个AEM版本。
同样，如果自动更新开发环境失败，将不会更新暂存和生产环境。

>[!NOTE]
>
>如果自定义代码推送到暂存而不是生产环境，则下次AEM更新将删除这些更改，以反映上次成功发布到生产环境的客户的Git标记。 因此，必须再次部署仅在暂存时可用的自定义代码。

## 复合节点存储 {#composite-node-store}

在大多数情况下，更新将引发零停机时间，包括创作实例（节点集群）的停机时间。 滚动更新可能是由于 [Oak中的复合节点存储功能。](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

此功能允许AEM同时引用多个存储库。 在 [滚动部署，](/help/implementing/deploying/overview.md#how-rolling-deployments-work) 新的AEM版本包含它自己的 `/libs` （基于TarMK的不可变存储库），与较旧的AEM版本不同，不过两者都引用基于DocumentMK的共享可变存储库，该存储库包含如下区域 `/content` ， `/conf` ， `/etc` 和其他人。

因为旧版本和新版本都有各自版本的 `/libs`，则它们都可以在滚动更新期间处于活动状态，并且都可承担流量，直到新完全替换旧流量为止。
