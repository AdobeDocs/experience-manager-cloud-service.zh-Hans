---
title: 将对新区域设置的支持添加到自适应表单
seo-title: Learn to add support for new locales to your adaptive forms
description: AEM Forms可讓您新增語言環境，以將最適化表單當地語系化。 英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西文(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)語言環境。
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# 支援最適化Forms本地化的新地區設定 {#supporting-new-locales-for-adaptive-forms-localization}

AEM Forms提供英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西文(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)地區設定的立即可用支援。 您也可以新增對更多地區設定的支援，例如印地文(hi_IN)。

## 瞭解地區設定字典 {#about-locale-dictionaries}

最適化表單本地化依賴兩種型別的地區設定字典：

* **表單特定字典** 包含最適化表單中使用的字串。 例如，標籤、欄位名稱、錯誤訊息、說明說明。 它被管理為每個地區設定的一組XLIFF檔案，您可以在以下位置存取它： `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **全域字典** AEM使用者端資料庫中有兩個全域字典，以JSON物件形式管理。 這些字典包含預設錯誤訊息、月份名稱、貨幣符號、日期和時間模式等。 這些字典位於 `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. 這些位置包含每個地區設定的個別資料夾。 由於全域字典不會經常更新，因此針對每個地區設定保留個別的JavaScript檔案，可讓瀏覽器在存取相同伺服器上的不同最適化表單時，快取檔案並降低網路頻寬使用量。

## 新增新地區設定的支援 {#add-support-for-new-locales}

執行以下步驟來新增新地區設定的支援：

1. [新增不支援地區設定的本地化支援](#add-localization-support-for-non-supported-locales)
1. [在最適化Forms中使用新增的地區設定](#use-added-locale-in-af)

### 新增不支援地區設定的本地化支援 {#add-localization-support-for-non-supported-locales}

AEM FormsForms目前支援英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西文(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)本地化內容。

若要在Adaptive Forms執行階段新增對新地區設定的支援：

1. [複製您的存放庫](#clone-the-repository)
1. [新增地區設定至GuideLocalizationService服務](#add-a-locale-to-the-guide-localization-service)
1. [新增地區名稱特定資料夾](#add-locale-name-specific-folder)
1. [為字典新增地區設定支援](#add-locale-support-for-the-dictionary)
1. [認可存放庫中的變更並部署管道](#commit-changes-in-repo-deploy-pipeline)

#### 1.複製存放庫 {#clone-the-repository}

1. 從命令列，導覽至您要複製FormsCloud Service存放庫的位置。
1. 執行您指定的指令 [從Cloud Manager擷取。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) 它類似於 `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. 使用Git使用者名稱和密碼來複製存放庫。
1. 在您偏好的編輯器中，開啟複製的FormsCloud Service存放庫資料夾。

#### 2.新增地區設定至「本地化指南」服務 {#add-a-locale-to-the-guide-localization-service}

1. 找到 `Guide Localization Service.cfg.json` 檔案並新增您要新增到支援地區設定的清單中的地區設定。

   >[!NOTE]
   >
   > 建立名為的檔案 `Guide Localization Service.cfg.json` 檔案（如果尚未存在）。

#### 3.新增地區名稱特定的資料夾使用者端資料庫 {#add-locale-name-specific-folder}

1. 在UI.content資料夾中，建立 `etc/clientlibs` 資料夾。
1. 進一步建立名為的資料夾 `locale-name` 在 `etc/clientlibs` 做為xfa和af clientlibs的容器。

##### 3.1為locale-name資料夾中的地區設定新增XFA使用者端資料庫

建立名為的節點 `[locale-name]_xfa` 並輸入為 `cq:ClientLibraryFolder` 在 `etc/clientlibs/locale_name`，含類別 `xfaforms.I18N.<locale>`，並新增下列檔案：

* **I18N.js** 定義 `xfalib.locale.Strings` 的 `<locale>` 如中的定義 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt** 包含下列專案：
   */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2.為地區設定locale-name資料夾新增最適化表單使用者端資料庫

1. 建立名為的節點 `[locale-name]_af` 並輸入為 `cq:ClientLibraryFolder` 在 `etc/clientlibs/locale_name`，類別為 `guides.I18N.<locale>` 和相依性 `xfaforms.3rdparty`， `xfaforms.I18N.<locale>` 和 `guide.common`.
1. 建立名為的資料夾 `javascript` 並新增下列檔案：

   * **i18n.js** 定義 `guidelib.i18n`，有「calendarSymbols」的模式， `datePatterns`， `timePatterns`， `dateTimeSymbols`， `numberPatterns`， `numberSymbols`， `currencySymbols`， `typefaces` 的 `<locale>` 根據XFA規格，詳見 [地區設定規格](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **logmessages.js** 定義 `guidelib.i18n.strings` 和 `guidelib.i18n.LogMessages` 的 `<locale>` 如中的定義 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. 新增 **js.txt** 包含下列專案：

   ```
     i18n.js
     LogMessages.js
   ```

#### 4.為字典新增地區設定支援 {#add-locale-support-for-the-dictionary}

只有在 `<locale>` 您新增的專案不屬於 `en`， `de`， `es`， `fr`， `it`， `pt-br`， `zh-cn`， `zh-tw`， `ja`， `ko-kr`.

1. 建立資料夾 `languages` 在 `etc`，如果尚未出現。

1. 新增多值字串屬性 `languages` 至節點（如果尚未出現）。
1. 新增 `<locale-name>` 預設地區設定值 `de`， `es`， `fr`， `it`， `pt-br`， `zh-cn`， `zh-tw`， `ja`， `ko-kr`，如果尚未出現。

1. 新增 `<locale>` 至的值 `languages` 屬性 `/etc/languages`.
1. 將新建立的資料夾新增至 `filter.xml` 在etc/META-INF/[資料夾階層] 作為：

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

將變更提交至AEM Git存放庫之前，您需要存取 [Git存放庫資訊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

#### 5.認可存放庫中的變更並部署管道 {#commit-changes-in-repo-deploy-pipeline}

在新增地區設定支援後，將變更提交到GIT存放庫。 使用完整棧疊管道部署您的計畫碼。 瞭解 [如何設定管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) 以新增地區設定支援。
管道完成後，新新增的地區設定會顯示在AEM環境中。

### 在最適化Forms中使用新增的地區設定 {#use-added-locale-in-af}

執行以下步驟，使用新增的地區設定來使用及轉譯調適型表單：

1. 登入您的AEM編寫執行個體。
1. 前往 **Forms** >  **Forms和檔案**.
1. 選取最適化表單並按一下 **新增字典** 和 **新增字典至翻譯專案** 精靈隨即出現。
1. 指定 **專案標題** 並選取 **目標語言** 從「 」的下拉式功能表 **新增字典至翻譯專案** 精靈。
1. 按一下 **完成** 並執行已建立的翻譯專案。
1. 選取最適化表單並按一下 **以HTML預覽**.
1. 新增 `&afAcceptLang=<locale-name>` 在最適化表單的URL中。
1. 重新整理頁面，最適化表單會以指定的地區設定呈現。

識別最適化表單的地區設定有兩種方法。 最適化表單在轉譯時，會透過以下方式識別要求的地區設定：

* 正在擷取 `[local]` 最適化表單URL中的選取器。 URL的格式為 `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. 使用 `[local]` 選擇器允許快取最適化表單。

* 正在以列出的順序擷取下列引數：

   * 請求引數 `afAcceptLang`
若要覆寫使用者的瀏覽器地區設定，您可以傳遞 
`afAcceptLang` 要求引數以強制地區設定。 例如，下列URL會強制以加拿大 — 法語地區設定來轉譯表單：
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * 為使用者設定的瀏覽器地區設定，這在使用請求的指定 `Accept-Language` 標頭。

如果要求的地區設定的使用者端程式庫不存在，它會檢查地區設定中存在的語言程式碼的使用者端程式庫。 例如，如果要求的地區設定為 `en_ZA` （南非英文）和的使用者端資料庫 `en_ZA` 不存在，調適型表單會將使用者端程式庫用於 `en` （英文）語言（如果存在）。 不過，如果兩者都不存在，適用性表單會將該字典用於 `en` 地區設定。


地區設定一經識別，「最適化表單」就會挑選特定於表單的字典。 如果找不到所要求地區設定的表單特定字典，則會使用最適化表單編寫語言的字典。

如果沒有地區設定資訊，最適化表單會以表單的原始語言傳送。 原始語言是開發最適化表單時使用的語言。

取得 [範例使用者端資源庫](/help/forms/assets/locale-support-sample.zip) 以新增新地區設定的支援。 您需要以所需的地區設定變更資料夾的內容。

## 支援新本地化的最佳實務 {#best-practices}

* Adobe建議您在建立最適化表單後建立翻譯專案。

* 在現有的最適化表單中新增欄位時：
   * **對於機器翻譯**：重新建立字典並執行翻譯專案。 建立翻譯專案後新增至最適化表單的欄位仍維持未翻譯狀態。
   * **針對人工翻譯**：透過匯出字典 `[server:port]/libs/cq/i18n/gui/translator.html`. 更新新新增欄位的字典並上傳。
