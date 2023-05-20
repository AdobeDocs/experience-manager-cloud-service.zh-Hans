---
title: 批次集预设
description: 了解如何使用 Dynamic Media 中的批次集预设自动创建图像集和旋转集。
contentOwner: Rick Brough
feature: Image Presets,Viewer Presets
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 1%

---

# 關於批次集預設集 {#about-bsp}

使用 **[!UICONTROL 批次集預設集]** 當您個別或使用大量擷取將資產檔案上傳至資料夾時，可在影像集或迴轉集中建立及組織多個資產。 您可以讓預設集與您排程的資產匯入作業一起執行 [!DNL Dynamic Media]. 每個預設集都是一組唯一命名、獨立的指示，定義如何使用符合預設集中定義的命名約定的影像來建構影像集或迴轉集。

>[!IMPORTANT]
>
>您是否使用批次集預設集於 [!DNL Dynamic Media Classic]，並從移轉 [!DNL Dynamic Media Classic] 至Adobe Experience Manager as a Cloud Service？ 若是如此，您必須手動重新建立批次集預設集定義 [!DNL Adobe Experience Manager as a Cloud Service].

**最佳實務**  — 使用批次集預設集時，Adobe建議使用下列工作流程：

1. 建立批次集預設集。 另請參閱 [為影像集或迴轉集建立批次集預設集](#creating-bsp).
1. 建立資產資料夾或使用現有的資產資料夾，並確保已將其同步至 [!DNL Dynamic Media]. 另請參閱 [建立資料夾](/help/assets/manage-digital-assets.md#creating-folders).
1. 將批次集預設集套用至資產資料夾。 另請參閱 [關於將批次集預設集套用至資料夾](#apply-bsp).
1. 將影像上傳至資產資料夾。 另請參閱 [上傳影像集的資產](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets)， [上傳迴轉集的資產](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)，或 [將數位資產新增至Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. 影像集或迴轉集會在所需的資料夾中自動產生。
1. 發佈影像集或迴轉集。 另請參閱 [發佈Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## 為影像集或迴轉集建立批次集預設集 {#creating-bsp}

若要建立批次集預設集，最好熟悉並瞭解規則運算式。

理想情況下，貴公司已針對資產在集合中的分組方式定義命名慣例。
為了幫助您瞭解使用命名慣例的重要性，假設您公司定義的命名慣例是 `<style>-<color>-<view>`. 而且，集合的基本名稱必須一律為 `<style>-<color>`，並將副檔名設為 `-SET`. 如果您上傳名為的影像 `0123-RED-01`，則會建立一個集合，並命名為 `0123-RED-SET`. 如果您稍後上傳影像 `0123-RED-03` 和 `0123-BLUE-01`，然後 `RED-03` 影像會新增至集合（在第二個位置），因為它的排序低於 `01`. 不過， `BLUE-01` 影像將成為名為的新集的一部分 `0123-BLUE-SET`. 若要下一次上傳資產，請新增檔案 `0123-RED-02` 和 `0123-BLUE-02`. 每個資產都會新增至其各自的集合。 此 `RED-02` 影像會自動在現有檔案之間排序 `01` 和 `03` 影像，因為排序順序。

此 **[!UICONTROL 批次集預設集]** 第頁於 [!DNL Dynamic Media] 可讓您建立、編輯或刪除批次集預設集，以及將批次集預設集套用至資產資料夾或從資產資料夾中移除批次集預設集。 您可以使用表單欄位下拉式清單來定義批次集預設集，或使用 **[!UICONTROL 原始程式碼]** 欄位，可讓您輸入規則運算式語法。

您可以建立許多批次集預設集，以涵蓋所需的所有資產擷取作業。

### 關於資產命名慣例

此 **[!UICONTROL 資產命名慣例]** 區域 **[!UICONTROL 批次集預設集]** 頁面有兩個可用來定義批次集預設集的元素： **[!UICONTROL 符合]** 和 **[!UICONTROL 基本名稱]**. 這些元素可讓您定義命名慣例，並識別用來命名包含這些元素的集的慣例部分。 <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

公司的個別命名慣例通常使用來自這兩個元素中每個元素的一或多行定義。 您可以針對唯一的定義使用儘可能多的線條，並將其群組為不同的元素，例如針對「主要影像」、「顏色」元素、「替代檢視」元素和「色票」元素。

例如，常值比對規則運算式的語法可能如下所示：

`(\w+)-\w+-\w+`

### 關於序列順序

您可以選擇定義將影像集或迴轉集分組之後影像的顯示順序 [!DNL Dynamic Media]. 依預設，您的資產會依字母數字排序。 不過，您可以使用逗號分隔的規則運算式清單來定義順序。

關於序列排序自動化，您可以指定必要時，以特定方式強制排序資產的規則。 例如，假設您的第一個資產一律名為 `_main` 您希望它後面有 `_alt1`， `_alt2`， `_alt3`、等等。 在這種情況下，您可以使用以下語法建立序列排序規則：

`.*_main,.*_alt[0-9]`

雖然可以使用強制排序順序，但最好儘可能使用英數字元編號來排序順序。 此外，您還可以在以下位置使用影像集或迴轉集編輯器工具： [!DNL Dynamic Media] 以重新排列資產的順序順序，或使用拖放操作在資產集中新增和刪除新資產。

當您完成建立批次集預設集時，可將其套用至您已建立的一個或多個資料夾。 另請參閱 [關於將批次集預設集套用至資料夾](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**若要為影像集或迴轉集建立批次集預設集，請執行下列動作：**

1. 選取Experience Manager標誌，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批次集預設集]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. 於 **[!UICONTROL 批次集預設集]** 頁面，右上角附近，選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立批次集預設集]** 對話方塊，在 **[!UICONTROL 預設集名稱]** 文字欄位，輸入描述性名稱。 如果您稍後決定變更預設集名稱，則無法編輯預設集名稱。

1. 在 **[!UICONTROL 預設集型別]** 下拉式清單，選取 **[!UICONTROL 影像集]** 或 **[!UICONTROL 迴轉集]**. 請確定您選擇正確的預設集型別；之後將無法編輯。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在右側 **[!UICONTROL 編輯批次集預設集]** 頁面，在「 」下方設定您要編輯的選項 **[!UICONTROL 預設集詳細資訊]** 和 **[!UICONTROL 設定命名慣例]** 標題。
若要進一步瞭解您可用的可編輯選項，請參閱 [預設集詳細資訊、設定命名慣例和規則結果 — RegX選項](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. 建立一或多個規則運算式群組。

   * 在左側 **[!UICONTROL 編輯批次集預設集]** 頁面，底下 **[!UICONTROL 符合]**， **[!UICONTROL 基本名稱]**，或 **[!UICONTROL 序列順序]**，選取 **[!UICONTROL 新增群組]**.
   * 此 **[!UICONTROL 符合]** 欄位為必填。 **[!UICONTROL 基本名稱]** 只有在以下情況下為必要： **[!UICONTROL 符合]** 欄位尚未使用括弧群組指定基底名稱。 **[!UICONTROL 序列順序]** 是選用專案。
   * 使用群組表單中的下拉式清單和文字方塊，指定您要用來定義影像集或迴轉集資產成員命名條件的運算式群組。
      * 當您選取並指定群組的運算式時，請注意實際的規則運算式語法會反映在頁面右下方 **[!UICONTROL 規則結果 — RegX]** 標題。 若要檢視右下角更新的規則運算式字串，請選取表單區域以外的任何位置。 這些規則運算式字串代表您要在搜尋中比對的模式 [!DNL Dynamic Media] 資產，以建立您的影像集或迴轉集。
      * 如果您已新增群組且想要移除該群組，請選取「 」 **[!UICONTROL X]**.
   * 當您新增兩個或多個群組時，請在 **[!UICONTROL 和]** 下拉式清單，選取 **[!UICONTROL 和]** 將新增的群組與先前新增的任何運算式群組結合。 或者，選取 **[!UICONTROL 或]** 在先前運算式群組與您建立的新群組之間新增替代專案。 此 **[!UICONTROL 或]** 運算元是使用垂直行字元來定義 `|` 規則運算式語法本身中的。

1. 执行下列操作之一：

   * 若要新增另一個群組，請在 **[!UICONTROL 符合]**， **[!UICONTROL 基本名稱]**，或 **[!UICONTROL 排序順序]**，選取 **[!UICONTROL 新增群組]**. 建立另一個規則運算式群組，就像在上一步中所做的那樣。
   * 檢閱中的規則運算式語法 **[!UICONTROL 規則結果 — RegX]** 區域。 如果您必須變更語法，請在頁面左側的個別群組中編輯。
   * 如果您已完成建立運算式群組，請繼續進行下一個步驟。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]**.

您現在可以將批次集預設集套用至資產資料夾。 然後，您會將資產上傳至該資料夾。 此工作流程會自動產生影像集或迴轉集。 另請參閱 [關於將批次集預設集套用至資產資料夾](#apply-bsp).

### 預設集詳細資訊、設定命名慣例和規則結果 — RegX選項 {#features-options-bsp}

這些選項可在 **[!UICONTROL 編輯批次集預設集]** 建立或編輯批次集預設集時的頁面。

另請參閱 [為影像集或迴轉集建立批次集預設集](#creating-bsp) 或 [編輯批次集預設集](#edit-bsp).

| **[!UICONTROL 预设详细信息]** | 描述 |
| --- | --- |
| 预设名称 | 只读. 您第一次建立批次集時所指定的名稱。 如果您必須重新命名預設集，可以複製現有的批次集預設集並指定新名稱。 另請參閱 [複製現有的批次集預設集](#copy-bsp). |
| 类型 | 只读. 當您首次建立批次集時指定了型別。 複製現有批次集預設集不允許您變更其 [!UICONTROL 型別]；您必須改為建立預設集。 |
| 包括派生的资产 | 可选. 擁有 [!DNL Dynamic Media]的IPS （影像生產系統）包含隨迴轉集或影像集產生的或「衍生」影像，請選取 **[!UICONTROL 是]** （預設）。 衍生資產是使用者未直接上傳的影像。 而是在上傳主要資產時，由IPS產生資產。 例如，在上傳PDF時，IPS從PDF中的頁面產生的影像資產 [!DNL Dynamic Media]，會視為衍生資產。 |
| 目标文件夹 | 可选. 如果您定義大量影像集或迴轉集，Adobe建議您將這些集與包含資產本身的資料夾分開。 因此，請考慮建立「影像集」或「迴轉集」資料夾，並將應用程式重新導向，將批次集產生的集放置在此處。<br>在這種情況下，請指定Experience Manager Assets資料夾結構中的哪個資料夾(`/content/dam`)讓批次集預設集作用中。 請確定資料夾已啟用 [!DNL Dynamic Media] 同步化，以允許它作為目的地資料夾。 另請參閱 [在Dynamic Media中設定檔案夾層級的選擇性發佈](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>如果透過資料夾的「 」套用預設集，則可以為多個資料夾指派指定的批次集預設集 **[!UICONTROL 屬性]**. 另請參閱 [從資產資料夾的「屬性」頁面套用批次集預設集](#apply-bsp-to-folders-via-properties).<br>如果您未指定資料夾，批次集預設集產生的影像集或迴轉集會建立在與您上傳至的資產資料夾相同的資料夾中。 |
| **[!UICONTROL 设置命名规则]** |  |
| 前置詞<br>或<br>字尾 | 可选. 在個別欄位中輸入字首、字尾或兩者。<br>字首與字尾欄位可讓您使用特定內容集的替代自訂檔案命名慣例，建立許多批次集預設集。 在公司定義的預設命名配置有例外的情況下，此方法特別有用。<br>首碼或尾碼會新增至 **[!UICONTROL 基本名稱]** 您在中定義 **[!UICONTROL 資產命名慣例]** 區域。 藉由新增首碼或尾碼，您可以確保您的影像集或迴轉集是獨立於其他資產以獨佔方式建立的。 它也可以進一步協助其他人識別檔案型別。 例如，若要判斷所使用的顏色模式，可以新增作為字首或字尾 `rgb` 或 `cmyk`.<br>雖然指定集命名慣例並非使用批次集預設集功能所必需，但最佳實務建議您使用集命名慣例。 此作法可讓您定義命名慣例的元素，並將這些元素群組在集合中，以協助簡化批次集的建立。 |
| **[!UICONTROL 规则结果 - RegX]** |  |
| 資產命名慣例 — 相符 | 只读. 根據您選擇的「符合」表單選項或您輸入的原始程式碼顯示規則運算式語法。 |
| 資產命名慣例 — 基本名稱 | 只读. 根據您選擇的「基本名稱」表單選項或您輸入的原始程式碼顯示規則運算式語法。 |
| 序列順序 — 相符 | 只读. 根據您選擇的表單選項或您輸入的原始程式碼顯示規則運算式語法。 |

## 關於將批次集預設集套用至資產資料夾 {#apply-bsp}

將批次集預設集指派給一個或多個資產資料夾時，任何子資料夾都會自動從其父資料夾繼承預設集。

您可以將多個批次集預設集套用至資產資料夾。

指派了批次預設集的資料夾會顯示在使用者介面中，並在資料夾中的以下位置顯示預設集名稱： **[!UICONTROL 卡片]** 檢視。

若要將批次集預設集套用至資產資料夾，請使用下列兩種方法之一：

* [從「批次集預設集」頁面將批次集預設集套用至資產資料夾](#apply-bsp-to-folders-via-bsp-page)  — 此方法提供您最大的彈性。 您可以將單一預設集或多個預設集套用至單一資料夾或多個資料夾。
* [從資產資料夾的「屬性」頁面套用批次集預設集](#apply-bsp-to-folders-via-properties)  — 此方法可讓您將一個或多個批次集預設集套用至單一資料夾。

最佳做法是確認資產資料夾已同步 [!DNL Dynamic Media]，然後套用您想要的預設集。

如果您遇到以下兩種情況之一，請重新處理資料夾中的資產：

* 您想要對已上傳資產的現有資產資料夾執行批次集預設集。
* 您稍後會編輯先前套用至資產資料夾的現有批次集預設集。

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### 從「批次集預設集」頁面將批次集預設集套用至資產資料夾 {#apply-bsp-to-folders-via-bsp-page}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批次集預設集]**.
1. 於 **[!UICONTROL 批次集預設集]** 頁面，在頁面左側 **[!UICONTROL 預設集名稱]** 欄中，選取要套用至資料夾之每個批次集預設集的核取方塊。
1. 在工具列中，選取 **[!UICONTROL 將批次預設集套用至資料夾]**.
1. 於 **[!UICONTROL 選取資料夾]** 頁面上，選取要套用批次集預設集的每個資料夾的核取方塊。
1. 在的右上角 **[!UICONTROL 選取資料夾]** 頁面，選取 **[!UICONTROL 套用]**.

### 從資產資料夾的「屬性」頁面套用批次集預設集 {#apply-bsp-to-folders-via-properties}

1. 選取Experience Manager標誌，並前往 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 導覽至您要套用一或多個批次集預設集的資料夾。
1. 在頁面上，左側的 **[!UICONTROL 名稱]** 欄中，選取資料夾的核取方塊。
1. 在工具列中，選取 **[!UICONTROL 屬性]**.
1. 在資料夾的「屬性」頁面上，選取 **[!UICONTROL Dynamic Media處理中]** 標籤。

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. 下 **[!UICONTROL 批次集預設集]**，來自 **[!UICONTROL 預設集名稱]** 下拉式清單方塊中，選取您要套用的批次集預設集名稱。 上面的熒幕擷圖顯示套用至資產資料夾的兩個選取批次集預設集。

   如果批次集預設集名稱不存在於 **[!UICONTROL 預設集名稱]** 下拉式清單方塊，表示您尚未建立任何批次集預設集。 另請參閱 [為影像集或迴轉集建立批次集預設集](#creating-bsp).

   若要移除套用的批次集預設集，請選取 **[!UICONTROL X]** 在預設集型別的右側。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存並關閉]**.

## 編輯批次集預設集 {#edit-bsp}

您可以編輯已建立的現有批次集預設集。 您可以變更您為資產命名慣例或序列順序建立的任何運算式群組。 如有需要，您也可以更新目的地資料夾並設定命名慣例。

但是，您無法變更預設集的名稱或預設集型別（「影像集」或「迴轉集」）。 如果必須變更預設集的名稱，請複製現有預設集並指定新名稱。 另請參閱 [複製批次集預設集](#copy-bsp).

如果您編輯先前套用至資料夾的批次集預設集，新編輯的批次集預設集只會套用至上傳至該資料夾的新資產。

如果您要將新編輯的預設集重新套用至資料夾中的現有資產，則必須重新處理資料夾。 <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->如此一來，現有資產便可加入影像集或迴轉集。 此外，已包含於影像集或迴轉集的現有資產（根據先前使用的批次集預設集）不會被移除並顯示原狀。 此情境假設他們不再符合新編輯的預設集資格。

**若要編輯批次集預設集，請執行下列動作：**

1. 選取Experience Manager標誌，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批次集預設集]**.
1. 於 **[!UICONTROL 批次集預設集]** 頁面，在頁面左側 **[!UICONTROL 預設集名稱]** 欄，勾選您要變更的批次集預設集。
1. 在工具列中，選取 **[!UICONTROL 編輯批次集預設集]**.
1. 視需要編輯預設集。
1. 在的右上角 **[!UICONTROL 批次集預設集]** 頁面，選取 **[!UICONTROL 儲存]**.

## 複製現有的批次集預設集 {#copy-bsp}

您可以複製現有的批次集預設集，以避免手動重新建立複雜的預設集，或您只是想重新命名預設集。 但是，您無法變更使用的預設集型別（影像集或迴轉集）。

如果您複製資產資料夾所參照的現有預設集，這些資料夾不受影響。

**複製現有的批次集預設集：**

1. 選取Experience Manager標誌，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批次集預設集]**.
1. 於 **[!UICONTROL 批次集預設集]** 頁面，在頁面左側 **[!UICONTROL 預設集名稱]** 欄中，選取您要複製的批次集預設集核取方塊。
1. 在工具列中，選取 **[!UICONTROL 複製]**.
1. 在 **[!UICONTROL 複製批次集預設集]** 對話方塊，在 **[!UICONTROL 標題]** 文字方塊中，輸入預設集的新名稱。

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. 選取 **[!UICONTROL 複製]**.

## 關於從資料夾中移除批次集預設集 {#remove-bsp-from-folder}

當您從資料夾中移除批次集預設集時，您上傳到這些資料夾的任何新資產都不會套用批次集預設集。 資料夾中已新增至影像集的現有資產，或根據套用至資料夾的批次集預設集以列印集為基礎的現有資產 — 繼續按原樣顯示。

如果您想要 *刪除* 請改為參閱資料夾中的預設集 [刪除批次集預設集](#delete-bsp).

您可以使用兩種方法從資料夾中移除批次集預設集。

* [透過「批次集預設集」頁面，從資料夾中移除批次集預設集](#remove-bsp-from-folders-via-bsp-page)  — 此方法提供您最大的彈性。 您可以從單一資料夾或多個資料夾中移除單一預設集或多個預設集。
* [從資料夾的「屬性」頁面移除批次集預設集](#remove-bsp-from-folders-via-properties)  — 此方法僅可讓您從單一資料夾中移除一個或多個批次集預設集。

### 透過「批次集預設集」頁面，從資料夾中移除批次集預設集 {#remove-bsp-from-folders-via-bsp-page}

1. 選取Experience Manager標誌，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批次集預設集]**.
1. 於 **[!UICONTROL 批次集預設集]** 頁面，在頁面左側 **[!UICONTROL 預設集名稱]** 欄中，選取一或多個批次集預設集的核取方塊，以將其從一或多個資料夾中移除。
1. 在工具列中，選取 **[!UICONTROL 從資料夾中移除批次預設集]**.

1. 於 **[!UICONTROL 選取資料夾]** 頁面上，選取一個或多個要移除批次集預設集的資料夾。
1. 在的右上角 **[!UICONTROL 選取資料夾]** 頁面，選取 **[!UICONTROL 移除]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. 在 **[!UICONTROL 移除設定檔]** 對話方塊，選取 **[!UICONTROL 移除]**.

### 從資料夾的「屬性」頁面移除批次集預設集 {#remove-bsp-from-folders-via-properties}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 導覽至您要移除一或多個批次集預設集的資料夾。
1. 在頁面上，左側的 **[!UICONTROL 名稱]** 欄中，選取資料夾的核取方塊。
1. 在工具列中，選取 **[!UICONTROL 屬性]**.
1. 在資料夾的「屬性」頁面上，選取「 」 **[!UICONTROL Dynamic Media處理中]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. 下 **[!UICONTROL 批次集預設集]**，選取 **[!UICONTROL X]** 在預設集型別的右側。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存並關閉]**.

## 刪除批次集預設集 {#delete-bsp}

您可以刪除批次集預設集，以將其永久從中移除 [!DNL Dynamic Media]. 也就是說，它們不會再顯示在 [!UICONTROL 批次集預設集] 頁面中也不會顯示 **[!UICONTROL 批次集預設集]** 下拉式清單 **[!UICONTROL Dynamic Media處理中]** 索引標籤在資料夾的 **[!UICONTROL 屬性]** 頁面。 因此，在重新處理資料夾或上傳新資產至資料夾時，預設集不會套用至現有資產。

如果您刪除先前套用至一或多個資料夾的預設集，則從這些資料夾中的資產建立的任何影像集或迴轉集都會繼續按原樣顯示。

如果您想要 *移除* 請改為參閱資料夾中的預設集 [從資料夾中移除批次集預設集](#remove-bsp-from-folder).

**若要刪除批次集預設集，請執行下列動作：**

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批次集預設集]**.
1. 於 **[!UICONTROL 批次集預設集]** 頁面，在頁面左側 **[!UICONTROL 預設集名稱]** 欄中，選取一或多個要刪除之批次集預設集的核取方塊。
1. 在工具列中，選取 **[!UICONTROL 刪除批次集預設集]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. 在 **[!UICONTROL 刪除批次集預設集]** 對話方塊，選取 **[!UICONTROL 刪除]**.

   如果您要刪除的預設集被資產資料夾引用，請選取「 」 **[!UICONTROL 強制刪除]** 而非。

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [图像集](/help/assets/dynamic-media/image-sets.md)
>* [旋转集](/help/assets/dynamic-media/spin-sets.md)
>* [在Dynamic Media中設定檔案夾層級的選擇性發佈](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)  — 如果您想深入瞭解將單一資料夾同步至，請參閱主題中的「同步模式」 [!DNL Dynamic Media].
>* [在Cloud Services中建立Dynamic Media設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)  — 如果您想深入瞭解同步處理所有資料夾，請參閱主題中的「Dynamic Media同步處理模式」 [!DNL Dynamic Media].

