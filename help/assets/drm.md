---
title: Digital Rights Management於 [!DNL Assets]
description: 瞭解如何在中管理已授權資產的資產到期狀態和資訊 [!DNL Experience Manager] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 5%

---

# 數位資產的Digital Rights Management {#digital-rights-management-in-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/drm.html?lang=en) |
| AEM as a Cloud Service | 本文 |

數位資產通常與指定使用條款和使用期間的授權相關聯。 使用 [!DNL Experience Manager] 平台，您可以有效率地管理資產到期資訊和授權資訊。

## 資產有效期 {#asset-expiration}

若要強制執行資產的授權要求，請使用資產到期資訊。 到期資訊可確保已發佈的資產在到期時取消發佈，以防止授權違規。 沒有管理員許可權的使用者無法編輯、複製、移動、發佈和下載過期的資產。

您可以在下列位置檢視資產的到期狀態：

* **卡片檢視**：對於過期的資產，卡片上的旗標會指出資產已過期。
* **清單檢視**：對於已到期的資產， **[!UICONTROL 狀態]** 欄顯示 **[!UICONTROL 已過期]** 橫幅。
* **時間表**：您可以在時間軸中檢視資產的到期狀態。 選取資產，然後選擇「時間軸」。
* **參考邊欄**：您也可以在「 」中檢視資產的到期狀態 **[!UICONTROL 引用]** 邊欄。 它可管理資產到期狀態以及複合資產和參照的子資產、集合和專案之間的關係。

若要檢視資產的參照網頁和複合資產，請遵循下列步驟：

1. 導覽至該資產，選取該資產，然後按一下 ![左側欄內容參考圖示](assets/do-not-localize/content-rail-icon.png). 左側邊欄隨即開啟。
1. 選取 **[!UICONTROL 引用]** 從左側邊欄。
1. 對於已到期的資產， [!UICONTROL 引用] 到期狀態顯示為 **[!UICONTROL 資產已過期]**. 如果資產具有過期的子資產，則 [!UICONTROL 引用] 邊欄顯示狀態 **[!UICONTROL 資產已過期的子資產]**.

### 搜尋過期的資產 {#search-expired-assets}

若要搜尋過期的資產（包括過期的子資產），請遵循下列步驟：

1. 在 [!DNL Assets] 主控台，按一下 **[!UICONTROL 搜尋]** ，然後按下 `Enter`.

1. 按一下「全域導覽」圖示並選取 **[!UICONTROL 到期狀態]** 選項。

1. 選取 **[!UICONTROL 已過期]**. 搜尋結果會顯示過期的資產。

當您選擇 **[!UICONTROL 已過期]** 選項， [!DNL Assets] console只會顯示複合資產所參考的過期資產和子資產。 參考過期子資產的複合資產不會在子資產過期後立即顯示。 相反地，它們會在以下時間後顯示 [!DNL Experience Manager] 會偵測到它們在下次排程器執行時參考過期的子資產。

您可以將已發佈資產的到期日修改為早於目前排程器週期的日期。 然而，排程仍會在下次執行時偵測此類資產為已到期資產，並且 [!DNL Experience Manager] 會在報表中反映狀態。 對於不同時區的使用者，資產的到期日顯示方式不同。

此外，如果錯誤阻止排程器偵測到目前週期中的過期資產，排程器會在下一個週期中重新檢查這些資產，並偵測其過期狀態。

若要啟用 [!DNL Assets] 若要顯示參照的複合資產以及過期的子資產，請設定 **[!UICONTROL Adobe CQ DAM到期通知]** 中的工作流程 [!DNL Experience Manager]. 基於時間的排程器會排程工作，以在特定時間檢查資產是否已過期的子資產。 工作完成後，已過期的子資產和參考資產會在搜尋結果中顯示為已過期。

1. 存取 [!DNL Cloud Manager] 與您的環境相關聯的Git存放庫。
1. 提交名為的檔案 `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` 存放庫中，包含下列內容。

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. 遵循以下指示： [如何在中進行OSGi設定 [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

您可以使用以下屬性來設定排程器：

* A `true` 屬性的值 `cq.dam.expiry.notification.scheduler.istimebased` 啟動排程器。 *屬性的值 `cq.dam.expiry.notification.scheduler.timebased.rule` 是用於定義時間的規則運算式。 上述範例會在00小時起始排程器工作。
* 若 `send_email` 設為 `true`，資產建立者（將特定資產上傳到的人） [!DNL Assets])會在資產過期時收到電子郵件。
* 排程器一個反複專案內過期的資產最大數量是屬性的值 `asset_expired_limit`.
* 若要定期執行工作，請設定屬性的值 `cq.dam.expiry.notification.scheduler.istimebased` 作為 `false` 並設定屬性的值 `cq.dam.expiry.notification.scheduler.period.rule` 以秒為單位的時間。

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## 資產狀態 {#asset-states}

此 [!DNL Assets] 主控台可顯示資產的各種狀態。 根據特定資產的目前狀態，其卡片檢視會顯示描述其狀態的標籤，例如，已過期、已發佈、已核准、已拒絕等。

1. 在 [!DNL Assets] 使用者介面，選取資產。

1. 選取 **[!UICONTROL 發佈]** （從工具列）。 如果您沒有看見 [!UICONTROL 發佈] 選項下，按一下 **[!UICONTROL 更多]** 在工具列上並找到 **[!UICONTROL 發佈]** 選項。

1. 選擇 **[!UICONTROL 發佈]** ，然後關閉確認對話方塊。

1. 結束選取模式。 資產的發佈狀態會顯示在卡片檢視的資產縮圖底部。 在清單檢視中，「已發佈」欄會顯示資產的發佈時間。

1. 若要顯示其資產詳細資訊頁面，請前往 [!DNL Assets] 介面，選取資產並按一下 **[!UICONTROL 屬性]**.

1. 在 [!UICONTROL 進階] 索引標籤中，設定資產的到期日 **[!UICONTROL 過期]** 欄位。

1. 按一下 **[!UICONTROL 儲存]** 然後按一下 **[!UICONTROL 關閉]** 以顯示「資產」主控台。

1. 資產的發佈狀態會指出卡片檢視中資產縮圖底部的過期狀態。 在清單檢視中，資產狀態會顯示為 **[!UICONTROL 已過期]**.

1. 在 [!DNL Assets] 主控台，選取資料夾並在資料夾上建立稽核任務。

1. 稽核及核准/拒絕稽核任務中的資產，然後按一下 **[!UICONTROL 完成]**.

1. 導覽至您建立稽核任務的資料夾。 您核准/拒絕的資產狀態會顯示在卡片檢視的底部。 在清單檢視中，核准和到期狀態會顯示在適當的欄中。

1. 若要根據資產的狀態來搜尋資產，請按一下 **[!UICONTROL 搜尋]** 以顯示搜尋列。

1. 選取 `Return` 並按一下 [!DNL Experience Manager].

1. 在搜尋面板中，按一下 **[!UICONTROL 發佈狀態]** 並選取 **[!UICONTROL 已發佈]** 若要在中搜尋已發佈的資產 [!DNL Assets].

1. 若要搜尋已核准或已拒絕的資產，請選取 **[!UICONTROL 核准狀態]** 並選取適當的選項。

1. 若要根據資產的到期狀態來搜尋資產，請選取 **[!UICONTROL 到期狀態]** 在「搜尋」面板中選取適當的選項。

1. 您也可以根據各種搜尋Facet下的狀態組合來搜尋資產。 例如，您可以搜尋在稽核任務中核准且未過期的已發佈資產。 若要搜尋這類資產，請在搜尋Facet中選取適當的選項。

## Digital Rights Management於 [!DNL Assets] {#digital-rights-management-in-assets-1}

DRM功能強制接受授權合約，然後您才可以從下載授權資產 [!DNL Assets].

如果您選取受保護的資產並按一下 **[!UICONTROL 下載]**，您會重新導向至授權頁面，以接受授權合約。 如果您不接受授權合約，則 **[!UICONTROL 下載]** 選項無法使用。

如果選取範圍包含多個受保護的資產，請一次選取一個資產、接受授權合約，然後繼續下載資產。

若符合下列任一條件，資產即視為受保護：

* 資產中繼資料屬性 `xmpRights:WebStatement` 指向包含資產授權合約的頁面路徑。
* 資產中繼資料屬性的值 `adobe_dam:restrictions` 是指定授權合約的原始HTML。

>[!NOTE]
>
>位置 `/etc/dam/drm/licences` 在舊版中用來儲存授權 [!DNL Experience Manager]. 該位置現已棄用。 如果您建立或修改授權頁面，或移植先前頁面的頁面 [!DNL Experience Manager] 版本、Adobe建議您將這類資產儲存在 `/apps/settings/dam/drm/licenses` 或 `/conf/*/settings/dam/drm/licenses` 位置。

### 下載受DRM保護的資產 {#downloading-drm-assets}

1. 在卡片檢視中，選取您要下載的資產，然後選取 **[!UICONTROL 下載]**.
1. 在&#x200B;**[!UICONTROL 版权管理]**&#x200B;页面，从列表中选择要下载的资产。
1. 在 [!UICONTROL 授權] 窗格，選擇 **[!UICONTROL 同意]**. 資產旁會出現核取標籤。 選取 **[!UICONTROL 下載]** 選項。

   >[!NOTE]
   >
   >此 **[!UICONTROL 下載]** 只有當您選擇同意受保護資產的授權合約時，才會啟用此選項。 但是，如果您的選擇同時包含受保護和不受保護的資產，則只有受保護的資產會列在窗格和 **[!UICONTROL 下載]** 選項可用於下載未受保護的資產。 要同时接受多个受保护资产的许可协议，请从列表中选择资产，然后选择“同 **[!UICONTROL 意”]**。

1. 若要下載資產或其轉譯，請選取「 」 **[!UICONTROL 下載]** 在對話方塊中。

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
