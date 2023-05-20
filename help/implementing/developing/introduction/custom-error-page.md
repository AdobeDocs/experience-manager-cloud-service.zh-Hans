---
title: 自定义错误页面
description: AEM隨附處理HTTP錯誤的標準錯誤處理常式，且可自訂。
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
source-git-commit: b20d40a9f5f4bda51c67cda1164d0c4d74943aa1
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# 自訂錯誤頁面 {#customizing-error-pages}

AEM隨附處理HTTP錯誤的標準錯誤處理常式；例如，顯示：

![標準錯誤訊息](assets/error-message-standard.png)

為了回應錯誤，AEM提供 `404.jsp` 下的指令碼 `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>由於AEM是以Apache Sling為基礎，因此提供進一步資訊 [（位於Apache錯誤處理檔案中）。](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>在作者執行個體上， [CQ WCM偵錯篩選器](/help/implementing/deploying/configuring-osgi.md) 預設為啟用。 這會一律產生回應代碼200。 預設錯誤處理常式會透過將完整棧疊追蹤寫入回應來回應。
>
>在發佈執行個體上，CQ WCM偵錯篩選器為 **一律** 停用（即使設定為已啟用）。

## 如何自訂錯誤處理常式顯示的頁面 {#how-to-customize-pages-shown-by-the-error-handler}

您可以開發自己的指令碼，以便在發生錯誤時自訂錯誤處理常式顯示的頁面。 為此，您將運用 [AEM標準覆蓋機制](/help/implementing/developing/introduction/overlays.md) 以便您的自訂頁面建立在 `/apps` 和覆蓋下的預設頁面 `/libs`.

1. 在存放庫中，複製預設指令碼：

   * 从 `/libs/sling/servlet/errorhandler/`
   * 到 `/apps/sling/servlet/errorhandler/`

   目的地路徑預設不存在，因此在第一次執行此動作時，您將需要建立路徑。

1. 导航到 `/apps/sling/servlet/errorhandler`。您可以：

   * 編輯適當的現有指令碼，以提供所需的資訊。 或者
   * 建立和編輯所需程式碼的新指令碼。

1. 儲存變更並測試。

>[!CAUTION]
>
>此 `404.jsp` Script是專為滿足AEM驗證而設計；特別是為了在出現這些錯誤時允許系統登入。
>
>因此，應謹慎取代此指令碼。

### 自訂HTTP 500錯誤的回應 {#customizing-the-response-to-http-errors}

HTTP [500內部伺服器錯誤](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) 表示伺服器端錯誤，例如伺服器遇到無法完成要求的非預期狀況。

當請求處理導致例外狀況時，Apache Sling架構(AEM建置在其上)：

* 記錄例外狀況
* 並在回應內文中傳回：
   * HTTP回應代碼500
   * 例外狀況棧疊追蹤

作者： [自訂錯誤處理常式顯示的頁面](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` 可建立指令碼。 但是，它僅用於 `HttpServletResponse.sendError(500)` 明確地執行，即從例外狀況收集器。

否則，回應代碼會設為500，但 `500.jsp` 指令碼未執行。

若要處理500個錯誤，錯誤處理常式指令碼的檔案名稱必須與exception類別（或超類別）相同。 若要處理所有此類例外，您可以建立指令碼 `/apps/sling/servlet/errorhandler/Throwable.jsp` 或 `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!NOTE]
>
>在AEM as Cloud Service中，從後端收到5XX錯誤時，CDN會提供一般錯誤頁面。 為了允許後端的實際回應通過，您需要將以下標頭新增到回應中： `x-aem-error-pass: true`.
>這僅適用於來自AEM或Apache/Dispatcher層的回應。 其他來自中繼基礎結構層的非預期錯誤仍會顯示一般錯誤頁面。

>[!CAUTION]
>
>在作者執行個體上， [CQ WCM偵錯篩選器](/help/implementing/deploying/configuring-osgi.md) 預設為啟用。 這會一律產生回應代碼200。 預設錯誤處理常式會透過將完整棧疊追蹤寫入回應來回應。
>
>對於自訂錯誤處理常式，需要程式碼為500的回應，因此 [需要停用CQ WCM偵錯篩選器。](/help/implementing/deploying/configuring-osgi.md) 如此可確保傳回回應代碼500，而這會觸發正確的Sling錯誤處理常式。
>
>在發佈執行個體上，CQ WCM偵錯篩選器為 **一律** 停用（即使設定為已啟用）。
