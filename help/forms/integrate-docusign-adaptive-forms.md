---
title: 將DocuSign與最適化表單整合
description: 瞭解如何搭配最適化表單使用DocuSign來收集電子簽章。
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 8%

---

# 搭配最適化表單使用DocuSign {#integrate-aem-forms-with-DocuSign}

DocuSign是顯眼的電子簽章解決方案。 您可以使用它來電子簽署合約。 您可以將DocuSign與最適化表單整合。 它可協助您傳送電子簽章的最適化表單給多個收件者。 使用電子簽章可協助您：

- 透過完全自動化的提案、報價和合約程式，完成任何裝置的交易。
- 更快完成人力資源流程，為員工提供數位體驗。
- 縮短合約週期時間，讓您的廠商更快上線。

AEM Formsas a Cloud Service提供 [DocuSign的自訂提交動作](#deploy-custom-submit-action). 提交動作可協助您使用DocuSign API傳送電子簽章的最適化表單。

| 您也可以使用Adobe的電子簽章解決方案Adobe Sign在最適化表單上進行電子簽章。 AEM Forms與Adobe Sign的整合更深入，並提供更精細的控制項，例如循序和並行簽署、多種驗證方法、表單內簽署體驗等。 如需詳細資訊，請參閱 [在最適化表單中使用Adobe Sign](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## 前提条件 {#prerequisites}

以下是DocuSign與AEM Forms整合的必要條件：

- A DocuSign [開發人員帳戶](https://developers.docusign.com/platform/account/)
- DocuSign應用程式
- DocuSign API應用程式的認證（使用者端ID和使用者端密碼）。
- [適用於DocuSign的自訂提交動作和雲端服務](https://github.com/adobe/aem-forms-docusign-sample)
- （僅適用於本機開發環境） [設定記錄檔案](setup-local-development-environment.md#docker-microservices).

## 設定適用於DocuSign的自訂提交動作和雲端服務 {#deploy-custom-submit-action}

AEM Formsas a Cloud Service提供DocuSign的自訂提交動作。 提交動作可協助您使用DocuSign API傳送電子簽章的最適化表單。 自訂提交動作的程式碼可在以下網址取得： [AEM Forms範例公開Git存放庫](https://github.com/adobe/aem-forms-docusign-sample). 您可以在您的AEM Forms環境中依原樣部署程式碼，或根據貴組織的需求自訂程式碼。

執行以下步驟來設定現成的自訂提交動作和DocuSignCloud Service：

1. [複製您的AEM Formsas a Cloud Service專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment) 或建立 [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 專案依據 [AEM原型27](https://github.com/adobe/aem-project-archetype) 或更新版本。 若要建立 [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 根據AEM原型的專案：
   </br> 開啟命令提示字元並執行以下命令以建立 [!DNL Experience Manager Forms] as a Cloud Service專案：

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   另外，請變更 `appTitle`， `appId`、和 `groupId`，以反映您的環境。

1. 原地複製 [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample) 存放庫。 此存放庫包含用於DocuSign的自訂提交動作以及連線到DocuSign伺服器的設定詳細資料。

1. 開啟在步驟1中建立的AEM Formsas a Cloud Service專案，以便在您選擇的IDE中進行編輯。

1. 開啟 `[AEM Forms as a Cloud Service project]\pom.xml` 進行編輯的檔案，並進行下列變更：

   1. 將下列文字新增至 `<properties>` 標籤：

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. 將下列文字新增至 `<repositories>` 標籤：

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      如果沒有 `<repositories>` 標籤，在下方建立標籤 `<properties>` 標籤之間。

   1. 將下列文字新增至 `<dependencyManagement>` 標籤：

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. 在「 」中執行下列步驟 `all/pom.xml` Cloud Service專案資料夾中可用的檔案：

   1. 將下列文字新增至 `<embeddeds>` 標籤：

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. 將下列文字新增至 `<dependencies>` 標籤：

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. 開啟命令提示字元並瀏覽至 `aem-forms-samples\forms-integration-docusign` （在步驟3中複製）並執行下列命令：

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` 是指在此程式的步驟1中建立的資料夾名稱。

1. 將專案部署到您的本機開發環境。 您可以使用以下命令來部署到您的本機開發環境

   `mvn -PautoInstallPackage clean install`

   執行這些步驟後，您可以檢視新的自訂提交動作 [使用DocuSign電子簽章提交](#enabledocusign) 最適化表單和的提交選項清單中提供 [DocuSign雲端服務設定](#configure-docusign-with-aem-forms) 本機開發環境中。

1. 編譯和 [將程式碼部署至您的 [!DNL AEM Forms] as a Cloud Service環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## 整合 [!DNL DocuSign] 替換為 [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

已具備下列先決條件後，請執行以下步驟以整合 [!DNL DocuSign] 替換為 [!DNL AEM Forms] 在Author執行個體上。

1. 導覽至 **[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL DocuSign]** 並選取要裝載設定的資料夾。

1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL DocuSign] AEM Forms中的設定。
1. 在 **[!UICONTROL 一般]** 的標籤 **[!UICONTROL 建立DocuSign設定]** 頁面，指定 **[!UICONTROL 名稱]** ，然後點選「 」 **[!UICONTROL 下一個]**. 您可以選擇指定 **[!UICONTROL 標題]**.

1. 将当前浏览器窗口中的 URL 复制到记事本。在下一个步骤中使用 [!DNL AEM Forms] 配置 [!DNL DocuSign] 应用程序时需要此 URL。

1. 配置 [!DNL DocuSign] 应用程序的 OAuth 设置：

   1. 開啟瀏覽器視窗並登入 [!DNL DocuSign] [開發人員帳戶](https://admindemo.docusign.com/apps-and-keys).
   1. 開啟為設定的應用程式 [!DNL AEM Forms].
   1. 在 **[!UICONTROL 重新導向URI]** 方塊中，新增在上一步中複製的URL並按一下 **[!UICONTROL 儲存]**.
   1. 記下整合和秘密金鑰。

   有关为 [!DNL DocuSign] 应用程序配置 OAuth 设置并获取密钥的分步信息，请参阅[为应用程序配置 OAuth 设置](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys)开发人员文档。

1. 返回 **[!UICONTROL 建立DocuSign設定]** 頁面。 在 **[!UICONTROL 設定]** 標籤， **[!UICONTROL OAuth URL]** 欄位提及下列預設URL：

   `https://account-d.docusign.com/oauth/auth`

1. 指定 **[!UICONTROL 使用者端ID]** （DocuSign整合金鑰）和 **[!UICONTROL 使用者端密碼]** （DocuSign秘密金鑰）。

1. 點選 **[!UICONTROL 連線到DocuSign]**. 在系统提示输入凭据时，提供在创建 [!DNL DocuSign] 应用程序时所用帐户的用户名和密码。當要求確認存取時 `your developer account`，按一下 **[!UICONTROL 允許存取]**. 如果認證正確，則會顯示成功訊息。

1. 點選 **[!UICONTROL 建立]** 建立 [!DNL DocuSign] 設定。

1. 選取設定並按一下 **[!UICONTROL 發佈]**，選取設定，然後按一下 **[!UICONTROL 發佈]**. 这会将配置复制到相应的发布环境。

1. 在开发人员实例、暂存实例和生产实例（以剩下的实例为准）上重复上述所有步骤以使用 [!DNL AEM Forms] 为环境配置 [!DNL DocuSign]。

現在，您的AEM Forms環境已設定為使用DocuSign。 确保将用于 Cloud Service 的配置容器添加到为 [!DNL DocuSign] 启用的所有自适应表单。您可以在自适应表单的属性中指定配置容器。

### 使用 [!DNL DocuSign] 在最適化表單中 {#enabledocusign}

您可以啟用 [!DNL DocuSign] 適用於現有的最適化表單或建立 [!DNL DocuSign] 啟用最適化表單。 選擇下列其中一項：

- [建立 [!DNL DocuSign] 啟用最適化表單](#create-an-adaptive-form-for-docusign)
- [啟用 [!DNL DocuSign] 適用於現有的最適化表單](#editafsign).

#### 建立DocuSign的最適化表單 {#create-an-adaptive-form-for-docusign}

若要建立可啟用簽名的最適化表單：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **[!UICONTROL 建立]** 並選取 **[!UICONTROL 最適化表單]**. 範本清單隨即顯示。 選取範本並點選 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 基本]** 標籤：

   1. 指定 **[!UICONTROL 名稱]** 和 **[!UICONTROL 標題]** 最適化表單的預設值。

   1. 選取 [設定容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 建立時間 [整合 [!DNL DocuSign] 替換為 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   設定容器包含 [!DNL DocuSign] 為您的環境設定的Cloud Services。 這些服務可在最適化表單編輯器中選取。

1. 在 **[!UICONTROL 表單模型]** 索引標籤中，選取下列其中一個選項：

   - 如果您有自訂表單範本，且需要根據表單範本的記錄檔案，請選取 **[!UICONTROL 建立表單範本為記錄檔案範本的關聯]** 選項並選取記錄檔案範本。 當您使用選項時，傳送供簽署的檔案只會顯示以相關表單範本為基礎的欄位。 它不會顯示最適化表單的所有欄位。

   - 如果您沒有自訂表單範本，請選取 **[!UICONTROL 產生記錄檔案]** 選項。 當您使用選項時，傳送以供簽署的檔案會顯示最適化表單的所有欄位。

1. 點選 **[!UICONTROL 建立。]** 已建立可啟用簽名的最適化表單。 您可以新增 [!DNL DocuSign] 欄位放入表單並傳送以進行簽署。
1. 在編輯模式下開啟最適化表單。 在 **[!UICONTROL 內容]** 標籤，點選 **[!UICONTROL 表單容器]** 並點選 ![設定](assets/configure-icon.svg).

1. 在 **[!UICONTROL 提交]** 區段，選取 **[!UICONTROL 使用DocuSign電子簽章提交]** 從 **[!UICONTROL 提交動作]** 下拉式清單。

1. 在 **[!UICONTROL 動作設定]** 區段，點選 **[!UICONTROL 新增]** 以新增收件者並指定收件者的電子郵件地址。 點選 **[!UICONTROL 新增]** 以新增更多收件者。

1. 在中指定電子郵件訊息的主旨 **[!UICONTROL 電子郵件主旨]** 欄位。 選取 **包含附件** 將附件加入電子郵件中。

1. 點選 ![儲存](assets/save_icon.svg) 以儲存屬性。

#### 啟用 [!DNL DocuSign] 最適化表單 {#editafsign}

使用 [!DNL DocuSign] 在現有的最適化表單中：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取最適化表單並點選 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 基本]** 索引標籤中，選取 [設定容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 整合時建立 [!DNL DocuSign] 替換為 [!DNL AEM Forms].
1. 在 **[!UICONTROL 表單模型]** 索引標籤中，選取下列其中一個選項：

   - 如果您有自訂表單範本，且需要根據表單範本的記錄檔案，請選取 **[!UICONTROL 建立表單範本為記錄檔案範本的關聯]** 選項並選取記錄檔案範本。 當您使用選項時，傳送供簽署的檔案只會顯示以相關表單範本為基礎的欄位。 它不會顯示最適化表單的所有欄位。

   - 如果您沒有自訂表單範本，請選取 **[!UICONTROL 產生記錄檔案]** 選項。 當您使用選項時，傳送以供簽署的檔案會顯示最適化表單的所有欄位。

1. 點選 **[!UICONTROL 儲存並關閉]**. 已針對以下專案啟用最適化表單 [!DNL DocuSign]. 現在，您可以新增 [!DNL DocuSign] 欄位放入表單並傳送以進行簽署。

1. 在編輯模式下開啟最適化表單。 在 **[!UICONTROL 內容]** 標籤，點選 **[!UICONTROL 表單容器]** 並點選 ![設定](assets/configure-icon.svg).

1. 在 **[!UICONTROL 提交]** 區段，選取 **[!UICONTROL 使用DocuSign電子簽章提交]** 從 **[!UICONTROL 提交動作]** 下拉式清單。

1. 在 **[!UICONTROL 動作設定]** 區段，點選 **[!UICONTROL 新增]** 以新增收件者並指定收件者的電子郵件地址。 點選 **[!UICONTROL 新增]** 以新增更多收件者。

1. 在中指定電子郵件訊息的主旨 **[!UICONTROL 電子郵件主旨]** 欄位。 選取 **包含附件** 將附件加入電子郵件中。

1. 點選 ![儲存](assets/save_icon.svg) 以儲存屬性。
