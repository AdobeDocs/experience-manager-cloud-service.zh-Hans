---
title: 如何建立表單資料模型？
description: Experience Manager Forms資料整合提供直覺式使用者介面，用於建立和使用表單資料模型。 瞭解如何使用或不使用已設定的資料來源來建立表單資料模型。
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 1f3104d4a986018675f751afa04fe0ed3b7f5c26
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 0%

---

# 创建表单数据模型 {#create-form-data-model}

![資料整合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 資料整合提供直覺式使用者介面，可建立和使用表單資料模型。 表單資料模型仰賴資料來源交換資料；不過，您可以建立具有或不具有資料來源的表單資料模型。 根據您是否已設定資料來源，從資料模型建立有兩個方法：

* **使用預先設定的資料來源**：如果您已如所述設定資料來源 [設定資料來源](configure-data-sources.md)，您可在建立表單資料模型時選取它們。 它會從選定的資料來源帶入所有資料模型物件、屬性和服務，以供表單資料模型使用。

* **沒有資料來源**：如果您尚未為表單資料模型設定資料來源，您仍可以在沒有資料來源的情況下建立它。 您可以使用表單資料模型來撰寫最適化Forms <!--and interactive communication--> 並使用範例資料加以測試。 當資料來源可用時，您可以將表單資料模型與資料來源繫結，這會自動反映在關聯的Adaptive Forms中<!--and interactive communications-->.

>[!NOTE]
>
>您必須同時為兩者 **fdm-author** 和 **forms-user** 群組，以便能夠建立和使用表單資料模型。 聯絡您的 [!DNL Experience Manager] 成為群組成員的管理員。

## 创建表单数据模型 {#data-sources}

請確定您已依照中的說明，設定您要用於表單資料模型中的資料來源 [設定資料來源](configure-data-sources.md). 執行下列動作，根據已設定的資料來源建立表單資料模型：

1. 在 [!DNL Experience Manager] 作者執行個體，導覽至 **[!UICONTROL Forms >資料整合]**.
1. 點選 **[!UICONTROL 建立>表單資料模型]**.
1. 在建立表單資料模型對話方塊中：

   * 指定表單資料模型的名稱。
   * (**可選**)指定表單資料模型的標題、說明和標籤。
   * (**選填，且僅在資料來源已設定時適用**)點選「 」旁的勾選圖示 **[!UICONTROL 資料來源組態]** 欄位並選取您要使用之資料來源的cloud service所在的設定節點。 它會將下一頁可供選取的資料來源清單，限制在所選設定節點中可供選取的資料來源。 但是，任何 [!DNL Experience Manager] 預設會列出使用者設定檔資料來源。 如果您未選取設定節點，則會列出所有設定節點的資料來源。

1. 點選 **[!UICONTROL 下一個]**.

1. (**僅適用於已設定資料來源時**) **[!UICONTROL 選取資料來源]** 畫面會列出可用的資料來源（若有）。 選取您要在表單資料模型中使用的資料來源。
1. 點選 **[!UICONTROL 建立]** 在確認對話方塊上，點選 **[!UICONTROL 開啟]** 以開啟表單資料模型編輯器。

   讓我們檢閱表單資料模型編輯器UI的不同元件。

   ![具有三個資料來源的表單資料模型 — RESTful服務、 [!DNL Experience Manager] 使用者設定檔和RDBMS](assets/fdm-ui.png)

   答： **[!UICONTROL 資料來源]** 列出表單資料模型中的資料來源。 展開資料來源以檢視其資料模型物件與服務。

   B. **[!UICONTROL 重新整理資料來源定義]** 從已設定的資料來源擷取資料來源定義的任何變更，並在表單資料模型編輯器的「資料來源」標籤中更新這些變更。

   C. **[!UICONTROL 模型]** 新增的資料模型物件出現的內容區域。

   D. **[!UICONTROL 服務]** 新增的資料來源作業或服務出現的內容區域。

   E. **[!UICONTROL 工具列]** 使用表單資料模型的工具。 工具列會根據表單資料模型中選取的物件顯示更多選項。

   F. **[!UICONTROL 新增選取專案]** 將選取的資料模型物件和服務新增至表單資料模型。

如需表單資料模型編輯器以及如何使用它來編輯和設定表單資料模型的詳細資訊，請參閱 [使用表單資料模型](work-with-form-data-model.md).

## 更新資料來源 {#update}

執行下列動作，將資料來源新增或更新至現有表單資料模型。

1. 前往 **[!UICONTROL Forms >資料整合]**，選取您要新增或更新資料來源的表單資料模型，然後點選 **[!UICONTROL 屬性]**.
1. 在表單資料模型屬性中，前往 **[!UICONTROL 更新來源]** 標籤。

   在 **[!UICONTROL 更新來源]** 標籤：

   * 點選「 」中的「 」瀏覽圖示 **[!UICONTROL 內容感知設定]** 欄位並選取您要新增之資料來源的雲端設定所在的設定節點。 如果您未選取節點，則雲端設定僅駐留在 `global` 點選時列出節點 **[!UICONTROL 新增來源]**.

   * 若要新增資料來源，請點選 **[!UICONTROL 新增來源]** 並選取要新增至表單資料模型的資料來源。 所有資料來源均設定於 `global` 和選取的設定節點（如果有的話）會顯示出來。

   * 若要以相同型別的另一個資料來源取代現有資料來源，請點選 **[!UICONTROL 編輯]** 圖示並選取可用資料來源清單中的「 」。
   * 若要刪除現有的資料來源，請點選 **[!UICONTROL 刪除]** 資料來源的圖示。 如果將資料來源中的資料模型物件新增至表單資料模型，則會停用「刪除」圖示。

      ![fdm-properties](assets/fdm-properties.png)

1. 點選 **[!UICONTROL 儲存並關閉]** 以儲存更新。

>[!NOTE]
>
>在表單資料模型中新增資料來源或更新現有資料來源後，請務必視需要在Adaptive Forms中更新繫結參考<!--and interactive communications--> 使用更新後表單資料模型的使用者。

## 特定執行模式的內容感知設定 {#runmode-specific-context-aware-config}

[!UICONTROL 表單資料模型] 利用 [Sling內容感知設定](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) 支援不同的資料來源引數，以連線不同的資料來源 [!DNL Experience Manager] 執行模式。

時間 [!UICONTROL 表單資料模型] 使用雲端設定來儲存引數，這些引數在登入和透過原始檔控制（Cloud-Manager GIT存放庫）部署時，會為所有執行模式（開發、測試和生產）使用相同的引數來建立雲端設定。 不過，在測試和生產環境需要不同資料集的使用案例中，我們會針對不同使用資料來源引數（例如資料來源URL） [!DNL Experience Manager] 執行模式。

為此，您需要建立包含資料來源引數 — 值配對的OSGi設定。 這會覆寫來自的相同配對 [!UICONTROL 表單資料模型] 執行階段的雲端設定。 由於OSGi設定預設支援這些執行模式，因此您可以根據執行模式將資料來源引數覆寫為不同的值。

若要在中啟用部署專用雲端設定 [!UICONTROL 表單資料模型]：

1. 在本機開發執行個體上建立雲端設定。 如需詳細步驟，請參閱 [如何設定資料來源](/help/forms/configure-data-sources.md).

1. 將您的雲端設定儲存至檔案系統。
   1. 使用篩選器建立封裝 `/conf/{foldername}/settings/cloudconfigs/fdm`. 使用相同的 `{foldername}` 如步驟1所示。 和取代 `fdm` 替換為 `azurestorage` 用於Azure儲存體設定。
   1. 建置和下載套件。 如需詳細資訊，請參閱 [套件動作](/help/implementing/developing/tools/package-manager.md).

1. 在中整合雲端設定 [!DNL Experience Manager] 原型專案。
   1. 將下載的套件解壓縮。
   1. 複製 `jcr_root` 資料夾並將其放在您的 `ui.content` > `src` > `main` > `content`.
   1. 更新 `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` 以包含篩選器 `/conf/{foldername}/settings/cloudconfigs/fdm`. 如需詳細資訊，請參閱 [AEM專案原型的ui.content模組](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). 透過CM管道部署此原型專案時，相同的雲端設定會安裝在所有環境（或執行模式）上。 若要根據環境變更雲端設定的欄位值（例如URL），請使用以下步驟中討論的OSGi設定。

1. 建立Apache Sling內容感知設定。 若要建立OSGi設定：
   1. **在中設定OSGi設定檔 [!DNL Experience Manager] 原型專案。**
使用PID建立OSGi Factory設定檔 
`org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`. 在每個執行模式資料夾下建立名稱相同的檔案，其中值需在每個執行模式中變更。 如需詳細資訊，請參閱 [設定OSGi用於 [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **設定OSGI設定json。** 若要使用Apache Sling內容感知設定覆寫提供者：
      1. 在本機開發執行個體上 `/system/console/configMgr`，選取名稱為的工廠OSGi設定 **[!UICONTROL Apache Sling內容感知設定覆寫提供者： OSGi設定]**.
      1. 提供說明。
      1. 選取 **[!UICONTROL 已啟用]**.
      1. 在覆寫下，根據sling覆寫語法中的環境，提供需要變更的欄位。 如需詳細資訊，請參閱 [Apache Sling內容感知設定 — 覆寫](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). 例如， `cloudconfigs/fdm/{configName}/url="newURL"`.
選取「 」，可新增多個覆寫 **[!UICONTROL +]**.
      1. 选择&#x200B;**[!UICONTROL 保存]**。
      1. 若要取得OSGi Configuration JSON，請遵循中的步驟 [使用AEM SDK快速入門產生OSGi設定](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart).
      1. 將JSON放在上一步建立的OSGi Factory設定檔案中。
      1. 變更值 `newURL` 根據環境（或runmode）。
      1. 若要根據runmode變更密碼值，可以使用以下專案建立密碼變數 [cloud manager API](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) 和更新版本可在以下連結中參照： [OSGi設定](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
透過CM管道部署此原型專案時，覆寫將在不同的環境（或執行模式）上提供不同的值。

      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] 使用者可使用加密支援來加密加密加密值(如需詳細資訊，請參閱 [設定屬性的加密支援](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) 並將加密的文字放在之後的值中 [上下文感知設定在service pack 6.5.13.0中提供](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. 使用選項重新整理資料來源定義，以重新整理 [表單資料模型編輯器](#data-sources) 以透過FDM UI重新整理FDM快取並取得最新設定。

## 后续步骤 {#next-steps}

您現在擁有已新增資料來源的表單資料模型。 接下來，您可以編輯「表單資料模型」以新增及設定資料模型物件與服務、新增資料模型物件之間的關聯、編輯屬性、新增自訂資料模型物件與屬性、產生範例資料等。

如需詳細資訊，請參閱 [使用表單資料模型](work-with-form-data-model.md).
