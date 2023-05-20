---
title: 使用使用者對應工具（舊版）
description: 使用使用者對應工具（舊版）
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: 8a258c2c929f9af84a1cde99072291a3e7f6cfc3
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 3%

---

# 使用使用者對應工具（舊版） {#using-user-mapping-tool}

>[!INFO]
>
>本檔案旨在說明該工具的已棄用版本。 如需最新版本的詳細資訊，請參閱 [使用者對應和主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

使用者對應工具使用API，可透過電子郵件查詢AdobeIdentity Management System (IMS)使用者並傳回其IMS ID。 此API要求使用者為其組織建立使用者端ID、使用者端密碼以及存取權或持有人權杖。

## 設定使用者對應工具 {#setting-up-user-mapping}

**先決條件：** 使用者對應要求對應到其IMS ID的每個使用者在其AEM和IMS中的設定檔中都有一個電子郵件地址。  請注意，即使使用者使用電子郵件地址作為使用者ID登入，除非該電子郵件地址也位於設定檔以及IMS中，否則對應無法用於該使用者。

請依照下列步驟進行設定：

1. 導覽至 [Adobe Developer主控台](https://console.adobe.io) 使用您的Adobe ID。
1. 建立新專案或開啟現有專案。
1. 新增API — 按一下 **新增至專案** 並選取 **API**
1. 選擇使用者管理API。  您必須擁有系統管理員許可權才能使用此選項。
1. 建立JWT認證。
1. 產生金鑰組，或上傳公開金鑰（rsa沒有用）。  有一個按鈕， **產生公開/私密金鑰組**，會為您執行此操作。  請務必儲存公開金鑰和私密金鑰。
1. 導覽至「使用者管理API」。
1. 將您的私密金鑰內容貼入文字方塊並按一下，產生存取權杖（或持有人權杖） **產生Token**.
1. 儲存所有這些資訊，例如 **使用者端ID**， **使用者端密碼**， **技術帳戶ID**， **技術帳戶電子郵件**， **組織ID**、和 **存取Token** 安全。

## 存取使用者對映工具的使用者介面 {#user-interface}

「使用者對應工具」已整合至「內容轉移工具」。 您可以從以下位置下載「內容轉移工具」： [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). 如需最新版本的詳細資訊，請參閱 [最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. 選取Adobe Experience Manager並導覽至工具 — > **作業** -> **內容移轉**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. 按一下 **使用者對應** 卡片。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. 按一下 **建立使用者對應設定**.

   >[!NOTE]
   >如果您略過此步驟，在擷取階段將會略過使用者和群組對應。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   填入欄位 **使用者管理API設定**，如下所述。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **組織ID**：輸入要移轉使用者之組織的AdobeIdentity Management System (IMS)組織ID。

      >[!NOTE]
      >若要取得組織ID，請登入 [Admin Console](https://adminconsole.adobe.com/) 和選擇您的組織（在右上角區域），如果您屬於多個組織。 組織ID會位於該頁面的URL中，格式如下 `xx@AdobeOrg`，其中xx為IMS組織ID。  或者，您也可以在以下位置找到組織ID： [Adobe Developer主控台](https://console.adobe.io) 產生存取Token的頁面。

   * **使用者端ID**：輸入您在設定步驟中儲存的使用者端ID。

   * **存取Token**：輸入您從設定步驟儲存的存取Token。

      >[!NOTE]
      >存取Token每24小時過期一次，且需要建立新的Token。 若要建立新Token，請返回 [Adobe Developer主控台](https://console.adobe.io)，選擇您的專案，然後按一下 **使用者管理API** 並將相同的私密金鑰貼入方塊中。

1. 填入欄位後，按一下 **測試設定** 測試與使用者管理API服務的連線。 如果連線成功，您就可以按一下 **儲存** 以儲存設定。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 儲存設定後，選取設定並按一下 **開始使用者對應**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. 按一下 **開始** 從對話方塊開始「使用者對應」程式。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   它顯示 **狀態** 作為 **執行中**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. 使用者對應完成後，請按一下 **結果** 以檢視摘要。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* 使用者對應完成後，您可以使用階層連結導覽回「內容移轉」頁面。 「使用者對應」卡片會顯示狀態和時間戳記。 按一下 **內容轉移** 建立移轉集以執行擷取。 請參閱 [執行內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) 以取得更多詳細資料。


### 繼續使用者對應程式 {#resume-user-mapping-process}

如果「使用者對應」程式由於下列任何原因而停止：

* 選取的使用者 **停止使用者對應**
* 存取Token在程式期間過期，或
* 一些其他原因

   >[!NOTE]
   >進度會從程式停止的位置儲存。

請依照下列步驟繼續使用者對應程式：

1. 按一下 **檢視記錄** 檢閱使用者對應記錄以檢查儲存的進度。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. 按一下 **開始使用者對應** 按鈕以從先前關閉的位置繼續。

   >[!NOTE]
   >在重新啟動之前，請確定存取權杖仍然有效或已重新整理。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. 按一下 **開始** 從對話方塊中繼續使用者對應程式。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   「使用者對應」程式完成後，您將檢視 **狀態** 作為 **已完成** 的特定設定。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
