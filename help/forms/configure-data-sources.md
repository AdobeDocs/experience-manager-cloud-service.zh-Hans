---
title: 如何設定資料來源？
description: Experience Manager Forms資料整合可讓您設定並連線至不同的資料來源。 瞭解如何將RESTful Web服務、以SOAP為基礎的Web服務和OData服務設定為資料來源，並使用它們來建立表單資料模型。
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: ac525d2500177229221a5d6f79d2a8feeefe3f06
workflow-type: tm+mt
source-wordcount: '2195'
ht-degree: 2%

---

# 配置数据源 {#configure-data-sources}

![資料整合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 資料整合可讓您設定並連線至不同的資料來源。 下列是支援的現成可用型別：

* 關聯式資料庫 — MySQL、 [!DNL Microsoft SQL Server]， [!DNL IBM DB2]、和 [!DNL Oracle RDBMS]
* RESTful Web服務
* 以SOAP為基礎的網站服務
* OData服務（4.0版）
* Microsoft® Dynamics
* SalesForce
* Microsoft® Azure Blob儲存體

資料整合支援OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)， [使用者端認證](https://oauth.net/2/grant-types/client-credentials/))、基本驗證和API金鑰驗證型別為現成可用，並允許實作自訂驗證以存取Web服務。 設定RESTful、SOAP和OData服務的時間 [!DNL Experience Manager] as a Cloud Service，關聯式資料庫的JDBC和聯結器 [!DNL Experience Manager] 使用者設定檔設定於 [!DNL Experience Manager] 網頁主控台。

## 設定關聯式資料庫 {#configure-relational-database}

### 前提条件

使用設定關聯式資料庫之前 [!DNL Experience Manager] Web主控台設定，必須：
* [透過Cloud Manager API啟用進階網路](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)，因為連線埠預設為停用。
* [在Maven中新增JDBC驅動程式相依性](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies).


### 設定關聯式資料庫的步驟

您可以使用以下專案設定關聯式資料庫： [!DNL Experience Manager] Web主控台設定。 执行以下操作：

1. 前往 [!DNL Experience Manager] Web主控台： `https://server:host/system/console/configMgr`.
1. 尋找 **[!UICONTROL Day Commons JDBC連線集區]** 設定。 點選以在編輯模式中開啟設定。

   ![JDBC聯結器集區](/help/forms/assets/jdbc_connector.png)

1. 在設定對話方塊中，指定您要設定的資料庫詳細資訊，例如：

   * JDBC驅動程式的Java™類別名稱
   * JDBC連線URI
   * 與JDBC驅動程式建立連線的使用者名稱和密碼
   * 在中指定SQL SELECT查詢 **[!UICONTROL 驗證查詢]** 用於驗證來自集區的連線的欄位。 查詢至少必須傳回一列。 根據您的資料庫，指定下列其中一項：
      * 選取1 （MySQL和MS SQL）
      * 選擇1個，雙(Oracle)
   * 資料來源的名稱

   設定關聯式資料庫的範例字串：

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > 參考 [使用JDBC DataSourcePool的SQL連線](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html) 以取得更多詳細資訊。

1. 點選 **[!UICONTROL 儲存]** 以儲存設定。

現在，您可以將已設定的關聯式資料庫與表單資料模型搭配使用。

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties will be available for use in form data model. Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Tap **[!UICONTROL Save]** to save the configuration. -->

## 設定雲端服務設定的資料夾 {#cloud-folder}

設定RESTful、SOAP和OData服務的雲端服務需要雲端服務資料夾的設定。

中的所有雲端服務設定 [!DNL Experience Manager] 已整合至 `/conf` 資料夾位於 [!DNL Experience Manager] 存放庫。 根據預設， `conf` 資料夾包含 `global` 資料夾，您可在其中建立雲端服務設定。 不過，您必須手動為雲端設定啟用它。 您也可以在中建立其他資料夾 `conf` 建立和組織Cloud Service設定。

若要設定雲端服務設定的資料夾：

1. 前往 **[!UICONTROL 「工具」>「一般」>「設定瀏覽器」]**.
   * 請參閱 [設定瀏覽器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) 說明檔案以取得詳細資訊。
1. 請執行以下操作來啟用雲端設定的全域資料夾，或跳過此步驟來建立和設定雲端服務設定的另一個資料夾。

   1. 在 **[!UICONTROL 設定瀏覽器]**，選取 `global` 資料夾並點選 **[!UICONTROL 屬性]**.

   1. 在 **[!UICONTROL 設定屬性]** 對話方塊，啟用 **[!UICONTROL 雲端設定]**.

   1. 點選 **[!UICONTROL 儲存並關閉]** 以儲存設定並結束對話方塊。

1. 在 **[!UICONTROL 設定瀏覽器]**，點選 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定資料夾的標題，然後啟用 **[!UICONTROL 雲端設定]**.
1. 點選 **[!UICONTROL 建立]** 以建立為雲端服務設定啟用的資料夾。

## 設定RESTful Web服務 {#configure-restful-web-services}

RESTful Web服務可使用以下方式描述： [Swagger規格](https://swagger.io/specification/v2/) JSON或YAML格式 [!DNL Swagger] 定義檔案。 若要在中設定RESTful Web服務 [!DNL Experience Manager] as a Cloud Service，請確定您擁有 [!DNL Swagger] 檔案([Swagger 2.0版](https://swagger.io/specification/v2/))或 [!DNL Swagger] 檔案([Swagger 3.0版](https://swagger.io/specification/v3/))或託管檔案的URL上。

### 為Open API規格2.0版設定RESTful服務 {#configure-restful-services-open-api-2.0}

1. 前往 **[!UICONTROL 「工具>Cloud Services>資料來源」]**. 點選以選取您要建立雲端設定的資料夾。

   另請參閱 [設定雲端服務設定的資料夾](configure-data-sources.md#cloud-folder) 以取得為雲端服務設定建立和設定資料夾的資訊。

1. 點選 **[!UICONTROL 建立]** 以開啟 **[!UICONTROL 建立資料來源設定精靈]**. 指定設定的名稱及標題（選擇性），選取 **[!UICONTROL RESTful服務]** 從 **[!UICONTROL 服務型別]** 下拉式清單（選擇性）瀏覽並選取設定的縮圖影像，然後點選 **[!UICONTROL 下一個]**.
1. 指定RESTful服務的下列詳細資料：

   * 選取URL或檔案，從 [!UICONTROL Swagger來源] 下拉式清單，並據此指定 [!DNL Swagger URL] 至[!DNL  Swagger] 定義檔案或上傳 [!DNL Swagger] 從您的本機檔案系統取得的檔案。
   * 根據[!DNL  Swagger] 來源輸入。下列欄位已預先填入值：

      * 配置： REST API使用的傳輸通訊協定。 下拉式清單中所顯示的配置型別數目，取決於 [!DNL Swagger] 來源。
      * 主機：提供REST API之主機的網域名稱或IP位址。 它是必填欄位。
      * 基本路徑：所有API路徑的URL首碼。 此為選用欄位。\
         如有需要，請編輯這些欄位的預先填入值。
   * 選取驗證型別 — 無、OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)， [使用者端認證](https://oauth.net/2/grant-types/client-credentials/))、基本驗證、API金鑰或自訂驗證 — 存取RESTful服務，並相應地提供驗證的詳細資訊。

   如果您選取 **[!UICONTROL API金鑰]** 由於是驗證型別，請指定API金鑰的值。 API金鑰可作為請求標頭或查詢引數傳送。 從以下選項中選取其中一個選項： **[!UICONTROL 位置]** 下拉式清單，並在 **[!UICONTROL 引數名稱]** 欄位中輸入。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 點選 **[!UICONTROL 建立]** 以建立RESTful服務的雲端設定。

### 為Open API規格3.0版設定RESTful服務 {#configure-restful-services-open-api-3.0}

1. 前往 **[!UICONTROL 「工具>Cloud Services>資料來源」]**. 點選以選取您要建立雲端設定的資料夾。

   另請參閱 [設定雲端服務設定的資料夾](configure-data-sources.md#cloud-folder) 以取得為雲端服務設定建立和設定資料夾的資訊。

1. 點選 **[!UICONTROL 建立]** 以開啟 **[!UICONTROL 建立資料來源設定精靈]**. 指定設定的名稱及標題（選擇性），選取 **[!UICONTROL RESTful服務]** 從 **[!UICONTROL 服務型別]** 下拉式清單（選擇性）瀏覽並選取設定的縮圖影像，然後點選 **[!UICONTROL 下一個]**.
1. 指定RESTful服務的下列詳細資料：

   * 選取URL或檔案，從 [!UICONTROL Swagger來源] 下拉式清單，並據此指定 [!DNL Swagger 3.0 URL] 至[!DNL  Swagger] 定義檔案或上傳 [!DNL Swagger] 從您的本機檔案系統取得的檔案。
   * 根據[!DNL  Swagger] 來源輸入，會顯示與目標伺服器的連線資訊。
   * 選取驗證型別 — 無、OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)， [使用者端認證](https://oauth.net/2/grant-types/client-credentials/))、基本驗證、API金鑰或自訂驗證 — 存取RESTful服務，並相應地提供驗證的詳細資訊。

   如果您選取 **[!UICONTROL API金鑰]** 由於是驗證型別，請指定API金鑰的值。 API金鑰可作為請求標頭或查詢引數傳送。 從以下選項中選取其中一個選項： **[!UICONTROL 位置]** 下拉式清單，並在 **[!UICONTROL 引數名稱]** 欄位中輸入。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 點選 **[!UICONTROL 建立]** 以建立RESTful服務的雲端設定。

RESTful服務Open API Specification 3.0版不支援的部分操作包括：
* 回呼
* oneof/anyof
* 遠端參考
* 链接
* 針對單一作業的不同MIME型別，有不同的要求內文

您可參閱 [OpenAPI 3.0規格](https://swagger.io/specification/v3/) 詳細資訊。

### 表單資料模型HTTP使用者端設定以最佳化效能 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 表單資料模型，當整合RESTful Web服務時，因為資料來源包括用於效能最佳化的HTTP使用者端設定。

設定以下屬性 **[!UICONTROL REST資料來源的表單資料模型HTTP使用者端設定]** 設定以指定規則運算式：

* 使用 `http.connection.max.per.route` 屬性來設定表單資料模型和RESTful Web服務之間允許的最大連線數目。 預設值為20個連線。

* 使用 `http.connection.max` 屬性，指定每個路由允許的連線數目上限。 預設值為40個連線。

* 使用 `http.connection.keep.alive.duration` 屬性來指定持續性HTTP連線持續運作的持續時間。 預設值為15秒。

* 使用 `http.connection.timeout` 屬性來指定持續時間，而 [!DNL Experience Manager Forms] 伺服器會等待建立連線。 預設值為10秒。

* 使用 `http.socket.timeout` 屬性，指定兩個資料封包之間閒置的最長時間。 預設值為30秒。

下列JSON檔案會顯示範例：


```json
{   
   "http.connection.keep.alive.duration":"15",   
   "http.connection.max.per.route":"20",   
   "http.connection.timeout":"10",   
   "http.socket.timeout":"30",   
   "http.connection.idle.connection.timeout":"15",   
   "http.connection.max":"40" 
} 
```

1. 點選 **[!UICONTROL REST資料來源的表單資料模型HTTP使用者端設定]**.

1. 在 [!UICONTROL REST資料來源的表單資料模型HTTP使用者端設定] 對話方塊：

   * 指定表單資料模型和RESTful Web服務之間允許的最大連線數。 **[!UICONTROL 連線總數限制]** 欄位。 預設值為20個連線。

   * 指定中每個路由允許的連線數目上限 **[!UICONTROL 每個路由的連線限制]** 欄位。 預設值為兩個連線。

   * 在「 」中指定持續HTTP連線保持連線的持續時間 **[!UICONTROL 保持連線]** 欄位。 預設值為15秒。

   * 指定持續時間，期間為 [!DNL Experience Manager Forms] 伺服器會等待連線建立，在 **[!UICONTROL 連線逾時]** 欄位。 預設值為10秒。

   * 指定中兩個資料封包之間閒置的最長時間 **[!UICONTROL 通訊端逾時]** 欄位。 預設值為30秒。

## 設定SOAP Web服務 {#configure-soap-web-services}

以下說明以SOAP為基礎的Web服務： [Web服務描述語言(WSDL)規格](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] 不支援RPC樣式WSDL模型。

若要在中設定以SOAP為基礎的Web服務 [!DNL Experience Manager] as a Cloud Service，請確定您有Web服務的WSDL URL，並執行下列動作：

1. 前往 **[!UICONTROL 「工具>Cloud Services>資料來源」]**. 點選以選取您要建立雲端設定的資料夾。

   另請參閱 [設定雲端服務設定的資料夾](configure-data-sources.md#cloud-folder) 以取得為雲端服務設定建立和設定資料夾的資訊。

1. 點選 **[!UICONTROL 建立]** 以開啟 **[!UICONTROL 建立資料來源設定精靈]**. 指定設定的名稱及標題（選擇性），選取 **[!UICONTROL SOAP Web服務]** 從 **[!UICONTROL 服務型別]** 下拉式清單（選擇性）瀏覽並選取設定的縮圖影像，然後點選 **[!UICONTROL 下一個]**.
1. 指定SOAP Web服務的下列專案：

   * Web服務的WSDL URL。
   * 服务端点. 在此欄位中指定值，以覆寫WSDL中提到的服務端點。
   * 選取驗證型別 — 無、OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)， [使用者端認證](https://oauth.net/2/grant-types/client-credentials/))、基本驗證或自訂驗證 — 存取SOAP服務，並相應地提供驗證的詳細資訊。

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 點選 **[!UICONTROL 建立]** 建立SOAP Web服務的雲端設定。

### 啟用在SOAP Web服務WSDL中使用匯入陳述式 {#enable-import-statements}

您可以指定一個規則運算式，用來篩選允許在SOAP Web服務WSDL中作為匯入陳述式的絕對URL。 依預設，此欄位中沒有值。 因此， [!DNL Experience Manager] 會封鎖WSDL中可用的所有匯入陳述式。 如果您指定 `.*` 作為此欄位中的值， [!DNL Experience Manager] 允許所有匯入陳述式。

設定 `importAllowlistPattern` 的屬性 **[!UICONTROL 表單資料模型SOAP Web服務匯入允許清單]** 設定以指定規則運算式。 下列JSON檔案會顯示範例：


```json
{
  "importAllowlistPattern": ".*"
}
```


要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)。

## 設定OData服務 {#config-odata}

OData服務由其服務根URL識別。 若要在中設定OData服務 [!DNL Experience Manager] as a Cloud Service，請確定您有服務的服務根URL，然後執行下列動作：

>[!NOTE]
>
> 表單資料模型支援 [OData版本4](https://www.odata.org/documentation/).
>如需設定的逐步指南 [!DNL Microsoft® Dynamics 365]，線上或內部部署，請參閱 [[!DNL Microsoft® Dynamics] OData設定](ms-dynamics-odata-configuration.md).

1. 前往 **[!UICONTROL 「工具>Cloud Services>資料來源」]**. 點選以選取您要建立雲端設定的資料夾。

   另請參閱 [設定雲端服務設定的資料夾](#cloud-folder) 以取得為雲端服務設定建立和設定資料夾的資訊。

1. 點選 **[!UICONTROL 建立]** 以開啟 **[!UICONTROL 建立資料來源設定精靈]**. 指定設定的名稱及標題（選擇性），選取 **[!UICONTROL OData服務]** 從 **[!UICONTROL 服務型別]** 下拉式清單（選擇性）瀏覽並選取設定的縮圖影像，然後點選 **[!UICONTROL 下一個]**.
1. 指定OData服務的下列詳細資料：

   * 要設定之OData服務的服務根URL。
   * 選取驗證型別 — 無、OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)， [使用者端認證](https://oauth.net/2/grant-types/client-credentials/))、基本驗證、API金鑰或自訂驗證 — 存取OData服務，並相應地提供驗證的詳細資訊。

   如果您選取 **[!UICONTROL API金鑰]** 由於是驗證型別，請指定API金鑰的值。 API金鑰可作為請求標頭或查詢引數傳送。 從以下選項中選取其中一個選項： **[!UICONTROL 位置]** 下拉式清單，並在 **[!UICONTROL 引數名稱]** 欄位中輸入。

   >[!NOTE]
   您必須選取要連線的OAuth 2.0驗證型別 [!DNL Microsoft® Dynamics] 使用OData端點作為服務根的服務。

1. 點選 **[!UICONTROL 建立]** 以建立OData服務的雲端設定。

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## 后续步骤 {#next-steps}

您已設定資料來源。 接下來，您可以建立表單資料模型，或者，如果您已建立不含資料來源的表單資料模型，則可以將其與您設定的資料來源建立關聯。 另請參閱 [建立表單資料模型](create-form-data-models.md) 以取得詳細資訊。
