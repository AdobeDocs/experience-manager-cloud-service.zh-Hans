---
title: 为服务器端 API 生成访问令牌
description: 瞭解如何產生安全JWT權杖，以促進第三方伺服器與AEMas a Cloud Service之間的通訊
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: dd869397feca593f93ee8ed5030828e01cc45c4d
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 1%

---

# 为服务器端 API 生成访问令牌 {#generating-access-tokens-for-server-side-apis}

某些架構依賴對AEM的呼叫與AEM基礎架構以外伺服器上託管的應用程式as a Cloud Service。 例如，呼叫伺服器的行動應用程式，接著會向AEM發出as a Cloud Service的API請求。

伺服器對伺服器的流程如下所述，以及簡化的開發流程。 AEMas a Cloud Service [開發人員主控台](development-guidelines.md#crxde-lite-and-developer-console) 用於產生驗證程式所需的權杖。

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## 伺服器對伺服器流量 {#the-server-to-server-flow}

具有IMS組織管理員角色的使用者，也是AEM作者上的AEM使用者或AEM管理員產品設定檔的成員，可以產生一組AEMas a Cloud Service憑證，每個憑證都是JSON裝載，包括憑證（公開金鑰）、私密金鑰和由以下憑證組成的技術帳戶： `clientId` 和 `clientSecret`. 這些認證隨後可由具有AEMas a Cloud Service環境管理員角色的使用者擷取，並應安裝在非AEM伺服器上並仔細視為秘密金鑰。 此JSON格式檔案包含與AEMas a Cloud ServiceAPI整合所需的所有資料。 資料可用來建立已簽署的JWT權杖，該權杖會與AdobeIdentity Management服務(IMS)交換，以取得IMS存取權杖。 然後，可將此存取權杖用作持有者驗證權杖，以向AEM發出as a Cloud Service請求。 憑證中的憑證預設會在一年後到期，但可視需要重新整理，如上所述 [此處](#refresh-credentials).

伺服器對伺服器流程涉及以下步驟：

* 從開發人員控制檯擷取AEMas a Cloud Service認證
* 在呼叫AEM的非AEM伺服器上安裝AEMas a Cloud Service認證
* 產生JWT權杖並使用Adobe的IMS API將該Token交換為存取權杖
* 以存取權杖作為持有者驗證權杖來呼叫AEM API
* 在AEM環境中為技術帳戶使用者設定適當的許可權

### 擷取AEMas a Cloud Service認證 {#fetch-the-aem-as-a-cloud-service-credentials}

有權存取AEMas a Cloud Service開發人員控制檯的使用者將在開發人員控制檯中看到給定環境的整合索引標籤。 具有AEMas a Cloud Service環境管理員角色的使用者可以建立、檢視或管理認證。

按一下 **建立新的技術帳戶** 按鈕，將會建立一組新的認證，其中包含使用者端id、使用者端密碼、私密金鑰、憑證，以及環境製作和發佈層級的設定，不論pod選取範圍為何。

![建立新的技術帳戶](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

新瀏覽器標籤將會開啟，顯示認證。 您可以按狀態標題旁的下載圖示，使用此檢視來下載認證：

![下載認證](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

建立認證後，它們會顯示在 **技術帳戶** 索引標籤中的 **整合** 區段：

![檢視認證](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

使用者稍後可以使用「檢視」動作來檢視認證。 此外，如文章稍後所述，使用者可以建立新的私密金鑰或憑證，以修改相同技術帳戶的認證，以應付憑證需要更新或撤銷的情況。

具有AEMas a Cloud Service環境管理員角色的使用者稍後可以為其他技術帳戶建立新認證。 當不同的API有不同的存取要求時，這會很有用。 例如，讀取與讀寫。

>[!NOTE]
>
>客戶最多可建立10個技術帳戶，包括已刪除的帳戶。

>[!IMPORTANT]
>
>AEM AEM IMS組織管理員（通常是透過Cloud Manager布建環境的相同使用者）必須首先存取開發人員主控台，然後按一下 **建立新的技術帳戶** 按鈕，以便具有AEMas a Cloud Service環境管理員許可權的使用者產生和稍後擷取認證。 如果IMS組織管理員尚未執行此動作，則會出現訊息，通知他們需要IMS組織管理員角色。

### 在非AEM伺服器上安裝AEM服務認證 {#install-the-aem-service-credentials-on-a-non-aem-server}

呼叫AEM的應用程式應能存取AEMas a Cloud Service認證，並將其視為秘密。

### 產生JWT權杖並將其交換為存取權杖 {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

在呼叫Adobe的IMS服務中使用憑證來建立JWT權杖，以擷取有效期為24小時的存取權杖。

可以使用為此目的而設計的使用者端程式庫，將AEM CS服務認證交換為存取權杖。 使用者端程式庫可從以下位置取得： [Adobe的公開GitHub存放庫](https://github.com/adobe/aemcs-api-client-lib)，其中包含更詳細的指引和最新資訊。

```
/*jshint node:true */
"use strict";

const fs = require('fs');
const exchange = require("@adobe/aemcs-api-client-lib");

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

相同交換能以能夠產生具有正確格式的已簽署JWT權杖並呼叫IMS權杖交換API的任何語言執行。

存取權杖將定義其到期時間，通常為24小時。 Git存放庫中有範常式式碼，可用於管理存取權杖並在其過期前重新整理。

>[!NOTE]
>如果有多個認證，請務必參考適當的json檔案，以便稍後叫用對AEM的API呼叫。

### 呼叫AEM API {#calling-the-aem-api}

對AEMas a Cloud Service環境發出適當的伺服器對伺服器API呼叫，包括標頭中的存取權杖。 所以對於「Authorization」標頭，請使用值 `"Bearer <access_token>"`. 例如，使用 `curl`：

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### 在AEM中為技術帳戶使用者設定適當的許可權 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

首先，需要在Adobe Admin Console中建立新產品設定檔。 您可以依照下列步驟完成此操作：

1. 前往Adobe Admin Console，網址為 [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)
1. 按下 **管理** 連結在 **產品和服務** 欄中找出。
1. 選取 **AEMas a Cloud Service**
1. 按下 **新設定檔** 按鈕

   ![新配置文件](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. 為設定檔命名，然後按 **儲存**

   ![儲存設定檔](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. 從設定檔清單中選取您剛建立的設定檔
1. 按下 **新增使用者** 按鈕

   ![添加用户](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. 新增您剛才建立的技術帳戶（在此案例中） `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`)並按 **儲存**

   ![新增技術帳戶](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. 等待10分鐘讓變更生效，並使用從新認證產生的存取權杖對AEM進行API呼叫。 若為cURL命令，其表示方式將與以下範例類似：

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


進行API呼叫後，產品設定檔會在AEMas a Cloud Service作者執行個體中顯示為使用者群組，而適當的技術帳戶會顯示為該群組的成員。

若要檢查此專案，您需要：

1. 登入作者執行個體
1. 前往 **工具** - **安全性** 並按一下 **群組** 卡片
1. 在群組清單中找出您建立的設定檔名稱，然後按一下該名稱：

   ![群組設定檔](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. 在下列視窗中，切換至 **成員** 索引標籤並檢查此處是否正確列出技術帳戶：

   ![「成員」標籤](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


或者，您也可以透過在作者執行個體上執行以下步驟來驗證技術帳戶是否出現在使用者清單中：

1. 前往 **工具** - **安全性** - **使用者**
1. 檢查您的技術帳戶是否為使用者清單，然後按一下它
1. 按一下 **群組** 索引標籤來驗證使用者是否屬於與您的產品設定檔相對應的群組。 此使用者也是其他幾個群組的成員，包括「貢獻者」：

   ![组成员资格](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>在2023年中之前，在可以建立多個憑證之前，未引導客戶在AdobeAdmin Console中建立產品設定檔，因此技術帳戶未與AEMas a Cloud Service執行個體中「貢獻者」以外的群組相關聯。 為了保持一致性，建議您針對此技術帳戶，在Adobe Admin Console中建立如上所述的新產品設定檔，並將現有技術帳戶新增至該群組。

<u>**設定適當的群組許可權**</u>

最後，以所需的適當許可權設定群組，以適當叫用或鎖定API。 您可以透過以下方式執行此操作：

1. 登入適當的作者執行個體並前往 **設定** - **安全性** - **許可權**
1. 在左側窗格中，搜尋與產品設定檔對應的群組名稱（在此案例中是唯讀API），然後按一下它：

   ![搜尋群組](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. 在下列視窗中按一下「編輯」按鈕：

   ![编辑权限](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. 適當地修改許可權，然後按一下 **儲存**

   ![確認編輯許可權](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>若要進一步瞭解AdobeIdentity Management System (IMS)和AEM使用者和群組，請參閱 [檔案](/help/security/ims-support.md).

## 開發人員流程 {#developer-flow}

開發人員可能會想要使用非AEM應用程式的開發執行個體進行測試（在他們的筆記型電腦上執行或託管），這些執行個體會向開發AEMas a Cloud Service開發環境提出要求。 不過，由於開發人員不一定具備IMS管理員角色許可權，因此我們假設他們無法產生一般伺服器對伺服器流程中說明的JWT持有者。 因此，我們為開發人員提供一種機制，以直接產生存取權杖，其可用於對其有權存取的AEMas a Cloud Service環境的請求中。

請參閱 [開發人員指引檔案](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) 以取得使用AEMas a Cloud Service開發人員控制檯所需許可權的相關資訊。

>[!NOTE]
>
>本機開發存取權杖的有效期最長為24小時，之後必須使用相同方法重新產生。

開發人員可使用此代號，從非AEM測試應用程式呼叫AEMas a Cloud Service環境。 開發人員通常會在自己的筆記型電腦上搭配非AEM應用程式使用此代號。 此外，AEM as a Cloud通常是非生產環境。

開發人員流程涉及以下步驟：

* 從開發人員控制檯產生存取權杖
* 使用存取權杖呼叫AEM應用程式。

開發人員也可以對其本機電腦上執行的AEM專案進行API呼叫，這種情況下不需要存取權杖。

### 產生存取權杖 {#generating-the-access-token}

1. 前往 **本機權杖** 在 **整合**
1. 按一下 **取得本機開發權杖** 開發人員控制檯中的按鈕來產生存取權杖。

### 使用存取權杖呼叫AEM應用程式 {#call-the-aem-application-with-an-access-token}

從非AEM應用程式對AEMas a Cloud Service環境發出適當的伺服器對伺服器API呼叫，包括標頭中的存取權杖。 所以對於「Authorization」標頭，請使用值 `"Bearer <access_token>"`.

## 重新整理認證 {#refresh-credentials}

根據預設，AEMas a Cloud Service憑證會在一年後過期。 為確保服務的連續性，開發人員可以選擇重新整理憑證，將其可用性延長一年。

若要達成此目的，您可以：

* 使用 **新增憑證** 按鈕於 **整合** - **技術帳戶** 在開發人員控制檯中，如下所示

   ![認證重新整理](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* 按下按鈕後，將會產生一組憑證，其中包含新的憑證。 在off-AEM伺服器上安裝新憑證，並確保如預期般連線，而不移除舊憑證 
* 產生存取權杖時，請務必使用新憑證而非舊憑證
* 選擇性地撤銷（然後刪除）先前的憑證，使其無法再用來向AEMas a Cloud Service進行驗證。

## 認證撤銷 {#credentials-revocation}

如果私密金鑰受到危害，您需要使用新的憑證和新的私密金鑰來建立憑證。 應用程式使用新認證產生存取權杖後，您可以撤銷和刪除舊憑證。

可执行以下步骤来做到这一点：

1. 首先，新增金鑰。 這將會產生具有新私密金鑰和新憑證的認證。 新的私密金鑰將在UI中標籤為 **目前** 因此，和將用於此技術帳戶日後的所有新憑證。 請注意，與舊版私密金鑰相關聯的認證在撤銷前仍有效。 若要完成此操作，請按三個點(**...**)，然後按 **新增私人金鑰**：

   ![新增私人金鑰](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. 按下 **新增** 出現以下提示時：

   ![確認新增新的私密金鑰](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   將會開啟具有新憑證的新瀏覽標籤，且將會更新UI以顯示兩個私密金鑰，而新私密金鑰會標籤為 **目前**：

   ![UI中的私密金鑰](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. 在非AEM伺服器上安裝新認證，並確保連線正常運作。 請參閱 [伺服器對伺服器流量區段](#the-server-to-server-flow) 以取得如何執行此動作的詳細資訊
1. 撤銷舊憑證。 您可以選取三個點(**...**)並按「 」 **撤銷**：

   ![撤銷憑證](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   然後，在下列提示中按下 **撤銷** 按鈕：

   ![撤銷憑證確認](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. 最後，刪除已遭破壞的憑證。
