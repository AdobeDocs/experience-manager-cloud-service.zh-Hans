---
title: AEM 版本更新
description: 了解Adobe Experience Manager (AEM)as a Cloud Service如何使用持续集成和交付(CI/CD)将您的项目保持在最新版本上。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 9bfea65c07da5da044df8f698e409eab5c4320fb
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 3%

---


# AEM 版本更新 {#aem-version-updates}

了解Adobe Experience Manager (AEM)as a Cloud Service如何使用持续集成和交付(CI/CD)将您的项目保持在最新版本上。

## CI/CD {#ci-cd}

AEMas a Cloud Service使用持续集成和持续交付(CI/CD)，以确保您的项目使用的是最新的AEM版本。 此过程可无缝更新您的生产、暂存和开发实例，而不会造成任何用户中断。

在自动更新实例之前，将提前3-5天发布新的AEM维护版本。 在此期间内，您可以选择 [触发开发实例的手动更新](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment). 在这段时间过后，版本更新会首先自动应用于您的开发环境。 如果更新成功，则更新流程将继续到暂存和生产实例。 开发和暂存实例充当自动化的质量关卡，在生产环境应用更新之前，可在其中运行自定义编写的测试。

>[!NOTE]
>
> 注意：开发环境的自动更新将于2023年逐步为所有客户启用。 如果您的开发环境未自动更新，则可以使用手动更新来使其与暂存环境和生产环境保持同步。


## 更新类型 {#update-types}

有两种类型的 AEM 版本更新：

* [**AEM 维护更新**](/help/release-notes/maintenance/latest.md)

   * 它们主要用于维护目的，包括最新的错误修复和安全更新。
   * 由于定期应用更改，因此其影响最小。

* [**新增功能更新**](/help/release-notes/release-notes-cloud/release-notes-current.md)

   * 它们按照可预测的每月计划发布。

>[!NOTE]
>
> 在上查看每月发布的关键日期 [Experience Manager版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html#aem-as-cloud-service) 并标记您的日历，为关键活动做好准备以便发布。

## 更新失败 {#update-failure}

AEM更新需要执行大量且完全自动化的产品验证管道，该管道包含多个步骤，可确保生产中的任何系统都不会出现服务中断。 运行状况检查用于监视应用程序的运行状况。 如果这些检查在AEMas a Cloud Service更新期间失败，则发布不会继续，并且Adobe会调查更新导致此意外行为的原因。

当您在环境中部署新版本的自定义代码时， [产品和自定义功能测试](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) 扮演着至关重要的角色。 它们可确保生产系统在应用更改后仍保持稳定和正常运行。 这些测试还应用于AEM版本更新过程。

如果对生产环境的更新失败，Cloud Manager会自动回滚到暂存环境。 此操作将自动完成，以确保在更新完成后，暂存环境和生产环境均采用同一个AEM版本。
同样，如果自动更新开发环境失败，则不更新暂存环境和生产环境。

>[!NOTE]
>
>如果自定义代码推送到暂存而不是生产环境，则下次AEM更新时会删除这些更改，以反映上次成功发布到生产环境的客户的Git标记。 因此，必须重新部署仅在暂存上可用的自定义代码。

## 最佳实践 {#best-practices}

* **暂存环境使用**
   * 使用其他环境（而不是暂存）完成较长的QA/UAT周期。
   * 在暂存环境中完成健全性测试后，请在生产环境中移至验证。

* **生产管道**
   * 在部署到生产环境之前暂停。
   * 在暂存部署后取消管道表示代码是“放弃的”并且不是有效的生产候选项，请参阅 [配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

* **非生产管道**
   * 配置 [非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).
   * 加快生产管道故障的投放速度/频率。 通过启用产品功能测试、自定义功能测试和自定义UI测试，识别非生产管道中的问题。

* **内容复制**
   * 使用 [内容复制](/help/implementing/developing/tools/content-copy.md) 将相似的内容集移动到非生产环境。

* **自动化功能测试**
   * 在管道中包含自动测试，以便测试关键功能。
   * [客户功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) 和 [自定义用户界面测试](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) 正在阻止，如果失败，则不转出AEM版本。

## 回归 {#regression}

如果您遇到与回归相关的问题，请通过Admin Console提交支持案例。 如果问题为阻止程序且影响生产，则应引发P1。 提供重现回归问题所需的所有详细信息。

## 复合节点存储 {#composite-node-store}

通常，更新会产生零停机时间，包括创作实例（节点集群）的停机时间。 滚动更新可能是由于 [Oak中的复合节点存储功能。](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

此功能允许AEM同时引用多个存储库。 在 [滚动部署](/help/implementing/deploying/overview.md#how-rolling-deployments-work)，则新的AEM版本包含其自己的 `/libs` （基于TarMK的不可变存储库）。 它不同于旧版AEM，不过两者都引用了基于DocumentMK的共享可变存储库，该存储库包含以下区域 `/content` ， `/conf` ， `/etc` 和其他人。

因为旧版本和新版本都有各自版本的 `/libs`中，它们都可以在滚动更新期间处于活动状态。 而且，在旧设备完全被新设备取代之前，这两种设备都可以承受流量。
