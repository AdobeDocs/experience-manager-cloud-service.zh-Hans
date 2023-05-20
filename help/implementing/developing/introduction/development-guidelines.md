---
title: AEM as a Cloud Service 开发准则
description: 了解在 AEM as a Cloud Service 上进行开发的准则，以及它与本地 AEM 和 AMS 中的 AEM 的重要区别。
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 5a8d66c2ca2bed664d127579a8fdbdf3aa45c910
workflow-type: tm+mt
source-wordcount: '2591'
ht-degree: 4%

---

# AEM as a Cloud Service 开发准则 {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="AEM as a Cloud Service 开发准则"
>abstract="了解在 AEM as a Cloud Service 上进行开发的准则，以及它与本地 AEM 和 AMS 中的 AEM 的重要区别。"
>additional-url="https://video.tv.adobe.com/v/330555/" text="包结构演示"

本檔案說明在AEMas a Cloud Service上開發的准則，以及它與AEM內部部署和AMS中的AEM不同的重要方式。

## 程式碼必須可感知叢集 {#cluster-aware}

在AEMas a Cloud Service中執行的程式碼必須注意它一律在叢集中執行的事實。 这意味着始终会有多个实例在运行。程式碼必須是可復原的，尤其是因為例項可能隨時停止。

在AEMas a Cloud Service更新期間，會有執行個體同時執行舊程式碼和新程式碼。 因此，舊程式碼不得中斷新程式碼建立的內容，且新程式碼必須能夠處理舊內容。

如果需要識別叢集中的主要節點，可以使用Apache Sling Discovery API來偵測它。

## 記憶體中的狀態 {#state-in-memory}

狀態不得保留在記憶體中，而是保留在存放庫中。 否則，如果執行個體停止，此狀態可能會遺失。

## 檔案系統上的狀態 {#state-on-the-filesystem}

執行個體的檔案系統不應在AEMas a Cloud Service中使用。 磁碟是暫時性的，當執行個體回收時會加以處置。 可以限制將檔案系統用於與處理單一請求相關的臨時儲存，但不應濫用在大型檔案中。 這是因為這可能會對資源使用配額產生負面影響，並遇到磁碟限制。

舉例來說，若不支援使用檔案系統，發佈層級應確保任何需要儲存的資料都會運送至外部服務，以供長期儲存之用。

## 觀察 {#observation}

同樣地，由於所有非同步發生的事（例如對觀察事件採取行動）無法保證會在本機執行，因此必須謹慎使用。 JCR事件和Sling資源事件都是如此。 發生變更時，可能會移除執行個體，並由其他執行個體取代。 拓撲中當時處於作用中的其他執行個體將能夠對該事件做出反應。 但在這種情況下，這不會是本機事件，在發佈事件時甚至可能沒有活動中的領導者，因為正在進行領導人選舉。

## 背景任務和長時間執行的工作 {#background-tasks-and-long-running-jobs}

作為背景工作執行的程式碼必須假設執行所在的例項隨時都會停機。 因此，程式碼必須具有彈性，最重要的是可恢復。 這表示如果程式碼重新執行，就不應該從頭開始，而是從原本的地方開始。 雖然這並非此類程式碼的新需求，但在AEMas a Cloud Service中，執行個體減少的機率較高。

為了將問題降至最低，應儘可能避免長時間執行工作，並且這些工作應至少可恢復。 若要執行這類作業，請使用Sling作業，此作業有至少一次的保證，因此如果中斷，將會儘快重新執行。 但是他們或許不應該從頭開始。 若要排程這類工作，最好使用 [Sling工作](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) scheduler as this again successful the least-one execution.

Sling Commons Scheduler不應用於排程，因為無法保證執行。 只是更有可能將其排程。

同樣地，對於非同步發生的所有事情，例如對觀察事件執行操作（無論是JCR事件或Sling資源事件），無法保證執行，因此必須謹慎使用。 目前的AEM部署已經是如此。

## 傳出HTTP連線 {#outgoing-http-connections}

強烈建議任何傳出HTTP連線設定合理的連線和讀取逾時；連線逾時建議值為1秒，讀取逾時建議值為5秒。 確切的數字必須根據處理這些請求的後端系統的效能來確定。

對於未套用這些逾時的程式碼，在AEMas a Cloud Service上執行的AEM執行個體將強制執行全域逾時。 連線呼叫的逾時值為10秒，而連線的讀取呼叫則為60秒。

Adobe建議使用提供的 [Apache HttpComponents Client 4.x程式庫](https://hc.apache.org/httpcomponents-client-ga/) 用於建立HTTP連線。

已知有效但可能需要自行提供相依性的替代方案包括：

* [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) 和/或 [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (AEM提供)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不建議使用，因為它已過時並由4.x版取代）
* [確定Http](https://square.github.io/okhttp/) (AEM未提供)

除了提供逾時功能外，也應該實作適當處理這類逾時以及非預期的HTTP狀態代碼。

## 無傳統UI自訂 {#no-classic-ui-customizations}

AEMas a Cloud Service僅支援第三方客戶程式碼的Touch UI。 傳統UI無法供自訂。

## 避免原生二進位檔案 {#avoid-native-binaries}

程式碼將無法在執行階段下載或修改二進位檔案。 例如，它將無法解壓縮 `jar` 或 `tar` 檔案。

## 沒有透過AEMas a Cloud Service的串流二進位檔 {#no-streaming-binaries}

二進位檔應透過CDN存取，CDN將在核心AEM服務之外提供二進位檔。

例如，請勿使用 `asset.getOriginal().getStream()`，會觸發將二進位檔案下載至AEM服務的暫存磁碟。

## 沒有反向復寫代理 {#no-reverse-replication-agents}

AEMas a Cloud Service不支援從發佈到製作的反向復寫。 如果需要此類策略，您可以使用在發佈執行個體的陣列之間以及可能在Author叢集之間共用的外部持續性存放區。

## 可能需要移轉轉轉復寫代理 {#forward-replication-agents}

透過pub-sub機制，將內容從Author復寫到Publish。 不支援自訂復寫代理。

## 監視和偵錯 {#monitoring-and-debugging}

### 日志 {#logs}

對於本機開發，記錄專案會寫入本機檔案中的 `/crx-quickstart/logs` 資料夾。

在雲端環境中，開發人員可以透過Cloud Manager下載記錄，或使用命令列工具來追蹤記錄。 <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**設定記錄層級**

若要變更雲端環境的記錄層級，應修改Sling記錄OSGI設定，然後進行完整重新部署。 由於這不是即時的行為，因此在接收大量流量的生產環境中，請謹慎啟用詳細記錄檔。 未來可能會有更快速變更記錄層級的機制。

>[!NOTE]
>
>若要執行下面列出的設定變更，您需要在本機開發環境中建立它們，然後將它們推送到AEMas a Cloud Service執行個體。 如需如何執行此動作的詳細資訊，請參閱 [部署至AEMas a Cloud Service](/help/implementing/deploying/overview.md).

**啟動DEBUG記錄層級**

預設記錄層級為INFO，亦即DEBUG訊息不會被記錄。 若要啟用DEBUG記錄層級，請更新下列屬性以偵錯模式。

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

例如，設定 `/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` ，其值如下。

```json
{
   "org.apache.sling.commons.log.names": [
      "com.example"
   ],
   "org.apache.sling.commons.log.level": "DEBUG",
   "org.apache.sling.commons.log.file": "logs/error.log",
   "org.apache.sling.commons.log.additiv": "false"
}
```

請勿將記錄保留在DEBUG記錄層級超過必要的時間，因為這會產生許多專案。

若您想要一律登入，可使用執行模式式OSGi設定鎖定目標，針對不同的AEM環境設定分散式記錄層級 `DEBUG` 於開發期間。 例如：

|環境 |依據執行模式的OSGi設定位置 | `org.apache.sling.commons.log.level` 屬性值 | | - | - | - | |開發 | /apps/example/config/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json |偵錯 | |階段 | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json |警告 | |生產 | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json |錯誤 |

偵錯檔案中的某一行通常以DEBUG開頭，然後提供記錄層級、安裝程式動作和記錄訊息。 例如：

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

記錄層級如下：

| 0 | 嚴重錯誤 | 動作失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 错误 | 動作已失敗。 安裝會繼續，但部分CRX未正確安裝且將無法運作。 |
| 2 | 警告 | 動作已成功，但發生問題。 CRX不一定能正常運作。 |
| 3 | 信息 | 動作已成功。 |

### 執行緒傾印 {#thread-dumps}

雲端環境上的對話串傾印會持續收集，但目前無法自助下載。 同時，如果偵錯問題需要執行緒傾印，請聯絡AEM支援，並指定確切的時間範圍。

## CRX/DE Lite和開發人員主控台 {#crxde-lite-and-developer-console}

### 本地开发 {#local-development}

對於本機開發，開發人員擁有CRXDE Lite(`/crx/de`)和AEM Web Console (`/system/console`)。

請注意，在本機開發中（使用SDK）， `/apps` 和 `/libs` 可以直接寫入，這與雲端環境不同，在雲端環境中，頂層資料夾是不可變的。

### AEM as a Cloud Service 开发工具 {#aem-as-a-cloud-service-development-tools}

客戶可以在作者階層的開發環境中存取CRXDE Lite，但不能在預備或生產環境中存取。 不可變的存放庫(`/libs`， `/apps`)無法在執行階段寫入，因此嘗試這樣做將會導致錯誤。

而是可以從開發人員控制檯啟動存放庫瀏覽器，為作者、發佈和預覽層級的所有環境提供存放庫的唯讀檢視。 深入瞭解存放庫瀏覽器 [此處](/help/implementing/developing/tools/repository-browser.md).

適用於RDE、開發、測試和生產環境的開發人員控制檯中，提供了一組用於偵錯AEMas a Cloud Service開發人員環境的工具。 可透過調整作者或發佈服務URL來確定URL，如下所示：

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

作為捷徑，以下Cloud Manager CLI命令可用於根據下述環境引數啟動開發人員控制檯：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

另請參閱 [此頁面](/help/release-notes/home.md) 以取得詳細資訊。

開發人員可以產生狀態資訊，並解析各種資源。

如下圖所示，可用的狀態資訊包括套件組合、元件、OSGI設定、Oak索引、OSGI服務和Sling工作的狀態。

![開發主控台1](/help/implementing/developing/introduction/assets/devconsole1.png)

如下圖所示，開發人員可以解析套件相依性和servlet：

![開發主控台2](/help/implementing/developing/introduction/assets/devconsole2.png)

![開發主控台3](/help/implementing/developing/introduction/assets/devconsole3.png)

Developer Console有一個「說明查詢」工具的連結，對偵錯也很有用：

![開發主控台4](/help/implementing/developing/introduction/assets/devconsole4.png)

對於生產計畫，開發人員控制檯的存取權由Admin Console中的「Cloud Manager — 開發人員角色」定義，而對於沙箱計畫，開發人員控制檯則可供任何擁有產品設定檔的使用者使用，這些使用者可存取AEMas a Cloud Service。 對於所有程式，狀態傾印需要「Cloud Manager — 開發人員角色」，存放庫瀏覽器和使用者也必須在AEM使用者或AEM管理員產品設定檔中定義作者和發佈服務，以便檢視來自這兩個服務的資料。 如需設定使用者許可權的詳細資訊，請參閱 [Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### 性能监控 {#performance-monitoring}

Adobe會監控應用程式效能，並在發現狀況惡化時採取措施解決。 目前無法觀察應用程式量度。

## 傳送電子郵件 {#sending-email}

以下各節說明如何請求、設定和傳送電子郵件。

>[!NOTE]
>
>郵件服務可設定為OAuth2支援。 如需詳細資訊，請參閱 [郵件服務的OAuth2支援](/help/security/oauth2-support-for-mail-service.md).

### 啟用傳出電子郵件 {#enabling-outbound-email}

依預設，用來傳送電子郵件的連線埠會停用。 若要啟動連線埠，請設定 [進階網路](/help/security/configuring-advanced-networking.md)，請務必為每個需要的環境設定 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端點的連線埠轉送規則，將預期的連線埠（例如，465或587）對應到Proxy連線埠。

建議使用設定進階網路 `kind` 引數設定為 `flexiblePortEgress` 因為Adobe可以最佳化彈性連線埠輸出流量的效能。 如果需要唯一輸出IP位址，請選擇 `kind` 引數： `dedicatedEgressIp`. 如果您已因其他原因設定VPN，也可以使用該進階網路變數所提供的唯一IP位址。

您必須透過郵件伺服器傳送電子郵件，而非直接傳送給電子郵件使用者端。 否則，可能會封鎖電子郵件。

### 傳送電子郵件 {#sending-emails}

此 [Day CQ郵件服務OSGI服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) 應使用，且電子郵件必須傳送至支援請求中指出的郵件伺服器，而非直接傳送給收件者。

### 配置 {#email-configuration}

AEM中的電子郵件應使用 [Day CQ Mail Service OSGi服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

請參閱 [AEM 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) 以取得有關設定電子郵件設定的詳細資訊。 若為AEMas a Cloud Service，請注意下列必要的調整 `com.day.cq.mailer.DefaultMailService OSGI` 服務：

* SMTP伺服器主機名稱應該設定為$[env：AEM_PROXY_HOST；default=proxy.tunnel]
* 設定進階網路時，SMTP伺服器連線埠應該設定為portForwards引數中所設定的原始Proxy連線埠值，此引數用於API呼叫。 例如，30465 （而非465）

SMTP伺服器連線埠應該設定為 `portDest` 設定進階網路時，在API呼叫中使用的portForwards引數中設定的值，以及 `portOrig` 值應為有意義的值，且必須介於30000 - 30999的所需範圍內。 例如，如果SMTP伺服器連線埠是465，則連線埠30465應該用作 `portOrig` 值。

在此情況下，並假設需要啟用SSL，請在的 **Day CQ Mail Service OSGI** 服務：

* 設定 `smtp.port` 至 `30465`
* 設定 `smtp.ssl` 至 `true`

或者，如果目的地連線埠是587，則 `portOrig` 應使用30587的值。 假設應停用SSL，Day CQ郵件服務OSGI服務的設定會：

* 設定 `smtp.port` 至 `30587`
* 設定 `smtp.ssl` 至 `false`

此 `smtp.starttls` 屬性會由AEMas a Cloud Service在執行階段自動設定為適當的值。 因此，如果 `smtp.ssl` 設為true， `smtp.startls` 會忽略。 若 `smtp.ssl` 設為false `smtp.starttls` 設為true。 這與 `smtp.starttls` 在OSGI設定中設定的值。


您可以選擇使用OAuth2支援來設定郵件服務。 如需詳細資訊，請參閱 [郵件服務的OAuth2支援](/help/security/oauth2-support-for-mail-service.md).

### 舊版電子郵件設定 {#legacy-email-configuration}

在2021.9.0版之前，電子郵件是透過客戶支援要求設定。 請注意下列必要的調整 `com.day.cq.mailer.DefaultMailService OSGI` 服務：

AEMas a Cloud Service需要透過連線埠465傳送郵件。 如果郵件伺服器不支援連線埠465，只要啟用TLS選項，就可以使用連線埠587。

如果已要求連線埠465：

* set `smtp.port` 至 `465`
* set `smtp.ssl` 至 `true`

如果已要求連線埠587，則：

* set `smtp.port` 至 `587`
* set `smtp.ssl` 至 `false`

此 `smtp.starttls` 屬性會由AEMas a Cloud Service在執行階段自動設定為適當的值。 因此，如果 `smtp.ssl` 設為true， `smtp.startls` 會忽略。 若 `smtp.ssl` 設為false `smtp.starttls` 設為true。 這與 `smtp.starttls` 在OSGI設定中設定的值。

SMTP伺服器主機應該設定為郵件伺服器的主機。

## 避免大型多值屬性 {#avoid-large-mvps}

AEMas a Cloud Service底下的Oak內容存放庫不會用於過多的多值屬性(MVP)。 經驗法則是，將MVP保持在1000以下。 然而，實際效能取決於許多因素。

超過1000個之後，預設會記錄警告。 它們類似於以下內容。

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

大型的MVP可能會因為MongoDB檔案超過16 MB而導致錯誤，從而導致類似於以下內容的錯誤。

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

請參閱 [Apache Oak檔案](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property) 以取得更多詳細資料。

## [!DNL Assets] 開發指導方針和使用案例 {#use-cases-assets}

若要瞭解Assetsas a Cloud Service的開發使用案例、建議和參考資料，請參閱 [Assets的開發人員參考資料。](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis)
