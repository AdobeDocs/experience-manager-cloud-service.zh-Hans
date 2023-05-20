---
title: 如何建立最適化Forms
description: 瞭解如何使用建立最適化表單 [!DNL Experience Manager Forms]. 最適化Forms是回應式HTML5表單，可簡化資訊收集和處理。 深入瞭解如何根據表單資料模型和XML或JSON結構描述建立最適化表單。
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: 4279b4a880429f535cf341d35ac38c9b4dc55ae2
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 3%

---

# 建立最適化表單（Foundation元件） {#creating-an-adaptive-form}


最適化Forms可讓您建立吸引人、回應式、動態且最適化的表單。 AEM Forms為商業使用者提供好用的精靈，以便快速撰寫最適化Forms。 精靈具有快速索引標籤導覽，可輕鬆選取預先設定的範本、樣式、欄位和提交選項以建立調適型表單。

開始之前，請先瞭解您可用的Forms元件型別：

* [最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans) 是標準化的資料擷取元件。 对于您的数字注册体验，这些组件可以提供定制功能，缩短开发时间和降低维护成本。開發人員可以輕鬆自訂這些元件並設定其樣式。 Adobe建議運用這些現代且可擴充的元件來開發最適化Forms。

* [Adaptive Forms Foundation元件](creating-adaptive-form.md) 是傳統（舊）資料擷取元件。 您可以繼續使用這些專案來編輯現有的基礎元件型最適化表單。 如果您要建立新表單，Adobe建議使用  [最適化Forms核心元件](creating-adaptive-form-core-components.md) 以建立最適化Forms。



<!-- 

You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form: 

-->

![创建自适应表单的向导](/help/release-notes/assets/wizard.png)

<!-- 

Adaptive Forms allow you to create forms that are engaging, responsive, dynamic, and adaptive. [!DNL AEM Forms] provides an intuitive wizard and out-of-the-box components to create Adaptive Forms. You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form:

* **Using a form data model**
  [Data integration](data-integration.md) lets you integrate entities and services from disparate data sources in to a Form Data Model that you can use to create Adaptive Forms. Choose Form Data Model if the Adaptive Form you are creating involves fetching and write data from and to multiple data source.

  <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. 

* **Using an XML Schema Definition (XSD) or a JSON Schema**
   XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate the schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema will be available for use in the Data Model Objects tab of the Content browser when authoring Adaptive Forms.

* **Using none or without a form model**
   Adaptive Forms created with this option don't use any form model. The data XML generated from such forms has flat structure with fields and corresponding values. -->

## 先決條件

您需要下列專案才能建立最適化表單：

* **許可權**：將使用者新增至 [!DNL forms-users] 為使用者提供建立最適化表單的許可權。 如需特定使用者群組的表單詳細清單，請參閱 [群組與許可權](forms-groups-privileges-tasks.md).

* **最適化表單主題**：主題包含元件和面板的樣式詳細資訊。 樣式包含背景顏色、狀態顏色、透明度、對齊方式及大小等屬性。 套用主題時，指定的樣式會反映在相應的元件上。 您可以 [建立新主題](themes.md) 或 [匯入現有主題](import-export-forms-templates.md#uploading-a-theme). 您也可以部署 [最新原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html#create-project) 一些範例主題。

* **自適應表單範本**：範本提供基本結構，並定義調適型表單的外觀（版面配置和樣式）。 它有預先格式化的元件，包含特定屬性和內容結構。 它還提供定義主題和提交動作的選項。 主題定義外觀，提交動作定義提交最適化表單時要採取的動作。 例如，將收集的資料傳送至資料來源。 Cloud Service支援兩種範本：

   * **可編輯的範本**：您可以 [建立新的](template-editor.md) 或 [匯入現有的可編輯範本](migrate-to-forms-as-a-cloud-service.md). 您也可以部署 [最新原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20are%20Java型%20integration%20tests。) 以取得一些可編輯範本的範例。

   * **靜態範本**：這些是舊版範本，僅建議從Adobe Managed Services (AMS)和內部部署AEM Forms安裝(AEM 6.5 Forms或更舊版本)的客戶使用。 這些範本可讓您繼續運用靜態範本中的現有投資。 建立新的最適化表單時，建議使用可編輯的範本。



## 建立最適化表單（Foundation元件） {#create-an-adaptive-form-foundation-components}

1. 存取 [!DNL Experience Manager Forms] 作者執行個體。 可以是雲端例項或本機開發例項。

1. 在Experience Manager登入頁面中輸入您的認證。

   登入後，在左上角，點選 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.

1. 點選 **[!UICONTROL 建立]**  > **[!UICONTROL 最適化Forms]**. 精靈隨即開啟。
1. 在「來源」標籤中，選取範本：

   * 當您選取可編輯的範本時，範本中指定的主題和提交動作會自動選取，而且 **[!UICONTROL 建立]** 按鈕已啟用。 您可以前往 **[!UICONTROL 樣式]** 或 **[!UICONTROL 提交]** 標籤以選取不同的主題或提交動作。 如果選取的可編輯範本未指定主題，建立按鈕仍會停用。 您可以前往 **[!UICONTROL 樣式]** 標籤以手動選取主題。

      >[!NOTE]
      >
      > 您也可以建立 [!UICONTROL 記錄檔案] 使用最適化Forms編輯器的範本。 如需詳細資訊，請參閱 [最適化表單編輯器中的記錄檔案支援](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

   * 當您選取靜態範本時，無法使用資料、樣式、提交、傳送和預覽選項。 建立新的最適化表單時，建議使用可編輯的範本。

1. 在 **[!UICONTROL 樣式]** 索引標籤中，選取主題：

   * 當選取的範本指定主題時，會在精靈中自動選取主題。 您也可以從「樣式」標籤中選擇不同的主題。
   * 如果選取的範本未指定主題，您可以使用「樣式」標籤來選擇主題。 此 **[!UICONTROL 建立]** 只有在選取主題後，才會啟用按鈕。

1. （選用）在 **[!UICONTROL 資料]** 索引標籤中，選取資料模型：

   * **表單資料模型**：A [表單資料模型](data-integration.md) 可讓您將實體和服務從不同的資料來源整合至最適化表單。 如果您要建立的最適化表單涉及從多個資料來源擷取及寫入資料，請選擇「表單資料模型」。

   * **JSON結構描述**： [JSON結構](adaptive-form-json-schema-form-model.md) 代表組織中的後端系統產生或使用資料的結構。 您可以将架构与自适应表单相关联，并使用其元素将动态内容添加到自适应表单。編寫Adaptive Forms時，可在內容瀏覽器的「資料模型物件」索引標籤中使用結構描述元素，所有欄位也會新增到新建立的Adaptive Form。

   預設會選取資料模型的所有欄位。 建立最適化表單時，所有選取的資料模型欄位都會轉換為對應的最適化表單元件。 精靈會提供核取方塊，讓您僅選取應包含在調適型表單中的欄位。

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. 在 **[!UICONTROL 提交]** 索引標籤中，選取提交動作：

   * 當您選取範本時，範本中指定的提交動作會自動選取。 您可以從「提交」標籤中選取不同的提交動作。 此 **[!UICONTROL 提交]** 索引標籤會顯示所有可用的提交動作。

   * 當選取的範本未指定提交動作時，您可以使用 **[!UICONTROL 提交]** 標籤以選取提交動作

1. （選用）在「傳送」標籤中，您可以指定最適化表單的發佈或取消發佈日期。

1. 點選 **[!UICONTROL 建立]**. 會出現一個對話方塊，指定儲存最適化表單的標題、名稱和位置：

   * **[!UICONTROL 標題]** 指定表單的顯示名稱。 標題可協助您識別 [!DNL Experience Manager Forms] 使用者介面。
   * **[!UICONTROL 名稱：]** 指定表單的名稱。 在存放庫中會建立具有指定名稱的節點。 當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。
   * **[!UICONTROL 路徑：]** 指定最適化表單的儲存位置。 您可以直接將最適化表單儲存在 `/content/dam/formsanddocuments` 或建立資料夾，例如 `/content/dam/formsanddocuments/adaptiveforms` 以儲存最適化表單。 在路徑中使用資料夾之前，請務必先建立資料夾。 此 **[!UICONTROL 路徑：]** 欄位不會自動建立資料夾。

1. 點選 **[!UICONTROL 建立]**. 最適化表單會在最適化Forms編輯器中建立並開啟。 編輯器會顯示範本中可用的內容。 它也會顯示側邊欄，以根據需求自訂新建立的表單。

   根據最適化表單的型別，出現在相關聯中的表單元素 <!--XFA form template, XML schema or --> JSON結構描述或表單資料模型會顯示在 **[!UICONTROL 資料模型物件]** 的標籤 **[!UICONTROL 內容瀏覽器]** 在側欄中。 您也可以拖放這些元素來建置最適化表單。

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Tap to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Create an Adaptive Form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, tap on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Tap **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and tap Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
    * **[!UICONTROL Search in repository]** - Select this option to select from the list of schema definition files available in the repository. Select the XML or JSON schema file as form model. The selected schema is associated with the form by reference and is accessible for use in other Adaptive Forms.

      Ensure that the JSON schema filename ends with **.schema.json**. For example: mySchema.schema.json

   ![Selecting XML or JSON schema](assets/upload-schema.png)
**Figure:** *Selecting XML or JSON schema*

1. (For XML schema only) After you select or upload an XML Schema, specify a root element of the selected XSD file to map with the Adaptive Form.

   ![Selecting XSD root element](assets/xsd-root-element.png)
**Figure:** *Selecting XSD root element*

>[!NOTE]
>
>You can also change the schema for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model). -->

## 編輯最適化表單的表單模型屬性 {#edit-form-model}

您可以變更最適化表單的表單模型（JSON式或表單資料模型）。 您無法從一個表單模型變更為另一個表單模型。

1. 選取最適化表單，然後點選 **屬性** 圖示。
1. 開啟 **[!UICONTROL 表單模型]** 按tab鍵，然後執行下列任一項作業。

   * 如果最適化表單沒有表單模型，您可以選擇另一個表單模型，並相應地選擇 <!-- a form template, --> XML或JSON結構描述，或表單資料模型。
   * 如果最適化表單是以表單模型為基礎，您可以選擇其他模型 <!-- form template, --> XML或JSON結構描述，或相同表單模型的表單資料模型。

1. 點選 **[!UICONTROL 儲存]** 以儲存屬性。

您也可以從最適化表單編輯器或最適化表單範本編輯器修改表單模型屬性。

1. 選取 **[!UICONTROL 最適化表單容器（根）]** 元件。
1. 按一下 ![設定圖示](/help/forms/assets/configure-icon.svg) 圖示以開啟 **[!UICONTROL 屬性]** 最適化表單容器的預設值。
1. 選取 **[!UICONTROL 資料模型]** 標籤並執行下列任一項作業：

   * 如果最適化表單沒有表單模型，您可以選擇表單模型，並相應地選擇 <!-- a form template, --> XML或JSON結構描述，或表單資料模型。
   * 如果最適化表單是以表單模型為基礎，則無法變更表單模型。 您可以選擇其他 <!-- form template, --> 適用時，為相同表單模型的XML或JSON結構描述或表單資料模型。
1. 點選 ![儲存](/help/forms/assets/check-button.png) 以儲存屬性。

![FDM-Schema-Support](/help/forms/assets/fdmsupport.png)

>[!NOTE]
>
> 您也可以將自適應表單另存為範本。 如需詳細資訊，請參閱 [使用最適化表單建立範本](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template).