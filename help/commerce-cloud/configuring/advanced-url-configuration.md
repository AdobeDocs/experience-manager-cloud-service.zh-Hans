---
title: 進階URL設定
description: 瞭解如何自訂產品和類別頁面的URL。 這可讓實作將搜尋引擎的URL最佳化並促進探索。
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: 9c25d9991b41a5a714df3f07e84946162e5495c0
workflow-type: tm+mt
source-wordcount: '2211'
ht-degree: 4%

---

# 進階URL設定 {#url}

>[!NOTE]
>
> 搜索引擎优化 (SEO) 已成为许多营销人员关注的重点。因此，需要解决众多 Adobe Experience Manager (AEM) as a Cloud Service 项目中的 SEO 问题。請閱讀 [SEO和URL管理最佳作法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) 以取得其他資訊。

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) 提供進階設定，以便自訂產品和類別頁面的URL。 許多實施會針對搜尋引擎最佳化(SEO)目的自訂這些URL。 以下影片詳細說明如何設定 `UrlProvider` 的服務與功能 [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自訂產品和類別頁面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

若要設定 `UrlProvider` 根據SEO需求和需求提供的服務，專案必須提供 _CIF URL提供者設定_.

>[!NOTE]
>
> 自AEM CIF核心元件2.0.0版以來，「URL提供者」設定僅提供預先定義的URL格式，而非1.x版已知的自由文字可設定格式。 此外，使用選取器在URL中傳遞資料的做法已更換為尾碼。

### 產品頁面URL格式 {#product}

這會設定產品頁面的URL，並支援下列選項：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（默认）
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

若為 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}` 將取代為 `/content/venia/us/en/products/product-page`
* `{{sku}}` 將由產品的sku取代，例如 `VP09`
* `{{url_key}}` 將由產品的 `url_key` 屬性，例如， `lenora-crochet-shorts`
* `{{url_path}}` 將由產品的 `url_path`例如， `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 將由目前選取的變體取代，例如 `VP09-KH-S`

由於 `url_path` 已過時，預先定義的產品URL格式會使用產品的 `url_rewrites` 並挑選路徑分段最多的路徑作為替代路徑，如果 `url_path` 無法使用。

在上述範例資料中，使用預設URL格式的產品變體URL看起來會像 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### 類別頁面URL格式 {#product-list}

這會設定類別或產品清單頁面的URL，並支援下列選項：

* `{{page}}.html/{{url_path}}.html`（默认）
* `{{page}}.html/{{url_key}}.html`

若為 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}` 將取代為 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 將由類別的 `url_key` 屬性
* `{{url_path}}` 將由類別的 `url_path`

在上述範例資料中，使用預設URL格式化的類別頁面URL看起來會像 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> 此 `url_path` 是以下專案的串連： `url_keys` 產品或類別的祖先以及產品或類別的 `url_key` 分隔方式 `/` slash。 每個 `url_key` 在指定的存放區中被視為唯一。

### 存放區特定設定 {#store-specific-urlformats}

由設定的系統範圍類別和產品頁面URL格式 _CIF URL提供者設定_ 可針對每個商店進行變更。

在CIF設定中，編輯者可以選取替代產品或類別頁面URL格式。 如果未選取任何專案，則實作將會退回系統範圍設定。

變更已上線網站的URL格式可能會對您網站的自然流量產生負面影響。 請參閱 [最佳實務](#best-practices) 請事先仔細規劃URL格式的變更。

![CIF設定中的URL格式](assets/store-specific-url-formats.png)

>[!NOTE]
>
> 存放區特定的URL格式設定需要 [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 以及最新版本的Adobe Experience Manager Content and Commerce附加元件。

## 類別感知產品頁面URL {#context-aware-pdps}

由於可在產品URL中編碼類別資訊，因此屬於多個類別的產品也可能以多個產品URL來定址。

預設的URL格式將使用以下配置選取一個可能的替代方案：

* 如果 `url_path` 由電子商務後端使用它來定義（已棄用）
* 從 `url_rewrites` 使用結尾為產品的 `url_key` 作為替代方案
* 這些替代方案會使用具有最多路徑區段的替代方案
* 如果有多個專案，請依照電子商務後端所指定的順序進行第一個專案

此配置將選取 `url_path` 具有最多祖項，根據子類別比其父類別更具體的假設。 如此選取 `url_path` 已考慮 _規範_ 和將一律用作產品頁面或產品網站地圖中的規範連結。

不過，當購物者從類別頁面導覽至產品頁面，或從某個產品頁面導覽至相同類別中的另一個相關產品頁面時，有必要保留目前的類別內容。 在此案例中 `url_path` 選取範圍應偏好位於目前類別上下文中的替代專案，而非選取範圍 _規範_ 選取範圍如上所述。

此功能必須在 _CIF URL提供者設定_. 如果啟用，選擇範圍分數會高於選擇，當

* 它們符合指定類別的部分 `url_path` 從開頭（模糊首碼比對）
* 或符合指定類別的 `url_key` 任何位置（完全部分比對）

例如，假設回應為 [產品查詢](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) 下方的。 由於使用者在「New Products / New in Summer 2022」類別頁面上，且商店使用預設類別頁面URL格式，替代「new-products/new-in-summer-2022/gold-cirque-earrings.html」將會從頭匹配上下文路徑區段的2個：「new-products」和「new-in-summer-2022」。 如果商店使用的類別頁面URL格式僅包含類別 `url_key`，仍會選取相同的替代方案，因為它符合內容的 `url_key` 任何地方。 在這兩種情況下，都會為「new-products/new-in-summer-2022/gold-cirque-earrings.html」建立產品頁面URL `url_path`.

```
{
  "data": {
    "products": {
      "items": [
        {
          "sku": "VA18-GO-NA",
          "url_key": "gold-cirque-earrings",
          "url_rewrites": [
            {
              "url": "gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/venia-jewelry/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/new-in-summer-2022/gold-cirque-earrings.html"
            }
          ]
        }
      ]
    }
  }
}
```

>[!NOTE]
>
> 類別感知產品URL需要 [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 或更新版本。

## 特定類別和產品頁面 {#specific-pages}

可以建立 [多個類別和產品頁面](../authoring/multi-template-usage.md) 僅用於目錄的特定類別或產品子集。

### 選取條件 {#specific-pages-selection}

根據類別的，直接選擇特定的類別頁面 `url_path` 或 `url_key`. 只有包含完整類別的URL格式才支援符合子類別 `url_path`. 否則，只會將 `url_key` 是可能的。

特定產品頁面是由產品的SKU或類別所選取。 後者需要在產品URL中編碼某些類別資訊。 這僅適用於部分預設URL格式。 請參考下表，瞭解URL格式支援依SKU或類別特定頁面選擇的比較。


| URL格式 | 按sku | 依類別 |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | 否 | 否 |
| `{{page}}.html/{{category}}/{{url_key}}.html` | 否 | 僅完全相符 |
| `{{page}}.html/{{url_path}}.html` | 否 | 是 |
| `{{page}}.html/{{sku}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | 是 | 僅完全相符 |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | 是 | 是 |

{style="table-layout:auto"}

>[!NOTE]
>
> 依類別選取特定產品頁面需要 [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 或更新版本。

### 深度链接 {#specific-pages-deep-linking}

此 `UrlProvider` 已預先設定，可在作者層級例項上產生特定類別和產品頁面的深層連結。 這對編輯者很有用，他們可使用預覽模式瀏覽網站、導覽至特定產品或類別頁面，然後切換回編輯模式以編輯頁面。

另一方面，在發佈層級執行個體上，目錄頁面URL應保持穩定，以免失去搜尋引擎排名等優勢。 因此，根據預設，發佈層執行個體不會轉譯特定目錄頁面的深層連結。 若要變更此行為， _CIF URL提供者特定頁面策略_ 可設定為一律產生特定頁面URL。

### 多個目錄頁面 {#multiple-product-pages}

當編輯器想要完全控制網站的頂層導覽時，可能不需要使用單一目錄頁面來呈現目錄的頂層類別。 編輯器可以建立多個目錄頁面，每個類別各有一個要包含在頂層導覽中的目錄。

對於該使用案例，每個目錄頁面都可具有產品和類別頁面的參考，這些頁面特定於為目錄頁面配置的類別。 此 `UrlProvider` 會使用這些連結，為設定類別中的頁面和類別建立連結。 不過，基於效能考量，只會考量網站導覽根目錄/登陸頁面的直接目錄頁面子項。

建議將目錄頁面的產品和類別頁面子代至該目錄頁面，否則導覽或階層連結等元件可能無法正常運作。

>[!NOTE]
>
> 需要完整支援多個目錄頁面 [CIF Core Components 2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) 或更新版本。

## 自訂 {#customization}

### 自訂URL格式 {#custom-url-format}

若要提供自訂URL格式，專案可實作 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服務介面，並將實作註冊為OSGI服務。 這些實施（如果可用）將取代已設定的預先定義格式。 如果註冊了多個實作，則服務排名較高的實作會取代服務排名較低的實作。

自訂URL格式實作必須實作一組方法，以便從指定引數建立URL，並剖析URL以分別傳回相同的引數。

### 與Sling對應結合 {#sling-mapping}

除了 `UrlProvider`，也可以設定 [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 以便重寫及處理URL。 AEM原型專案也提供 [設定範例](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 為連線埠4503 （發佈）和80 （排程程式）設定一些Sling對應。

### 與AEM Dispatcher結合 {#dispatcher}

透過以下方式使用AEM Dispatcher HTTP伺服器也可實現URL重寫： `mod_rewrite` 模組。 此 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 提供已包含基本設定的AEM Dispatcher參考設定 [重寫規則](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 所產生的大小。

## 最佳实践 {#best-practices}

### 選擇最佳的URL格式 {#choose-url-format}

如在選取其中一個可用的預設格式，或甚至實作自訂格式之前所述，這在很大程度上取決於商店的需求和要求。 下列建議可協助您做出有根據的決定。

_**使用包含sku的產品頁面URL格式。**_

CIF核心元件會在所有元件中使用sku作為主要識別碼。 如果產品頁面URL格式不包含SKU，則需要使用GraphQL查詢來解析。 這可能會影響第一個位元組的時間。 此外，購物者可能希望透過使用搜尋引擎的SKU尋找產品。

_**使用包含類別內容的產品頁面URL格式。**_

只有在使用產品URL格式（會編碼類別內容，例如類別）時，CIF URL提供者的部分功能才可使用 `url_key` 或類別 `url_path`. 即使新商店可能不需要這些功能，一開始使用這些URL格式之一有助於減少未來的移轉工作。

_**URL長度和編碼資訊之間的平衡。**_

根據目錄大小，特別是類別樹狀結構的大小和深度，為完整目錄編碼可能不合邏輯 `url_path` 類別匯入URL中。 在這種情況下，可以只包含類別的 `url_key` 而非。 這將支援使用類別時可用的大部分功能 `url_path`.

此外，使用 [Sling對應](#sling-mapping) 以結合sku與產品 `url_key`. 在大多數電子商務系統中，SKU會遵循特定格式，並將SKU與 `url_key` 應該可以輕鬆處理傳入的要求。 考慮到這一點，應該可以將產品頁面URL重寫至 `/p/{{category}}/{{sku}}-{{url_key}}.html`，以及類別URL至 `/c/{{url_key}}.html` 兩者皆有。 此 `/p` 和 `/c` 若要將產品和類別頁面與其他內容頁面區分開來，仍需使用首碼。

### 移轉至新URL格式 {#migrate-url-formats}

許多預設URL格式以某種方式彼此相容，表示某一種格式的URL可能會被另一種格式剖析。 這有助於在URL格式之間移轉。

另一方面，搜尋引擎將需要一些時間，以新的URL格式重新編目所有目錄頁面。 為了支援此程式並改善一般使用者體驗，建議提供將使用者從舊URL轉送到新URL的重新導向。

其中一種方式可能是將預備環境連線到生產電子商務後端，並將其設定為使用新的URL格式。 之後取得 [CIF產品網站地圖產生器產生的產品網站地圖](../../overview/seo-and-url-management.md) 用於預備和生產環境，並使用它們來建立 [Apache httpd重寫對應](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). 此重寫對應可以連同新URL格式的轉出一起部署到Dispatcher。

## 示例 {#example}

此 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia) project包含示範產品和類別頁面使用自訂URL的設定範例。 這可讓每個專案根據其SEO需求，為產品和類別頁面設定個別URL模式。 CIF組合 `UrlProvider` 和Sling對應（如上所述）則會使用。

>[!NOTE]
>
>此設定必須使用專案使用的外部網域進行調整。 Sling對應是根據主機名稱和網域來運作。 因此，此設定預設為停用，必須在部署之前啟用。 若要這麼做，請重新命名Sling對應 `hostname.adobeaemcloud.com` 資料夾位於 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根據使用的網域名稱，並透過新增以啟用此設定 `resource.resolver.map.location="/etc/map.publish"` 至 `JcrResourceResolver` 專案的設定。

## 其他资源 {#additional}

* [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
* [AEM資源對應](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
