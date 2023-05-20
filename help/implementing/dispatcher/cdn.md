---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 25%

---

# AEM as a Cloud Service 中的 CDN {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service 中的 CDN"
>abstract="AEM as a Cloud Service 随附一个内置 CDN。其主要目的是通过从浏览器附近的边缘 CDN 节点提供可缓存的内容来减少延迟。它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。"

AEM as a Cloud Service 随附一个内置 CDN。其主要目的是通过从浏览器附近的边缘 CDN 节点提供可缓存的内容来减少延迟。它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。

AEM管理的CDN可滿足大多數客戶的效能與安全性需求。 对于发布层，客户可以选择从自己的 CDN 指向发布层，但这种情况下客户必须自行管理。 这种情况视个案而定，具体取决于是否在满足某些先决条件，包括但不限于客户及其 CDN 供应商具有难以舍弃的旧版集成。

<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## AEM管理的CDN  {#aem-managed-cdn}

請依照以下章節，使用Cloud Manager自助服務UI，使用AEM現成可用的CDN準備內容傳送：

1. [管理 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制流量**

根據預設，對於AEM管理的CDN設定，所有公共流量都可前往發佈服務，無論是用於生產環境還是非生產（開發和中繼）環境。 您可以透過Cloud Manager使用者介面，針對特定環境限制發佈服務的流量（例如，依IP位址範圍限制分段）。

请参阅[管理 IP 允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)了解详情。

>[!CAUTION]
>
>AEM受管理的CDN只會處理來自允許IP的請求。 如果您將自己的CDN指向AEM管理的CDN，則請確定CDN的IP包含在允許清單中。

## 客戶CDN指向AEM管理的CDN {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="客户 CDN 指向 AEM 托管 CDN"
>abstract="AEM as a Cloud Service 为客户提供了使用现有 CDN 的选项。对于发布层，客户可以选择从自己的 CDN 指向发布层，但这种情况下客户必须自行管理。 这种情况视个案而定，具体取决于是否在满足某些先决条件，包括但不限于客户及其 CDN 供应商具有难以舍弃的旧版集成。"

如果客戶必須使用其現有的CDN，他們可以管理該CDN，並將其指向AEM管理的CDN，前提是滿足以下條件：

* 客戶必須擁有現有的CDN，且必須重新安裝CDN之後才能順利完成更換。
* 客戶必須管理它。
* 客戶必須能夠設定CDN以搭配AEMas a Cloud Service使用 — 請參閱下列設定指示。
* 客戶必須有隨時待命的工程CDN專家，以備出現相關問題時使用。
* 客戶在前往生產環境之前，必須先執行並成功通過負載測試。

設定指示：

1. 將您的CDN指向AdobeCDN的輸入作為其原始網域。 例如：`publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 將SNI設為AdobeCDN的入口。
1. 將Host標頭設定為原始網域。 例如：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 設定 `X-Forwarded-Host` 具有網域名稱的標頭，以便AEM可以判斷主機標頭。 例如：`X-Forwarded-Host:example.com`。
1. 套 `X-AEM-Edge-Key`. 該值應來自Adobe。

   * 需要，以便AdobeCDN可驗證請求來源並傳遞 `X-Forwarded-*` 標頭到AEM應用程式。 例如，`X-Forwarded-For` 用於判斷使用者端IP。 因此，信任的呼叫者（即客戶管理的CDN）有責任確保 `X-Forwarded-*` 標題（請參閱下方的附註）。
   * 或者，您也可以在下列情況下封鎖對AdobeCDN入口的存取： `X-AEM-Edge-Key` 不存在。 如果您需要直接存取AdobeCDN的入口（將被封鎖），請通知Adobe。

請參閱 [CDN廠商設定範例](#sample-configurations) 一節，以瞭解來自主要CDN供應商的設定範例。

在接受即時流量之前，您應該向Adobe的客戶支援驗證端對端流量路由是否正常運作。

取得 `X-AEM-Edge-Key`，您可以測試要求是否正確路由，如下所示。

在Linux®中：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

在Windows中：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

>[!NOTE]
>
>使用您自己的CDN時，您不需要在Cloud Manager中安裝網域和憑證。 AdobeCDN中的路由是使用預設網域來完成 `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` 應在請求中傳送的內容 `Host` 標頭。 覆寫請求 `Host` 具有自訂網域名稱的標頭可能會導致AdobeCDN錯誤地路由請求。


>[!NOTE]
>
>管理自己CDN的客戶應確保傳送至AEM CDN的標頭的完整性。 例如，建議客戶全部清除 `X-Forwarded-*` 標頭並將其設定為已知和控制值。 例如， `X-Forwarded-For` 應包含使用者端的IP位址，而 `X-Forwarded-Host` 應包含網站的主機。

>[!NOTE]
>
>沙箱計畫環境不支援客戶提供的CDN。

只有在發生快取遺失時，才需要客戶CDN和AEM CDN之間的額外躍點。 使用本文所述的快取最佳化策略，新增客戶CDN應該只會帶來可忽略的延遲。

發佈層級支援此客戶CDN設定，但製作層級前不支援。

### CDN廠商設定範例 {#sample-configurations}

以下提供幾個來自數家頂尖CDN廠商的設定範例。

**Akamai**

![Akamai1](assets/akamai1.png "Akamai")
![Akamai2](assets/akamai2.png "Akamai")

**Amazon CloudFront**

![CloudFront1](assets/cloudfront1.png "Amazon CloudFront")
![CloudFront2](assets/cloudfront2.png "Amazon CloudFront")

**Cloudflare**

![Cloudflare1](assets/cloudflare1.png "Cloudflare")
![Cloudflare2](assets/cloudflare2.png "Cloudflare")

## 地理位置標題 {#geo-headers}

AEM管理的CDN會使用以下專案將標題新增至每個請求：

* 國家/地區代碼： `x-aem-client-country`
* 大陸代碼： `x-aem-client-continent`

>[!NOTE]
>
>如果有客戶管理的CDN，這些標題會反映客戶CDN Proxy伺服器的位置，而非實際使用者端。 因此，對於客戶管理的CDN，地理位置標題應由客戶CDN管理。

國家/地區代碼的值為描述的Alpha-2代碼 [此處](https://en.wikipedia.org/wiki/ISO_3166-1).

大陸代碼的值為：

* AF非洲
* 南極洲
* 亞洲
* 歐盟歐洲
* NA北美洲
* OC大洋洲
* 南美洲南部

此資訊可能適合用於使用案例，例如根據請求來源（國家/地區）重新導向至不同的URL。 使用Vary標頭可依地理資訊快取回應。 例如，重新導向至特定國家/地區的登陸頁面應一律包含 `Vary: x-aem-client-country`. 如有需要，您可以使用 `Cache-Control: private` 以防止快取。 另請參閱 [快取](/help/implementing/dispatcher/caching.md#html-text).
