---
title: AEM版本更新
description: 'AEM版本更新 '
translation-type: tm+mt
source-git-commit: 5032c503be8972879eff82d4919bb07dcff1db2a
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---


# AEM版本更新 {#aem-version-updates}

## 简介 {#introduction}

AEM作为Cloud Service现在使用连续集成和连续投放(CI/CD)来确保您的项目处于最新的AEM版本。 这意味着所有升级操作都是完全自动化的，因此不需要用户中断任何服务。

>[!NOTE]
>如果对生产环境的更新失败，Cloud Manager将自动回滚阶段环境。 这会自动完成，以确保更新完成后，阶段和生产环境都使用相同的AEM版本。

AEM版本更新有两种类型：

* **AEM推送更新**

   * 可以每天发布。
   * 主要是维护，包括最新的错误修复和安全更新。

      由于更改会定期应用，因此影响会逐渐增加，从而减少对服务的影响。

* **新增功能更新**

   * 通过可预测的月度计划发布。

AEM更新通过一个密集且完全自动化的产品验证管道，涉及多个步骤，确保不中断生产中任何系统的服务。 运行状况检查用于监视应用程序的运行状况。 如果这些检查在AEM作为Cloud Service更新期间失败，则发行版将不继续，Adobe将调查更新为何导致此意外行为。

[产品测试和客户功能测试](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) （防止产品升级和客户代码推送中断生产）也在AEM版本更新期间进行验证。

>[!NOTE]
>
>如果自定义代码被推送到暂存，然后被您拒绝，则下一个AEM更新将删除这些更改，以反映上次成功发布客户的git标签到生产。

## 复合节点存储 {#composite-node-store}

如上所述，在大多数情况下，更新将导致零停机，对于作者而言，这是一个节点群集。 由于Oak中的复合节点存储功 *能，可以进行* 滚动更新。

此功能允许AEM同时引用多个存储库。 在滚动部署中，新的绿色AEM版本包含其自己的(基于TarMK的不可变 `/libs` 存储库)，与旧的蓝色AEM版本不同，但两者都引用了一个共享的基于DocumentMK的可变存储库，该存储库包含 `/content` 、 `/conf` 、 `/etc` 等区域。 由于蓝色和绿色都有其自己的版本，因此在滚动更新期间 `/libs`，它们都可以处于活动状态，在蓝色被绿色完全替换之前，它们都会保持流量。

