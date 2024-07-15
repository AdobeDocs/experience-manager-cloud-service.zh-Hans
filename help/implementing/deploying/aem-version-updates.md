---
title: AEM 版本更新
description: 了解Adobe Experience Manager (AEM) as a Cloud Service如何使用持续集成和交付(CI/CD)将您的项目保持在最新版本上。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
role: Admin
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 1%

---


# AEM 版本更新 {#aem-version-updates}

了解Adobe Experience Manager (AEM) as a Cloud Service如何使用持续集成和交付(CI/CD)将您的项目保持在最新版本上。

## CI/CD {#ci-cd}

AEM as a Cloud Service使用持续集成和持续交付(CI/CD)，以确保您的项目使用的是最新的AEM版本。 此过程可无缝更新您的生产、暂存和开发实例，而不会造成任何用户中断。

>[!NOTE]
> 由于开发实例已自动更新，因此&#x200B;_某些_&#x200B;程序可能无法使用开发实例的手动更新。 此功能正在转换为自动更新。

在自动更新实例之前，将提前3-5天发布新的AEM维护版本。 在此期间，您的开发实例可能会自动更新，如果该实例可用，您可以选择[触发开发实例的更新](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)。 版本更新首先自动应用于您的开发环境。 如果更新成功，则更新流程将继续到暂存和生产实例。 开发和暂存实例充当自动化的质量关卡，在生产环境应用更新之前，可在其中运行自定义编写的测试。

### NIMU（非侵入式维护更新） {#nimu}

非侵入式维护更新是自动更新，应用时不会涉及客户管道。
通过NIMU，客户随时可以使用管道，即使已计划或正在进行AEM版本更新，并且维护更新将不再出现在客户管道执行历史记录中，从而更容易遵循代码部署历史记录。

#### 更新活动

与之前一样，使用Cloud Manager UI环境面板仍然可以检查每个环境的当前AEM版本。 非侵入式维护更新（包括客户编写的测试）使用管道中使用的相同质量审核。
每当对程序的环境应用非侵入式维护更新时，将发送Cloud Manager UI通知。 您可以将其配置为也发送到您的电子邮件。

>[!NOTE]
>
> 注意：非侵入式维护更新将于2024年逐步为所有客户启用。


## 更新类型 {#update-types}

有两种类型的 AEM 版本更新：

* [**AEM维护更新**](/help/release-notes/maintenance/latest.md)

   * 它们主要用于维护目的，包括最新的错误修复和安全更新。
   * 由于定期应用更改，因此其影响最小。

* [**AEM功能激活**](/help/release-notes/release-notes-cloud/release-notes-current.md)

   * 它们按照可预测的每月计划发布。

>[!NOTE]
>
> 在[Experience Manager版本路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html#aem-as-cloud-service)上检查每月发布的关键日期，并标记您的日历，自行为关键活动做好准备以便进行发布。

## 更新失败 {#update-failure}

AEM更新需要执行大量且完全自动化的产品验证管道，该管道包含多个步骤，可确保生产中的任何系统都不会出现服务中断。 运行状况检查用于监视应用程序的运行状况。 如果这些检查在AEM as a Cloud Service更新期间失败，则发布不会继续，并且Adobe会调查更新导致此意外行为的原因。

当您在环境中部署新版本的自定义代码时，[产品和自定义功能测试](/help/implementing/cloud-manager/overview-test-results.md#functional-testing)将发挥关键作用。 它们可确保生产系统在应用更改后仍保持稳定和正常运行。 这些测试还应用于AEM版本更新过程。

如果对生产环境的更新失败，Cloud Manager会自动回滚到暂存环境。 此操作将自动完成，以确保在更新完成后，暂存环境和生产环境均采用同一个AEM版本。
同样，如果自动更新开发环境失败，则不更新暂存环境和生产环境。

>[!NOTE]
>
>如果自定义代码推送到暂存而不是生产环境，则下次AEM更新时会删除这些更改，以反映上次成功发布到生产环境的客户的Git标记。 因此，必须重新部署仅在暂存上可用的自定义代码。

## 最佳实践 {#best-practices}

* **暂存环境使用情况**
   * 使用其他环境（而不是暂存）完成较长的QA/UAT周期。
   * 在暂存环境中完成健全性测试后，请在生产环境中移至验证。

* **生产管道**
   * 在部署到生产环境之前暂停。
   * 在暂存部署后取消管道表明代码是“放弃的”并且不是有效的生产候选项，请参阅[配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)。

* **非生产管道**
   * 配置[非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)。
   * 加快生产管道故障的投放速度/频率。 通过启用产品功能测试、自定义功能测试和自定义UI测试，识别非生产管道中的问题。

* **内容副本**
   * 使用[内容副本](/help/implementing/developing/tools/content-copy.md)将相似的内容集移动到非生产环境。

* **自动化功能测试**
   * 在管道中包含自动测试，以便测试关键功能。
   * [客户功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)和[自定义UI测试](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)如果失败，则将阻止AEM版本，并且不会推出。

## 回归 {#regression}

如果您遇到与回归相关的问题，请通过Admin Console提交支持案例。 如果问题为阻止程序且影响生产，则应引发P1。 提供重现回归问题所需的所有详细信息。

## 复合节点存储 {#composite-node-store}

通常，更新会产生零停机时间，包括创作实例（节点集群）的停机时间。 由于Oak中的[复合节点存储功能，可能会进行滚动更新。](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

此功能允许AEM同时引用多个存储库。 在[滚动部署](/help/implementing/deploying/overview.md#how-rolling-deployments-work)中，新AEM版本包含其自己的`/libs` （基于TarMK的不可变存储库）。 它与旧版AEM不同，不过两者都引用基于DocumentMK的共享可变存储库，该存储库包含`/content`、`/conf`、`/etc`等区域。

由于旧版本和新版本都有各自的`/libs`版本，因此在滚动更新期间它们都可以处于活动状态。 而且，在旧设备完全被新设备取代之前，这两种设备都可以承受流量。
