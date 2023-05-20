---
title: 安装 [!DNL Workfront for Experience Manager enhanced connector]
description: 安装 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 648f0d4899237484f24faa003a796bdd1f508cb2
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# 安装 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

在中擁有管理員存取許可權的使用者 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 安裝增強型聯結器。 安裝之前，請先檢閱平台支援及其他 [聯結器的先決條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe需要部署和設定 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署與設定沒有認證合作夥伴或 [!DNL Adobe Professional Services]，Adobe不支援。
>
>* Adobe可能會將更新發行至 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 讓此聯結器成為備援；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
>
>* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請參閱的步驟5(a) [增強型聯結器安裝指示](workfront-connector-install.md).
>
>* 另請參閱 [適用於Experience Manager Assets增強型聯結器的Workfront合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 如需有關考試的資訊，請參閱 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


在安裝聯結器之前，請遵循下列預先安裝步驟：

1. [設定防火牆](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). 若要瞭解中的IP叢集 [!DNL Workfront]，導覽至 [!UICONTROL 設定] > [!UICONTROL 系統] > [!UICONTROL 客戶資訊].

1. 在Dispatcher上，允許名為的HTTP標頭 `authorization`， `username`、和 `apikey`. 允許 `GET`， `POST`、和 `PUT` 要求 `/bin/workfront-tools`.

1. 請確定以下路徑不存在於 [!DNL Experience Manager] 存放庫：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. 此安裝需要知識才能在中設定Maven專案 [!DNL Experience Manager] as a [!DNL Cloud Service]. 使用下列資源瞭解如何在您的Maven專案中包含協力廠商套件：

   * [在您的Maven專案中包含協力廠商套件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [部署方式 [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

若要在中安裝附加元件 [!DNL Experience Manager] as a [!DNL Cloud Service]，請遵循下列步驟：

1. 從下載增強型聯結器 [Adobe軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [存取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) 並從Cloud Manager複製您的AEMas a Cloud Service存放庫。

1. 使用您選擇的IDE開啟複製的AEMas a Cloud Service存放庫。

1. 將步驟1中下載的增強型聯結器zip檔案放在下列路徑中：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果 `resources` 資料夾不存在，請建立資料夾。


1. 新增 `pom.xml` 相依性：

   1. 在父系中新增相依性 `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
      ```

      >[!NOTE]
      >
      >在將相依性複製到父項之前，請務必更新增強型聯結器版本號碼 `pom.xml`.

   1. 在中新增相依性 `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. 新增 `pom.xml` 內嵌。 新增 [!DNL Workfront for Experience Manager enhanced connector] 封裝到 `embeddeds` 部分 `pom.xml` 您的所有子專案的。 需要將其內嵌於所有模組中 `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   內嵌區段的目標設定為 `/apps/<path-to-project-install-folder>/install`. 此JCR路徑 `/apps/<path-to-project-install-folder>` 必須包含在的篩選規則中 `all/src/main/content/META-INF/vault/filter.xml` 檔案。 存放庫的篩選規則通常衍生自方案名稱。 使用資料夾名稱作為現有規則中的目標。

1. 將變更推送至存放庫。

1. 執行管道至 [將變更部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. 若要建立系統使用者組態，請建立 `wf-workfront-users` 在 [!DNL Experience Manager] 使用者群組並指派許可權 `jcr:all` 至 `/content/dam`. 系統使用者 `workfront-tools` 會自動建立，並自動管理所需的許可權。 所有使用者來自 [!DNL Workfront] 使用增強型聯結器的使用者會自動新增為此群組的一部分。

如需更新 [!DNL Workfront for Experience Manager enhanced connector] 從舊版到最新版，按一下 [此處](update-workfront-enhanced-connector.md).

## 設定之間的連線 [!DNL Experience Manager] as a [!DNL Cloud Service] 和 [!DNL Workfront] {#configure-connection}

若要建立連線，使用 [!DNL Workfront]，請遵循下列步驟：

1. 在 [!DNL Experience Manager]，選取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具設定]**.

1. 選取 `workfront-tools` 在左側面板中並選取 **[!UICONTROL 建立]** 選項。

1. 在 **[!UICONTROL Workfront連線]** 對話方塊，提供您所需的詳細資料 [!DNL Workfront] 部署，並選取 **[!UICONTROL 連線至Workfront]** 選項。 成功連線後， [!DNL Workfront] 檔案自訂整合會自動建立於 [!DNL Workfront] 環境。

   ![Connect [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 導覽至 **[!UICONTROL 進階]** 標籤並選取選項 **[!UICONTROL 伺服器AEM是as a Cloud Service的]**.
