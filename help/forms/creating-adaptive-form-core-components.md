---
title: 如何建立最適化表單
description: 瞭解如何使用建立最適化表單 [!DNL Experience Manager Forms]. 最適化Forms是回應式HTML5表單，可簡化資訊收集和處理。 深入瞭解如何根據表單資料模型和XML或JSON結構描述建立最適化表單。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 4279b4a880429f535cf341d35ac38c9b4dc55ae2
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 7%

---

# 建立最適化表單（核心元件） {#creating-an-adaptive-form-core-components}

最適化Forms可讓您建立吸引人、回應式、動態且最適化的表單。 AEM Forms為商業使用者提供好用的精靈，以便快速建立最適化Forms。 精靈具有快速索引標籤導覽，可輕鬆選取預先設定的範本、樣式、欄位和提交選項以建立調適型表單。

開始之前，請先瞭解您可用的Forms元件型別：

* [最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)：這些是標準化的資料擷取元件。 這些元件提供自訂功能、縮短開發時間，並降低數位註冊體驗的維護成本。 開發人員可以輕鬆自訂這些元件並設定其樣式。 Adobe建議運用這些現代且可擴充的元件來開發最適化Forms。

* [Adaptive Forms Foundation元件](creating-adaptive-form.md)：這些是傳統（舊）資料擷取元件。 您可以繼續使用這些專案來編輯現有的基礎元件型最適化表單。 如果您要建立新表單，Adobe建議使用  [最適化Forms核心元件](creating-adaptive-form-core-components.md) 以建立最適化Forms。

![创建自适应表单的向导](/help/release-notes/assets/wizard.png)


## 先決條件

您需要下列專案才能建立最適化表單：

* **為您的環境啟用最適化Forms核心元件**：建立新程式時，最適化Forms核心元件已為您的環境啟用。 如果您有基于 Archetype 39 或更早版本的 Forms as a Cloud Service 环境，请[为您的环境启用自适应表单核心组件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project)。在为您的环境启用核心组件时，即将&#x200B;**自适应表单（核心组件）**&#x200B;模板和画布主题添加到您的环境。如果您的 AEM SDK 版本低于 2023.02.0，请[确保在您的环境上启用 `prerelease` 标志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features)，因为自适应表单核心组件是 2023.02.0 发布之前预发布的一部分。

* **自適應表單範本**：範本提供基本結構，並定義調適型表單的外觀（版面配置和樣式）。 它有預先格式化的元件，包含特定屬性和內容結構。 它還提供定義主題和提交動作的選項。 主題定義外觀，提交動作定義提交最適化表單時要採取的動作。 例如，將收集的資料傳送至資料來源。 雲端服務提供名為空白的OOTB範本：

   * 此 `blank` 範本隨附於每個新的AEM Formsas a Cloud Service程式中。
   * 您可以透過「封裝管理員」安裝參考封裝，以新增 `blank` 範本至您的AEM Formsas a Cloud Service程式。
   * 您也可以 [建立新的Adaptive Forms範本（核心元件）](template-editor.md) 從頭開始。

* **最適化表單主題**：主題包含元件和面板的樣式詳細資訊。 樣式包含背景顏色、狀態顏色、透明度、對齊方式及大小等屬性。 套用主題時，指定的樣式會反映在相應的元件上。  此 `Canvas` 範本隨附於每個新的AEM Formsas a Cloud Service程式中。

   <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **許可權**：將使用者新增至 [!DNL forms-users] 群組。 的成員 [!DNL forms-users] 群組有權建立最適化表單。 如需特定使用者群組的表單詳細清單，請參閱 [群組與許可權](forms-groups-privileges-tasks.md).


## 建立最適化表單（核心元件） {#create-an-adaptive-form-core-components}

1. 登入您的 [!DNL Experience Manager Forms] 作者執行個體。 可以是雲端例項或本機開發例項。

1. 在Experience Manager登入頁面中輸入您的認證。 登入後，在左上角，點選 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.

1. 點選 **[!UICONTROL 建立]**  > **[!UICONTROL 最適化Forms]**. 精靈隨即開啟。 在「來源」標籤中，選取範本：

   ![核心元件範本](/help/forms/assets/core-components-template.png)

   當您選取範本時，會自動選取範本中指定的主題和提交動作，而且 **[!UICONTROL 建立]** 按鈕已啟用。 您可以前往 **[!UICONTROL 樣式]** 或 **[!UICONTROL 提交]** 標籤以選取不同的主題或提交動作。 如果選取的範本未指定主題，建立按鈕仍會停用。 您可以前往 **[!UICONTROL 樣式]** 標籤以手動選取主題。

   >[!NOTE]
   >
   >
   > 如果您沒有， **最適化Forms （核心元件）** 您環境上的範本， [為您的環境啟用最適化Forms核心元件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). 為您的環境啟用核心元件時， **最適化Forms （核心元件）** 範本已新增至您的環境。

1. 在 **[!UICONTROL 樣式]** 索引標籤中，選取主題：

   * 當選取的範本指定主題時，會在精靈中自動選取主題。 您也可以從「樣式」標籤中選擇不同的主題。

   * 如果選取的範本未指定主題，您可以使用「樣式」標籤來選擇主題。 此 **[!UICONTROL 建立]** 只有在選取主題後，才會啟用按鈕。

1. （選用）在資料標籤中，選取資料模型：

   * **表單資料模型**：A [表單資料模型](data-integration.md) 可讓您將實體和服務從不同的資料來源整合至最適化表單。 如果您要建立的最適化表單涉及從多個資料來源擷取及寫入資料，請選擇「表單資料模型」。

   * **JSON結構描述**： [JSON結構](adaptive-form-json-schema-form-model.md) 我們的核心元件式最適化表單提供關聯JSON結構描述的功能，代表所生產或使用資料的結構，讓您與組織的後端系統無縫整合。 此關聯可讓作者使用結構描述的元素，以動態方式將內容新增至最適化表單。 在製作過程中，您可以在內容瀏覽器的資料模型物件索引標籤中輕鬆存取結構描述的元素，而且所有欄位都會自動新增到任何新建立的調適型表單中。

   依預設，系統會自動選取相關JSON結構描述的所有欄位，並將其轉換為對應的最適化表單元件，進而簡化編寫程式。 精靈提供額外的便利性，可讓您透過使用核取方塊，選擇性地選擇應包含在調適型表單中的欄位。

1. 在 **[!UICONTROL 提交]** 索引標籤中，選取提交動作：

   * 當您選取範本時，範本中指定的提交動作會自動選取。 您可以從「提交」標籤中選取不同的提交動作。 此 **[!UICONTROL 提交]** 索引標籤會顯示所有可用的提交動作。

   * 當選取的範本未指定提交動作時，您可以使用 **[!UICONTROL 提交]** 標籤以選取提交動作

1. （選用）在 **[!UICONTROL 傳遞]** 索引標籤上，您可以指定最適化表單的發佈或取消發佈日期。

1. 點選 **[!UICONTROL 建立]**. 會出現一個對話方塊，指定儲存最適化表單的標題、名稱和位置：

   * **[!UICONTROL 標題]** 指定表單的顯示名稱。 標題可協助您識別 [!DNL Experience Manager Forms] 使用者介面。
   * **[!UICONTROL 名稱：]** 指定表單的名稱。 在存放庫中會建立具有指定名稱的節點。 當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。
   * **[!UICONTROL 路徑：]** 指定最適化表單的儲存位置。 您可以直接將最適化表單儲存在 `/content/dam/formsanddocuments` 或建立資料夾，例如 `/content/dam/formsanddocuments/adaptiveforms` 以儲存最適化表單。 在路徑中使用資料夾之前，請務必先建立資料夾。 此 **[!UICONTROL 路徑]** 欄位不會自動建立資料夾。

1. 點選 **[!UICONTROL 建立]**. 最適化表單會在最適化Forms編輯器中建立並開啟。 編輯器會顯示範本中可用的內容。  根據最適化表單的型別，出現在相關聯中的表單元素 <!--XFA form template, XML schema or --> JSON結構描述或表單資料模型會顯示在 **[!UICONTROL 資料模型物件]** 的標籤 **[!UICONTROL 內容瀏覽器]** 在側欄中。 您也可以拖放這些元素來建置最適化表單。

現在，您可以拖放最適化Forms核心元件至最適化Forms容器，以設計和建立表單。

## 可用的最適化Forms核心元件

最適化Forms核心元件是標準化的資料擷取元件。 這些元件提供自訂功能，有助於縮短開發時間，並降低數位註冊體驗的維護成本。 [Adaptive Forms核心元件檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans) 具有可用元件的詳細清單，以及有關每個元件功能的詳細資訊。 您也可以造訪 [https://aemcomponents.dev/](https://aemcomponents.dev/) 以檢視作用中的可用核心元件。

## 編輯最適化表單的表單模型屬性 {#edit-form-model}

1. 選取最適化表單並點選 ![頁面資訊](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 開啟屬性]**. 「表單屬性」頁面隨即開啟。

1. 前往 **[!UICONTROL 表單模型]** 標籤並選擇表單模型。 如果最適化表單沒有表單模型，您可以自由選擇JSON結構描述或表單資料模型。 另一方面，如果最適化表單已基於表單模型，您可以選擇切換到相同型別的另一個表單模型。 例如，如果表單使用JSON結構描述，您可以輕鬆切換到另一個JSON結構描述，同樣如果表單使用表單資料模型，您可以切換到另一個表單資料模型。

1. 點選 **[!UICONTROL 儲存]** 以儲存屬性。
