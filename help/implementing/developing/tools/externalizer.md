---
title: 將URL外部化
description: Externalizer是一種OSGi服務，可讓您以程式設計方式將資源路徑轉換為外部和絕對URL。
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# 將URL外部化 {#externalizing-urls}

在AEM中， **Externalizer** 是一項OSGi服務，可讓您以程式設計方式轉換資源路徑(例如 `/path/to/my/page`)轉換成外部和絕對URL (例如， `https://www.mycompany.com/path/to/my/page`)，將路徑加上預先設定的DNS當作前置詞。

由於AEMas a Cloud Service執行個體無法知道其外部可見的URL，而且有時必須在請求範圍外建立連結，因此此服務會提供一個中央位置，讓您設定這些外部URL並建置它們。

本文說明如何設定Externalizer服務及其使用方式。 如需此服務的技術詳細資訊，請參閱 [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## 外部化程式的預設行為以及如何覆寫 {#default-behavior}

開箱即用的Externalizer服務會將一些網域識別碼對應到與已針對環境產生的AEM服務URL相符的絕對URL首碼，例如 `author https://author-p12345-e6789.adobeaemcloud.com` 和 `publish https://publish-p12345-e6789.adobeaemcloud.com`. 這些預設網域的基礎URL都是從Cloud Manager定義的環境變數中讀取的。

若需參考，此專案的預設OSGi設定 `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` 有效：

```json
{
   "externalizer.domains": [
      "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
      "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
      "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]",
      "preview $[env:AEM_EXTERNALIZER_PREVIEW;default=http://localhost:4503]"
   ]
}
```

>[!CAUTION]
>
>預設 `local`， `author`， `preview`、和 `publish` OSGi設定中的Externalizer網域對應必須保留為原始的 `$[env:...]` 值列於上面。
>
>部署自訂 `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` 檔案到AEMas a Cloud Service時，若省略這些現成可用的網域對應，可能會導致無法預測的應用程式行為。

覆寫 `preview` 和 `publish` 值，請依照文章所述使用Cloud Manager環境變數 [為AEMas a Cloud Service設定OSGi](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) 並設定預先定義的 `AEM_CDN_DOMAIN_PUBLISH` 和 `AEM_CDN_DOMAIN_PREVIEW` 變數。

## 設定Externalizer服務 {#configuring-the-externalizer-service}

Externalizer服務可讓您集中定義網域，以程式設計方式為資源路徑加上前置詞。 Externalizer服務只應用於具有單一網域的應用程式。

>[!NOTE]
>
>如同套用任何 [AEMas a Cloud Service的OSGi設定、](/help/implementing/deploying/overview.md#osgi-configuration) 下列步驟應在本機開發人員執行個體上執行，然後提交至您的專案程式碼以供部署。

若要定義Externalizer服務的網域對應：

1. 透過以下方式瀏覽至Configuration Manager：

   `https://<host>:<port>/system/console/configMgr`

1. 按一下 **Day CQ連結外部化器** 以開啟組態對話方塊。

   ![外部化程式OSGi設定](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >設定的直接連結為 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. 定義 **網域** 對應。 對應包含唯一名稱，可用於程式碼中參照網域、空格和網域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **`scheme`** 通常為http或https，但可以是其他通訊協定。

      * 建議使用https來強制執行https連結。
      * 若使用者端代碼在要求外部化URL時未覆寫配置，則會使用它。
   * **`server`** 是主機名稱（網域名稱或ip位址）。
   * **`port`** （選用）是連線埠號碼。
   * **`contextpath`** （選用）只有當AEM安裝為Webapp且位於不同的內容路徑下時，才會設定。

   例如：`production https://my.production.instance`

   下列對應名稱是預先定義的，必須一律設定為AEM依賴這些名稱：

   * `local`  — 本機執行個體
   * `author`  — 編寫系統DNS
   * `publish`  — 面向公眾的網站DNS

   >[!NOTE]
   >
   >自訂設定可讓您新增類別，例如 `production`， `staging` 甚至外部非AEM系統，例如 `my-internal-webservice`. 避免在專案的程式碼基底中跨不同位置對這類URL進行硬式編碼很有用。

1. 按一下 **儲存** 以儲存變更。

### 使用Externalizer服務 {#using-the-externalizer-service}

本節顯示幾個如何使用Externalizer服務的範例。

>[!NOTE]
>
>不應在HTML內容中建立任何絕對連結。 因此，不應在此情況下使用此公用程式。

* **若要使用「發佈」網域外部化路徑：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假設網域對應：

   * `publish https://www.website.com`

   * `myExternalizedUrl` 最後會得到值：

   * `https://www.website.com/contextpath/my/page.html`

* **若要使用「作者」網域外部化路徑：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假設網域對應：

   * `author https://author.website.com`

   * `myExternalizedUrl` 最後會得到值：

   * `https://author.website.com/contextpath/my/page.html`

* **若要使用「本機」網域外部化路徑：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假設網域對應：

   * `local https://publish-3.internal`

   * `myExternalizedUrl` 最後會得到值：

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>如需更多範例，請參閱 [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
