---
title: AEM as a Cloud Service 中的缓存
description: AEM as a Cloud Service 中的缓存
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: 6bca307dcf41b138b5b724a8eb198ac35e2d906e
workflow-type: tm+mt
source-wordcount: '2832'
ht-degree: 2%

---

# 简介 {#intro}

流量會透過CDN傳遞至Apache網頁伺服器層，該層支援包括Dispatcher在內的模組。 為了提高效能，Dispatcher主要用作快取，以限制發佈節點上的處理。
規則可以套用至Dispatcher設定，以修改任何預設快取逾期設定，從而在CDN上產生快取。 請注意，在以下情況下，Dispatcher也會遵守產生的快取逾期標頭： `enableTTL` 會在Dispatcher設定中啟用，這表示它會重新整理特定內容，即使是在重新發佈的內容以外也是如此。

此頁面也說明Dispatcher快取如何失效，以及快取如何在關於使用者端程式庫的瀏覽器層級運作。

## 缓存 {#caching}

### HTML/文字 {#html-text}

* 根據預設，瀏覽器會快取五分鐘 `cache-control` Apache圖層發出的標頭。 CDN也會遵守此值。
* 預設HTML/文字快取設定可透過定義 `DISABLE_DEFAULT_CACHING` 中的變數 `global.vars`：

```
Define DISABLE_DEFAULT_CACHING
```

例如，如果您的商業邏輯需要微調年齡標題（具有以行事曆日期為基準的值），因為依預設，年齡標題設為0，則此功能會很有用。 也就是說， **關閉預設快取時，請務必小心。**

* 可透過定義「 」以覆寫所有HTML/文字內容 `EXPIRATION_TIME` 中的變數 `global.vars` 使用AEMas a Cloud ServiceSDK Dispatcher工具。
* 可在較精細的層級上覆寫，包括獨立控制CDN和瀏覽器快取，且搭配下列Apache `mod_headers` 指令：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >Surrogate-Control標頭會套用至Adobe管理的CDN。 若使用 [客戶管理的CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN)，視您的CDN提供者而定，可能需要不同的標頭。

   設定全域快取控制標頭或符合寬規則運算式的標頭時，請務必小心，以免這些標頭套用至需要設為私密的內容。 請考慮使用多個指示詞，以確保以微調的方式套用規則。 話雖如此，如果AEMas a Cloud Service偵測到快取標頭已套用至偵測到Dispatcher無法快取的內容，則會移除快取標頭，如Dispatcher檔案所述。 為了強制AEM一律套用快取標頭，您可以新增 **一律** 選項如下所示：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header unset Cache-Control
        Header unset Expires
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   您必須確保檔案位於 `src/conf.dispatcher.d/cache` 擁有下列規則（在預設設定中）：

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* 防止快取特定內容 **在CDN**，將Cache-Control標頭設為 *私人*. 例如，下列專案會防止在名為的目錄下有html內容 **secure** 從CDN快取：

   ```
      <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
      Header unset Cache-Control
      Header unset Expires
      Header always set Cache-Control "private"
     </LocationMatch>
   ```

* 雖然設定為私密的HTML內容將不會在CDN上快取，但可以在以下情況下在Dispatcher上快取 [許可權敏感型快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hans) 已設定，確保只能向授權使用者提供內容。

   >[!NOTE]
   >其他方法，包括 [dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)，將不會成功覆寫值。

   >[!NOTE]
   >請注意，Dispatcher可能仍會根據自己的快取內容 [快取規則](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html). 若要讓內容真正成為私人，您應該確保Dispatcher不會快取該內容。

### 使用者端資料庫(js，css) {#client-side-libraries}

* 使用AEM使用者端程式庫架構時，JavaScript和CSS程式碼的產生方式會讓瀏覽器無限期快取，因為任何變更都會顯示為具有唯一路徑的新檔案。  換言之，將會視需要產生參考使用者端資料庫的HTML，以便客戶在發佈新內容時體驗這些內容。 若舊版瀏覽器不遵循「不可變」值，則cache-control會設為「不可變」或30天。
* 請參閱區段 [使用者端程式庫和版本一致性](#content-consistency) 以取得其他詳細資訊。

### 影像和任何足夠大以儲存在blob儲存空間中的內容 {#images}

對於在2022年5月中旬之後建立的程式(特別是高於65000的程式ID)，預設行為是快取，同時也遵循請求的驗證上下文。 較舊程式(程式id等於或低於65000)預設不會快取blob內容。

在這兩種情況下，都可以使用Apache在Apache/Dispatcher層的更精細層級上覆寫快取標頭 `mod_headers` 指示詞，例如：

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

修改Dispatcher層上的快取標頭時，請注意不要快取太廣泛，請參閱HTML/文字區段中的討論 [以上](#html-text). 此外，請確定原本要私密儲存（而非快取）的資產並未包含在 `LocationMatch` 指示詞篩選器。

#### 新的預設快取行為 {#new-caching-behavior}

AEM層會根據是否已設定快取標頭及請求型別的值來設定快取標頭。 請注意，如果尚未設定快取控制標頭，則會快取公開內容，且已驗證的流量會設定為私人。 如果已設定快取控制標頭，則快取標頭將保持不變。

| 快取控制標頭是否存在？ | 请求类型 | AEM將快取標頭設為 |
|------------------------------|---------------|------------------------------------------------|
| 否 | 公共 | Cache-Control： public， max-age=600， immutable |
| 否 | 已驗證 | Cache-Control： private， max-age=600， immutable |
| 是 | 任何 | 未變更 |

雖然不建議使用，但您可以設定Cloud Manager環境變數，將新的預設行為變更為遵循舊行為(程式id等於或低於65000) `AEM_BLOB_ENABLE_CACHING_HEADERS` 為false。

#### 較舊的預設快取行為 {#old-caching-behavior}

AEM層預設不會快取blob內容。

>[!NOTE]
>建議將Cloud Manager環境變數AEM_BLOB_ENABLE_CACHING_HEADERS設定為true，以將舊預設行為變更為與新行為(高於65000的程式ID)一致。 如果程式已上線，請務必確認在變更後，內容會如預期般運作。

目前，在Blob儲存空間中標示為私用的影像無法在使用的Dispatcher上快取 [許可權敏感型快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hans). 影像一律會從AEM來源要求，並在使用者獲得授權時提供。

>[!NOTE]
>其他方法，包括 [dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)，將無法成功覆寫值。

### 節點存放區中的其他內容檔案型別 {#other-content}

* 無預設快取
* 預設值不可設定為 `EXPIRATION_TIME` 用於html/文字檔案型別的變數
* 透過指定適當的規則運算式，可以使用html/text區段中描述的相同LocationMatch策略來設定快取有效期

### 進一步最佳化 {#further-optimizations}

* 避免使用 `User-Agent` 作為 `Vary` 標頭。 舊版預設Dispatcher設定（原型版本28之前）包含此專案，建議您使用下列步驟將其移除。
   * 在中找到vhost檔案 `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * 移除或註釋掉該行： `Header append Vary User-Agent env=!dont-vary` 來自所有vhost檔案，但default.vhost除外，其為唯讀
* 使用 `Surrogate-Control` 標頭可控制CDN快取，不受瀏覽器快取影響
* 考慮套用 [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) 和 [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) 指示可允許背景重新整理並避免快取遺漏，讓使用者可以快速且新鮮地保留您的內容。
   * 套用這些指示詞的方法有很多種，但新增30分鐘即可 `stale-while-revalidate` 對於所有快取控制標題而言，這是一個良好的起點。
* 以下是各種內容型別的範例，在設定自己的快取規則時，這些範例可作為指南。 請仔細考慮並測試您的特定設定和需求：

   * 快取可變使用者端程式庫資源12h及12h後背景重新整理。

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 透過背景重新整理來快取不可變的使用者端程式庫資源長期（30天），以避免遺漏。

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 在瀏覽器上快取HTML頁面5分鐘，背景重新整理1小時，在CDN上快取12小時。 將一律新增Cache-Control標頭，因此請務必確保將/content/*下相符的html頁面設為公開。 如果沒有，請考慮使用更具體的規則運算式。

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 在瀏覽器上快取內容服務/Sling模型匯出程式json回應達5分鐘，背景重新整理為1小時，在CDN上為12小時。

      ```
      <LocationMatch "^/content/.*\.model\.json$">
         Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 透過背景重新整理來長期（30天）快取核心影像元件中的不可變URL，以避免遺漏。

      ```
      <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 快取來自DAM的可變資源（例如影像和視訊）24h，並在12h後重新整理背景以避免遺漏

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### HEAD要求行為 {#request-behavior}

在AdobeCDN收到資源的HEAD要求時，該資源 **not** 快取後，請求會進行轉換，然後由Dispatcher和/或AEM執行個體接收為GET請求。 如果回應可快取，則會從CDN提供後續HEAD請求。 如果回應無法快取，則後續的HEAD請求將會在一段時間內傳遞給Dispatcher和/或AEM執行個體，具體時間取決於 `Cache-Control` 總計

### 行銷活動引數 {#marketing-parameters}

網站URL經常包含用來追蹤促銷活動成功的行銷活動引數。 為了有效使用Dispatcher快取，建議您配置Dispatcher設定的 `ignoreUrlParams` 屬性為 [在此處記錄](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters).

此 `ignoreUrlParams` 區段必須取消註解，並應參考檔案 `conf.dispatcher.d/cache/marketing_query_parameters.any`. 您可取消註解行銷管道相關引數的對應行，以修改檔案。 您也可以新增其他引數。

```
/ignoreUrlParams {
{{ /0001 { /glob "*" /type "deny" }}}
{{ $include "../cache/marketing_query_parameters.any"}}
}
```

## Dispatcher快取失效 {#disp}

一般而言，不需要讓Dispatcher快取失效。 反之，您應該仰賴Dispatcher在重新發佈內容時重新整理其快取，並且CDN遵循快取到期標頭。

### Dispatcher快取在啟用/停用期間失效 {#cache-activation-deactivation}

和舊版AEM一樣，發佈或取消發佈頁面會從Dispatcher快取中清除內容。 如果懷疑有快取問題，您應重新發佈有問題的頁面，並確保有符合的虛擬主機可用 `ServerAlias` Dispatcher快取失效所需的localhost。

>[!NOTE]
>為了讓Dispatcher正確失效，請確定來自「127.0.0.1」、「localhost」、「.local」、「.adobeaemcloud.com」和「.adobeaemcloud.net」的請求都符合，並由vhost設定處理，以便可以提供這些請求。 您可以按照參照中的模式，在全域比對「*」的捕獲所有vhost設定中執行此操作 [AEM原型](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost) 或確保上述清單是由其中一個vhosts擷取。

當發佈執行個體從作者收到新版本的頁面或資產時，它會使用排清代理程式來讓其Dispatcher上的適當路徑失效。 更新的路徑會與其父項一起從Dispatcher快取中移除，最多可移除一個層級(您可以透過 [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level))。

## 明確使Dispatcher快取失效 {#explicit-invalidation}

Adobe建議使用標準快取標頭來控制內容傳送生命週期。 不過，如有需要，可直接使Dispatcher中的內容失效。

下列清單包含您想要明確讓快取失效的情境（在選擇接聽讓失效完成時）：

* 發佈體驗片段或內容片段等內容後，讓參考這些元素的已發佈和快取內容失效。
* 參考頁面成功失效時通知外部系統。

有兩種方式可明確讓快取失效：

* 偏好使用的方法是使用Author的Sling內容發佈(SCD)。
* 使用復寫API叫用發佈Dispatcher排清復寫代理程式。

方法因層級可用性、重複事件刪除能力及事件處理保證而異。 下表總結了這些選項：

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>不适用</th>
    <th>層級可用性</th>
    <th>重複資料刪除 </th>
    <th>保證 </th>
    <th>操作 </th>
    <th>影响 </th>
    <th>描述 </th>
  </tr>  
  <tr>
    <td>Sling內容發佈(SCD) API</td>
    <td>创作</td>
    <td>可能使用Discovery API或啟用 <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">去重複化模式</a>.</td>
    <td>至少一次。</td>
    <td>
     <ol>
       <li>添加</li>
       <li>删除</li>
       <li>失效</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>階層/統計層級</li>
       <li>階層/統計層級</li>
       <li>僅限資源層級</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>發佈內容並讓快取失效。</li>
       <li>移除內容並讓快取失效。</li>
       <li>讓內容失效而不發佈。</li>
     </ol>
     </td>
  </tr>
  <tr>
    <td>复制 API</td>
    <td>发布</td>
    <td>不可能，會在每個發佈執行個體上引發事件。</td>
    <td>盡最大努力。</td>
    <td>
     <ol>
       <li>啟動</li>
       <li>停用</li>
       <li>删除</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>階層/統計層級</li>
       <li>階層/統計層級</li>
       <li>階層/統計層級</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>發佈內容並讓快取失效。</li>
       <li>從作者/發佈層 — 移除內容並使快取失效。</li>
       <li><p><strong>來自作者階層</strong>  — 移除內容並讓快取失效（如果從發佈代理程式上的AEM作者層級觸發）。</p>
           <p><strong>從發佈階層</strong>  — 僅讓快取失效（如果從Flush或僅限資源的排清代理程式上的AEM Publish層級觸發）。</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

請注意，與快取失效直接相關的兩個動作是Sling內容發佈(SCD) API失效和復寫API停用。

此外，從表格中，我們發現：

* 當必須保證每個事件時（例如，與需要精確知識的外部系統同步），就需要SCD API。 如果在失效呼叫時存在發佈層級升級事件，則當每個新發佈處理失效時，會引發一個額外事件。

* 使用復寫API不是常見的使用案例，但應用於觸發使快取失效的觸發器來自發佈層級，而不是作者層級的情況。 如果已設定Dispatcher TTL，這可能會很有用。

總而言之，如果您想要讓Dispatcher快取失效，建議的選項是使用Author的SCD API失效動作。 此外，您也可以接聽事件，以便接著觸發後續的下游動作。

### Sling內容發佈(SCD) {#sling-distribution}

>[!NOTE]
>使用下列指示時，請注意您應在AEM Cloud Service開發環境中測試自訂程式碼，而不是在本機測試。

使用Author的SCD動作時，實作模式如下：

1. 從Author撰寫自訂程式碼以叫用Sling內容發佈 [API](https://sling.apache.org/documentation/bundles/content-distribution.html)，使用路徑清單傳遞失效動作：

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* （可選）接聽反映所有Dispatcher執行個體已失效之資源的事件：


```
package org.apache.sling.distribution.journal.shared;

import org.apache.sling.discovery.DiscoveryService;
import org.apache.sling.distribution.journal.impl.event.DistributionEvent;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import static org.apache.sling.distribution.DistributionRequestType.INVALIDATE;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_PATHS;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_TYPE;
import static org.apache.sling.distribution.event.DistributionEventTopics.AGENT_PACKAGE_DISTRIBUTED;
import static org.osgi.service.event.EventConstants.EVENT_TOPIC;

@Component(immediate = true, service = EventHandler.class, property = {
        EVENT_TOPIC + "=" + AGENT_PACKAGE_DISTRIBUTED
})
public class InvalidatedHandler implements EventHandler {
    private static final Logger LOG = LoggerFactory.getLogger(InvalidatedHandler.class);

    @Reference
    private DiscoveryService discoveryService;

    @Override
    public void handleEvent(Event event) {

        String distributionType = (String) event.getProperty(DISTRIBUTION_TYPE);

        if (INVALIDATE.name().equals(distributionType)) {
            boolean isLeader = discoveryService.getTopology().getLocalInstance().isLeader();
            // process the OSGi event on the leader author instance
            if (isLeader) {
                String[] paths = (String[]) event.getProperty(DISTRIBUTION_PATHS);
                String packageId = (String) event.getProperty(DistributionEvent.PACKAGE_ID);
                invalidated(paths, packageId);
            }
        }
    }

    private void invalidated(String[] paths, String packageId) {
        // custom logic
        LOG.info("Successfully applied package with id {}, paths {}", packageId, paths);
    }
}
```

<!-- Optionally, instead of using the isLeader approach, one could add an OSGi configuration for the PID org.apache.sling.distribution.journal.impl.publisher.DistributedEventNotifierManager and property deduplicateEvent=true. But we'll stick with just one strategy and not mention it (double-check this).**review this**-->

* （選擇性）在中執行商業邏輯 `invalidated(String[] paths, String packageId)` 上方的方法。

>[!NOTE]
>
>當Dispatcher失效時，不會排清AdobeCDN。 Adobe管理的CDN會遵守TTL，因此不需要進行清除。

### 复制 API {#replication-api}

以下是使用「復寫API停用」動作時的實作模式：

1. 在發佈層上，呼叫復寫API以觸發發佈Dispatcher Flush復寫代理程式。

無法設定排清代理程式端點，而是預先設定為指向Dispatcher，與排清代理程式旁邊執行的發佈服務相符。

排清代理程式通常可由根據OSGi事件或工作流程的自訂程式碼觸發。

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals("flush");
  }
});

Replicator.replicate (session,ReplicationActionType.DELETE,paths, options);
```

<!-- In general, it will not be necessary to manually invalidate content in the dispatcher, but it is possible if needed.

>[!NOTE]
>Prior to AEM as a Cloud Service, there were two ways of invalidating the dispatcher cache.
>
>1. Invoke the replication agent, specifying the publish dispatcher flush agent
>2. Directly calling the `invalidate.cache` API (for example, `POST /dispatcher/invalidate.cache`)
>
>The dispatcher's `invalidate.cache` API approach will no longer be supported since it addresses only a specific dispatcher node. AEM as a Cloud Service operates at the service level, not the individual node level and so the invalidation instructions in the [Invalidating Cached Pages From AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) page are not longer valid for AEM as a Cloud Service.

The replication flush agent should be used. This can be done using the [Replication API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). The flush agent endpoint is not configurable but pre-configured to point to the dispatcher, matched with the publish service running the flush agent. The flush agent can typically be triggered by OSGi events or workflows.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 

The diagram presented below illustrates this.

![CDN](assets/cdnd.png "CDN")

If there is a concern that the dispatcher cache isn't clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## 使用者端程式庫和版本一致性 {#content-consistency}

頁面由HTML、Javascript、CSS和影像組成。 建議客戶善用 [使用者端資料庫(clientlibs)架構](/help/implementing/developing/introduction/clientlibs.md) 以將Javascript和CSS資源匯入HTML頁面，同時考量JS程式庫之間的相依性。

clientlibs架構提供自動版本管理，這表示開發人員可以在原始檔控制中籤入JS程式庫的變更，而且當客戶推送其版本時，將可使用最新版本。 若沒有此專案，開發人員將需要手動變更HTML，並參考新版本的程式庫，而如果許多HTML範本共用相同的程式庫，則這項作業會特別繁重。

將程式庫的新版本發佈到生產環境時，會更新參考HTML頁面，並包含這些已更新程式庫版本的新連結。 指定HTML頁面的瀏覽器快取過期後，就不必擔心系統會從瀏覽器快取載入舊程式庫，因為重新整理的頁面(來自AEM)現在保證會參照新版本的程式庫。 換言之，重新整理的HTML頁面將包含所有最新程式庫版本。

其機制是序列化雜湊，這會附加至使用者端程式庫連結，確保瀏覽器有唯一、版本化的URL來快取CSS/JS。 只有在使用者端程式庫的內容變更時，才會更新序列化雜湊。 換句話說，即使使用新部署，如果發生不相關的更新（即使用者端程式庫的基礎css/js沒有變更），參照仍會維持不變，可確保對瀏覽器快取的中斷較少。

### 啟用Longcache版本的使用者端資料庫 — AEMas a Cloud ServiceSDK快速入門 {#enabling-longcache}

預設clientlib包含在HTML頁面上看起來像下面的範例：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

啟用嚴格clientlib版本設定時，會將長期雜湊金鑰作為選擇器新增到使用者端程式庫。 因此，clientlib參考看起來像這樣：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

在所有AEMas a Cloud Service環境中，預設會啟用嚴格clientlib版本設定。

若要在本機SDK快速入門中啟用嚴格的clientlib版本設定，請執行下列動作：

1. 導覽至OSGi Configuration Manager `<host>/system/console/configMgr`
1. 尋找AdobeGraniteHTML庫管理員的OSGi設定：
   * 勾選核取方塊以啟用嚴格版本設定
   * 在標示為長期使用者端快取金鑰的欄位中，輸入/的值。*；雜湊
1. 保存更改。不需要在原始檔控制中儲存此設定，因為AEMas a Cloud Service會自動在開發、中繼和生產環境中啟用此設定。
1. 每次變更使用者端程式庫的內容時，都會產生新的雜湊金鑰，且會更新HTML參考。
