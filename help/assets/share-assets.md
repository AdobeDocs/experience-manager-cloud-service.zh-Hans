---
title: 分發和共用資產、資料夾和集合
description: 使用共用作為連結、下載和透過之類的方法散發您的數位資產 [!DNL Brand Portal]， [!DNL desktop app]、和 [!DNL Asset Link].
contentOwner: Vishabh Gupta
feature: Asset Management, Collaboration, Asset Distribution
role: User, Admin
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 5%

---

# 共用和發佈在中管理的資產 [!DNL Experience Manager] {#share-assets-from-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/link-sharing.html?lang=en) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Experience Manager Assets] 可讓您和組織成員及外部實體（包括合作夥伴和廠商）共用資產、資料夾和集合。 使用下列方法共用資產： [!DNL Experience Manager Assets] as a [!DNL Cloud Service]：

* [以連結形式共用](#sharelink).
* [下載資產](/help/assets/download-assets-from-aem.md) 並分別分享。
* 分享方式： [[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html).
* 分享方式： [[!DNL Adobe Asset Link]](https://www.adobe.com/cn/creativecloud/business/enterprise/adobe-asset-link.html).
* 分享方式： [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html).

## 以链接方式共享资产 {#sharelink}

透過連結共用資產，是讓外部對象、行銷人員和其他人可以使用資源的便利方式 [!DNL Experience Manager] 使用者。 功能可讓匿名使用者存取及下載與其共用的資產。 從共用連結下載資產時， [!DNL Experience Manager Assets] 使用非同步服務，提供更快速且無中斷的下載。 要下載的資產會在背景排入可管理檔案大小的ZIP封存檔中。 對於大型下載，下載會整合到多個檔案中，每個檔案大小為100 GB。

<!--
Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. 
-->

>[!NOTE]
>
>* 您需要對要以連結形式共用的資料夾或資產具有「編輯ACL」許可權。
>* [啟用傳出電子郵件](/help/implementing/developing/introduction/development-guidelines.md#sending-email) 與使用者共用連結之前。


使用連結共用功能共用資產的方式有兩種：

1. 產生共用連結， [複製並共用資產連結](#copy-and-share-assets-link) 與其他使用者整合。 連結的預設到期時間為一天。 與其他使用者共用複製的連結時，您無法變更到期時間。

1. 產生共用連結並 [透過電子郵件共用資產連結](#share-assets-link-through-email). 在此情況下，您可以修改預設值（例如到期日和時間），並允許下載原始資產及其轉譯。 您可以新增使用者的電子郵件地址，以傳送電子郵件給多位使用者。

![連結共用對話方塊](assets/link-sharing-dialog.png)

### 複製並共用資產連結{#copy-and-share-asset-link}

若要以公用URL形式共用資產：

1. 登入 [!DNL Experience Manager Assets] 並導覽至 **[!UICONTROL 檔案]**.
1. 選取資產或包含資產的檔案夾。 在工具列中按一下 **[!UICONTROL 共用連結]**.
1. 此 **[!UICONTROL 連結共用]** 對話方塊隨即出現，其中包含中自動產生的資產連結 **[!UICONTROL 共用連結]** 欄位。
1. 複製資產連結並與使用者共用。

### 透過電子郵件通知共用資產連結 {#share-assets-link-through-email}

若要透過電子郵件共用資產：

1. 選取資產或包含資產的檔案夾。 在工具列中按一下 **[!UICONTROL 共用連結]**.
1. 此 **[!UICONTROL 連結共用]** 對話方塊隨即出現，其中包含中自動產生的資產連結 **[!UICONTROL 共用連結]** 欄位。

   * 在電子郵件地址方塊中，輸入您要共用連結之使用者的電子郵件ID。 您可以與多位使用者共用連結。 如果使用者是您組織的成員，請從下拉式清單中顯示的建議中選取其電子郵件ID。 如果使用者是外部使用者，請輸入完整的電子郵件ID並按 **[!UICONTROL 輸入]**；電子郵件ID會新增至使用者清單。

   * 在 **[!UICONTROL 主旨]** 方塊中，輸入主旨以指定共用資產的用途。
   * 在 **[!UICONTROL 訊息]** 方塊，視需要輸入訊息。
   * 在 **[!UICONTROL 有效期]** 欄位中，使用日期選擇器來指定連結的到期日和時間。
   * 啟用 **[!UICONTROL 允許下載原始檔案]** 核取方塊可允許收件者下載原始轉譯。

1. 按一下 **[!UICONTROL 共用]**. 訊息會確認此連結已與使用者共用。 使用者會收到包含共用連結的電子郵件。

![連結共用電子郵件](assets/link-sharing-email-notification.png)

### 使用資產連結下載資產

任何有權存取共用資產連結的使用者都可以下載zip資料夾中隨附的資產。 無論使用者是存取複製的資產連結，還是使用透過電子郵件共用的資產連結，下載過程都相同。

* 按一下資產連結或在瀏覽器中貼上URL。 此 [!UICONTROL 連結共用] 介面會開啟，您可在其中切換至 [!UICONTROL 卡片檢視] 或 [!UICONTROL 清單檢視].

* 在 [!UICONTROL 卡片檢視]，您可以將滑鼠停留在共用資產或共用資產資料夾上，以選取資產或將它們排入下載佇列。

* 依預設，使用者介面會顯示 **[!UICONTROL 下載收件匣]** 選項。 它反映所有排入下載佇列的共用資產或資料夾的清單及其狀態。

* 選取資產或資料夾時， **[!UICONTROL 將下載排入佇列]** 選項隨即顯示在畫面上。 按一下 **[!UICONTROL 將下載排入佇列]** 啟動下載程式的選項。

   ![將下載排入佇列](assets/queue-download.png)

* 當下載檔案準備就緒時，按一下 **[!UICONTROL 下載收件匣]** 選項以檢視下載狀態。 若下載次數較多，請按一下 **[!UICONTROL 重新整理]** 按鈕以更新狀態。

   ![下載收件匣](assets/link-sharing-download-inbox.png)

* 處理完成後，按一下 **[!UICONTROL 下載]** 按鈕以下載zip檔案。

<!--
You can also copy the auto-generated link and share it with the users. The default expiration time for the link is one day.
-->

>[!NOTE]
>
>如果共用資產移至其他位置，其連結會停止運作。 重新建立連結，並與使用者重新共用。


<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to Experience Manager Assets.

>[!NOTE]
>
>* You need Edit ACL permission on the folder or the asset that you want to share as a link.
>* Before you share a link with users, ensure that Day CQ Mail Service is configured. Otherwise, an error occurs.

1. In the Assets user interface, select the asset to share as a link.
1. From the toolbar, click/tap the **[!UICONTROL Share Link]**.

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. Copy this link and share it with the users. The default expiration time for the link is one day.

   Alternatively, proceed to perform steps 3-7 of this procedure to add email recipients, configure the expiration time for the link, and send it from the dialog.

   >[!NOTE]
   >
   >If a shared asset is moved to a different location, its link stops working. Re-create the link and re-share with the users.

1. From the web console, open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against each:

    * local
    * author
    * publish

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single Experience Manager author instance. For publish, provide the URL for the publish instance.

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. You can also share the link with multiple users.

   If the user is a member of your organization, select the user's email ID from the suggested email IDs that appear in the list below the typing area. For an external user, type the complete email ID and then select it from the list.

   To enable emails to be sent out to users, configure the SMTP server details in [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice).

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words "External User" are prefixed with the email ID of the user.

1. In the **[!UICONTROL Subject]** box, enter a subject for the asset you want to share.
1. In the **[!UICONTROL Message]** box, enter an optional message.
1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. By default, the expiration date is set for a week from the date you share the link.
1. To let users download the original image along with the renditions, select **[!UICONTROL Allow download of original file]**.

   >[!NOTE]
   >
   >By default, users can only download the renditions of the asset that you share as a link.

1. Click **[!UICONTROL Share]**. A message confirms that the link is shared with the users through an email.
1. To view the shared asset, click/tap the link in the email that is sent to the user. The shared asset is displayed in the **[!UICONTROL Adobe Marketing Cloud]** page.

   To toggle to the list view, click/tap the layout icon in the toolbar.

1. To generate a preview of the asset, click/tap the shared asset. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click/tap **[!UICONTROL Parent Folder]** to return to the parent folder.

   >[!NOTE]
   >
   >Experience Manager supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## 分別下載資產和共用 {#download-and-share-assets}

使用者可以下載所需的資產，並在以下位置之外共用這些資產： [!DNL Experience Manager]. 如需詳細資訊，請參閱 [如何搜尋資產](/help/assets/search-assets.md)， [如何下載資產](/help/assets/download-assets-from-aem.md)、和 [如何下載集合](manage-collections.md#download-a-collection)

## 與創意專業人士共用資產 {#share-with-creatives}

行銷人員和業務線使用者可以輕鬆地與他們的創意專業人員共用已核准的資產，使用

* **Experience Manager案頭應用程式**：應用程式可在Windows和Mac上運作。 另請參閱 [案頭應用程式總覽](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html). 若要瞭解任何授權案頭使用者如何輕鬆存取共用資產，請參閱 [瀏覽、搜尋和預覽資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). 桌上型電腦使用者可以建立資產，並與Experience Manager使用者的對應人員共用資產，例如透過上傳新影像。 另請參閱 [使用案頭應用程式上傳資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

* **Adobe資產連結**：創意專業人士可直接從中搜尋和使用資產 [!DNL Adobe InDesign]， [!DNL Adobe Illustrator]、和 [!DNL Adobe Photoshop].

## 配置资产共享 {#configure-sharing}

共用資產的不同選項需要特定設定，且有特定先決條件。

### 設定資產連結共用 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

若要產生您要與使用者共用之資產的URL，請使用連結共用對話方塊。 具有管理員許可權或讀取許可權的使用者： `/var/dam/share` 位置可檢視與其共用的連結。 透過連結共用資產是讓外部對象無需先登入即可使用資源的便利方式 [!DNL Assets].

>[!NOTE]
>
>如果您想要將來自Author例項的連結分享至外部實體，請確定您只公開下列URL `GET` 要求。 封鎖其他URL以確保您的Author執行個體安全無虞。
>
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.
### Configure maximum data size {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, Experience Manager compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. However, in the absence of limits to the amount of data that can be compressed in a ZIP file, huge amounts of data is subjected to compression, which causes out of memory errors in JVM. To secure the system from a potential denial of service attack due to this situation, you can configure the maximum size of the downloaded files. If uncompressed size of the asset exceeds the configured value, asset download requests are rejected. The default value is 100 MB.

1. Click/Tap the Experience Manager logo and then go to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the web console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Save the changes.
-->

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### 啟用案頭動作以搭配案頭應用程式使用 {#desktop-actions}

從 [!DNL Assets] 使用者介面在瀏覽器中，您可以瀏覽資產位置或取出資產，然後在您的案頭應用程式中開啟資產進行編輯。 這些選項稱為案頭動作，要啟用案頭動作，請參閱 [在中啟用案頭動作 [!DNL Assets] 網頁介面](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2).

![啟用案頭動作，以便在使用案頭應用程式時作為捷徑使用](assets/enable_desktop_actions.png)

### 要使用的設定 [!DNL Adobe Asset Link] {#configure-asset-link}

「Adobe資產連結」可簡化創意人員與行銷人員在內容建立過程中的共同作業。 它會連線 [!DNL Adobe Experience Manager Assets] 替換為 [!DNL Creative Cloud] 案頭應用程式 [!DNL Adobe InDesign]， [!DNL Adobe Photoshop]、和 [!DNL Adobe Illustrator]. 此 [!DNL Adobe Asset Link] 面板可讓創意人員存取及修改中儲存的內容 [!DNL Assets] 而不用離開他們最熟悉的創意應用程式。

另請參閱 [如何設定 [!DNL Assets] 以搭配使用 [!DNL Adobe Asset Link]](https://helpx.adobe.com/cn/enterprise/using/configure-aem-assets-for-asset-link.html).

## 最佳作法和疑難排解 {#bestpractices}

* 名稱中包含空白字元的資產資料夾或集合可能無法共用。
* 如果使用者無法下載共用資產，請向您的Experience Manager管理員查詢下載限制是什麼。 預設值為100 MB。
* 若要讓使用者預覽使用連結共用所共用的視訊，該視訊必須具備靜態視訊轉譯，位於 `/jcr:content/renditions` 在存放庫中視訊節點中的位置。 預覽不取決於的可用性 [!DNL Dynamic Media] 轉譯。
* 透過連結共用下載視訊資產時， [!DNL Dynamic Media] 轉譯不會包含在下載的封存檔中。

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your Experience Manager administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
-->

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
