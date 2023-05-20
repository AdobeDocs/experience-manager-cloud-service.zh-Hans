---
title: 在Dynamic Media中使用3D資產
description: 瞭解如何在Dynamic Media中使用3D資產。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: 347da5edf4c8ad2ae72284f4e1a4003493596194
workflow-type: tm+mt
source-wordcount: '2260'
ht-degree: 3%

---

# 在Dynamic Media中使用3D資產 {#working-with-three-d-assets-dm}

Dynamic Media可讓您上傳、管理、檢視及傳遞3D資產，以盡情享受身臨其境的體驗。

* 一鍵式發佈(使用 **[!UICONTROL 快速發佈]** （在工具列上）以產生URL。
* 透過由Adobe Dimension提供支援的高品質互動式Dimensional檢視器預設集，針對檢視3D資產提供最佳化支援。
* 3D Media WCM元件可讓您輕鬆將3D資產新增至 [!DNL Adobe Experience Manager Sites] 頁面。

在Dynamic Media中使用3D資產無需額外安裝。

![3d鞋子](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media支援的3D格式 {#supported-three-d-file-formats-in-dm}

Dynamic Media支援下列3D檔案格式。

另請參閱 [Experience Manager Assets支援的3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D副檔名 | 檔案格式 | MIME型別 | 注释 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | model/gltf-binary | 將材質和紋理納入為單一資產。 |
| 物件 | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體光刻 | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene說明Zip封存 | model/vnd.usdz+zip | *僅支援內嵌；不提供檢視或互動。* USDZ是專屬的3D格式，可由Safari或iOS以原生方式檢視。 |

資產「詳細資訊」頁面上的3D Media WCM元件和3D預覽版與最新版Chrome (97.x)不相容。 若要使用3D資產，請使用Firefox或Safari，或使用舊版Chrome (96.x)。

## 快速入門：Dynamic Media中的3D資產 {#quick-start-three-d}

下列逐步工作流程說明可協助您快速上手並執行Dynamic Media中的3D資產。

在Dynamic Media中使用3D資產之前，請確定 [!DNL Experience Manager] 管理員已啟用並設定Dynamic MediaCloud Services。

另請參閱 [設定Dynamic MediaCloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **上傳3D資產**

   * [上傳您的3D資產以用於Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Dynamic Media支援的上傳3D檔案格式](#supported-three-d-file-formats-in-dm)

1. **管理立體資產**

   * 組織和搜尋3D資產

      * [組織數位資產](/help/assets/organize-assets.md)
      * [搜尋三維資產](/help/assets/search-assets.md)
   * 檢視三維資產

      * [檢視及與3D資產互動](#viewing-three-d-assets)
      * [管理維度檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)
   * 使用3D資產中繼資料

      * [管理數位資產的中繼資料](/help/assets/manage-digital-assets.md#editing-properties)
      * [元数据架构](/help/assets/metadata-schemas.md)



1. **發佈3D資產**

   * [發佈靜態Dynamic Media 3D資產](#publishing-three-d-assets)
   * [使用維度檢視器發佈Dynamic Media 3D資產的替代方法](#alternate-publish-methods)

## 關於檢視和與3D資產互動 {#viewing-three-d-assets}

本節說明如何以兩種不同的方式檢視及與3D資產互動：從資產詳細資訊頁面內和從Sites的3D媒體元件內。

互動式3D檢視器包含一系列互動式相機控制項，可供您環繞、縮放和平移3D資產。

在「資產詳細資訊」頁面檢視中開啟3D資產所需的時間取決於幾個因素。 這些因素包括：

* 伺服器的頻寬。
* 伺服器的延遲
* 影像的複雜性。

此外，使用者端電腦的功能（例如工作站、筆記型電腦或行動觸控裝置）也是您以互動方式操作相機時也必須考量的重要因素。 功能相當強大、圖形功能良好的系統，可讓互動式3D觀賞體驗更順暢、更理想。

>[!TIP]
>
>您可以在檢視器預設集編輯器中開啟維度檢視器預設集，以練習導覽3D資產，而無需先上傳任何3D檔案。 維度檢視器預設集內建了3D資產，可供您互動。
>
>另請參閱 [管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md).

## 從資產詳細資訊頁面檢視3D資產並與其互動 {#viewing-three-d-assets-from-asset-details-page}

另請參閱 [使用軟體介面預覽資產](/help/assets/dynamic-media/previewing-assets.md).

**若要從資產詳細資訊頁面檢視3D資產並與其互動：**

1. 請確定您已將3D資產上傳至 [!DNL Experience Manager].

   另請參閱 [上傳您的3D資產以用於Dynamic Media](/help/assets/add-assets.md#upload-assets).

1. 從 [!DNL Experience Manager]，位於 **[!UICONTROL 導覽]** 頁面，選取 **[!UICONTROL 「資產」>「檔案」]**.
1. 在頁面的右上角附近，從 **[!UICONTROL 檢視]** 下拉式清單，選取 **[!UICONTROL 卡片檢視]**.
1. 導覽至您要檢視的3D資產。
1. 若要在詳細資訊頁面中開啟資產，請選取3D資產的卡片。
1. 在3D資產的「詳細資訊」頁面上，執行下列任一項作業：

   | 查看 | 描述 | 滑鼠動作 | 觸控熒幕動作 |
   | --- | --- | --- | --- |
   | **轉動相機** | 围绕 3D 场景和对象旋转视图。 | 按一下左鍵+拖曳。 | 單指按下+拖曳。 |
   | **平移相機** | 向左、向右、向上或向下平移檢視。 | 按一下滑鼠右鍵+拖曳。 | 兩指按下+拖曳。 |
   | **縮放相機** | 在3D場景中移入和移出區域。 | 滾輪。 | 兩指捏合。 |
   | **重新將相機置中** | 將相機重新置中至3D場景中物件上的一點。 | 按兩下。 | 點兩下。 |
   | **重置** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點恢復到3D資產的中心。 重設也會將相機移到更近或更遠的位置，以完整的方式顯示資產，並維持合理的檢視大小。 |  |  |
   | **全屏模式** | 若要進入全熒幕模式，請在頁面的右下角，選取「全熒幕」圖示。 |  |  |

1. 在頁面的右上角，選取 **[!UICONTROL 關閉]** 返回「資產」頁面。

## 在3D媒體元件中檢視3D資產並與其互動 {#interacting-with-asset-inside-three-d-media-component}

當網頁位於 **[!UICONTROL 編輯]** 模式，無法與3D資產互動。 若要讓資產具有互動式，您可以使用 **[!UICONTROL 預覽]** 可在頁面編輯器中檢視網頁的功能，並可完整存取3D媒體元件的功能。

>[!IMPORTANT]
>
>您必須先將3D媒體元件新增至網頁並指派3D資產至元件，才能完成此工作。 另請參閱 [將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page) 和 [將3D資產指派給3D媒體元件](#assigning-a-three-d-asset-to-the-component).

另請參閱 [使用軟體介面預覽資產](/help/assets/dynamic-media/previewing-assets.md).

**若要在3D媒體元件中檢視3D資產並與其互動：**

1. 當網頁位於 **[!UICONTROL 編輯]** 模式，執行下列任一項作業：

   * 在頁面的右上角附近，按一下 **[!UICONTROL 預覽]** 以輸入 **[!UICONTROL 預覽]** 模式。
   * 刪除 `/editor.html` 從瀏覽器中的頁面URL。

完全互動的3D資產，顯示於    ![3D資產顯示在3D媒體元件內](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
完全互動的3D資產，顯示於 **[!UICONTROL 預覽]** 模式。

1. 當在 **[!UICONTROL 預覽]** 模式，執行下列任一項作業：

   | 查看 | 描述 | 滑鼠動作 | 觸控熒幕動作 |
   | --- | --- | --- | --- |
   | **轉動相機** | 围绕 3D 场景和对象旋转视图。 | 按一下左鍵+拖曳。 | 單指按下+拖曳。 |
   | **平移相機** | 向左、向右、向上或向下平移檢視。 | 按一下滑鼠右鍵+拖曳。 | 兩指按下+拖曳。 |
   | **縮放相機** | 在3D場景中移入和移出區域。 | 滾輪。 | 兩指捏合。 |
   | **重新將相機置中** | 將相機重新置中至3D場景中物件上的一點。 | 按兩下。 | 點兩下。 |
   | **重置** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點恢復到3D資產的中心。 重設也會將相機移到更近或更遠的位置，以完整的方式顯示資產，並維持合理的檢視大小。 |  |  |
   | **全屏模式** | 若要進入全熒幕模式，請在頁面的右下角，選取「全熒幕」圖示。 |  |  |

## 關於使用3D媒體元件 {#working-with-three-d-media-component}

Dynamic Media內含Dynamic Media 3D媒體元件，您可在以下專案中使用： [!DNL Experience Manager Sites] 讓您以互動方式檢視網頁上的3D模型。

* [將3D媒體元件新增至頁面範本](#adding-three-d-media-component-to-page-template)
* [將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page)
   * [可選 — 設定3D媒體元件](#configuring-the-three-d-component)
* [將3D資產指派給3D媒體元件](#assigning-a-three-d-asset-to-the-component)

## 將3D媒體元件新增至頁面範本 {#adding-three-d-media-component-to-page-template}

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]**.
1. 導覽至您要啟用3D元件的頁面範本，然後選取範本。
1. 若要開啟範本，請選取 **[!UICONTROL 編輯]**.
1. 在頁面的右上角附近，在下拉式選單中選取 **[!UICONTROL 結構]** 模式（如果尚未啟用）。

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. 若要選取空白區域並開啟其相關工具列，請在 **[!UICONTROL 配置容器]** 區域。
1. 在工具列上，選取 **[!UICONTROL 原則]** 圖示以開啟 **[!UICONTROL 原則編輯器]**.
1. 在 **[!UICONTROL 屬性]** 區段，在 **[!UICONTROL 允許的元件]** 標籤，捲動至 **[!UICONTROL Dynamic Media]**，然後展開清單並勾選 **[!UICONTROL 3D媒體]**.
1. 點選 **[!UICONTROL 完成]** 以儲存變更並關閉 **[!UICONTROL 原則編輯器]**.

   您現在可以將Dynamic Media 3D媒體元件放置在使用此範本的所有頁面上。

## 將3D媒體元件新增至網頁 {#adding-the-three-d-media-component-to-a-web-page}

如果您使用 [!DNL Experience Manager] 作為您的網頁內容管理系統，您可以透過3D媒體元件將3D資產新增至您的網頁。

另請參閱 [將Dynamic Media資產新增至頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. 開啟 [!DNL Experience Manager Sites] 並選取您要新增Dynamic Media 3D Media元件的網頁。
1. 若要在頁面編輯器中開啟頁面，請選取 **[!UICONTROL 編輯]** （鉛筆）圖示。 請確定 **[!UICONTROL 編輯]** 模式會選取在頁面右上角附近。

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. 在工具列上，選取「側面板」圖示以切換或「開啟」面板的顯示。

1. 在側面板中，選取加號圖示以開啟 **[!UICONTROL 元件]** 清單。

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. 拖曳 **[!UICONTROL 3D媒體]** 元件來自 **[!UICONTROL 元件]** 列出要在頁面上顯示3D檢視器的位置。

您現在已準備好為元件指派3D資產。

另請參閱 [將3D資產指派給3D媒體元件](#assigning-a-three-d-asset-to-the-component)

### 可選 — 設定3D媒體元件 {#configuring-the-three-d-component}

1. 在 [!DNL Experience Manager Sites] 頁面編輯器，選取 **[!UICONTROL 3D媒體檢視器]** 先前新增至頁面的元件。
1. 若要開啟元件組態對話方塊，請選取 **[!UICONTROL 設定]** 圖示（扳手）。

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. 在「3D媒體」對話方塊中，從「檢視器預設集」下拉式清單中選取 **[!UICONTROL 維度]** 將「維度」檢視器預設集指派給元件。

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. 在右上角，選取核取記號以儲存變更。

## 將3D資產指派給3D媒體元件 {#assigning-a-three-d-asset-to-the-component}

將3D媒體元件新增至網頁後，即可為其指派3D資產。

另請參閱 [將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page).

1. 在 [!DNL Experience Manager Sites] 頁面編輯器，按一下 **[!UICONTROL 資產]** 圖示以開啟 **[!UICONTROL 資產]** 於側面板中。
1. 在下拉式清單中，選取 **[!UICONTROL 三維]** 以僅顯示3D資產檔案型別。
1. 在側面板中，搜尋或捲動至您要在編輯的頁面上檢視的3D資產。
1. 從「資產」側面板拖曳3D資產，並將其拖放至 **[!UICONTROL 3D媒體]** 先前新增至頁面的元件。

   ![將3d資產指派給3d媒體元件](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>當網頁位於 [!DNL Experience Manager Sites] **[!UICONTROL 編輯]** 模式，「3D媒體」元件會顯示3D資產，但無法與資產互動。 若要讓資產具有互動式，您可以使用 **[!UICONTROL 預覽]** 可在頁面編輯器中檢視網頁的功能，並可完整存取3D媒體元件的功能。

## 發佈靜態Dynamic Media 3D資產 {#publishing-three-d-assets}

Dynamic Media接受以下支援的各種3D檔案格式 *靜態內容* 在Dynamic Media中。 靜態內容表示您可以上傳和發佈3D資產，但不支援 *動態* 與3D資產相關聯的影像或影像重新調整。 原因在於Dynamic Media Imaging Server無法辨識3D格式。 因此，在Dynamic Media中發佈3D資產後，您就可以立即複製URL。 3D資產的URL會遵循一般的Dynamic Media URL結構。 不過，與Dynamic Media中的傳統影像資產不同，您無法編輯資產URL中的任何引數。

另請參閱 [取得靜態資產的URL](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

在 **[!UICONTROL 卡片檢視]**，資產名稱正下方及其日期和時間左側會出現一個小地球圖示，指出資產已發佈。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

如果您使用 [!DNL Experience Manager] 如果您使用WCM，請使用此發佈方法直接在網頁上新增Dynamic Media 3D資產。

另請參閱 [發佈Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

另請參閱 [發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

**若要發佈靜態Dynamic Media 3D資產：**

1. 開啟3D資產（GLB、OBJ或STL檔案格式）。
1. 在「詳細資訊」頁面的工具列上，選取 **[!UICONTROL 快速發佈]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. 點選 **[!UICONTROL 關閉]** 以結束對話方塊並返回資產詳細資訊頁面。
1. 從3D資產檔案名稱左側的下拉式清單中，選取 **[!UICONTROL 轉譯]**.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. 點選 **[!UICONTROL 原始]**. 發佈（或「啟動」）3D資產時， **[!UICONTROL URL]** 如果符合下列3D資產條件，按鈕會出現在頁面左下角附近：
   * 3D資產是支援的格式（GLB、OBJ、STL和USDZ）。
   * 3D資產已內嵌至Dynamic Media Image Production System (IPS)。
   * 3D資產隨即發佈。

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. 若要顯示3D資產的直接生產URL （您可以在網頁上複製和使用），請選取「 」 **[!UICONTROL URL]**.

### 使用維度檢視器發佈Dynamic Media 3D資產的替代方法 {#alternate-publish-methods}

若要發佈Dynamic Media 3D資產，請遵循下列兩種方法： *not* 使用 [!DNL Experience Manager] 作為您的WCM。

* **[!UICONTROL URL]**  — 使用 **[!UICONTROL URL]** 如果您使用協力廠商網頁內容管理系統，且想使用「維度」檢視器將Dynamic Media 3D資產連結至網頁。

   另請參閱 [將URL連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL 內嵌]**  — 使用 **[!UICONTROL 內嵌]** 當您想要使用「維度」檢視器來檢視內嵌在網頁上的Dynamic Media 3D資產時。 将嵌入代码复制到剪贴板，以便将其粘贴到网页中。 中不允許編輯程式碼 **[!UICONTROL 內嵌]** 對話方塊。

   另請參閱 [將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
