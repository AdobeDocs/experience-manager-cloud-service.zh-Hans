---
title: AEM as a Cloud Service 中的基础设施和服务监控
description: AEM as a Cloud Service 中的基础设施和服务监控
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
source-git-commit: f55439552e253b8b71b40525454130c6f163e6d4
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 5%

---

# AEM as a Cloud Service 中的基础设施和服务监控 {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service提供基礎架構、服務和使用者體驗的可觀察性和監控。 由於使用了各種解決方案，且監控層數眾多，因此本頁面分為三個區段：

* [外部可用性](#external-availability)
* [內部模組監控](#module-monitoring)
* [客戶可觀察性](#customer-observability)

AEMas a Cloud Service使用數百部雲端原生監視器，每年365天持續報告每個環境的狀態(24/7)。 監視器定義不是靜態的，會持續檢閱以改進早期偵測能力。 此外，Adobe已設定待命程式來回應警示。

如果您需要其他監控型別（例如透過Cloud Manager的記錄或監控）的相關資訊，請參閱 [其他資源](#resources) 區段。

## 外部可用性 {#external-availability}

外部可用性由兩部分組成：服務邊緣和自訂監視。

### 服務邊緣 {#service-edge}

您的所有AEMas a Cloud Service環境都受到可用性監控。 不過， Service Edge Monitoring僅適用於生產環境，而且會使用量度來計算客戶的SLA。 這會考量到環境執行階段和AEMas a Cloud ServiceCDN。 Service Edge Monitoring會採用靠近您所選區域的五個不同位置，並定期檢查可用性。 網站無法使用將觸發警報，並與Adobe的待命支援團隊和流程互動。

### 自訂監視 {#custom-monitoring}

透過自訂監視，客戶可選擇在之前提供最多五個不同的Web屬性URL [上線](/help/journey-migration/go-live.md). 這些URL應有效並傳回HTTP 200回應代碼。 這些顯示器支援以下客戶： [自備CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) 在AdobeCDN之前以及在AEMas a Cloud Service之前採用且非Adobe控制的任何外部流量路由。 自訂監控檢查產生的警報將與Adobe的支援團隊和流程互動。

>[!NOTE]
>
> 此功能僅提供給具有下列專案的客戶： [進階雲端支援。](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html#support-add-ons) 如果您有任何問題，請透過Admin Console提出支援案例。

## 內部模組監控 {#module-monitoring}

雖然外部可用性主要針對一般使用者監控，但內部模組監控會觀察架構子系統是否名義上運作且功能或效能並未降低。 一旦發生問題，就會觸發警報，因此可自動進行修復，或透過營運團隊參與進行修復，以防止可用性受損。 有各種不同的監視器類別，下面顯示了一些檢查範例：

* CPU iowait百分比未超過特定臨界值。
* 執行個體重新部署不會超過特定頻率。
* 磁碟使用量低於某個臨界值。
* 作者存放庫大小在特定範圍內。
* 已成功完成備份作業。
* 資料庫健康狀況和效能受到監視。
* AEM Cloud Services如預期般運作，包括沒有封鎖的復寫佇列、一致的資料和效能查詢。

為Forms布建的環境會新增其他檢查。 請記住，檢查定義並非靜態，且可能會變更和更新。

## 客戶可觀察性 {#customer-observability}

客戶可以使用 [New Relic應用程式效能監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) 此套裝提供收集到的即時效能資料，並製成圖表以供分析和疑難排解。 客戶可以使用監控套裝直接觀察各種量度，例如：JVM效能量度、Java交易時間、背景外部呼叫和資料庫呼叫。

## 其他资源 {#resources}

* [New Relic應用程式效能監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [AEMas a Cloud Service記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [监控环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
