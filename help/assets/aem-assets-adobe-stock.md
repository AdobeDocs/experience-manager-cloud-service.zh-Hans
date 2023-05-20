---
title: 管理 [!DNL Adobe Stock] 中的資產 [!DNL Assets].
description: 搜尋、擷取、授權和管理 [!DNL Adobe Stock] 資產來源： [!DNL Adobe Experience Manager]. 使用授權資產就像任何其他數位資產一樣。
contentOwner: Vishabh Gupta
feature: Search,Adobe Stock
role: Admin,User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 8%

---

# 使用 [!DNL Adobe Stock] 中的資產 [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/aem-assets-adobe-stock.html?lang=en) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Stock] 此服務可讓設計師和企業存取數百萬張高品質、精選且免版稅的像片、向量、插圖、影片、範本和3D資產，以供其所有創意專案使用。

[!DNL Adobe Stock] 對於企業方案，預設會包含整個組織的共用許可權。 當資產獲得貴組織的使用者授權後，貴組織的其他使用者就可以識別、下載和使用此資產，而無需再次授權。 資產一經貴組織授權，便享有永久的使用權。

組織可以整合其企業 [!DNL Adobe Stock] 計畫方式 [!DNL Experience Manager Assets] 藉由的強大資產管理功能，確保授權資產可廣泛用於其創意和行銷專案 [!DNL Experience Manager]. [!DNL Experience Manager] 使用者可以快速尋找、預覽和授權儲存於的Adobe Stock資產 [!DNL Experience Manager]，而不離開 [!DNL Experience Manager] 介面。

## 整合 [!DNL Experience Manager] 和 [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] 讓使用者能夠搜尋、預覽、儲存和授權 [!DNL Adobe Stock] 資產直接來自 [!DNL Experience Manager].

**前提条件**

集成需要：

* 啟動並執行 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 例項
* 一個 [企業 [!DNL Adobe Stock] 計畫](https://stockenterprise.adobe.com/)
* 具有預設Stock產品設定檔Admin Console許可權的使用者
* 具有開發人員存取設定檔許可權的使用者，可在Adobe Developer Console中建立整合

企業 [!DNL Adobe Stock] 計畫，

* 提供以下專案的產品權益： [!DNL Adobe Stock] (與Experience Manager連結的庫存)
* 購買至的積分 [!DNL Adobe Admin Console] 您股票權益的
* 啟用內的服務帳戶(JWT)驗證 [!DNL Adobe Developer Console] 您股票權益的
* 可讓您從內部管理全域信用額度與授權 [!DNL Adobe Admin Console]

在權利內，的預設產品設定檔 [!DNL Adobe Stock] 存在於 [!DNL Admin Console]. 可以建立多個設定檔，這些設定檔決定誰可以授權Stock資產。 對產品設定檔具有直接存取許可權的使用者可以存取 [https://stock.adobe.com/](https://stock.adobe.com/) 並授權Stock資產。 然而，有其他方法可使用開發人員存取權建立整合(API)。 此整合可驗證以下專案之間的通訊： [!DNL Experience Manager Assets] 和 [!DNL Adobe Stock].

>[!NOTE]
>
>Stock服務帳戶(JWT)驗證隨企業的Stock權益提供。
>
>整合不支援企業庫存權益的Oauth驗證。


<!--
### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->
<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in User Preferences panel. To access the panel from Experience Manager home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.

-->

## 整合步驟 [!DNL Experience Manager] 和 [!DNL Adobe Stock] {#integration-steps}

若要整合 [!DNL Experience Manager] 和 [!DNL Adobe Stock]，請依照列出的順序執行下列步驟：

1. [获取公共证书](#public-certificate)

   在 [!DNL Experience Manager]，建立IMS帳戶並產生公開憑證（公開金鑰）。

1. [建立服務帳戶(JWT)連線](#createnewintegration)

   在 [!DNL Adobe Developer Console]，為您的建立專案 [!DNL Adobe Stock] 組織。 在專案下，使用公開金鑰設定API以建立服務帳戶(JWT)連線。 取得服務帳戶憑證和JWT裝載資訊。

1. [設定IMS帳戶](#create-ims-account-configuration)

   在 [!DNL Experience Manager]，使用服務帳戶憑證和JWT裝載設定IMS帳戶。

1. [配置云服务](#configure-the-cloud-service)

   在 [!DNL Experience Manager]，設定 [!DNL Adobe Stock] 使用IMS帳戶的雲端服務。


### 建立IMS設定 {#create-an-ims-configuration}

IMS設定會驗證您的 [!DNL Experience Manager Assets] 具有的作者執行個體 [!DNL Adobe Stock] 權利。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [設定IMS帳戶](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公開金鑰（憑證）會在Adobe Developer Console中驗證您的產品設定檔。

1. 登入您的 [!DNL Experience Manager Assets] 雲端例項。

1. 從 **[!UICONTROL 工具]** 面板，導覽至 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**.

1. 在Adobe IMS設定頁面中，按一下 **[!UICONTROL 建立]**. 此 **[!UICONTROL Adobe IMS技術帳戶設定]** 頁面隨即開啟。

1. 在 **[!UICONTROL 憑證]** 索引標籤，選取 **[!UICONTROL Adobe Stock]** 從 **[!UICONTROL 雲端解決方案]** 下拉式清單。

1. 您可以建立憑證或針對設定重複使用現有憑證。

   若要建立憑證，請選取 **[!UICONTROL 建立新憑證]** 核取方塊並指定 **別名** 以取得公開金鑰。 別名會作為公開金鑰的名稱。

1. 单击&#x200B;**[!UICONTROL 创建证书]**。然後，按一下 **[!UICONTROL 確定]** 以產生公開金鑰。

1. 按一下 **[!UICONTROL 下載公開金鑰]** 圖示並將公開金鑰(.crt)檔案儲存在電腦上。 公開金鑰稍後會用於設定Brand Portal租使用者的API，以及在Adobe Developer主控台中產生服務帳戶認證。

   单击&#x200B;**[!UICONTROL 下一步]**。

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. 在 **帳戶** 索引標籤中，會建立需要服務帳戶憑證的Adobe IMS帳戶。

   開啟新標籤並 [在Adobe Developer主控台中建立服務帳戶(JWT)連線](#createnewintegration).

### 建立服務帳戶(JWT)連線 {#createnewintegration}

在Adobe Developer Console中，專案和API是在組織層級設定。 設定API會建立服務帳戶(JWT)連線。 有兩種設定API的方法，透過產生金鑰組（私密金鑰和公開金鑰）或透過上傳公開金鑰。 在此範例中，服務帳戶認證是透過上傳公開金鑰產生的。

若要產生服務帳戶認證和JWT裝載：

1. 以系統管理員許可權登入Adobe Developer主控台。 預設URL為 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   確保您已從下拉式清單（組織）中選取正確的IMS組織（庫存權益）。

1. 按一下 **[!UICONTROL 建立新專案]**. 系統會為您的組織建立名稱由系統產生的空白專案。

   按一下 **[!UICONTROL 編輯專案]**. 更新 **[!UICONTROL 專案標題]** 和 **[!UICONTROL 說明]**，然後按一下 **[!UICONTROL 儲存]**.

1. 在 **[!UICONTROL 專案概述]** 標籤，按一下 **[!UICONTROL 新增API]**.

1. 在 **[!UICONTROL 新增API視窗]**，選取 **[!UICONTROL Adobe Stock]**. 单击&#x200B;**[!UICONTROL 下一步]**。

1. 在 **[!UICONTROL 設定API]** 視窗，選取 **[!UICONTROL 服務帳戶(JWT)]** 驗證。 单击&#x200B;**[!UICONTROL 下一步]**。

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. 按一下 **[!UICONTROL 上傳您的公開金鑰]**. 按一下 **[!UICONTROL 選取檔案]** 並上傳您在中下載的公開金鑰（.crt檔案） [取得公開憑證](#public-certificate) 區段。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 驗證公開金鑰並按一下 **[!UICONTROL 下一個]**.

1. 選取預設值 **[!UICONTROL Adobe Stock]** 產品設定檔並按一下 **[!UICONTROL 儲存已設定的API]**.

1. 設定API後，您會重新導向至API概觀頁面。 從左側導覽列於 **[!UICONTROL 認證]**，按一下 **[!UICONTROL 服務帳戶(JWT)]** 選項。 在這裡，您可以檢視認證並執行產生JWT權杖、複製認證詳細資料和擷取使用者端密碼等動作。

1. 從 **[!UICONTROL 使用者端認證]** 標籤，複製 **[!UICONTROL 使用者端ID]**.

   按一下 **[!UICONTROL 擷取使用者端密碼]** 並複製 **[!UICONTROL 使用者端密碼]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. 導覽至 **[!UICONTROL 產生JWT]** 標籤並複製 **[!UICONTROL JWT裝載]** 資訊。

您現在可以將使用者端ID （API金鑰）、使用者端密碼和JWT裝載使用至 [設定IMS帳戶](#create-ims-account-configuration) 在 [!DNL Experience Manager Assets].

### 設定IMS帳戶 {#create-ims-account-configuration}

您必須擁有 [憑證](#public-certificate) 和 [服務帳戶(JWT)認證](#createnewintegration) 以設定IMS帳戶。

若要設定IMS帳戶：

1. 開啟IMS設定並導覽至 **[!UICONTROL 帳戶]** 標籤。 您保持頁面開啟的時間 [取得公開憑證](#public-certificate).

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在 **[!UICONTROL 授權伺服器]** 欄位，輸入URL： [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   在中輸入使用者端ID **[!UICONTROL API金鑰]** 欄位， **[!UICONTROL 使用者端密碼]**、和 **[!UICONTROL 裝載]** （JWT裝載）您複製的時間 [建立服務帳戶(JWT)連線](#createnewintegration).

1. 单击&#x200B;**[!UICONTROL 创建]**。已建立IMS帳戶設定。

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. 選取IMS帳戶設定並按一下 **[!UICONTROL 檢查健康狀態]**.

   按一下 **[!UICONTROL Check]** （在對話方塊中）。 在成功設定時，會出現一則訊息， *已成功擷取權杖*.

   ![健康情況檢查](assets/aem-stock-healthcheck.png)


### 配置云服务 {#configure-the-cloud-service}

若要設定 [!DNL Adobe Stock] 雲端服務：

1. 在 [!DNL Experience Manager] 使用者介面，瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. 在 [!DNL Adobe Stock Configurations] 頁面，按一下 **[!UICONTROL 建立]**.

1. 指定 **[!UICONTROL 標題]** 雲端設定的。

   選取您建立的IMS設定，同時 [設定IMS帳戶](#create-ims-account-configuration).

   從下拉式清單中選取您的地區設定。

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. 单击“**[!UICONTROL 保存并关闭]**”。

   您的 [!DNL Experience Manager Assets] 製作執行個體現在已與 [!DNL Adobe Stock]. 您可以建立多個 [!DNL Adobe Stock] 設定（例如地區設定的設定）。 您現在可以存取、搜尋及授權 [!DNL Adobe Stock] 資產來自 [!DNL Experience Manager] 使用者介面。

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >在整合的這個階段，只有管理員才能存取 [!DNL Adobe Stock] 資產、搜尋Stock資產（使用Omnisearch），並授權 [!DNL Adobe Stock] 資產。
   >
   >管理員可進一步將使用者或群組新增至 [!DNL Adobe Stock] cloud service並授予這些非管理員使用者的許可權 [!DNL Experience Manager] 以存取Stock組態。

1. 若要新增使用者或群組，請選取 [!DNL Adobe Stock] 雲端設定並按一下 **[!UICONTROL 屬性]**.

1. 搜尋以新增您已指派許可權來存取Adobe Stock設定的使用者或群組。 另請參閱 [指派許可權給使用者群組](#assign-permissions-to-group).


## 指派許可權給使用者群組 {#assign-permissions-to-group}

管理員可以建立使用者群組，並將許可權授予特定使用者或群組以存取 [!DNL Adobe Stock] 雲端服務。

以下是使用者搜尋和授權Adobe Stock資產所需的許可權：

* 設定路徑： `/conf/global/settings/stock`
* 特权: `jcr:read`
* 权限类型: `Allow`

您可以建立使用者群組或指派許可權給現有的使用者群組。 許可權可透過以下方式指派： [!DNL Experience Manager Assets] 介面或從 [!DNL User Admin] 主控台。

**若要提供使用者群組的存取權，從 [!DNL Experience Manager]：**

1. 在 [!DNL Experience Manager] 使用者介面，瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 群組]**. 建立使用者群組 [!DNL Adobe Stock].

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 許可權]**.

1. 在左側面板中搜尋使用者群組並新增 **[!UICONTROL 存取控制專案(ACE)]** 適用於Adobe Stock。

   * 設定路徑： `/conf/global/settings/stock`
   * 特权: `jcr:read`
   * 权限类型: `Allow`

   按一下 **[!UICONTROL 新增]**.

   ![user-permissions](assets/aem-stock-user-permissions.png)

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**. 選取 [!DNL Adobe Stock] 雲端設定並按一下 **[!UICONTROL 屬性]**.

1. 將新建立的使用者群組新增至 [!DNL Adobe Stock] 設定。 单击“**[!UICONTROL 保存并关闭]**”。

   ![assign-user](assets/aem-stock-adduser.png)

**若要提供使用者存取許可權，請從 [!DNL User Admin Console]：**

1. 開啟 [!DNL Experience Manager] 使用者Admin Console。 預設URL為 `http://localhost:4502/userdamin`.

1. 在左側面板中，透過輸入 `user_id` 或 `name`. 按兩下以開啟使用者屬性。

1. 導覽至 **[!UICONTROL 許可權]** 定位點並允許 `read` 的許可權 [!DNL Adobe Stock] 雲端設定： `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >如果不允許雲端設定，使用者只能存取 **[!UICONTROL 資產]** 在 [!DNL Experience Manager] 介面。
   >
   >若要允許存取 [!UICONTROL 資產] 和 [!DNL Adobe Stock] assets，確定該雲端設定可供使用者使用。

1. 按一下 **[!UICONTROL 儲存]** 以更新許可權。

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. 將使用者或群組新增至 [!DNL Adobe Stock] 雲端設定。


## 存取Adobe Stock資產 {#access-stock-assets}

非管理員使用者擁有 [!DNL Adobe Stock] 雲端設定可以搜尋並授權 [!DNL Adobe Stock] 資產來自 [!DNL Experience Manager] 介面。

使用者必須執行額外的步驟，才能啟用 [!DNL Adobe Stock] 存取前的雲端設定 [!DNL Adobe Stock] 資產。 此為一次性活動。 如果使用者被指派多個許可權 [!DNL Adobe Stock] 雲端設定，使用者可以從以下位置選取所需的設定： **[!UICONTROL 使用者偏好設定]**.

若要啟用 [!DNL Adobe Stock] 雲端設定：

1. 登入 [!DNL Experience Manager].

1. 從右上角按一下使用者圖示，然後按一下 **[!UICONTROL 我的偏好設定]**. 此 **[!UICONTROL 使用者偏好設定]** 視窗隨即開啟。

1. 選取所需的 **[!UICONTROL Stock設定]** 從下拉式清單中按一下 **[!UICONTROL Accept]** 以啟動設定。

   ![使用者偏好設定](assets/aem-stock-preferences.png)

1. 導覽至 **[!UICONTROL 資產]** > **[!UICONTROL Adobe Stock]**. 您現在可以檢視、搜尋和授權 [!DNL Adobe Stock] 資產。

下表說明使用者許可權在存取時的運作方式 [!DNL Adobe Stock] 資產：

| 用户 | 组 | 权限 | 接受使用者偏好設定中的Stock設定 | 存取資產 | 存取Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| 管理员 | 不适用 | 所有 | 不适用 | 是 | 是 |
| test-doc1 | DAM 用户 | /conf/global/settings/stock/cloud-config | 是 | 是 | 是 |
| test-doc1 | DAM 用户 | /conf/global/settings/stock/cloud-config | 否 | 錯誤：無法載入資料 | 否 |
| test-doc1 | DAM 用户 | **允許**： /conf/global/settings/stock **拒絕**： /cloud-config | Stock設定不可見 | 是 | 否 |

## 使用和管理 [!DNL Adobe Stock] 中的資產 [!DNL Experience Manager] {#usemanage}

使用此功能，組織可允許其使用者使用 [!DNL Adobe Stock] 中的資產 [!DNL Experience Manager Assets]. 從 [!DNL Experience Manager] 使用者介面，使用者可搜尋 [!DNL Adobe Stock] 資產並授權必要的資產。

一次an [!DNL Adobe Stock] 資產授權於 [!DNL Experience Manager]，其使用和管理方式與一般資產類似。 在 [!DNL Experience Manager]，使用者可以搜尋及預覽資產、複製及發佈資產、共用資產 [!DNL Brand Portal]；透過以下方式存取及使用資產： [!DNL Experience Manager] 案頭應用程式；等等。

![搜尋 [!DNL Adobe Stock] 資產並從中篩選結果 [!DNL Adobe Experience Manager] 工作區](assets/adobe-stock-search-results-workspace.png)

**A.**[!DNL Adobe Stock] 搜索与提供 ID 的资产类似的资产。**B.** 搜索与您选择的形状或方向匹配的资产。**C.** 搜索一种或多种受支持的资产类型 **D.** 打开或折叠过滤器窗格 **E.** 在 中授权并保存选定的资产 [!DNL Experience Manager]**F.**[!DNL Experience Manager] 在 中保存带水印的资产 **G.**[!DNL Adobe Stock] 在 网站上浏览与选定资产类似的资产 **H.**[!DNL Adobe Stock] 在 网站上查看选定资产 **I.** 搜索结果中的选定资产数 **J.** 在卡片视图和列表视图之间切换

### 尋找資產 {#find-assets}

您的 [!DNL Experience Manager] 使用者，可以在以下位置搜尋資產： [!DNL Experience Manager] 和 [!DNL Adobe Stock]. 當搜尋位置不限於 [!DNL Adobe Stock]，搜尋結果來自 [!DNL Experience Manager] 和 [!DNL Adobe Stock] 都會顯示。

* 若要搜尋 [!DNL Adobe Stock] 資產，按一下 **[!UICONTROL 導覽]** > **[!UICONTROL 資產]** > **[!UICONTROL 搜尋Adobe Stock]**.

* 若要搜尋中的資產 [!DNL Adobe Stock] 和 [!DNL Experience Manager Assets]，按一下搜尋 ![搜尋](assets/do-not-localize/search_icon.png).

或者，開始輸入 `Location: Adobe Stock` 在搜尋列中選取 [!DNL Adobe Stock] 資產。 [!DNL Experience Manager] 對搜尋的資產提供進階篩選功能，讓使用者能使用篩選器快速鎖定所需的資產，例如支援的資產型別、影像方向和授權狀態。

>[!NOTE]
>
>搜尋來源資產 [!DNL Adobe Stock] 顯示於 [!DNL Experience Manager]. [!DNL Adobe Stock] 資產會擷取並儲存在 [!DNL Experience Manager] 只有在使用者符合以下任一條件時，才儲存庫： [儲存資產](/help/assets/aem-assets-adobe-stock.md#saveassets) 或 [授權並儲存資產](/help/assets/aem-assets-adobe-stock.md#licenseassets). 已儲存在中的資產 [!DNL Experience Manager] 會顯示並反白以方便參照和存取。 此外， [!DNL Stock] 資產會與一些其他中繼資料一起儲存，以指出來源為 [!DNL Stock].

![搜尋中的篩選器 [!DNL Experience Manager] 和醒目提示 [!DNL Adobe Stock] 搜尋結果中的資產](assets/aem-search-filters2.jpg)

### 儲存並檢視必要的資產 {#saveassets}

選取您要儲存的資產 [!DNL Experience Manager]. 按一下 [!UICONTROL 儲存] ，並提供資產的名稱和位置。 未授權資產會以浮水印儲存在本機。

下次搜尋資產時，儲存的資產會以徽章醒目顯示，以表示此類資產可用於 [!DNL Experience Manager Assets].

>[!NOTE]
>
>最近新增的資產會顯示新徽章，而非授權徽章。

### 授權資產 {#licenseassets}

使用者可以授權 [!DNL Adobe Stock] 資產(透過其設定檔的 [!DNL Adobe Stock] 企業計畫。 當您授權資產時，儲存資產時不會加上浮水印，且可用於搜尋和使用 [!DNL Experience Manager Assets].

![授權和儲存的對話方塊 [!DNL Adobe Stock] 中的資產 [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### 存取中繼資料和資產屬性 {#access-metadata-and-asset-properties}

使用者可以存取和預覽中繼資料，包括 [!DNL Adobe Stock] 資產的中繼資料屬性儲存在 [!DNL Experience Manager]，並新增 **[!UICONTROL 授權參考]** 資產的。 不過，授權參考的更新並未在兩者之間同步 [!DNL Experience Manager] 和 [!DNL Adobe Stock] 網站。

使用者可以看到已授權和未授權資產的屬性。

![檢視和存取已儲存資產的中繼資料和授權參考](assets/metadata_properties.jpg)


## 已知限制 {#known-limitations}

* **限制使用者授權的功能無法正常運作**：所有使用者具有 `read` stock設定的許可權可用於搜尋和授權 [!DNL Adobe Stock] 資產。

* **非管理員使用者必須手動啟用 [!DNL Adobe Stock] 雲端設定**：在 **[!UICONTROL 使用者偏好設定]** 視窗， **[!UICONTROL Stock設定]** 顯示 [!DNL Adobe Stock] 雲端設定已啟用，但無法用於非管理員使用者。 使用者必須按一下 **[!UICONTROL Accept]** 按鈕以啟動Stock設定。 如果沒有此步驟，系統會在存取時顯示錯誤訊息 **[!UICONTROL 資產]**.

* **未顯示編輯影像警告**：授權影像時，使用者無法檢查影像是否僅限編輯使用。 為防止可能的誤用，管理員可以從Admin Console關閉編輯資產的存取權。

* **顯示錯誤的授權型別**：可能顯示不正確的授權型別 [!DNL Experience Manager] 資產的。 使用者可以登入 [!DNL Adobe Stock] 網站以檢視授權型別。

* **參考欄位和中繼資料未同步**：當使用者更新授權參考欄位時，授權參考資訊會更新： [!DNL Experience Manager] 但不會在 [!DNL Adobe Stock] 網站。 同樣地，如果使用者更新 [!DNL Adobe Stock] 網站中，更新未同步處理 [!DNL Experience Manager].

<!--
## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations users can work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.
-->

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

<!--
### Find assets {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* To search for assets across [!DNL Adobe Stock] and [!DNL Experience Manager Assets], click search ![search](assets/do-not-localize/search_icon.png).

Alternatively, start typing `Location: Adobe Stock` in the search bar to select [!DNL Adobe Stock] assets. [!DNL Experience Manager] offers advanced filtering capabilities on the searched assets, allowing users to quickly zero-in on the required assets using filters, such as types of supported assets, image orientation, and licensed state.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] assets are fetched and stored in [!DNL Experience Manager] repository only after a user either [saves an asset](/help/assets/aem-assets-adobe-stock.md#saveassets) or [licenses and saves an asset](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Search filters in Experience Manager and highlighted Adobe Stock assets in search results](assets/aem-search-filters2.jpg)

*Figure: Search filters in [!DNL Experience Manager] and highlighted [!DNL Adobe Stock] assets in search results.*

### Save and view the required assets {#saveassets}

Select an asset that you want to save in [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. The unlicensed assets are saved locally with a watermark.

Next time when you search for assets, the saved assets are highlighted with a badge, to indicate that such assets are available in [!DNL Experience Manager Assets].

>[!NOTE]
>
>The recently added assets display a New badge instead of Licensed badge.

### License assets {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. When you license an asset, it is saved without a watermark and is available for searching and using in [!DNL Experience Manager Assets].

![Dialog to license and save Adobe Stock assets in Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figure: Dialog to license and save [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets].*

### Access metadata and asset properties {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

Users can see the properties for both, licensed and unlicensed assets.

![View and access metadata and license references of saved assets](assets/metadata_properties.jpg)

*Figure: View and access metadata and license references of saved assets.*

## Known limitations {#known-limitations}

* **Editorial image warning is not displayed**: When licensing an image, users cannot check if an image is Editorial Use Only. To prevent possible misuse, the administrators can turn off the access to editorial assets from the Admin Console.

* **Wrong license type is displayed**: It is possible that an incorrect license type is displayed in [!DNL Experience Manager] for an asset. Users can log into the [!DNL Adobe Stock] website to see the license type.

* **Reference fields and metadata are not synced**: When a user updates a license reference field, the license reference information is updated in [!DNL Experience Manager] but not on the [!DNL Adobe Stock] website. Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].
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

>[!MORELIKETHIS]
>
>* [有關搭配Experience Manager Assets使用Adobe Stock資產的教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Adobe Stock企業計畫說明](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock常見問題集](https://helpx.adobe.com/stock/faq.html)

