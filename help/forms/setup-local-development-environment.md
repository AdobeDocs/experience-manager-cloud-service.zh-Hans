---
title: 設定Adobe Experience Manager Formsas a Cloud Service的本機開發環境
description: 設定Adobe Experience Manager Formsas a Cloud Service的本機開發環境
exl-id: 12877a77-094f-492a-af58-cffafecf79ae
source-git-commit: a1b186fec2d6de0934ffebc96967d36a967c044e
workflow-type: tm+mt
source-wordcount: '3042'
ht-degree: 4%

---

# 設定本機開發環境和初始開發專案 {#overview}

當您設定並設定 [!DNL  Adobe Experience Manager Forms] as a [!DNL  Cloud Service] 環境，您可在雲端上設定開發、測試和生產環境。 此外，您也可以設定並設定本機開發環境。

您可以在不登入雲端開發環境的情況下，使用本機開發環境執行下列動作：

* [建立表單](creating-adaptive-form.md) 和相關資產（主題、範本、自訂提交動作等）
* [将 PDF 表单转换为自适应表单](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=zh-Hans)
* 建置要產生的應用程式 [客戶通訊](aem-forms-cloud-service-communications-introduction.md) 依需求或批次模式。

在本機開發執行個體或應用程式準備就緒要產生的最適化表單或相關資產後 [客戶通訊] 準備就緒，您可以從本機開發環境將調適型表單或客戶通訊應用程式匯出到Cloud Service環境，以便進一步測試或移至生產環境。

您也可以在本機開發環境中開發和測試自訂程式碼，例如自訂元件和預填服務。 當自訂計畫碼測試並準備就緒時，您可以使用Cloud Service開發環境的Git存放庫來部署自訂計畫碼。

若要設定新的本機開發環境並使用它來開發活動，請依下列順序執行下列動作：

* [設定開發工具](#setup-development-tools-for-AEM-projects)

* [設定本機作者和發佈執行個體](#set-up-local-experience-manager-environment-for-development)

* [將Forms封存新增至本機開發執行個體並設定使用者](#add-forms-archive-configure-users)

* [設定微服務的本機開發環境](#docker-microservices)

* [設定開發專案](#forms-cloud-service-local-development-environment)

* [設定本機Dispatcher工具](#setup-local-dispatcher-tools)

<!--
You can use the local development environment to create and test Adaptive Forms without connecting to the Cloud Service. [!DNL AEM Forms] provides an SDK to help test all the cloud-ready functionalities on the local development environment. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can also develop and test custom code like custom components and prefill service on the local development environment. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code. 

>[!NOTE]
>
> Pre-pilot release does not support using an [!DNL AEM Forms] as a Cloud Service development instance to create forms. You can create forms, related assets, and custom code only on a local development environment.-->

<!--
You configure two types of development environments:

* **[!DNL AEM Forms] as a Cloud Service development environment:** Use the [[!DNL AEM Forms] as a Cloud Service](setup-forms-cloud-service.md) environment to store, manage, and publish Adaptive Forms and related assets. Do not use an [!DNL AEM Forms] as a Cloud Service environment to create Adaptive Forms and related assets <!--, form-centric workflows, a form data model, or to generate a Document of Record. -->

<!--
* **Local development environment:** You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. 
Use a local development environment:
    
    * To create forms and related assets (themes, templates, custom Submit Actions, and more) and convert PDF forms to Adaptive Forms. After an Adaptive Form or related assets are ready on the local development instance, you can export the Adaptive Form and related assets from the local development environment to an [!DNL AEM Forms] as a Cloud Service development environment for publishing.  
    
    * To update configuration settings and develop and test custom code like custom components and prefill service. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code.  

You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can use the [development tools](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/dev-tools.html) to write custom code, customize or create new Adaptive Forms components, create a custom prefill service, or modify default configurations of an [!DNL AEM Forms] as a Cloud Service instance. 

-->

## 前提条件

您需要下列軟體來設定本機開發環境。 開始設定本機開發環境之前，請先下載這些專案：

| 軟體 | 描述 | 下載連結 |
|---|---|---|
| ADOBE EXPERIENCE MANAGER AS A CLOUD SERVICE SDK | SDK包含 [!DNL Adobe Experience Manager] QuickStart和Dispatcher工具 | 從下載最新的SDK [Software Distribution](#software-distribution) |  |
| Adobe Experience Manager Forms功能封存(AEM Forms附加元件) | 建立、調整樣式及最佳化最適化Forms和其他Adobe Experience Manager Forms功能的工具 | 下載來源 [Software Distribution](#software-distribution) |
| （選用） Adobe Experience Manager Forms參考內容 | 建立、調整樣式及最佳化最適化Forms和其他Adobe Experience Manager Forms功能的工具 | 下載來源 [Software Distribution](#software-distribution) |
| （選用） Adobe Experience Manager Forms Designer | 建立、調整樣式及最佳化最適化Forms和其他Adobe Experience Manager Forms功能的工具 | 下載來源 [Software Distribution](#software-distribution) |

### 從Software Distribution下載最新版本的軟體 {#software-distribution}

若要下載最新版Adobe Experience Manager as a Cloud Service SDK、Experience Manager Forms功能封存(AEM Forms附加元件)、表單參考資產或Forms Designer，請前往 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)：

1. 登入 <https://experience.adobe.com/#/downloads> 使用您的Adobe ID

   >[!NOTE]
   >
   > 您的Adobe組織必須布建為AEMas a Cloud Service，才能下載AEMas a Cloud ServiceSDK。

1. 導覽至 **[!UICONTROL AEMas a Cloud Service]** 標籤。
1. 依發佈日期遞減排序。
1. 按一下最新的Adobe Experience Manager as a Cloud Service SDK、Experience Manager Forms功能封存(AEM Forms附加元件)、表單參考資產或Forms Designer。
1. 檢閱並接受EULA。 點選 **[!UICONTROL 下載]** 按鈕。

## 設定AEM專案的開發工具 {#setup-development-tools-for-AEM-projects}

Adobe Experience Manager Forms專案是自訂程式碼基底。 它包含透過Cloud Manager部署的程式碼、設定和內容 [!DNL Adobe Experience Manager] as a Cloud Service。 此 [AEM專案Maven原型](https://github.com/adobe/aem-project-archetype) 提供專案的基準線結構。

設定下列開發工具，以用於 [!DNL Adobe Experience Manager] 開發專案：

* [Java™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up)
* [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git)
* [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js)
* [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven)

如需設定上述開發工具的詳細指示，請參閱 [設定開發工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html).

## 設定本機開發Experience Manager環境

Cloud ServiceSDK提供QuickStart檔案。 它執行本機版本的Experience Manager。 您可以在本機執行Author或Publish執行個體。

雖然QuickStart提供本機開發體驗，但並沒有提供所有功能 [!DNL Adobe Experience Manager] as a Cloud Service。 因此，務必使用測試您的功能和程式碼 [!DNL Adobe Experience Manager] 將功能移至中繼或生產環境之前，需要as a Cloud Service的開發環境。

若要安裝並設定本機Experience Manager環境，請執行下列步驟：

* [下載並解壓縮](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 此 [!DNL Adobe Experience Manager] AS A CLOUD SERVICESDK
* [設定作者執行個體](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-author-service)
* [設定發佈執行個體](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-publish-service)

## 將Forms封存新增至本機作者和發佈執行個體，並設定Forms專屬的使用者 {#add-forms-archive-configure-users}

請依照所列順序執行下列步驟，將Forms封存新增至Experience Manager執行個體，並設定表單特定使用者：

### 安裝最新的Forms附加功能封存 {#add-forms-archive}

Adobe Experience Manager Formsas a Cloud Service功能封存提供在本機開發環境中建立、樣式化和最佳化Adaptive Forms的工具。 安裝套件以建立最適化表單，並使用的各種其他功能 [!DNL AEM Forms]. 若要安裝套件：

1. 下載並解壓縮最新版本 [!DNL AEM Forms] 適用於您作業系統的封存來源： [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

1. 導覽至crx-quickstart/install目錄。 如果資料夾不存在，請建立它。

1. 停止您的AEM執行個體，將 [!DNL AEM Forms] 附加功能封存， `aem-forms-addon-<version>.far`，然後重新啟動執行個體。

### 設定使用者和許可權 {#configure-users-and-permissions}

建立使用者，例如表單開發人員和表單從業者，以及 [將這些使用者新增至預先定義的表單群組](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=en#accessing) 以向他們提供必要許可權。 下表列出所有型別的使用者以及每種型別表單使用者的預先定義群組：

| 使用者型別 | AEM群組 |
|---|---|
| 表單從業者/ | [!DNL forms-users] (AEM Forms使用者)， [!DNL template-authors]， [!DNL workflow-users]， [!DNL workflow-editors]、和 [!DNL fdm-authors] |
| 表單開發人員 | [!DNL forms-users] (AEM Forms使用者)， [!DNL template-authors]， [!DNL workflow-users]， [!DNL workflow-editors]、和 [!DNL fdm-authors] |
| 客戶體驗領導者或UX設計人員 | [!DNL forms-users]、[!DNL template-authors] |
| AEM 管理员 | [!DNL aem-administrators]、[!DNL fd-administrators] |
| 一般使用者 | 當使用者必須登入才能檢視並提交最適化表單時，請將這類使用者新增到 [!DNL forms-users] 群組。 </br> 當不需要使用者驗證即可存取Adaptive Forms時，請勿將任何群組指派給這類使用者。 |

<!--  

## Set up a local AEM instance for development

Perform the following steps in the listed order to set up and configure your local development environment:

1. **Set up an AEM author instance:** You require an author instance to create Adaptive Forms. Download and extract the latest AEM SDK archive. Run the quick start file in author run mode to set up an author instance. For detailed instructions, see [default local instance](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html).  

1. **Install the latest [!DNL AEM Forms] add-on feature archive:** [!DNL AEM Forms] add-on feature archive provides tools to create, style, and optimize Adaptive Forms on the local development environment. Install the package to create an Adaptive Form and use various other features of [!DNL AEM Forms]. To install the package:

    1. Download and extract the latest [!DNL AEM Forms] archive for your operating system from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

    1. Navigate to the crx-quickstart/install directory. If the folder does not exist, create it.

    1. Stop your Cloud ready AEM instance, place the [!DNL AEM Forms] add-on feature archive, `aem-forms-addon-<version>.far`,  in the install folder, and restart the instance.

1. **Configure users and permissions:** Create users like Form Developer and Form Practitioner a nd add these users to pre-defined forms group to provide them required permissions. The table below lists all types of users and pre-defined groups for each type of forms users:
  
    | User Type | AEM Group |
    |---|---|
    | Form Practitioner  | forms-users (AEM Forms Users), template-authors  |
    | Form Developer | forms-users (AEM Forms Users), template-authors |
    | End-User| everyone* |

    `*` When a user should log in to access or submit Adaptive Forms, add such users to the everyone group.  -->

<!--    
### Set up an AEM project for the development tasks related to local AEM 6.5.5 Forms instance

Use this project to update configurations, create overlays, develop custom Adaptive Form components, and custom code using the local development environment. To set up the project:

1. **Install and configure Maven and set up an AEM project based on Apache Maven:** Apache Maven is an open-source tool for managing software projects. It helps automate builds and provides quality project information. It is the recommended build management tool for AEM projects. For detailed instructions to set up an AEM project based on Apache Maven, see [How to Build AEM Projects using Apache Maven](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/ht-projects-maven.html).

1. Configure the project to use [uber-jar](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=en#install-aem-forms-jee-installer) version 6.5.5 or later and [[!DNL AEM Forms] Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/) version 6.0.160 or later.  

1. **Set Up an Integrated Development Environment:**  Set up an IDE of your choice for development, see [Set Up an Integrated Development Environment](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) for detailed instructions.
 -->

## 設定記錄檔案(DoR)的本機開發環境{#docker-microservices}

AEM Forms as a Cloud Services提供以Docker為基礎的SDK環境，以便更輕鬆地開發記錄檔案並使用其他微服務。 它可讓您無須手動設定平台特定的二進位檔和改寫專案。 若要設定環境：

1. 安裝和配置Docker：

   * (適用於Microsoft® Windows)安裝 [Docker案頭](https://www.docker.com/products/docker-desktop). 它會設定 `Docker Engine` 和 `docker-compose` 在您的電腦上。

   * (Apple macOS)安裝 [適用於Mac的Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac). 它包括Docker引擎、Docker CLI客戶端、Docker撰寫、Docker內容信任、Kubernetes和Credential Helper。

   * (適用於Linux®)安裝 [Docker引擎](https://docs.docker.com/engine/install/#server) 和 [Docker撰寫](https://docs.docker.com/compose/install/) 在您的電腦上。
   >[!NOTE]
   >
   > * 對於Apple macOS，允許列出包含本機AEM作者執行個體的資料夾。
   >
   > * Docker Desktop for Windows支援兩個後端，Hyper-V
      > （舊版）和WSL2 （新版）。 檔案共用已自動完成
      > 使用WSL2 （現代化）時由Docker管理。 您必須
      > 使用Hyper-V （舊版）時明確設定檔案共用。


1. 建立與作者和發佈執行個體平行的資料夾（例如aem-sdk）。 例如C:\aem-sdk。

1. 擷取 `aem-forms-addon-<version>.zip\aem-forms-addon-native-<version>.zip` 檔案。

   ![擷取的aem forms附加於原生](assets/microservice-docker.png)

1. 建立環境變數AEM_HOME，並指向本機AEM Author安裝。 例如C:\aem\author\。

1. 開啟sdk.bat或sdk.sh進行編輯。 將AEM_HOME設定為指向本機AEM Author安裝。 例如C:\aem\author\。

1. 開啟命令提示字元並導覽至 `aem-forms-addon-native-<version>` 資料夾。

1. 確保您的本機AEM Author執行個體已啟動並執行。 執行以下命令以啟動SDK：

   * (在Microsoft® Windows上) `sdk.bat start`
   * (在Linux®或Apple macOS上) `AEM_HOME=[local AEM Author installation] ./sdk.sh start`

   >[!NOTE]
   >
   > 如果您已在sdk.sh檔案中定義環境變數，則可選擇在命令列指定該變數。 提供在命令列定義環境變數的選項，以在不更新shell指令碼的情況下執行命令。

   ![start-sdk-command](assets/start-sdk.png)

您現在可以使用本機開發環境來呈現記錄檔案。 若要測試，請上傳XDP檔案至您的環境並加以呈現。 例如， <http://localhost:4502/libs/xfaforms/profiles/default.print.pdf?template=crx:///content/dam/formsanddocuments/cheque-request.xdp> 將XDP檔案轉換為PDF檔案。

## 根據Experience Manager原型設定Forms的開發專案 {#forms-cloud-service-local-development-environment}

使用此專案在本機建立最適化Forms、部署設定更新、覆蓋、建立自訂最適化表單元件、測試和自訂程式碼 [!DNL Experience Manager Forms] SDK. 在本機測試後，您可以將專案部署至  [!DNL Experience Manager Forms] as a Cloud Service的生產和非生產環境。 部署專案時，也會部署下列AEM Forms資產：

| 主题 | 模板 | 表单数据模型 |
---------|----------|---------
| Canvas 3.0 | 基本 | Microsoft® Dynamics 365 |
| 寧靜 | 空白 | Salesforce |
| 城市 |  |  |
| Ultraminary |  |  |
| Beryl |  |  |

>[!NOTE]
>
> 設定AEM Archetype 30版或更新版本的專案，以取得並使用Microsoft® Dynamics 365和Salesforce表單資料模型搭配AEM Formsas a Cloud Service。
設定AEM Archetype 32版或更新版本的專案，以透過AEM Formsas a Cloud Service取得和使用Tranquil、Urbane和Ultraminary主題。

若要設定專案：

1. **在本機開發執行個體上複製Cloud Manager Git存放庫：**  您的Cloud Manager Git存放庫包含預設的AEM專案。 它根據 [AEM原型](https://github.com/adobe/aem-project-archetype/). 使用Cloud Manager UI中的自助Git帳戶管理來複製您的Cloud Manager Git存放庫，將專案帶到您的本機開發環境中。 如需存取存放庫的詳細資訊，請參閱 [存取存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

<!-- 1. 
After the repository is cloned, [integrate your Git repo with Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)

**Make cloned AEM project compatible with [!DNL AEM Forms] as a Cloud Service:** Remove uber-jar and other non-cloud dependencies from the pom.xml files of the project. You can refer the pom.xml files of the [sample AEM project](assets/FaaCSample.zip) for the list of required dependencies and update your AEM project accordingly. You can also refer [AEM Project Structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html) to learn changes required to make an AEM project compatible with AEM as a Cloud Service.  -->

1. **建立 [!DNL Experience Manager Forms] as a [Cloud Service] 專案：** 建立 [!DNL Experience Manager Forms] as a [Cloud Service] 根據最新版本的專案 [AEM原型](https://github.com/adobe/aem-project-archetype) 或更新版本。 原型可協助開發人員輕鬆開始開發 [!DNL AEM Forms] as a Cloud Service。 其中也包含一些範例主題和範本，可幫助您快速入門。

   開啟命令提示字元並執行以下命令以建立 [!DNL Experience Manager Forms] as a Cloud Service專案。

   ```shell
   mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="41" -D appTitle=mysite -D appId=mysite -D groupId=com.mysite -D includeFormsenrollment="y" -D aemVersion="cloud"
   ```

   變更 `appTitle`， `appId`、和 `groupId` 以反應您的環境。 此外，請將includeFormsenrollment、includeFormscommunications和includeFormsheadless的值設定為 `y` 或 `n` 視您的授權和需求而定。 includeFormsheadless是根據核心元件建立最適化Forms時的必要專案。

   * 使用 `includeFormsenrollment=y` 此選項可包含Forms的特定設定、主題、範本、核心元件，以及建立Adaptive Forms所需的相依性。 如果您使用Forms入口網站，請將 `includeExamples=y` 選項。 它也會將Forms Portal核心元件新增至專案。

   * 使用 `includeFormscommunications=y` 包含Forms核心元件的選項，以及包含客戶通訊功能所需的相依性。

1. 將專案部署到您的本機開發環境。 您可以使用以下命令來部署到您的本機開發環境

   `mvn -PautoInstallPackage clean install`

   如需完整的命令清單，請參閱 [建置和安裝](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [將程式碼部署至您的 [!DNL AEM Forms] as a Cloud Service環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## 設定本機Dispatcher工具 {#setup-local-dispatcher-tools}

Dispatcher是Apache HTTP Web伺服器模組，在CDN和AEM Publish層級之間提供安全和效能層。 Dispatcher是整體Experience Manager架構不可或缺的一部分，並應成為本機開發環境的一部分。

執行以下步驟來設定本機Dispatcher，然後向其新增Forms特定規則：

### 設定本機傳送器 {#setup-local-dispatcher}

此 [!DNL Experience Manager] as a Cloud ServiceSDK包含建議的Dispatcher工具版本，可促進本機設定、驗證和模擬Dispatcher。 Dispatcher工具以Docker為基礎，並提供命令列工具，將Apache HTTP Web Server和Dispatcher設定檔案傳輸為相容的格式，並將其部署到Docker容器中執行的Dispatcher。

Dispatcher上的快取允許 [!DNL AEM Forms] 以在使用者端預先填入Adaptive Forms。 它改善了預填表單的演算速度。

如需設定Dispatcher的詳細指示，請參閱 [設定本機Dispatcher工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#local-development-environment-set-up)

### 將Forms特定規則新增至Dispatcher {#forms-specific-rules-to-dispatcher}

執行以下步驟，為Experience Manager Formsas a Cloud Service設定Dispatcher快取：

1. 開啟您的AEM專案並導覽至 `\src\conf.dispatcher.d\available_farms`
1. 建立 `default.farm` 檔案。 例如：`forms.farm`。
1. 開啟新建立的 `forms.farm` 檔案來編輯和取代下列程式碼：

   ```json
   #/ignoreUrlParams {
   #/0001 { /glob "*" /type "deny" }
   #/0002 { /glob "q" /type "allow" }
   #}
   ```

   替换为

   ```json
   /ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   /0002 { /glob "dataRef" /type "allow" }
   }
   ```

1. 儲存並關閉您的檔案。
1. 前往 `conf.d/enabled_farms` 並建立指向 `forms.farm` 檔案。
1. 編譯專案並將其部署至您的 [!DNL AEM Forms] as a Cloud Service環境。

### 關於快取的考量事項 {#considerations-about-caching}

* Dispatcher快取允許 [!DNL AEM Forms] 以在使用者端預先填入Adaptive Forms。 它改善了預填表單的演算速度。
* 預設會停用快取安全內容功能。 若要啟用此功能，您可以執行 [快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=en) 文章
* Dispatcher可能無法讓某些最適化Forms和相關的最適化Forms失效。 若要解決這類問題，請參閱 [[!DNL AEM Forms] 快取](troubleshooting-caching-performance.md) 在疑難排解一節中。
* 快取本地化的最適化Forms：
   * 使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求最適化表單的當地語系化版本，而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * 瀏覽器地區設定選項預設為停用。 若要變更瀏覽器地區設定，
* 當您使用URL格式時 `http://host:port/content/forms/af/<adaptivefName>.html`，且在Configuration Manager中使用瀏覽器地區設定已停用，則會提供最適化表單的非當地語系化版本。 非當地語系化語言是開發最適化表單時使用的語言。 系統不會考量為瀏覽器設定的地區設定（瀏覽器地區設定），而是提供最適化表單的非當地語系化版本。
* 當您使用URL格式時 `http://host:port/content/forms/af/<adaptivefName>.html`，且啟用「在Configuration Manager中使用瀏覽器地區設定」 ，就會提供最適化表單的當地語系化版本（如果有的話）。 本地化的最適化表單的語言取決於為您的瀏覽器設定的地區設定（瀏覽器地區設定）。 這可能導致 [僅快取最適化表單的第一個例項]. 若要防止執行個體發生問題，請參閱 [僅快取最適化表單的第一個例項](troubleshooting-caching-performance.md) 在疑難排解一節中。

您的本機開發環境已準備就緒。

## 為現有AEM原型專案啟用最適化Forms核心元件 {#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project}

如果您使用AEM Formsas a Cloud Service的AEM Archetype版本40或更新版程式，核心元件將自動為您的環境啟用。 在为您的环境启用核心组件时，即将&#x200B;**自适应表单（核心组件）**&#x200B;模板和画布主题添加到您的环境。如果您的 AEM SDK 版本低于 2023.02.0，请[确保在您的环境上启用 `prerelease` 标志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features)，因为自适应表单核心组件是 2023.02.0 发布之前预发布的一部分。

若要根據舊版Archetype為您的AEM Formsas a Cloud Service環境啟用最適化Forms核心元件，請在您的專案中內嵌WCM核心元件範例成品和Forms核心元件成品（包括範例）：

1. 以純文字程式碼編輯器開啟AEM Archetype專案資料夾。 例如，VS程式碼。

1. 開啟頂層 `.pom` AEM檔案（父系pom），將以下屬性新增至檔案並儲存。

   ```XML
   <properties>
       <core.forms.components.version>2.0.4</core.forms.components.version> <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
       <core.wcm.components.version>2.21.2</core.wcm.components.version>
   </properties>
   ```

   適用於最新版本的 `core.forms.components` 和 `core.wcm.components`，檢查 [核心元件檔案](https://github.com/adobe/aem-core-forms-components).

1. 在頂層（父系）的相依性區段中 `pom.xml` 檔案中，新增下列相依性：

   ```XML
       <!-- WCM Core Component Examples Dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <version>${core.wcm.components.version}</version>
               <type>zip</type>
           </dependency>    
           <!-- End of WCM Core Component Examples Dependencies -->
            <!-- Forms Core Component Dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
     <!-- End of AEM Forms Core Component Dependencies -->
   ```

1. 開啟 `all/pom.xml` 檔案並將下列相依性新增至 `embedded` 區段以將Adaptive Forms核心元件成品新增至AEM Archetype專案：

   ```XML
       <!-- WCM Core Component Examples Dependencies -->
   
           <!-- inside plugin config of filevault-package-maven-plugin -->  
           <!-- embed wcm core components examples artifacts -->
   
           <embedded>
           <groupId>com.adobe.cq</groupId>
           <artifactId>core.wcm.components.examples.ui.apps</artifactId>
           <type>zip</type>
           <target>/apps/${appId}-vendor-packages/content/install</target>
           </embedded>
           <embedded>
           <groupId>com.adobe.cq</groupId>
           <artifactId>core.wcm.components.examples.ui.content</artifactId>
           <type>zip</type>
           <target>/apps/${appId}-vendor-packages/content/install</target>
            </embedded>
           <embedded>
           <groupId>com.adobe.cq</groupId>
           <artifactId>core.wcm.components.examples.ui.config</artifactId>
           <type>zip</type>
           <target>/apps/${appId}-vendor-packages/content/install</target>
           </embedded>
           <!-- embed forms core components artifacts -->
           <embedded>
           <groupId>com.adobe.aem</groupId>
           <artifactId>core-forms-components-af-apps</artifactId>
           <type>zip</type>
           <target>/apps/${appId}-vendor-packages/application/install</target>
            </embedded>
           <embedded>
           <groupId>com.adobe.aem</groupId>
           <artifactId>core-forms-components-af-core</artifactId>
           <target>/apps/${appId}-vendor-packages/application/install</target>
            </embedded>
           <embedded>
           <groupId>com.adobe.aem</groupId>
           <artifactId>core-forms-components-examples-apps</artifactId>
           <type>zip</type>
           <target>/apps/${appId}-vendor-packages/content/install</target>
           </embedded>
           <embedded>
           <groupId>com.adobe.aem</groupId>
           <artifactId>core-forms-components-examples-content</artifactId>
           <type>zip</type>
           <target>/apps/${appId}-vendor-packages/content/install</target>
           </embedded>
   ```

   >[!NOTE]
   將${appId}取代為您原型的appId。

1. 在的相依性區段中 `all/pom.xml` 檔案中，新增下列相依性：

   ```XML
       <!-- Other existing dependencies -->
       <!-- wcm core components examples dependencies -->
        <dependency>
        <groupId>com.adobe.cq</groupId>
        <artifactId>core.wcm.components.examples.ui.apps</artifactId>
        <type>zip</type>
       </dependency>
       <dependency>
        <groupId>com.adobe.cq</groupId>
        <artifactId>core.wcm.components.examples.ui.config</artifactId>
        <type>zip</type>
        </dependency>
       <dependency>
        <groupId>com.adobe.cq</groupId>
        <artifactId>core.wcm.components.examples.ui.content</artifactId>
        <type>zip</type>
       </dependency>
        <!-- forms core components dependencies -->
       <dependency>
        <groupId>com.adobe.aem</groupId>
        <artifactId>core-forms-components-af-apps</artifactId>
        <type>zip</type>
       </dependency>
       <dependency>
        <groupId>com.adobe.aem</groupId>
        <artifactId>core-forms-components-examples-apps</artifactId>
        <type>zip</type>
       </dependency>
        <dependency>
        <groupId>com.adobe.aem</groupId>
        <artifactId>core-forms-components-examples-content</artifactId>
        <type>zip</type>
       </dependency>
   ```

1. 包含 `af-core bundle` 中的相依性 `ui.apps/pom.xml`

   ```XML
        <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   確保您的專案中不包含下列最適化Forms核心元件成品。
   `<dependency>`
   `<groupId>com.adobe.aem</groupId>`
   `<artifactId>core-forms-components-apps</artifactId>`
   `</dependency>`
   和
   `<dependency>`
   `<groupId>com.adobe.aem</groupId>`
   `<artifactId>core-forms-components-core</artifactId>`
   `</dependency>`

1. [运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html). 管道成功執行後，Adaptive Forms核心元件會為您的環境啟用。 此外，最適化Forms （核心元件）範本和畫布主題也會新增至您的Formsas a Cloud Service環境。


## 升級您的本機開發環境 {#upgrade-your-local-development-environment}

將SDK升級至新版本需要取代整個本機開發環境，導致本機存放庫中的所有程式碼、設定和內容遺失。 確保任何不應損毀的程式碼、設定或內容都能安全地提交至Git，或從本機Experience Manager執行個體匯出為CRX套件。

### 升級SDK時如何避免內容遺失 {#avoid-content-loss-when-upgrading--SDK}

升級SDK實際上會建立全新的製作和發佈執行個體，包括新的存放庫([設定AEM專案](#forms-cloud-service-local-development-environment))，這表示對先前SDK存放庫所做的任何變更都會遺失。 如需在SDK升級之間協助保留內容的可行策略，請參閱 [升級AEM SDK時如何避免內容遺失](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#optional-local-aem-runtime-set-up-tasks)

<!--When you update any  Forms-specifc configuration, create overlays, develop custom Adaptive Form components, or develop and test any custom code in AEM project for the development tasks related to local development instance, use the AEM project cloned from the Cloud Manager Git repository to [deploy the custom code and other changes to your [!DNL AEM Forms] as a Cloud Service's production or non-production environment](https://video.tv.adobe.com/v/30191?quality=9).

## Upgrade your local development environment {#update-local-setup}

Update the local AEM setup (AEM SDK) to latest version at least monthly on, or shortly after, the last Thursday of each month, which is the release cadence for AEM as a Cloud Service "feature releases". You can download local AEM SDK from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

Updating the AEM SDK to a new version requires replacing the entire local development environment, resulting in a loss of all code, configuration and content in the local AEM repositories. Ensure that any code, config or content that should not be destroyed is safely committed to Git, or exported from the local AEM instance as AEM Packages.

### How to avoid content loss when upgrading the AEM SDK {#avoid-content-loss-when-upgrading--AEM-SDK}

Upgrading the AEM SDK is effectively creating a brand new AEM runtime ([Set up a local AEM instance](setup-forms-cloud-service.md)), including a new repository ([Set up AEM project](#forms-cloud-service-local-development-environment)), meaning any changes made to a prior AEM SDK's repository are lost. The following are viable strategies for aiding in persisting content between AEM SDK upgrades, and can be used discretely or in concert:

1. Create a content package dedicated to containing the sample content to aid in development and maintain it in Git. Any content that should be persisted through AEM SDK upgrades would be persisted into this package and re-deployed after upgrading the AEM SDK.
1. Use [oak-upgrade](https://jackrabbit.apache.org/oak/docs/migration.html) with the `includepaths` directive, to copy content from the prior AEM SDK repository to the new AEM SDK repository.
1. Back up any content using AEM Package Manager and content packages on the prior AEM SDK and re-install them on the new AEM SDK.

Remember, using the above approaches to maintain code between AEM SDK upgrades, indicates a development anti-pattern. Non-disposable code should originate in your Development IDE and flow into AEM SDK via deployments.

For information about troubleshooting, stopping local AEM environment, run modes, and deployment, see [Set up local AEM Runtime](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#local-development-environment-set-up).-->

### 備份並匯入Forms特定內容至新的SDK環境 {#backup-and-import-Forms-specific-content-to-new-SDK-environment}

若要將資產從現有SDK備份並移至新的SDK環境：

* 建立現有內容的備份。

* 設定全新SDK環境。

* 將備份匯入至您的新SDK環境。

### 建立現有內容的備份 {#create-backup-of-your-existing-content}

備份最適化Forms、範本、表單資料模型、主題、設定和自訂程式碼。 您可以執行下列動作來建立備份：

1. [下載](import-export-forms-templates.md#manage-forms-and-related-assets) 最適化Forms、主題和PDF forms。
1. 匯出自適應表單範本。

1. 下載表單資料模型

1. 匯出可編輯的範本、雲端設定和工作流程模型。 若要從您現有的SDK匯出所有先前提及的專案，請建立 [CRX-Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html) 篩選條件：

   * /conf/ReferenceEditableTemplates
   * /conf/global/settings/cloudconfigs
   * /conf/global/settings/wcm
   * /var/workflow/model
   * /conf/global/settings/workflow
1. 從您的本機開發環境匯出電子郵件設定、提交和預填動作程式碼。 若要匯出這些設定和組態，請在您的本機開發環境中建立下列資料夾和檔案的復本：

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

### 將備份匯入至您的新SDK環境 {#import-the-backup-to-your-new-SDK-environment}

將最適化Forms、範本、表單資料模型、主題、設定和自訂程式碼匯入全新環境。 您可以執行下列動作來匯入備份：

1. [匯入](import-export-forms-templates.md#manage-forms-and-related-assets) 最適化Forms、主題和新SDK環境的PDF forms。
1. 將最適化表單範本匯入新的SDK環境。

1. 將表單資料模型上傳至新的SDK環境。

1. 匯入可編輯的範本、雲端設定和工作流程模型。 若要匯入新SDK環境中所有先前提到的專案，請將包含這些專案的CRX套件匯入新SDK環境。

1. 從您的本機開發環境匯入電子郵件設定、提交和預填動作程式碼。 若要匯入這些設定和組態，請將下列檔案從舊的Archetype專案放入新的Archetype專案：

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

您的新環境現在具有舊環境的表單和相關資產。
