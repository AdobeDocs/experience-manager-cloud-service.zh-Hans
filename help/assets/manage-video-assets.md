---
title: 管理视频资源
description: 上傳、預覽、註釋和發佈視訊資產 [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '4938'
ht-degree: 6%

---

# 管理视频资源 {#manage-video-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=en) |
| AEM as a Cloud Service | 本文 |

視訊格式是組織數位資產的重要部分。 [!DNL Adobe Experience Manager] 提供成熟的產品和功能，可管理視訊資產建立後的整個生命週期。

瞭解如何在中管理和編輯視訊資產 [!DNL Adobe Experience Manager Assets]. 視訊編碼和轉碼（例如FFmpeg轉碼）可以使用「處理設定檔」和 [!DNL Dynamic Media] 整合。 不含 [!DNL Dynamic Media] 授權， [!DNL Experience Manager] 提供視訊的基本支援，例如使用FFmpeg轉碼、擷取支援的檔案格式的預覽縮圖，以及直接在瀏覽器中支援播放的格式的使用者介面預覽。

## 上傳和預覽視訊資產 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 產生擴充功能為MP4之視訊資產的預覽。 您可以在中預覽轉譯 [!DNL Assets] 使用者介面。

1. 在數位資產資料夾或子資料夾中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請按一下 **[!UICONTROL 建立]** 從工具列中選擇 **[!UICONTROL 檔案]**. 或者，在使用者介面上拖曳檔案。 另請參閱 [上傳資產](manage-digital-assets.md#uploading-assets) 以取得詳細資訊。
1. 若要在卡片檢視中預覽視訊，請按一下 **[!UICONTROL 播放]** ![播放選項](assets/do-not-localize/play.png) 視訊資產選項。 您只能在卡片檢視中暫停或播放視訊。 此 [!UICONTROL 播放] 和 [!UICONTROL 暫停] 選項在清單檢視中無法使用。
1. 若要在資產詳細資訊頁面中預覽視訊，請選取 **[!UICONTROL 編輯]** 在卡片上。 視訊會在瀏覽器的原生視訊播放器中播放。 您可以播放、暫停、控制音量，以及將視訊縮放至全熒幕。

## 發佈視訊資產 {#publish-video-assets}

發佈後，您可以將視訊資產以URL形式納入網頁中，或直接內嵌資產。 如需詳細資訊，請參閱 [發佈 [!DNL Dynamic Media] 資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## 將視訊發佈至YouTube {#publishing-videos-to-youtube}

您可以將Experience Manager Assets中管理的視訊資產直接發佈至您先前建立的YouTube頻道。

若要將視訊資產發佈至YouTube，請在Experience Manager Assets中使用標籤來標籤視訊資產。 您可以將這些標籤與YouTube頻道建立關聯。 如果影片資產的標籤符合YouTube頻道的標籤，則影片會發佈至YouTube。 只要使用關聯的標籤，發佈至YouTube就會伴隨著視訊的正常發佈。

YouTube會自行編碼。 因此，上傳至Experience Manager的原始視訊檔案會發佈至YouTube，而不是Dynamic Media的編碼建立的任何視訊轉譯。 雖然您不需要使用Dynamic Media處理影片，但預計他們會在需要檢視器預設集進行播放時這樣做。

當您略過視訊處理設定檔並直接發佈至YouTube時，這僅僅表示您在Experience Manager資產中的視訊資產沒有取得可檢視的縮圖。 這也表示未編碼的視訊不適用於任何Dynamic Media資產型別。

若要將視訊資產發佈至YouTube伺服器，必須完成下列工作，以確保透過YouTube進行安全無虞的伺服器對伺服器驗證：

1. [配置Google雲端設定](#configuring-google-cloud-settings)
1. [建立YouTube頻道](#creating-a-youtube-channel)
1. [新增標籤以進行發佈](#adding-tags-for-publishing)
1. [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem)
1. [（可選）自動為您上傳的視訊設定預設YouTube屬性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [將影片發佈至您的YouTube頻道](#publishing-videos-to-your-youtube-channel)
1. [（可選）驗證YouTube上發佈的影片](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [將YouTube URL連結至您的網頁應用程式](#linking-youtube-urls-to-your-web-application)

您也可以 [取消發佈視訊以從YouTube中將其移除](#unpublishing-videos-to-remove-them-from-youtube).

### 配置Google雲端設定 {#configuring-google-cloud-settings}

若要發佈至YouTube，您需要Google帳戶。 如果您有GMAIL帳戶，表示您已擁有Google帳戶；如果您沒有Google帳戶，可以輕鬆建立帳戶。 您需要帳戶，因為您需要憑證才能將視訊資產發佈到YouTube。 <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

Google Cloud使用的帳戶和用於YouTube的Google帳戶不需要相同。

Google會定期變更其使用者介面。 因此，將視訊發佈至YouTube的步驟可能會與以下說明稍有不同。 當您嘗試檢查影片是否已上傳到YouTube時，此警告同樣適用。

>[!NOTE]
>
>在撰寫時，下列步驟是準確的。 不過，Google會定期更新其雲端網頁，恕不另行通知。 因此，某些設定選項在Google使用者介面中的名稱可能與步驟中使用的名稱略有不同。

**若要設定Google Cloud設定：**

1. 建立Google帳戶。
   [https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp](https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp)

   如果您已有Google帳戶，可跳至下一個步驟。

1. 前往 [https://cloud.google.com/](https://cloud.google.com/).
1. 於 **[!UICONTROL Google Cloud]** 頁面，右上角附近，選取 **[!UICONTROL 主控台]**.

   如有需要， **[!UICONTROL 登入]** 使用您的Google帳戶認證來檢視 **[!UICONTROL 主控台]** 選項。

1. 於 **[!UICONTROL 儀表板]** 頁面，右側 **[!UICONTROL Google Cloud Platform]**，選取 **[!UICONTROL 專案]** 下拉式清單來開啟 **[!UICONTROL 選取專案]** 對話方塊。
1. 在 **[!UICONTROL 選取專案]** 對話方塊，選取 **[!UICONTROL 新增專案]**.
1. 在 **[!UICONTROL 新增專案]** 對話方塊，在 **[!UICONTROL 專案名稱]** 欄位，輸入新專案的名稱。

   您的專案ID是以專案名稱為基礎。 因此，請謹慎選擇專案名稱；專案建立後即無法變更。 此外，您稍後在Experience Manager中設定YouTube時，必須再次輸入相同的專案ID。 因此，請將其寫下來。

1. 选择&#x200B;**[!UICONTROL 创建]**。

1. 執行下列任一項作業：

   * 在您專案的控制面板上，於 **[!UICONTROL 快速入門]** 卡片，選取 **[!UICONTROL 探索及啟用API]**.
   * 在您專案的控制面板上，於 **[!UICONTROL API]** 卡片，選取 **[!UICONTROL 前往API概述]**.

1. 靠近上中間 **[!UICONTROL API和服務]** 頁面，選取 **[!UICONTROL 啟用API和服務]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. 於 **[!UICONTROL API程式庫]** 頁面，左側，下方 **[!UICONTROL 類別]**，選取 **[!UICONTROL YouTube]**. 在頁面右側，選取 **[!UICONTROL YouTube]**.
1. 於 **[!UICONTROL YouTube]** 頁面，選取 **[!UICONTROL YouTube Data API v3]**.
1. 於 **[!UICONTROL YouTube Data API v3]** 頁面，選取 **[!UICONTROL 管理]**.

   ![6_5_google帳戶 — apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. 若要使用API，您需要憑證。 如有必要，請前往左側的 **[!UICONTROL API和服務]** 頁面，選取 **[!UICONTROL 認證]**.
1. 於 **[!UICONTROL 認證]** 頁面，在頂端附近，選取 **[!UICONTROL 建立認證]**，然後選取 **[!UICONTROL OAuth使用者端ID]**.
1. 於 **[!UICONTROL 建立OAuth使用者端ID]** 頁面，在 **[!UICONTROL 應用程式型別]** 下拉式清單，選取 **[!UICONTROL 網頁應用程式]**.

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. 执行下列操作之一：

   * 在 **[!UICONTROL 名稱]** 欄位中，為您的OAuth 2.0使用者端輸入唯一名稱。
   * 使用Google在中提供的預設名稱 **[!UICONTROL 名稱]** 欄位。

1. 在 **[!UICONTROL 授權的JavaScript來源]** 標題，選取 **[!UICONTROL 新增URI]**.

   ![6_5_google帳戶 — apis-nameauthorizations](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. 在 **[!UICONTROL URI]** 文字欄位，輸入以下路徑，在路徑中取代您自己的網域和連線埠號碼，然後按下 **[!UICONTROL 輸入]** 若要將路徑新增至清單：

   `https://<servername.domain>:<port_number>`

   例如，`https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >上述URI路徑範例是假設的，僅供說明之用。

1. 在 **[!UICONTROL 授權的重新導向URI]** 標題中，選取新增URI。
1. 在 **[!UICONTROL URI]** 文字欄位，輸入以下路徑，在路徑中取代您自己的網域和連線埠號碼，然後按下 **[!UICONTROL 輸入]** 若要將路徑新增至清單：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如，`https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >上述URI路徑範例是假設的，僅供說明之用。

1. 接近底部 **[!UICONTROL 建立OAuth使用者端ID]** 頁面，選取 **[!UICONTROL 建立]**.
1. 於 **[!UICONTROL 已建立OAuth使用者端]** 對話方塊中，執行下列動作：

   * （可選）將值複製到 **[!UICONTROL 您的使用者端ID]** 和 **[!UICONTROL 您的使用者端密碼]** 欄位並儲存。
   * 選取 **[!UICONTROL 下載JSON]**，然後儲存JSON檔案。

   稍後在Adobe Experience Manager中設定YouTube時，您需要此下載的JSON檔案。

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. 於 **[!UICONTROL 已建立OAuth使用者端]** 對話方塊，選取 **[!UICONTROL 確定]**.
1. 登出您的Google帳戶。 現在建立YouTube頻道。

### 建立YouTube頻道 {#creating-a-youtube-channel}

將影片發佈至YouTube需要您有一或多個管道。 如果您已建立YouTube頻道，您可以略過此任務並前往 [新增標籤以進行發佈](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>請確定您已在YouTube中設定一或多個管道 *早於* 您在「Experience Manager中的YouTube設定」下新增管道(請參閱 [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem) 下)。 如果您無法進行管道設定，則不會警告您沒有現有管道。 不過，當您新增頻道時，Google驗證仍會發生，但無法選擇傳送視訊的頻道。

**若要建立YouTube頻道：**

1. 前往 [https://www.youtube.com](https://www.youtube.com/) 並使用您的Google帳戶憑證登入。
1. 在YouTube頁面的右上角，選取您的個人資料圖片（也可以顯示為實色圓圈內的字母），然後選取 **[!UICONTROL YouTube設定]** （圓形齒輪圖示）。
1. 在「概述」頁面的「其他功能」標題下，選取「 」 **[!UICONTROL 檢視我的所有管道或建立管道]**.
1. 在管道頁面上，選取 **[!UICONTROL 建立新管道]**.
1. 在「品牌帳戶」頁面的「品牌帳戶名稱」欄位中，輸入您要發佈視訊資產的公司名稱或任何其他管道名稱，然後選取「 」 **[!UICONTROL 建立]**.

   請記住您在這裡輸入的名稱；您必須在Experience Manager中設定YouTube時才能再次輸入。

1. （選用）如有必要，請新增更多管道。

   現在新增標籤以進行發佈。

### 新增標籤以進行發佈 {#adding-tags-for-publishing}

若要將影片發佈至YouTube，Experience Manager會將標籤與一或多個YouTube管道建立關聯。 若要新增標籤以進行發佈，請參閱 [管理標籤](/help/sites-cloud/authoring/features/tags.md).

或者，如果您想在Experience Manager中使用預設標籤，您可以略過此任務並前往 [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem).

>[!NOTE]
>
>設定Cloud Service後，此時不需要其他設定即可啟用YouTube發佈復寫代理程式。 原因是因為它是在儲存Cloud Service設定時啟用。

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### 在Experience Manager中設定YouTube {#setting-up-youtube-in-aem}

從Experience Manager6.4開始，引進了新的觸控使用者介面方法，以在Experience Manager中設定YouTube發佈。 根據您所使用的Experience Manager安裝例項，執行下列任一項作業：

* 若要在6.4之前的Experience Manager中設定YouTube，請參閱 [在6.4之前的Experience Manager中設定YouTube](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* 若要在Experience Manager6.4或更新版本中設定YouTube，請參閱 [在Experience Manager6.4和更新版本中設定YouTube](#setting-up-youtube-in-aem-and-later).

#### 在Experience Manager6.4和更新版本中設定YouTube {#setting-up-youtube-in-aem-and-later}

1. 請確定您以管理員身分登入您的Dynamic Media執行個體。
1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中導覽至 **[!UICONTROL 工具]**（槌子圖示） > **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube發佈設定]**.
1. 選取 **[!UICONTROL 全域]** （請勿選取）。

1. 在全域頁面的右上角附近，選取 **[!UICONTROL 建立]**.
1. 在“创建 YouTube 配置”页面的“Google Cloud Platform 设置”下的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   您已在先前初始設定Google Cloud設定時指定專案ID。
「建立YouTube設定」頁面保持開啟；您稍後會回到。

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用純文字編輯器，開啟您先前在工作中下載並儲存的JSON檔案 [配置Google雲端設定](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
1. 選取並複製整個JSON文字。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**.

   現在在Experience Manager中設定YouTube管道。

1. 選取 **[!UICONTROL 新增頻道]**.
1. 在管道名稱欄位中，輸入您在任務中建立的管道名稱 **[!UICONTROL 新增一或多個管道至YouTube]** 較早。

   如有需要，您可以選擇新增說明。

1. 選取 **[!UICONTROL 新增]**.
1. 隨即顯示YouTube/Google驗證。 如果您尚未登入Google Cloud帳戶，請略過此步驟。

   * 輸入與Google專案ID關聯的Google使用者名稱和密碼，以及上述JSON文字。
   * 根據您的帳戶有多少個管道，您會看到兩個或多個專案。 選取頻道。 不要選取電子郵件地址；它不是頻道。
   * 在下一頁，選取 **[!UICONTROL Accept]** 以允許存取此頻道。

1. 選取 **[!UICONTROL 允許]**.

   現在設定標籤以進行發佈。

1. **[!UICONTROL 設定標籤以供發佈]**  — 在「Cloud Services> YouTube」頁面上，選取鉛筆圖示以編輯您要使用的標籤清單。
1. 若要在Experience Manager中顯示可用標籤清單，請選取下拉式清單圖示（倒置脫字元號）。
1. 若要新增這些標籤，請選取一或多個標籤。

   若要刪除您新增的標籤，請選取標籤，然後選取 **[!UICONTROL X]**.

1. 完成新增所需標籤後，選取「 」 **[!UICONTROL 儲存]**.

   現在您可將影片發佈至YouTube頻道。

#### 在6.4之前的Experience Manager中設定YouTube {#setting-up-youtube-in-aem-before}

1. 請確定您以管理員身分登入您的Dynamic Media執行個體。

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中導覽至 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 在「協力廠商服務」標題下方的YouTube下方，選取 **[!UICONTROL 立即設定]**.
1. 在「建立組態」對話方塊中，在個別欄位中輸入標題（必要）和名稱（選用）。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在“YouTube 帐户设置”对话框的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   您最初指定專案ID時 [已設定Google雲端設定](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) 較早。
保留「YouTube帳戶設定」對話方塊開啟；您稍後會回到。

1. 使用純文字編輯器，開啟您先前在「設定Google雲端設定」工作中下載並儲存的JSON檔案。
1. 選取並複製整個JSON文字。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 選取 **[!UICONTROL 確定]**.

   現在在Experience Manager中設定YouTube管道。

1. 右側 **[!UICONTROL 可用頻道]**，選取 **+** （加號圖示）。
1. 在“YouTube频道设置”对话框的“标题”字段中，输入您在之前向YouTube添加一个或多个频道任务中创建的频道 **[!UICONTROL 名称]** 。

   如有需要，您可以選擇新增說明。

1. 選取 **[!UICONTROL 確定]**.
1. 隨即顯示YouTube/Google驗證。 如果您尚未登入Google Cloud帳戶，請略過此步驟。

   * 輸入與Google專案ID關聯的Google使用者名稱和密碼，以及上述JSON文字。
   * 根據您的帳戶有多少個管道，您會看到兩個或多個專案。 選取頻道。 不要選取電子郵件地址；它不是頻道。
   * 在下一頁，選取 **[!UICONTROL Accept]** 以允許存取此頻道。

1. 選取 **[!UICONTROL 允許]**.

   現在設定標籤以進行發佈。

1. **[!UICONTROL 設定標籤以供發佈]**  — 在「Cloud Services> YouTube」頁面上，選取鉛筆圖示以編輯您要使用的標籤清單。
1. 若要在Experience Manager中顯示可用標籤清單，請選取下拉式清單圖示（倒置脫字元號）。
1. 若要新增這些標籤，請選取一或多個標籤。

   若要刪除您新增的標籤，請選取標籤，然後選取 **X**.

1. 完成新增所需標籤後，選取「 」 **[!UICONTROL 確定]**.

   現在您可將影片發佈至YouTube頻道。

### （可選）自動為您上傳的視訊設定預設YouTube屬性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以選擇在上傳視訊時自動設定YouTube屬性。 以Experience Manager建立中繼資料處理設定檔。

要创建元数据处理配置文件，您首先需要从&#x200B;**[!UICONTROL 字段标签]**、**[!UICONTROL 映射到属性]**&#x200B;和&#x200B;**[!UICONTROL 选择]**&#x200B;字段中复制值，所有这些字段均位于视频的元数据架构中。然後，您可以新增這些值，以建立您的YouTube視訊中繼資料處理設定檔。

**若要自動為您上傳的視訊設定預設YouTube屬性：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中導覽至 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.
1. 選取 **[!UICONTROL 預設]**. （請勿在「預設」左側的選取方塊中新增核取記號。）
1. 於 **[!UICONTROL 預設]** 頁面，勾選左側的方塊 **[!UICONTROL 視訊]**，然後選取 **[!UICONTROL 編輯]**.
1. 在「中繼資料結構編輯器」頁面上，選取 **[!UICONTROL 進階]** 標籤。
1. 在「YouTube發佈」標題下，選取 **[!UICONTROL YouTube類別]**.
1. 在頁面右側的 **[!UICONTROL 設定]** 索引標籤中，執行下列動作：

   * 在 **[!UICONTROL 對應至屬性]** 文字欄位，選取並複製值。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 讓文字編輯器保持開啟。

   * 下 **[!UICONTROL 選擇]**，選取並複製您要使用的預設值（例如People &amp; Blogs或Science &amp; Technology）。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 讓文字編輯器保持開啟。

1. 在「YouTube發佈」標題下，選取 **[!UICONTROL YouTube隱私權]**.
1. 在頁面右側的 **[!UICONTROL 設定]** 索引標籤中，執行下列動作：

   * 在 **[!UICONTROL 對應至屬性]** 文字欄位，選取並複製值。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 讓文字編輯器保持開啟。

   * 下 **[!UICONTROL 選擇]**，選取並複製您要使用的預設值。 請注意，「選擇」會分成兩組。 配對中的底部欄位是您要複製的預設值，例如public、unlisted或private。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 讓文字編輯器保持開啟。

1. 在「中繼資料結構編輯器」頁面的右上角附近，選取「 」 **[!UICONTROL 取消]**.
1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料設定檔]**.

1. 在「中繼資料描述檔」頁面的右上角附近，選取「 」 **[!UICONTROL 建立]**.
1. 在「新增中繼資料描述檔」對話方塊的 **[!UICONTROL 設定檔標題]** 文字欄位，輸入名稱 `YouTube Video` 然後選取 **[!UICONTROL 建立]**.
1. 在「中繼資料設定檔編輯器」頁面上，選取 **[!UICONTROL 前進]** 標籤。
1. 執行下列動作，將複製的YouTube發佈值新增至設定檔：

   * 在頁面的右側，選取 **[!UICONTROL 建置表單]** 標籤。
   * （可選）拖曳標示為 **[!UICONTROL 區段標題]** 左側，並將它放置在表單區域中。
   * （選用）選取 **[!UICONTROL 欄位標籤]** 以選取元件。
   * （可選）在頁面右側的「設定」標籤下方，在「欄位標籤」文字欄位中輸入 `YouTube Publishing`.
   * 選取 **[!UICONTROL 建置表單]** 標籤，然後拖曳標示為 **[!UICONTROL 多值文字]** 並將它拖放到 **[!UICONTROL YouTube發佈]** 您建立的標題。

   * 若要選取元件，請選取 **[!UICONTROL 欄位標籤]**.
   * 在頁面的右側，在「設定」標籤下方，將您先前複製的「YouTube發佈」值（「欄位標籤」值和「對應至屬性值」）貼到表單上各自的欄位中。 將「選擇」值貼到「預設值」欄位中。

1. 執行下列動作，將複製的YouTube隱私權值新增至設定檔：

   * 在頁面的右側，選取 **[!UICONTROL 建置表單]** 標籤。
   * （可選）拖曳標示為 **[!UICONTROL 區段標題]** 左側，並將它放置在表單區域中。
   * （選用）選取 **[!UICONTROL 欄位標籤]** 以選取元件。
   * （可選）在頁面右側的「設定」標籤下方，在「欄位標籤」文字欄位中輸入 `YouTube Privacy`.
   * 選取 **[!UICONTROL 建置表單]** 標籤，然後拖曳標示為 **[!UICONTROL 多值文字]** 並將它拖放到 **[!UICONTROL YouTube隱私權]** 您建立的標題。

   * 若要選取元件，請選取 **[!UICONTROL 欄位標籤]**.
   * 在頁面的右側，在「設定」標籤下方，將您先前複製的「YouTube發佈」值（「欄位標籤」值和「對應至屬性值」）貼到表單上各自的欄位中。 將「選擇」值貼到「預設值」欄位中。

1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**.
1. 將YouTube發佈中繼資料設定檔套用至您要上傳影片的資料夾。 您必須同時設定中繼資料設定檔和視訊設定檔。

   请参阅 [元数据配置文件](/help/assets/metadata-profiles.md) 和视 [频配置文件](/help/assets/dynamic-media/video-profiles.md)。

### 將影片發佈至您的YouTube頻道 {#publishing-videos-to-your-youtube-channel}

現在，您可將先前新增的標籤與影片資產建立關聯。 此程式可讓Experience Manager知道要將哪些資產發佈至您的YouTube頻道。

>[!NOTE]
>
>立即發佈不會自動發佈至YouTube。 设置 Dynamic Media 时，有两种发布选项可供选择：**[!UICONTROL 立即]**&#x200B;或&#x200B;**[!UICONTROL 激活时]**。
>
>**[!UICONTROL 立即發佈]** 這表示上傳的資產（與IPS同步後）會自動發佈至傳送系統。 雖然這對Dynamic Media來說是真的，但對YouTube不是這樣。 若要發佈至YouTube，您必須透過Experience Manager Author發佈。

>[!NOTE]
若要從YouTube發佈內容，Experience Manager會使用 **[!UICONTROL 發佈至YouTube]** 工作流程，可讓您監視進度並檢視任何失敗資訊。
另請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).
如需詳細進度資訊，您可以監視復寫下的YouTube記錄。 但是，請注意，此類監視需要管理員存取權。

**若要將視訊發佈至您的YouTube頻道：**

1. 在Experience Manager中，導覽至您要發佈至YouTube頻道的視訊資產。
1. 選取視訊資產（最適化視訊集）。
1. 在工具列上，選取 **[!UICONTROL 屬性]**.
1. 在基本索引標籤的中繼資料標題下，選取 **[!UICONTROL 開啟選取範圍對話方塊]** 標籤欄位右側。
1. 在「選取標籤」頁面上，導覽至您要使用的標籤，然後選取一或多個標籤。

   請記住，標籤必須與YouTube管道相關聯。

1. 在頁面的右上角，選取 **[!UICONTROL 選取]**.
1. 在視訊的屬性頁面的右上角，選取 **[!UICONTROL 儲存並關閉]**.
1. 在工具列上，選取 **[!UICONTROL 快速發佈]**.

   另請參閱 [透過Experience Manager Sites使用發佈管理](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring).

   您可以選擇在YouTube頻道上驗證發佈的影片。

### （可選）驗證YouTube上發佈的影片 {#optional-verifying-the-published-video-on-youtube}

您可以選擇監視YouTube發佈（或取消發佈）的進度。

另請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).

發佈時間會因多項因素而有很大的差異，包括主要來源視訊格式、檔案大小和上傳流量。 發佈程式可能需要幾分鐘到幾小時的時間。 此外，更高解析度的格式呈現得也慢得多。 例如，720p和1080p的出現時間會比480p長。

八小時後，如果您仍然看到顯示以下訊息的狀態訊息 **[!UICONTROL 已上傳（正在處理，請稍候）]**，請嘗試從您的網站移除視訊並重新上傳。

### 將YouTube URL連結至您的網頁應用程式 {#linking-youtube-urls-to-your-web-application}

您可以取得Dynamic Media在發佈影片後產生的YouTube URL字串。 當您複製YouTube URL時，它會貼到剪貼簿，以便您視需要將其貼到網站或應用程式中的頁面。

>[!NOTE]
您必須先將視訊資產發佈至YouTube，才能複製YouTube URL。

若要將YouTube URL連結至您的Web應用程式：

1. 導覽至 *YouTube已發佈* 您要複製其URL的視訊資產，然後選取它。

   請記住，YouTube URL僅供複製 *晚於* 您有 *已發佈* 將影片資產轉移到YouTube。

1. 在工具列上，選取 **[!UICONTROL 屬性]**.
1. 選取 **[!UICONTROL 進階]** 標籤。
1. 在「YouTube發佈」標題下方的「YouTube URL清單」中，選取URL文字，然後複製URL文字至網頁瀏覽器，以預覽資產或新增至網頁內容頁面。

### 取消發佈影片，以便從YouTube中將其移除 {#unpublishing-videos-to-remove-them-from-youtube}

當您在Experience Manager中取消發佈視訊資產時，該視訊會從YouTube中移除。

>[!CAUTION]
如果您直接從YouTube中移除視訊，Experience Manager不會察覺，並會繼續採取行動，彷彿視訊仍發佈至YouTube。 一律透過Experience Manager從YouTube取消發佈視訊資產。

>[!NOTE]
若要從YouTube移除內容，Experience Manager會使用 **[!UICONTROL 從YouTube取消發佈]** 工作流程，可讓您監視進度並檢視任何失敗資訊。
另請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).

**若要取消發佈視訊以從YouTube中將其移除：**

1. 導覽至您要從YouTube頻道取消發佈的視訊資產。
1. 在資產選擇模式中，選取一或多個已發佈的視訊資產。
1. 在工具列上，選取 **[!UICONTROL 管理發布]**. 如有必要，請選取三個點的圖示(`. . .`)，以檢視 **[!UICONTROL 管理發布]**.
1. 在「管理出版物」頁面上，選取 **[!UICONTROL 取消發佈]**.
1. 在頁面的右上角，選取 **[!UICONTROL 下一個]**.
1. 在頁面的右上角，選取 **[!UICONTROL 取消發佈]**.

## 監視視訊編碼和YouTube發佈進度 {#monitoring-video-encoding-and-youtube-publishing-progress}

當您將新視訊上傳至已套用視訊編碼的資料夾時，或者您將視訊發佈至YouTube時，請監視您的視訊編碼/Youtube發佈的進度（或失敗）。 實際的YouTube發佈進度只能透過記錄檔取得。 但無論成功與否，都會以下列程式所述的其他方式列出它。 此外，當YouTube發佈工作流程或視訊編碼完成或中斷時，您會收到電子郵件通知。

### 監視進度 {#monitoring-progress}

您可以監視進度，包括失敗的編碼/YouTube發佈。

1. 在資產資料夾中檢視視訊編碼進度：

   * 在卡片檢視中，視訊編碼進度會依百分比顯示在資產上。 如果出現錯誤，資產上也會顯示此資訊。

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * 在清單檢視中，視訊編碼進度會顯示在 **[!UICONTROL 處理狀態]** 欄。 如果出现错误，则同一列中将显示此消息。

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   默认情况下，此列不显示。若要啟用欄，請選取 **[!UICONTROL 檢視設定]** 從「檢視」下拉式選單中，新增 **[!UICONTROL 處理狀態]** 欄並選取 **[!UICONTROL 更新]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. 在資產詳細資訊中檢視進度。 選取資產時，請開啟下拉式功能表並選取 **[!UICONTROL 時間表]**. 若要將其縮小至編碼或YouTube發佈等工作流程活動，請選取「 」 **[!UICONTROL 工作流程]**.

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   任何工作流程資訊（例如編碼）都會顯示在時間軸中。 對於YouTube發佈，工作流程時間軸也包含YouTube頻道名稱和YouTube影片URL。 此外，發佈完成後，您會在工作流程時間軸中看到任何失敗通知。

   >[!NOTE]
   由於上的多個工作流程設定，最終記錄失敗/錯誤訊息可能需要很長時間 **[!UICONTROL 重試]**， **[!UICONTROL 重試延遲]**、和 **[!UICONTROL 逾時]** 從 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)例如：
   * Apache Sling工作佇列設定
   * AdobeGranite工作流程外部程式工作處理常式
   * Granite工作流程逾時佇列

   您可以調整 **[!UICONTROL 重試]**， **[!UICONTROL 重試延遲]**、和 **[!UICONTROL 逾時]** 這些設定中的屬性。

1. 有关进行中的工作流，请参阅“工具”>“工作流” **[!UICONTROL >“实例”中提供的“工作流实例]** ” **[!UICONTROL (Workflow]** ) **[!UICONTROL >“]**&#x200B;实例”。

   >[!NOTE]
   您需要管理許可權才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   選取執行個體並選取 **[!UICONTROL 開啟歷史記錄]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   您也可以從「工作流程例證」區域暫停、終止或重新命名工作流程。 另請參閱 [管理工作流程](/help/sites-cloud/authoring/workflows/overview.md) 以取得詳細資訊。

1. 有关失败的作业，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 失败]**&#x200B;中显示的“工作流失败”。**[!UICONTROL 工作流失败]**&#x200B;列出所有失败的工作流活动。

   >[!NOTE]
   您需要管理許可權才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   由於上的多個工作流程設定，最終記錄錯誤訊息可能需要很長時間 **[!UICONTROL 重試]**， **[!UICONTROL 重試延遲]**、和 **[!UICONTROL 逾時]** 從 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)例如：
   * Apache Sling工作佇列設定
   * AdobeGranite工作流程外部程式工作處理常式
   * Granite工作流程逾時佇列

   您可以調整 **[!UICONTROL 重試]**， **[!UICONTROL 重試延遲]**、和 **[!UICONTROL 逾時]** 這些設定中的屬性。

1. 有关已完成的工作流，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 存档]**&#x200B;中的可用工作流存档。**[!UICONTROL 工作流存档]**&#x200B;列出了所有已完成的工作流活动。

   >[!NOTE]
   您需要管理許可權才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. 您會收到有關已中止或失敗的工作流程作業的電子郵件通知。 管理員可設定這些電子郵件通知。 另請參閱 [設定電子郵件通知](#configuring-e-mail-notifications).

<!-- EMAIL NOT AVAILABLE IN SKYLINE

#### Configuring e-mail notifications {#configuring-e-mail-notifications}

>[!NOTE]
>
>You may need administrative rights to access the **[!UICONTROL Tools]** menu.

How you configure notification depends on whether you want notifications for YouTube publishing jobs.

* For encoding jobs, you can access the configuration page for all Experience Manager workflow email notifications at **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

For YouTube publishing jobs, do the following:

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Publish to YouTube]**, then select **[!UICONTROL Edit]** on the toolbar.
1. Near the upper-right corner of the Publish to YouTube workflow page, select **[!UICONTROL Edit]**.
1. Hover the mouse pointer on the YouTube Upload component, then select once to display the inline toolbar.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. On the inline toolbar, select the Configuration icon (wrench). Select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. In the YouTube Upload Process - Step Properties dialog box, select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. You can select or clear the following check boxes:

    * Publish Start
    * Publish Failure
    * Publish Completion - includes information on channels and URLs

   Clearing a check box means that you will not receive the specified email notification from the YouTube Publish workflow.

   >[!NOTE]
   >
   >These emails are specific to YouTube and are in addition to the generic workflow email notifications. As a result, you may receive two sets of email notification - the generic notification available in the **[!UICONTROL Day CQ Workflow Email Notification Service]** and one specific to YouTube depending on your configuration settings.

1. When you are finished, near the upper-right corner of the dialog box, select the **[!UICONTROL Done]** icon (check mark).
1. On the Publish to YouTube workflow page, near the upper-right corner, select **[!UICONTROL Sync]**.

-->

## 使用處理設定檔轉碼 {#transcode-video}

[!DNL Experience Manager] as a [!DNL Cloud Service] 可讓您使用處理設定檔進行MP4視訊檔案的基本轉碼。 功能不僅可讓您上傳，也可讓您預覽和縮放MP4視訊檔案。

![在中建立視訊轉碼的處理設定檔 [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*圖：中視訊轉碼的處理設定檔 [!DNL Experience Manager].*

如果您只提供寬度或高度，並將其他欄位保留為空白，則轉譯會維持長寬比。 H.264視訊轉碼器可用於轉碼。

若要使用處理設定檔處理資產，請將設定檔新增至資料夾。 另請參閱 [使用處理設定檔來處理資產](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## 為視訊資產加上註釋 {#annotate-video-assets}

您可以將註解新增至視訊資產。 在註解視訊時，播放器會暫停，讓您在影格上註解。 如需詳細資訊，請參閱 [管理視訊資產](manage-video-assets.md).

>[!NOTE]
視訊資產註解尚不支援MXF視訊格式。

1. 從 [!DNL Assets] 主控台，選取 **[!UICONTROL 編輯]** 以顯示「資產詳細資訊」頁面。
1. 若要播放視訊，請按一下 **[!UICONTROL 預覽]**.
1. 若要為視訊加上註釋，請按一下 **[!UICONTROL 註釋]**. 註解會在視訊中的特定時間（影格）新增。 在註釋時，您可以在畫布上繪圖，並在繪圖中包含註解。 註解會自動儲存。 若要結束註解精靈，請按一下 **[!UICONTROL 關閉]**.
1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。
1. 若要在時間軸中檢視它，請按一下註釋。 若要從時間軸刪除註釋，請按一下 **[!UICONTROL 刪除]**.

## 最佳作法和限制 {#tips-limitations}

* 不含 [!DNL Dynamic Media] 授權，您只能使用處理設定檔來處理MP4檔案。
* 使用處理設定檔轉碼MP4檔案時，適用下列准則和限制：

   * Apple ProRes檔案只能轉碼為最大解析度1080p。
   * 如果來源檔案的位元速率大於200 Mbps，您只能轉碼為最大解析度1080p。
   * 如果來源影格速率>=60 fps，則您可使用的來源檔案大小上限為

      * 4k轉碼為400 MB。
      * 1080p轉碼為800 MB。
      * 720p轉碼為8 GB。
   * 您可以轉碼為4k解析度的最大檔案大小為2.55 GB MP4檔案，解析度為4k、位元速率為12 Mbps和23 fps。

   **另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)

>[!MORELIKETHIS]
* [Dynamic Media影片檔案](/help/assets/dynamic-media/video.md).
* [進一步瞭解處理設定檔的使用、型別和設定](/help/assets/asset-microservices-configure-and-use.md).

