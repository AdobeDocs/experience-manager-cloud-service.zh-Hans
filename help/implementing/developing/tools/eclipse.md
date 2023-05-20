---
title: 适用于 Eclipse 的 AEM 开发人员工具
description: 适用于 Eclipse 的 AEM 开发人员工具
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 3%

---

# 适用于 Eclipse 的 AEM 开发人员工具{#aem-developer-tools-for-eclipse}

![適用於Eclipse標誌的Experience Manager開發人員工具](assets/eclipse-logo.png)

## 概述 {#overview}

_Experience ManagerEclipse開發者工具_ 是Eclipse外掛程式，根據 [Apache Sling的Eclipse外掛程式](https://sling.apache.org/documentation/development/ide-tooling.html) 以Apache授權2發行。

它提供數種讓AEM開發更輕鬆的功能：

* 透過Eclipse伺服器聯結器與AEM執行個體緊密整合
* 內容和OSGi套裝的同步
* 使用程式碼熱抽換功能提供偵錯支援
* 透過特定專案建立精靈簡單BootstrapAEM專案
* 輕鬆編輯JCR屬性

## 要求 {#requirements}

使用AEM開發人員工具之前，您需要：

* 下載並安裝 [適用於企業Java™開發人員的Eclipse IDE](https://www.eclipse.org/downloads/packages/).
* 設定eclipse安裝，透過編輯您的檔案，確保您至少有1 GB的棧積記憶體 `eclipse.ini` 組態檔，如 [Eclipse常見問題集](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>在macOS上，您需要按一下右鍵 **Eclipse.app** 然後選取 **顯示封裝內容** 以尋找 `eclipse.ini`**.**

## 如何安裝適用於Eclipse的AEM開發人員工具 {#how-to-install-the-aem-developer-tools-for-eclipse}

當您完成 [需求](#requirements) 如上所示，您可以安裝外掛程式：

1. 開啟 [AEM開發人員工具網站](https://eclipse.adobe.com/com.adobe.granite.ide.p2update-1.3.0.zip). <!-- RB: OLD URL was (https://eclipse.adobe.com/aem/dev-tools/) This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. 複製 **安裝連結**.

   您也可以下載封存，而不使用安裝連結。 此方法允許離線安裝，但您不會以這種方式收到未命中的自動更新通知。

1. 在Eclipse中，開啟 **說明** 功能表。
1. 按一下 **安裝新軟體**.
1. 按一下 **新增……**.
1. 在 **名稱** 欄位，輸入 `AEM Developer Tools`.
1. 在 **位置** 欄位中，複製安裝URL。
1. 按一下 **新增**.
1. 檢查兩者 **AEM** 和 **Sling** 外掛程式。
1. 单击&#x200B;**下一步**。
1. 在 **安裝詳細資料** 視窗，按一下 **下一個** 再來一次。
1. 接受授權合約，然後按一下 **完成**.
1. 按一下 **RestartNow** 以重新啟動Eclipse。

## AEM觀點 {#the-aem-perspective}

在Eclipse中，「透視」會決定視窗中可用的動作和檢視，並可與Eclipse中的資源進行以任務為導向的互動。 如需「透視」的詳細資訊，請參閱 [Eclipse檔案。](https://help.eclipse.org/latest/index.jsp)

_Eclipse的Experience Manager開發工具_ 提供AEM Perspective ，讓您能夠完全控制AEM專案和執行個體。 若要開啟「AEM透視」，請執行下列動作：

1. 從Eclipse功能表列中，選取 **視窗** -> **透視** -> **開啟透視** -> **其他**.
1. 選取 **AEM** 在對話方塊中並按一下 **開啟**.

![Eclipse中的AEM觀點](assets/eclipse-aem-perspective.png)

## 多模組專案範例 {#sample-multi-module-project}

此 _Experience ManagerEclipse開發者工具_ 隨附多模組專案範例，可幫助您快速熟悉Eclipse中的專案設定。 此外，它還是幾項AEM功能的最佳實務指南。 [進一步瞭解專案原型](https://github.com/adobe/aem-project-archetype).

請依照下列步驟建立範例專案：

1. 在 **檔案** > **新增** > **專案** 功能表，瀏覽至 **AEM** 區段並選取 **AEM範例多模組專案**.

   ![AEM範例多模組專案](assets/aem-sample-project.png)

1. 单击&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步驟可能需要一些時間，因為m2eclipse需要掃描原型目錄。

1. 選擇 `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` 在功能表中，然後按一下 **下一個**.

   ![選取原型版本](assets/select-archetype.png)

1. 為範例專案提供下列欄位：

   * **名称**
   * **群組ID**
   * **成品ID**
   * **appId**  — 您可能需要展開 **進階** 設定此值的選項。
   * **appTitle**  — 您可能需要展開 **進階** 設定此值的選項。
   * **封裝**  — 您可能需要展開 **進階** 設定此值的選項。

   ![定義原型屬性](assets/archetype-properties.png)

1. 单击&#x200B;**下一步**。

1. 接著，您可以設定Eclipse連線的AEM伺服器。

   若要使用偵錯工具功能，您必須以偵錯模式啟動AEM — 這可以透過在命令列新增下列內容來實現：

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![連線到AEM伺服器](assets/connect-server.png)

1. 按一下 **完成**. 專案結構隨即建立。

   >[!NOTE]
   >
   >在新安裝中（更具體地說，當從未下載maven相依性時），您可能會收到建立有錯誤的專案。 在此情況下，請遵循中所述的程式 [解析無效的專案定義](#resolving-invalid-project-definition).

## 如何匯入現有專案 {#how-to-import-existing-projects}

您可以使用 **新增專案** 建立正確結構的功能：

1. 依照指示建立 [多模組專案範例](#sample-multi-module-project) 而且您已為您建立下列專案，可健康地分離疑慮：

   * `PROJECT.ui.apps` 的 `/apps` 和 `/etc` 內容
   * `PROJECT.ui.content` 的 `/content` 已製作
   * `PROJECT.core` 對於Java™套裝(當您想要新增Java™程式碼時，這些套裝會變得有趣起來)
   * `PROJECT.it.launcher` 和 `PROJECT.it.tests` 用於整合測試

1. 取代的內容 `PROJECT.ui.apps` 專案與 `apps` 和 `etc` 封裝資料夾：

   1. 在「專案總管」面板中，展開 `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. 以右鍵按一下 `apps` 資料夾並選擇 **顯示位置** > **System Explorer**.
   1. 刪除 `apps` 和 `etc` 您現在應該看到的資料夾，並放置在這裡 `apps` 和 `etc` 內容封裝的資料夾。
   1. 在Eclipse中，以滑鼠右鍵按一下 `PROJECT.ui.apps` 專案並選擇 **重新整理**.

1. 然後對 `PROJECT.ui.content` 並將其內容資料夾取代為您的其中一個套件：

   1. 在「專案總管」面板中，展開 `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. 以滑鼠右鍵按一下較深入的內容資料夾，然後選擇 **顯示位置** -> **System Explorer**.
   1. 刪除您現在應該看到的內容資料夾，並在此處放置內容包的內容資料夾。
   1. 在Eclipse中，以滑鼠右鍵按一下 `PROJECT.ui.content` 專案並選擇 **重新整理**.

1. 現在您必須更新 `filter.xml` 這兩個專案的檔案，以對應至內容封裝的內容。 為此，請開啟 `META-INF/vault/filter.xml` 在個別文字/程式碼編輯器中的內容套件檔案。

   * 以下範例說明 `filter.xml` 檔案可以查詢：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. 至於分割為兩個專案的套件內容，您也必須將這些篩選規則分割為兩個並相應地更新 `filter.xml` 兩個專案的檔案。

   1. 在Eclipse中，開啟 `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. 取代 `<workspaceFilter>` 元素的開頭為您的套件規則 `/apps` 和 `/etc`
      * 例如：

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/apps/foo"/>
            <filter root="/apps/foundation/components/bar"/>
            <filter root="/etc/designs/foo"/>
         </workspaceFilter>
         ```
   1. 然後開啟 `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
   1. 將規則取代為您的套件中以開頭的規則 `/content`.
      * 例如：

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. 請務必儲存所有變更。 您現在可以將新內容同步至您的AEM執行個體。

1. 在「伺服器」面板中，確定您的連線已啟動，若未啟動，則確定已啟動。
1. 按一下 **清除並發佈** 圖示。

完成後，您應該在執行個體上執行套件，並在儲存時，任何變更都會自動同步到執行個體。

如果您想從專案重新建置套件，請用滑鼠右鍵按一下 `PROJECT.ui.apps` 或 `PROJECT.ui.content` 並選擇 **執行身分** -> **Maven安裝**.

您現在已建立目標資料夾，並在裡面裝入您的套件(例如，稱為 `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`)。

## 疑难解答 {#troubleshooting}

### 解析無效的專案定義 {#resolving-invalid-project-definition}

若要解析無效的相依性和專案定義，請依照下列步驟進行：

1. 選取所有已建立的專案。
1. 按一下滑鼠右鍵。
1. 在快顯選單中，選取 **Maven** -> **更新專案**.
1. Check **強制更新快照/版本**.
1. 单击&#x200B;**确定**。

Eclipse會下載必要的相依性。 這可能需要一些時間。

## 更多信息 {#more-information}

適用於Eclipse網站的官方Apache Sling IDE工具提供您有用的資訊：

* 此 [**適用於Eclipse的Apache Sling IDE工具** 使用手冊](https://sling.apache.org/documentation/development/ide-tooling.html)，本檔案會逐步引導您瞭解AEM開發工具支援的整體概念、伺服器整合和部署功能。
* 此 [疑難排解章節](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* 此 [已知問題清單](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

下列官方 [Eclipse](https://www.eclipse.org/) 說明檔案有助於設定您的環境：

* [Eclipse快速入門](https://www.eclipse.org/getting-started/)
* [Eclipse Luna說明系統](https://help.eclipse.org/latest/index.jsp)
* [Maven整合(m2eclipse)](https://www.eclipse.org/m2e/)
