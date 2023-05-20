---
title: 存储库浏览器
seo-title: Repository Browser
description: 存放庫瀏覽器為作者、發佈和預覽層級上的所有環境提供存放庫的唯讀檢視。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: 43429562ea4292f38d3459e03185270ec950a58a
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 2%

---

# 存储库浏览器 {#repository-browser}

>[!NOTE]
>
>存放庫瀏覽器適用於AEM 6582版及更新版本。

>[!INFO]
>
>您也可以觀看 [此剪輯](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) 有關如何使用存放庫瀏覽器對AEMas a Cloud Service進行偵錯的快速影片簡介。

## 简介 {#introduction}

存放庫瀏覽器是開發人員工具，可為作者、發佈和預覽層級的所有環境提供存放庫的唯讀檢視。 其設計旨在方便檢視內容結構，以便更輕鬆地檢視內容或為內容除錯。

可從開發人員控制檯存取，它可用來瀏覽所選環境的作者或發佈執行個體的存放庫。

### 存取必要條件 {#access-prerequisites}

若要存取開發人員控制檯或存放庫瀏覽器，以下條件必須滿足

若要存取開發人員主控台：

* 對於生產計畫，使用者必須具有 **Cloud Manager — 開發人員角色** 在Admin Console中
* 對於沙箱計畫，它可供任何具有產品設定檔的使用者使用，以讓他們存取AEMas a Cloud Service。

若要存取「存放庫瀏覽器」：

* 使用者必須具備 **Cloud Manager — 開發人員** 在Admin Console中檢視「作者」和「發佈」例項的角色。
* 此外，對於作者，具有AEM使用者產品設定檔的使用者能夠以最低的讀取存取權檢視存放庫瀏覽器；瀏覽存放庫時會考量使用者的許可權。 具有AEM管理員產品設定檔的使用者可以完整讀取許可權檢視存放庫瀏覽器。

如需設定使用者許可權的詳細資訊，請參閱 [Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### 啟動存放庫瀏覽器 {#launching-the-repository-browser}

您可以依照下列步驟啟動存放庫瀏覽器。

1. 在Cloud Manager中，按一下所選環境旁的三個點，然後選取 **開發人員主控台**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 接下來，按一下 **存放庫瀏覽器** 標籤
1. 按一下「 」，選擇與作者、發佈或預覽相對應的任何pod **Pod** 下拉式清單。

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 按一下「 」，啟動存放庫瀏覽器 **開啟存放庫瀏覽器** 進一步向下連結。 這會啟動與所選層級之代表性例項(pod)對應的瀏覽器。 這會啟動與所選層級之代表性例項(pod)對應的瀏覽器。 請注意，您無法控制已啟動之該階層的特定Pod。

## 功能 {#features}

### 瀏覽階層 {#navigate-the-hierarchy}

您可以使用左側導覽窗格來導覽內容階層。 按一下每個資料夾或節點會顯示其子系。 資料夾結構會反映Sling資源樹狀結構，這是JCR節點樹狀結構的超級集。

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

或者，您也可以直接導覽至路徑，方法是在 **路徑** 欄位，如下所示。 這也會擴展其在左側內容階層檢視中的位置。

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

每當您按一下左側的資料夾時，「路徑」欄位就會自動填入其位置。 這對於複製和貼上值以供稍後使用非常有用。

此外，當您按一下資料夾時，URL會動態修改以包含該資料夾的路徑。 這允許使用可書籤的URL。

對於發佈，依預設，存放庫瀏覽器將只會顯示公開內容，因此某些資料夾 `/conf` 或 `/home` 將不可見。

為了讓這些位置可見，您需要遵循以下程式。

1. 按一下所選環境旁的三個點，然後選取 **管理存取權**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. 尋找您的發佈執行個體，然後按一下它

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. 為發佈管理員建立新的產品設定檔。 在以下範例中，它稱為 **開發 — AEM管理員發佈**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. 將適當的使用者（對應於應能瀏覽發佈存放庫瀏覽器並擁有完整存取權的使用者）新增至新產品設定檔

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 等候幾分鐘，然後開啟 **AEM作者** 主控台
1. 將對應到新產品設定檔的群組新增為管理員群組的成員。 若要這麼做，請按一下 **工具 — 安全性 — 作者群組**，然後按一下 **管理員** 群組。 然後，新增群組，如下所示

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. 啟動 **管理員** 和新的 **開發 — AEM管理員發佈** 群組，以便在發佈時可用

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. 根據良好的安全性實務，請移除新的 **開發 — AEM管理員發佈** 管理員群組中的群組 **作者** 因此新群組會隔離以發佈

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. 存取發佈執行個體的存放庫瀏覽器時，所有資料夾皆可見，包括 `/home` 和 `/conf`.

### 檢視JCR屬性 {#view-jcr-properties}

按一下節點，會在導覽瀏覽器的右側窗格中顯示其JCR屬性。 以下範例適用於 `experience-fragments` 節點。

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### 查看内容 {#view-content}

您可以按一下導覽窗格中的資源，使用存放庫瀏覽器來檢視內容。 這會在瀏覽器右側的標籤下方，以個別資源命名的標籤開啟預覽。

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

預覽目前可用於下列清單中的影像型別：

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* x-icon
* tiff

以及下列文字型MIME型別：

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### 下載內容 {#download-content}

您也可以使用存放庫瀏覽器來下載內容。 在以下範例中，您可以按下 **下載** 下載連結 `jcr:data` 與所選節點相關聯。 導覽至包含屬性定義的節點，此功能適用於所有二進位屬性。

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
