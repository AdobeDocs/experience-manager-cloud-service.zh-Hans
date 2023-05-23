---
title: 如何在AEM中新增智慧標籤至資產？
description: 透過AEM中可套用情境式和描述性商業標籤的人為智慧型服務，將智慧標籤新增至資產。
contentOwner: AG
feature: Smart Tags,Tagging
role: Admin,User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: f8535b9d1b8334bede817714eab469fbb1fcbb03
workflow-type: tm+mt
source-wordcount: '2462'
ht-degree: 6%

---


# 將智慧標籤新增至AEM中的資產 {#smart-tags-assets-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/enhanced-smart-tags.html?lang=en) |
| AEM as a Cloud Service | 本文 |

處理數位資產的組織越來越多地在資產中繼資料中使用分類控制的辭彙。 基本上，其中包含員工、合作夥伴和客戶常用來參照和搜尋其數位資產的關鍵字清單。 使用分類控制的辭彙來標籤資產，以確保在搜尋中可輕鬆識別和擷取資產。

相較於自然語言辭彙，根據商業分類法標籤有助於讓資產與公司的業務保持一致，並確保最相關的資產出現在搜尋中。 例如，汽車製造商可以使用模型名稱來標籤汽車影像，以便在搜尋時只顯示相關影像來設計促銷活動。

在背景中，功能使用的人為智慧型架構 [Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html) 以根據您的標籤結構和商業分類訓練其影像識別演演算法。 然後，此內容智慧可用來將相關標籤套用至不同的資產集。 依預設，AEM會自動將智慧標籤套用至已上傳的資產。

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## AEM中智慧標籤的支援資產型別 {#smart-tags-supported-file-formats}

您可以標籤下列資產型別：

* **影像**：使用Adobe Sensei的智慧內容服務來標籤許多格式的影像。 您 [建立訓練模型](#train-model) 然後會自動標籤上傳的影像。 智慧標籤會套用至支援的檔案型別，這些檔案型別會產生JPG和PNG格式的轉譯。
* **文字型資產**： [!DNL Experience Manager Assets] 上傳時會自動標籤支援的文字型資產。
* **視訊資產**：視訊標籤預設為啟用 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. [視訊會自動加上標籤](/help/assets/smart-tags-video-assets.md) 上傳新影片或重新處理現有影片時。

| 影像（MIME型別） | 文字型資產（檔案格式） | 視訊資產（檔案格式和轉碼器） |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC，運動JPEG) |
| image/bmp | HTML | AVI (indeo4) |
| image/gif | PDF | FLV (H264/AVC、vp6f) |
| image/pjpeg | PPT | WMV (WMV2) |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| image/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap |  |  |
| image/x-xpixmap |  |  |
| image/x-icon |  |  |
| image/photoshop |  |  |
| image/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

AEM預設會將智慧標籤自動新增至文字型資產和影片。 若要自動將智慧標籤新增至影像，請完成下列工作。

* [瞭解標籤模型和准則](#understand-tag-models-guidelines).
* [訓練模型](#train-model).
* [標籤您的數位資產](#tag-assets).
* [管理標籤和搜尋](#manage-smart-tags-and-searches).

## 瞭解標籤模型和准則 {#understand-tag-models-guidelines}

標籤模型是一組相關標籤，這些標籤與所標籤影像的各種視覺方面相關聯。 標籤與影像明顯不同的視覺效果有關，因此套用標籤時，有助於搜尋特定型別的影像。 例如，一個鞋子系列可以有不同的標籤，但所有標籤都與鞋子相關，並且可以屬於相同的標籤模型。 套用時，標籤可協助尋找不同型別的鞋子，例如依設計或用途。 若要瞭解中訓練模型的內容表示 [!DNL Experience Manager]，將訓練模型視覺化為頂層實體，由一組手動新增的標籤和每個標籤的範例影像組成。 每個標籤都可專門套用至影像。

建立標籤模型並訓練服務之前，請先識別一組唯一標籤，這些標籤最能描述企業內容中影像中的物件。 確保組織集中的資產符合 [訓練指南](#training-guidelines).

### 訓練指南 {#training-guidelines}

請確定訓練集中的影像符合下列准則：

**數量與大小：** 每個標籤最少10個影像，最多50個影像。

**一致性**：確認標籤的影像在視覺上類似。 最好將相同視覺方面（例如影像中相同型別的物件）的標籤一起新增至單一標籤模型中。 例如，將所有影像標示為 `my-party` （適用於訓練），因為視覺上並不相似。

![說明性影像，以示範訓練准則](assets/do-not-localize/coherence.png)

**涵蓋範圍**：訓練中的影像應有足夠的變化。 我們的想法是提供一些相當多元化的範例，以便 [!DNL Experience Manager] 學習如何專注在正確的事。 如果您要在視覺上相異的影像上套用相同的標籤，請至少包含每種型別的五個範例。 例如，對於標籤 *模型向下姿態*，加入更多與下方醒目提示影像類似的培訓影像，以便服務在標籤期間更準確地識別類似影像。

![說明性影像，以示範訓練准則](assets/do-not-localize/coverage_1.png)

**干擾/阻礙**：此服務會針對干擾較少的影像（顯著背景、不相關的隨附，例如主要主題的物件/人員）提供更好的訓練。 例如，對於標籤 *休閒鞋*，第二個影像不是良好的訓練候選項。

![說明性影像，以示範訓練准則](assets/do-not-localize/distraction.png)

**完整性：**&#x200B;如果图像符合多个标记的条件，请在包含培训图像之前添加所有适用的标记。例如，对于 *Raincoat* 和 *model-side-view* 等标记，在将其加入培训之前，在符合条件的资产上添加这两个标记。

![說明性影像，以示範訓練准則](assets/do-not-localize/completeness.png)

**標籤數量**：Adobe建議您使用至少兩個相異標籤並為每個標籤使用至少十個不同影像來訓練模型。 在單一標籤模型中，新增的標籤不可超過50個。

**範例數量**：針對每個標籤，至少新增10個範例。 不過，Adobe建議使用約30個範例。 支援每個標籤最多50個範例。

**防止誤判和衝突**：Adobe建議為單一視覺化方面建立單一標籤模型。 以可避免標籤在模型之間重疊的方式建構標籤模型。 例如，請勿使用常見的標籤，例如 `sneakers` 在兩個不同的標籤模型名稱中 `shoes` 和 `footwear`. 針對常見關鍵字，訓練程式會以一個已訓練標籤模型來覆寫另一個已訓練標籤模型。

**範例**：其他指引範例包括：

* 建立只包含、

   * 與汽車模型相關的標籤。
   * 和成人及兒童外套相關的標籤。

* 不要建立，

   * 標籤模型，包含2019年和2020年發行的汽車模型。
   * 包含相同幾款車型的多重標籤車型。

**用來訓練的影像**：您可以使用相同的影像來訓練不同的標籤模型。 不過，請勿將影像與標籤模型中的多個標籤建立關聯。 您可以使用屬於不同標籤模型的不同標籤來標籤相同的影像。

您無法復原培訓。 上述准則應可協助您選擇要訓練的良好影像。

## 為您的自訂標籤訓練模型 {#train-model}

若要建立並訓練特定企業標籤的模型，請遵循下列步驟：

1. 建立必要的標籤和適當的標籤結構。 在DAM存放庫中上傳相關影像。
1. 在 [!DNL Experience Manager] 使用者介面，存取 **[!UICONTROL 資產]** > **[!UICONTROL 智慧標籤培訓]**.
1. 单击&#x200B;**[!UICONTROL 创建]**。提供 **[!UICONTROL 標題]**， **[!UICONTROL 說明]**.
1. 按一下中的資料夾圖示 **[!UICONTROL 標籤]** 欄位。 隨即開啟快顯視窗。
1. 從現有標籤中搜尋或選取適當的標籤 `cq-tags` 您想要新增至模型的物件。 单击&#x200B;**[!UICONTROL 下一步]**。

   >[!NOTE]
   >
   >您可以根據 **[!UICONTROL 名稱]** （依字母順序）， **[!UICONTROL 已建立]** 日期，或 **[!UICONTROL 修改時間]** 日期。


1. 在 **[!UICONTROL 選取資產]** 對話方塊，按一下 **[!UICONTROL 新增資產]** 標籤時。 在DAM存放庫中搜尋或瀏覽存放庫以選取至少10個和最多50個影像。 選取資產，而非資料夾。 選取影像後，請按一下 **[!UICONTROL 選取]**.

   ![檢視訓練狀態](assets/smart-tags-training-status.png)

1. 若要預覽所選影像的縮圖，請按一下標籤前方的摺疊式功能表。 您可以按一下「 」，修改您的選取範圍 **[!UICONTROL 新增資產]**. 對選取範圍感到滿意後，按一下 **[!UICONTROL 提交]**. 使用者介面會在頁面底部顯示通知，指示已開始培訓。
1. 在中檢查培訓的狀態 **[!UICONTROL 狀態]** 欄中指定每個標籤模型。 可能的狀態包括 [!UICONTROL 擱置中]， [!UICONTROL 已訓練]、和 [!UICONTROL 已失敗].

![訓練智慧標籤的標籤模型的工作流程](assets/smart-tag-model-training-flow.png)

*圖：訓練標籤模型的訓練工作流程步驟。*

### 檢視訓練狀態和報告 {#training-status}

若要檢查智慧標籤服務是否已針對您資產培訓集中的標籤進行培訓，請從「報表」控制檯檢閱培訓工作流程報表。

1. 在 [!DNL Experience Manager] 介面，前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**.
1. 在 **[!UICONTROL 資產報表]** 頁面，按一下 **[!UICONTROL 建立]**.
1. 選取 **[!UICONTROL 智慧標籤培訓]** 報表，然後按一下 **[!UICONTROL 下一個]** （從工具列）。
1. 指定报表的标题和描述。在&#x200B;**[!UICONTROL 计划报告]**&#x200B;下，保持选中&#x200B;**[!UICONTROL 立即]**&#x200B;选项。如果要安排以后的计划报告，请选择&#x200B;**[!UICONTROL 稍后]**，然后指定日期和时间。然後，按一下 **[!UICONTROL 建立]** （從工具列）。
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，选择生成的报表。若要檢視報表，請按一下 **[!UICONTROL 檢視]** （從工具列）。
1. 檢閱報告的詳細資訊。 报表显示您培训的标记的培训状态。中的綠色 **[!UICONTROL 訓練狀態]** 欄表示已針對標籤訓練智慧標籤服務。 黃色表示服務已針對特定標籤進行部分訓練。 若要針對標籤完整地訓練服務，請使用特定標籤新增更多影像，並執行訓練工作流程。 如果您在此報告中沒有看到您的標籤，請再次執行這些標籤的培訓工作流程。標籤
1. 若要下載報表，請從清單中選取報表，然後按一下 **[!UICONTROL 下載]** （從工具列）。 報表會下載為試算表。

<!--
### Tag assets from the workflow console {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. Specify a title for the workflow and an optional comment. Click **[!UICONTROL Run]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   *Figure: Navigate to the asset folder and review the tags to verify whether your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).*

### Tag assets from the timeline {#tagging-assets-from-the-timeline}

1. From the [!DNL Assets] user interface, select the folder containing assets or specific assets to which you want to apply smart tags.
1. From upper-left corner, open the **[!UICONTROL Timeline]**.
1. Open actions from the bottom of the left sidebar and click **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. Select the **[!UICONTROL DAM Smart Tag Assets]** workflow, and specify a title for the workflow.
1. Click **[!UICONTROL Start]**. The workflow applies your tags on assets. Navigate to the asset folder and review the tags to verify that your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).

>[!NOTE]
>
>In the subsequent tagging cycles, only the modified assets are tagged again with newly trained tags. However, even unaltered assets are tagged if the gap between the last and current tagging cycles for the tagging workflow exceeds 24 hours. For periodic tagging workflows, unaltered assets are tagged when the time gap exceeds six months.

### Tag uploaded assets {#tag-uploaded-assets}

[!DNL Experience Manager] can automatically tag the assets that users upload to DAM. To do so, administrators configure a workflow to add an available step that tags assets. See [how to enable Smart Tags for uploaded assets](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).
-->

## 使用AEM中的智慧標籤標籤標籤資產 {#tag-assets}

所有支援的資產型別都會自動以下列方式標籤 [!DNL Experience Manager Assets] 上傳時。 標籤預設為啟用並運作。 AEM會近乎即時套用適當的智慧標籤。 <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

* 針對影像和影片，智慧標籤是以某些視覺方面為基礎。

* 對於文字型資產，智慧標籤的功效並不取決於資產中的文字數量，而是取決於資產文字中存在的相關關鍵字或實體。 對於文字型資產，智慧標籤是出現在文字中的關鍵字，但最能描述資產的關鍵字。 若為支援的資產， [!DNL Experience Manager] 已擷取文字，然後將其編入索引，並用於搜尋資產。 不過，以文字中的關鍵字為基礎的智慧標籤可提供專用、結構化和更高優先順序的搜尋面向。 相較於搜尋索引，後者有助於改善資產探索。

## 管理智慧標籤和資產搜尋 {#manage-smart-tags-and-searches}

您可以組織智慧標籤，移除任何可能已指派給品牌資產的不準確標籤，以便僅顯示最相關的標籤。

仲裁智慧標籤也可確保您的資產出現在最相關標籤的搜尋結果中，有助於縮小資產的標籤式搜尋範圍。 基本上，它有助於避免不相關資產出現在搜尋結果中的機會。

您也可以為標籤指派較高的排名，以增加標籤與資產的相關性。 根據特定標籤執行搜尋時，為資產推廣標籤會增加資產出現在搜尋結果中的機會。

若要稽核數位資產的智慧標籤：

1. 在搜尋欄位中，根據標籤搜尋數位資產。

1. 若要識別您找不到與搜尋相關的數位資產，請檢查搜尋結果。

1. 選取資產，然後選取 ![管理標籤圖示](assets/do-not-localize/manage-tags-icon.png) （從工具列）。

1. 從 **[!UICONTROL 管理標籤]** 頁面，檢查標籤。 如果您不想根據特定標籤來搜尋資產，請選取標籤並選取 ![「刪除」圖示](assets/do-not-localize/delete-icon.png) （從工具列）。 或者，選取 `X` 標籤旁的符號。

1. 若要將較高排名指派給標籤，請選取該標籤並選取 ![「提升」圖示](assets/do-not-localize/promote-icon.png) （從工具列）。 您促銷的標籤會移至 **[!UICONTROL 標籤]** 區段。

1. 選取 **[!UICONTROL 儲存]** 然後選取 **[!UICONTROL 確定]** 以關閉 [!UICONTROL 成功] 對話方塊。

1. 導覽至 [!UICONTROL 屬性] 資產的頁面。 請注意，您促銷的標籤會獲得高關聯性，因此在搜尋結果中會顯示在較高的位置。

### 瞭解 [!DNL Experience Manager] 包含智慧標籤的搜尋結果 {#understand-search}

依預設， [!DNL Experience Manager] 搜尋會將搜尋字詞與 `AND` 子句。 使用智慧標籤不會變更此預設行為。 使用智慧標籤會新增 `OR` 子句來尋找已套用智慧標籤中的任何搜尋字詞。 例如，考慮搜尋 `woman running`. 資產，僅含 `woman` 或只是 `running` 根據預設，中繼資料中的關鍵字不會出現在搜尋結果中。 不過，資產若被以下任一專案標籤： `woman` 或 `running` 使用智慧標籤會出現在此搜尋查詢中。 因此搜尋結果是

* 資產，具有 `woman` 和 `running` 中繼資料中的關鍵字。

* 使用任一關鍵字進行智慧標籤的資產。

符合中繼資料欄位中所有搜尋字詞的搜尋結果會先顯示，接著顯示符合智慧標籤中任何搜尋字詞的搜尋結果。 在上述範例中，顯示搜尋結果的大約順序為：

1. 符合 `woman running` 於各種中繼資料欄位中。
1. 符合 `woman running` 在智慧標籤中。
1. 符合 `woman` 或 `running` 在智慧標籤中。

## 標籤相關的限制和最佳作法 {#limitations}

增強型智慧標籤是以學習的影像模型及其標籤為基礎。 這些模型並不總是能夠完美地識別標籤。 目前版本的智慧標籤有下列限制：

* 無法辨認影像中的細微差異。 例如，超薄襯衫和一般襯衫。
* 無法根據影像的微小模式或部分識別標籤。 例如，襯衫上的圖志。
* 支援的標籤語言為 [!DNL Experience Manager] 支援。
* 未處理的標籤與：

   * 非視覺化抽象層面。 例如，產品發佈的年份或季節、影像引發的情緒或情感，以及視訊的主觀內涵。
   * 產品中的細微視覺差異，例如襯衫（含或不含領子）或嵌入在產品上的小型產品標誌。

若要訓練模型，請使用最合適的影像。 訓練無法還原，或訓練模型無法移除。 您的標籤正確性取決於目前的訓練，所以請謹慎操作。

<!-- TBD: Add limitations related to text files. -->

若要搜尋包含智慧標籤（一般或增強功能）的檔案，請使用 [!DNL Assets] 搜尋（全文檢索搜尋）。 智慧標籤沒有獨立的搜尋述詞。

>[!NOTE]
>
>智慧標籤在標籤上訓練並將它們套用至其他影像的能力，取決於您用於訓練的影像品質。
>為達到最佳效果，Adobe建議您使用視覺上相似的影像，來訓練每個標籤的服務。

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
>* [瞭解智慧標籤如何協助管理您的數位檔案](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [對視訊使用智慧標籤](smart-tags-video-assets.md)

