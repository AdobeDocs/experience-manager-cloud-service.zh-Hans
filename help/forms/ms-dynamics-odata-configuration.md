---
title: 如何設定 [!DNL Microsoft Dynamics] OData？
description: 瞭解如何根據中定義的實體、屬性和服務建立表單資料模型 [!DNL Microsoft Dynamics] 服務。 表單資料模型可用來建立最適化Forms，並與互動 [!DNL Microsoft Dynamics] 伺服器以啟用業務工作流程。
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 2%

---

# [!DNL Microsoft Dynamics] OData設定 {#microsoft-dynamics-odata-configuration}

![資料整合](assets/data-integeration.png)

[!DNL Microsoft Dynamics] 是客戶關係管理(CRM)和企業資源規劃(ERP)軟體，提供企業解決方案，用於建立和管理客戶帳戶、聯絡人、銷售機會、機會和案例。 [[!DNL Experience Manager Forms] 資料整合](data-integration.md) 提供OData雲端服務設定，將Forms與線上和內部部署整合 [!DNL Microsoft Dynamics] 伺服器。 它可讓您根據中定義的實體、屬性和服務來建立表單資料模型 [!DNL Microsoft Dynamics] 服務。 表單資料模型可用來建立最適化Forms，並與互動 [!DNL Microsoft Dynamics] 伺服器以啟用業務工作流程。 例如：

* 查詢 [!DNL Microsoft Dynamics] 資料伺服器並預先填入Adaptive Forms
* 將資料寫入 [!DNL Microsoft Dynamics] 在最適化表單提交上
* 將資料寫入 [!DNL Microsoft Dynamics] 透過「表單資料模型」中定義的自訂實體（反之亦然）

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  MS Dynamics ODataCloud Service（OData服務）可用於所有執行模式。 有關設定執行模式的詳細資訊 [!DNL Experience Manager] 例項，請參閱 [執行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#runmodes).

## 前提条件 {#prerequisites}

開始設定與設定之前 [!DNL Microsoft Dynamics]，確定您擁有：

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* 已設定 [!DNL Microsoft Dynamics] 365已線上上或安裝下列其中一種執行個體 [!DNL Microsoft Dynamics] 版本：

   * [!DNL Microsoft Dynamics] 365內部部署
   * [!DNL Microsoft Dynamics] 2016年內部部署

* [已註冊以下專案的應用程式： [!DNL Microsoft Dynamics] 線上服務，使用 [!DNL Microsoft Azure] Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). 記下已註冊服務的使用者端ID （也稱為應用程式ID）和使用者端密碼的值。 這些值會用於 [為您的設定雲端服務 [!DNL Microsoft Dynamics] 服務](#configure-cloud-service-for-your-microsoft-dynamics-service).

## 設定已登入的回覆URL [!DNL Microsoft Dynamics] 應用計畫 {#set-reply-url-for-registered-microsoft-dynamics-application}

執行下列動作，設定已登入的回覆URL [!DNL Microsoft Dynamics] 應用：

>[!NOTE]
>
>只有在整合時才能使用此程式 [!DNL Experience Manager Forms] 使用線上 [!DNL Microsoft Dynamics] 伺服器。

1. 前往 [!DNL Microsoft Azure] Active Directory帳戶並在中新增下列雲端服務設定URL **[!UICONTROL 回覆URL]** 已註冊應用程式的設定：

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目錄](assets/azure_directory_new.png)

1. 保存配置。

## 設定 [!DNL Microsoft Dynamics] 若為IFD {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics] 使用宣告型驗證來提供資料存取權，其位置 [!DNL Microsoft Dynamics] CRM伺服器至外部使用者。 若要啟用此功能，請執行以下動作以設定 [!DNL Microsoft Dynamics] 適用於網際網路對向部署(IFD)，並設定宣告設定。

>[!NOTE]
>
>只有在整合時才能使用此程式 [!DNL Experience Manager Forms] 使用內部部署 [!DNL Microsoft Dynamics] 伺服器。

1. 設定 [!DNL Microsoft Dynamics] IFD的內部部署執行個體，如中所述 [設定IFD [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. 使用Windows PowerShell執行以下命令，在啟用IFD時設定宣告設定 [!DNL Microsoft Dynamics]：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   另請參閱 [CRM內部部署的應用程式註冊(IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) 以取得詳細資訊。

## 在AD FS電腦上設定OAuth使用者端 {#configure-oauth-client-on-ad-fs-machine}

執行下列動作，在Active Directory Federation Services (AD FS)電腦上註冊OAuth使用者端並授與AD FS電腦上的存取權：

>[!NOTE]
>
>只有在整合時才能使用此程式 [!DNL Experience Manager Forms] 使用內部部署 [!DNL Microsoft Dynamics] 伺服器。

1. 執行以下命令：

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID` 是您可以使用任何GUID產生器產生的使用者端ID。
   * `redirect-uri` 為的URL [!DNL Microsoft Dynamics] 上的OData雲端服務 [!DNL Experience Manager Forms]. 預設雲端服務已安裝 [!DNL Experience Manager Forms] 部署於下列URL：
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 執行以下命令以授與AD FS電腦上的存取權：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource` 是 [!DNL Microsoft Dynamics] 組織URL。

1. [!DNL Microsoft Dynamics] 使用HTTPS通訊協定。 從下列位置叫用AD FS端點： [!DNL Forms] 伺服器，安裝 [!DNL Microsoft Dynamics] 網站憑證使用到Java憑證存放區 `keytool` 執行的電腦上的命令 [!DNL Experience Manager Forms].

## 為您的設定雲端服務 [!DNL Microsoft Dynamics] 服務 {#configure-cloud-service-for-your-microsoft-dynamics-service}

OData服務由其服務根URL識別。 若要在中設定OData服務 [!DNL Experience Manager] as a Cloud Service，請確定您有服務的服務根URL，然後執行下列動作：

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>如需設定的逐步指南 [!DNL Microsoft Dynamics 365]，線上或內部部署，請參閱 [[!DNL Microsoft Dynamics] OData設定](ms-dynamics-odata-configuration.md).

1. 前往 **[!UICONTROL 「工具>Cloud Services>資料來源」]**. 點選以選取您要建立雲端設定的資料夾。

   另請參閱 [設定雲端服務設定的資料夾](#cloud-folder) 以取得為雲端服務設定建立和設定資料夾的資訊。

1. 點選 **[!UICONTROL 建立]** 以開啟 **[!UICONTROL 建立資料來源設定精靈]**. 指定設定的名稱及標題（選擇性），選取 **[!UICONTROL OData服務]** 從 **[!UICONTROL 服務型別]** 下拉式清單（選擇性）瀏覽並選取設定的縮圖影像，然後點選 **[!UICONTROL 下一個]**.
在 **[!UICONTROL 驗證設定]** 標籤：

   1. 輸入 **[!UICONTROL 服務根目錄]** 欄位。 前往Dynamics執行個體並導覽至 **[!UICONTROL 開發人員資源]** 以檢視「服務根目錄」欄位的值。 例如， https://&lt;tenant-name>/api/data/v9.1/

   1. 選取 **[!UICONTROL OAuth 2.0]** 做為驗證型別。

   1. 取代中的預設值 **[!UICONTROL 使用者端ID]** (也稱為 **應用程式ID**)， **[!UICONTROL 使用者端密碼]**， **[!UICONTROL OAuth URL]**， **[!UICONTROL 重新整理記號URL]**， **[!UICONTROL 存取權杖URL]**、和 **[!UICONTROL 資源]** 包含下列專案之值的欄位： [!DNL Microsoft Dynamics] 服務設定。 您必須在「 」中指定Dynamics執行個體URL **[!UICONTROL 資源]** 要設定的欄位 [!DNL Microsoft Dynamics] 使用表單資料模型。 使用服務根URL衍生動態執行個體URL。 例如， [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. 指定 **[!UICONTROL openid]** 在 **[!UICONTROL 授權範圍]** 授權程式的欄位 [!DNL Microsoft Dynamics].

      ![驗證設定](assets/dynamics_authentication_settings_new.png)
表單資料模型
1. 按一下 **[!UICONTROL 連線到OAuth]**. 您被重新導向至 [!DNL Microsoft Dynamics] 登入頁面。
1. 使用您的登入 [!DNL Microsoft Dynamics] 認證並接受以允許雲端服務設定連線至 [!DNL Microsoft Dynamics] 服務。 在Cloud Service和服務之間建立表單資料模型是一次性工作。

   您是表單資料模型Cloud Service設定頁面，此頁面會顯示OData設定已成功儲存的訊息。

MS Dynamics ODataCloud Service（OData服務）雲端服務已設定，並已與您的Dynamics服務連線。 表單資料模型表單資料模型

## 创建表单数据模型 {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

設定MS Dynamics OData雲端使用者表單資料模型(ce)雲端服務後，您可以在建立表單資料模型時使用該服務。 如需詳細資訊，請參閱 [建立表單資料模型](create-form-data-models.md).

接下來，您可以根據表單資料模型建立最適化表單，並將其用於各種最適化表單使用案例，例如：

* 透過查詢資訊預填調適型表單 [!DNL Microsoft Dynamics] 實體和服務
* 叫用 [!DNL Microsoft Dynamics] 使用最適化表單規則的表單資料模型中定義的伺服器作業
* 將提交的表單資料寫入 [!DNL Microsoft Dynamics] 實體

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

如需在業務工作流程中建立和使用表單資料模型的詳細資訊，請參閱 [資料整合](data-integration.md).
