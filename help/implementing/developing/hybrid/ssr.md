---
title: SPA和伺服器端轉譯
description: 在SPA中使用伺服器端轉譯(SSR)可以加速頁面的初始載入，然後將進一步的轉譯傳遞給使用者端。
exl-id: be409559-c7ce-4bc2-87cf-77132d7c2da1
source-git-commit: a9eb03d4db478a4db8e6d2436bd06dcde70a3eeb
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---

# SPA和伺服器端轉譯{#spa-and-server-side-rendering}

單頁應用程式(SPA)可為使用者提供豐富的動態體驗，以熟悉的方式反應和行為，通常就像原生應用程式一樣。 [這是透過依賴使用者端先載入內容，然後處理使用者互動來完成的](introduction.md#how-does-a-spa-work) 進而將使用者端與伺服器之間所需的通訊量減到最少，讓應用程式更具反應性。

不過，這可能會導致初始載入時間更長，尤其是當SPA較大且內容豐富時。 為了最佳化載入時間，部分內容可以在伺服器端轉譯。 使用伺服器端轉譯(SSR)可以加速頁面的初始載入，然後將進一步的轉譯傳遞給使用者端。

## 何時使用SSR {#when-to-use-ssr}

並非所有專案都需要SSR。 雖然AEM完全支援適用於SPA的JS SSR，但Adobe不建議為每個專案系統地實作它。

決定實作SSR時，您必須先評估新增SSR對專案（包括長期維護）實際代表的其他複雜性、工作量和成本。 只有在增加值明顯超過預估成本時，才應選擇SSR架構。

SSR通常會在下列任一問題明確為「是」時提供某些值：

* **SEO：** 您的網站是否仍需要SSR才能由帶來流量的搜尋引擎正確索引？ 請記住，主要搜尋引擎編目程式現在會評估JS。
* **頁面速度：** SSR是否能在實際環境中提供可衡量的速度提升，並增加整體使用者體驗？

只有當您的專案中至少有一個問題以明確的「是」回答時，Adobe才會建議實作SSR。 以下小節說明如何使用Adobe I/O Runtime （的一部分）執行此操作 [App Builder](https://developer.adobe.com/app-builder).

## Adobe I/O Runtime {#adobe-i-o-runtime}

若您 [確信您的專案需要實作SSR](#when-to-use-ssr)，Adobe建議的解決方案是使用Adobe I/O Runtime。

如需Adobe I/O Runtime的詳細資訊，請參閱

* [https://developer.adobe.com/runtime](https://developer.adobe.com/runtime)  — 概述App Builder的執行階段功能
* [https://developer.adobe.com/app-builder](https://developer.adobe.com/app-builder)  — 瞭解完整App Builder產品的詳細資訊
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs)  — 以取得詳細檔案

以下章節詳細說明如何使用Adobe I/O Runtime在兩種不同的模型中為您的SPA實作SSR：

* [AEM導向的通訊流程](#aem-driven-communication-flow)
* [Adobe I/O Runtime導向的通訊流程](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建議每個環境（預備、生產、測試等）使用個別的Adobe I/O Runtime工作區。 這允許典型的系統開發生命週期(SDLC)模式，以及部署到不同環境的單一應用程式不同版本。  檢視檔案 [App Builder應用程式的CI/CD](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) 以取得詳細資訊。
>
>除非每個執行個體型別的執行階段實作有所差異，否則每個執行個體（作者、發佈）不需要個別的工作區。

## 遠端轉譯器設定 {#remote-content-renderer-configuration}

AEM必須知道可以在哪裡擷取遠端呈現的內容。 不論 [您選擇為SSR實作的模式、](#adobe-i-o-runtime) 您必須向AEM指定如何存取此遠端呈現服務。

這是透過 **RemoteContentRenderer — 組態處理站OSGi服務**. 在Web主控台設定主控台中搜尋字串「RemoteContentRenderer」，網址為 `http://<host>:<port>/system/console/configMgr`.

![轉譯器設定](assets/renderer-configuration.png)

下列欄位可供設定使用：

* **內容路徑模式**  — 規則運算式，以符合部分內容（如有必要）
* **遠端端點URL**  — 負責產生內容的端點URL
   * 若不在本機網路中，請使用安全的HTTPS通訊協定。
* **其他請求標頭**  — 要新增至傳送至遠端端點的請求的其他標頭
   * 图案: `key=value`
* **請求逾時**  — 遠端主機要求逾時（毫秒）

>[!NOTE]
>
>無論您是否選擇實作 [AEM導向的通訊流程](#aem-driven-communication-flow) 或 [Adobe I/O Runtime導向的流量，](#adobe-i-o-runtime-driven-communication-flow) 您必須定義遠端內容轉譯器設定。

>[!NOTE]
>
>此設定會利用 [遠端內容轉譯器、](#remote-content-renderer) 提供其他擴充功能和自訂選項。

## AEM導向的通訊流程 {#aem-driven-communication-flow}

使用SSR時， [元件互動工作流程](introduction.md#interaction-with-the-spa-editor) AEM中的SPA包含在Adobe I/O Runtime上產生應用程式初始內容的階段。

1. 瀏覽器會向AEM要求SSR內容。
1. AEM會將模型發佈至Adobe I/O Runtime。
1. Adobe I/O Runtime會傳回產生的內容。
1. AEM透過後端頁面元件的HTL範本提供Adobe I/O Runtime傳回的HTML。

![SSE CMS導向的AEMAdobe I/O](assets/ssr-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime導向的通訊流程 {#adobe-i-o-runtime-driven-communication-flow}

上一節將說明AEM中與SPA有關的伺服器端轉譯的標準與建議實作，AEM在此會執行內容啟動載入與服務。

或者，您也可以實作SSR，讓Adobe I/O Runtime負責啟動程式，有效地反轉通訊流程。

這兩種模式都有效，並受到AEM支援。 不過，在實作特定模型之前，您應該先考量各自的優缺點。

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrapping</strong></th>
   <th><strong>优点</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <th><strong>透過AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM會視需要管理插入程式庫</li>
     <li>僅需在AEM上維護資源<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA開發人員可能不熟悉<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>透過Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>SPA開發人員更熟悉<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>AEM開發人員需透過 <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code> 屬性<br /> </li>
     <li>資源必須在AEM和Adobe I/O Runtime之間同步<br /> </li>
     <li>若要啟用SPA的撰寫功能，可能需要Adobe I/O Runtime的Proxy伺服器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 規劃SSR {#planning-for-ssr}

通常只需要將部分應用程式呈現在伺服器端。 常見的範例是在伺服器端轉譯頁面初始載入時，顯示在摺頁上方的內容。 這可傳送給使用者端已演算的內容，以節省時間。 當使用者與SPA互動時，其他內容會由使用者端轉譯。

當您考慮為SPA實作伺服器端轉譯時，需要檢閱應用程式的哪些部分有必要。

## 使用SSR開發SPA {#developing-an-spa-using-ssr}

SPA元件可由使用者端（在瀏覽器中）或伺服器端轉譯。 呈現伺服器端時，視窗大小和位置等瀏覽器屬性不存在。 因此，SPA元件應同構，不對其呈現的位置做任何假設。

若要運用SSR，您需要在AEM以及負責伺服器端轉譯的Adobe I/O Runtime上部署程式碼。 大部分的程式碼都會相同，但伺服器特定的工作會有所不同。

## AEM中SPA的SSR {#ssr-for-spas-in-aem}

AEM中適用於SPA的SSR需要Adobe I/O Runtime，此模組會在轉譯應用程式內容伺服器端時呼叫。 在應用程式的HTL中，會呼叫Adobe I/O Runtime上的資源來呈現內容。

就像AEM可立即支援Angular和React SPA架構一樣，Angular和React應用程式也支援伺服器端轉譯。 如需詳細資訊，請參閱這兩個架構的NPM檔案。

## 遠端內容轉譯器 {#remote-content-renderer}

此 [遠端內容轉譯器設定](#remote-content-renderer-configuration) SPA在AEM中搭配使用SSR時，需要用到更一般的轉譯服務，這些服務可以根據您的需求擴充和自訂。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` 是OSGi服務，用於擷取遠端伺服器上轉譯的內容，例如從Adobe I/O。傳送至遠端伺服器的內容是根據傳遞的請求引數。

`RemoteContentRenderingService` 當需要額外內容操作時，可透過相依性反轉插入自訂Sling模型或servlet中。

此服務由內部使用 [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

此 `RemoteContentRendererRequestHandlerServlet` 可用於以程式設計方式設定請求設定。 `DefaultRemoteContentRendererRequestHandlerImpl`提供的預設要求處理常式實作)可讓您建立多個OSGi設定，以將內容結構中的位置對應至遠端端點。

若要新增自訂請求處理常式，請實作 `RemoteContentRendererRequestHandler` 介面。 請務必設定 `Constants.SERVICE_RANKING` component屬性至大於100的整數，也就是排序方式 `DefaultRemoteContentRendererRequestHandlerImpl`.

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 設定預設處理常式的OSGi設定 {#configure-default-handler}

預設處理常式的設定必須依照一節中所述進行設定 [遠端內容轉譯器設定](#remote-content-renderer-configuration).

### 遠端內容轉譯器使用情形 {#usage}

要擷取servlet並傳回一些可插入頁面的內容：

1. 確定您的遠端伺服器可以存取。
1. 將下列其中一個片段新增至AEM元件的HTL範本。
1. 選擇性地建立或修改OSGi設定。
1. 瀏覽網站內容

通常，頁面元件的HTL範本是這類功能的主要收件者。

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要求 {#requirements}

此servlet會利用Sling模型匯出工具來序列化元件資料。 根據預設，兩者皆會 `com.adobe.cq.export.json.ContainerExporter` 和 `com.adobe.cq.export.json.ComponentExporter` 支援作為Sling模型介面卡。 如有必要，您可以使用 `RemoteContentRendererServlet` 並實作 `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. 其他類別必須擴充 `ComponentExporter`.
