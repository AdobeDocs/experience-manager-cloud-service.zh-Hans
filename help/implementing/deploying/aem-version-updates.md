---
title: AEM 版本更新
description: 瞭解AEMas a Cloud Service如何使用持續整合和傳遞(CI/CD)，讓您專案保持在最新版本。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 7cdc7bb56565cccc04a2dcb74a6c8088ed4e7847
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 23%

---


# AEM 版本更新 {#aem-version-updates}

瞭解AEMas a Cloud Service如何使用持續整合和傳遞(CI/CD)，讓您專案保持在最新版本。

## CI/CD {#ci-cd}

AEMas a Cloud Service使用持續整合和持續傳遞(CI/CD)，以確保您的專案使用最新的AEM版本。 这表示将生产实例和暂存实例更新到最新 AEM 版本而不中断用户的服务。

版本更新只會自動套用至生產和中繼執行個體。 [AEM更新必須手動套用至所有其他執行個體。](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)

## 更新型別 {#update-types}

有两种类型的 AEM 版本更新：

* **AEM 维护更新**

   * 可以每日发布。
   * 主要是用于维护目的，包括最新的错误修复和安全更新。
   * 由于定期应用更改，因此产生的影响最小。

* **新增功能更新**

   * 發行日期 [可預測、每月排程。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## 更新失敗 {#update-failure}

AEM更新會透過密集且完全自動化的產品驗證管道進行，涉及多個步驟，確保不會中斷任何生產系統的服務。 健康情況檢查用於監視應用程式的健康情況。 如果這些檢查在AEMas a Cloud Service更新期間失敗，則發行將不會繼續，並且Adobe將調查更新導致此意外行為的原因。

[產品測試和客戶功能測試，](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) 可防止產品升級和客戶程式碼推送破壞生產系統的功能，也會在AEM版本更新期間驗證。

如果未能更新生产环境，Cloud Manager 将自动回滚到暂存环境。此操作将自动完成，以确保在更新完成后，暂存环境和生产环境均采用同一个 AEM 版本。

>[!NOTE]
>
>如果自訂程式碼推送至測試環境而非生產環境，下次AEM更新會移除這些變更，以反映上次成功客戶發佈至生產環境的Git標籤。 因此，必須再次部署僅可用於測試的自訂程式碼。

## 複合節點存放區 {#composite-node-store}

在大多數情況下，更新會產生零停機時間，包括製作執行個體（節點叢集）。 滾動更新可能的原因是 [Oak中的複合節點存放區功能。](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

此功能可讓AEM同時參照多個存放庫。 在滾動中 [藍綠色部署，](/help/implementing/deploying/overview.md#how-rolling-deployments-work) 新的綠色AEM版本包含自己的 `/libs` （以TarMK為基礎的不可變存放庫），與舊版藍色AEM不同，不過兩者都參考共用的DocumentMK型可變存放庫，其中包含 `/content` ， `/conf` ， `/etc` 和其他。

因為藍色和綠色都有各自版本的 `/libs`中，在滾動更新期間兩者都可處於活動狀態，兩者都會接收流量，直到藍色被綠色完全取代為止。
