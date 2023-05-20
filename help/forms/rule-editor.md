---
title: 如何使用最適化Forms規則編輯器？
description: 最適化Forms規則編輯器可讓您新增動態行為，並將複雜的邏輯建置到表單中，而不需要編碼或指令碼。 開始瞭解選擇規則建構的規則和准則。 進一步瞭解規則編輯器中可用的運運算元型別和事件。
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
exl-id: 6fd38e9e-435e-415f-83f6-3be177738c00
source-git-commit: e64e15c9096f837daa7fff5c64b8394736297579
workflow-type: tm+mt
source-wordcount: '6346'
ht-degree: 0%

---

# 将规则添加到自适应表单 {#adaptive-forms-rule-editor}

## 概述 {#overview}

規則編輯器功能可讓表單業務使用者和開發人員在調適型表單物件上撰寫規則。 這些規則會根據預設條件、使用者輸入和使用者對表單的動作，定義要在表單物件上觸發的動作。 它有助於進一步簡化表單填寫體驗，確保準確度和速度。

規則編輯器提供直覺式且簡化的使用者介面來撰寫規則。 規則編輯器為所有使用者提供一個視覺化編輯器。<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. --> 您可以使用規則在最適化表單物件上執行的部分關鍵動作包括：

* 顯示或隱藏物件
* 啟用或停用物件
* 設定物件的值
* 驗證物件的值
* 執行函式以計算物件的值
* 叫用表單資料模型服務並執行作業
* 設定物件的屬性

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

新增至表單超級使用者群組的使用者可以建立指令碼並編輯現有指令碼。 中的使用者 [!DNL forms-users] 群組可以使用指令碼，但不能建立或編輯指令碼。

## 瞭解規則 {#understanding-a-rule}

規則是動作和條件的組合。 在規則編輯器中，動作包括隱藏、顯示、啟用、停用或計算表單中物件值等活動。 條件是布林運算式，會透過對表單物件的狀態、值或屬性執行檢查和作業來評估。 動作是根據值( `True` 或 `False`)傳回的結果。

規則編輯器提供一組預先定義的規則型別（例如「何時」、「顯示」、「隱藏」、「啟用」、「停用」、「設定值」和「驗證」）來協助您編寫規則。 每個規則型別都可讓您定義規則中的條件和動作。 本檔案會詳細說明每個規則型別。

規則通常會遵循下列其中一種建構：

**Condition-Action** 在此建構中，規則會先定義條件，接著定義要觸發的動作。 此建構與程式設計語言中的if-then陳述式類似。

在規則編輯器中， **時間** 規則型別會強制執行condition-action結構。

**Action-Condition** 在此建構中，規則會先定義要觸發的動作，接著定義評估條件。 此建構的另一個變數為action-condition-alternate action，這也會定義在條件傳回False時要觸發的替代動作。

規則編輯器中的「顯示」、「隱藏」、「啟用」、「停用」、「設定值」和「驗證」規則型別會強制執行動作條件規則結構。 依預設，「顯示」的替代動作是「隱藏」，而「啟用」的替代動作是「停用」，反之亦然。 您無法變更預設的替代動作。

>[!NOTE]
>
>可用的規則型別（包括您在規則編輯器中定義的條件和動作）也取決於您建立規則的表單物件型別。 規則編輯器僅顯示有效的規則型別和選項，用於寫入特定表單物件型別的條件和動作陳述式。 例如，您看不到面板物件的「驗證」、「設定值」、「啟用」和「停用」規則型別。

如需規則編輯器中可用規則型別的詳細資訊，請參閱 [規則編輯器中的可用規則型別](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### 選擇規則建構的准則 {#guidelines-for-choosing-a-rule-construct}

雖然您可以使用任何規則建構來達成大部分的使用案例，以下提供選擇建構勝過其他建構的一些准則。 如需規則編輯器中可用規則的詳細資訊，請參閱 [規則編輯器中的可用規則型別](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* 建立規則時通常的經驗法則是在您寫入規則的物件內容中考慮它。 假設您要根據使用者在欄位A中指定的值隱藏或顯示欄位B。在此情況下，您評估的是欄位A的條件，而且根據它傳回的值，您會觸發欄位B的動作。

   因此，如果您要在欄位B （評估條件的物件）上撰寫規則，請使用condition-action建構或When規則型別。 同樣地，使用動作條件建構或在欄位A上顯示或隱藏規則型別。

* 有時候，您必須根據一個條件執行多個動作。 在這種情況下，建議使用條件 — 動作建構。 在此建構中，您可以評估條件一次，並指定多個動作陳述式。

   例如，若要根據檢查使用者在欄位A中指定的值的條件來隱藏欄位B、C和D，請撰寫一個規則，並在欄位A上使用條件 — 動作結構或When規則型別，並指定動作來控制欄位B、C和D的可見性。否則，您需要在欄位B、C和D上有三個單獨的規則，每個規則會檢查條件並顯示或隱藏各自的欄位。 在此範例中，在一個物件上撰寫「When」規則型別比在三個物件上撰寫「Show」或「Hide」規則型別更有效率。

* 若要根據多個條件觸發動作，建議使用動作條件建構。 例如，若要藉由評估欄位B、C和D的條件來顯示和隱藏欄位A，請在欄位A上使用顯示或隱藏規則型別。
* 如果規則包含適用於一個條件的一個動作，請使用條件 — 動作或動作條件建構。
* 如果規則檢查條件，並在欄位中提供值或退出欄位時立即執行動作，建議在評估條件的欄位上使用條件 — 動作建構或When規則型別來撰寫規則。
* 當使用者變更套用When規則的物件值時，會評估When規則中的條件。 不過，如果您希望動作在伺服器端變更時觸發（例如預先填入值），建議編寫在欄位初始化時觸發動作的When規則。
* 在撰寫下拉清單、選項按鈕或核取方塊物件的規則時，規則編輯器中會預先填入表單中這些表單物件的選項或值。

## 規則編輯器中可用的運運算元型別和事件 {#available-operator-types-and-events-in-rule-editor}

規則編輯器提供下列邏輯運運算元和事件，您可使用它們建立規則。

* **等於**
* **不等於**
* **開頭為**
* **結尾為**
* **包含**
* **为空**
* **不为空**
* **已選取：** 當使用者為核取方塊、下拉式清單單選按鈕選取特定選項時傳回true。
* **已初始化（事件）：** 當表單物件在瀏覽器中呈現時傳回true。
* **已變更（事件）：** 當使用者變更表單物件的輸入值或選取的選項時，傳回true。
* **導覽（事件）：** 當使用者按一下導覽物件時傳回true。 導覽物件用於在面板之間移動。
* **步驟完成（事件）：** 規則的步驟完成時傳回true。
* **提交成功（事件）：** 成功將資料提交至表單資料模型時會傳回true。
* **提交時發生錯誤（事件）：**  資料提交至表單資料模型失敗時傳回true。

## 規則編輯器中的可用規則型別 {#available-rule-types-in-rule-editor}

規則編輯器提供了一組預先定義的規則型別，您可以使用這些型別來編寫規則。 讓我們來詳細瞭解每種規則型別。 如需在規則編輯器中寫入規則的詳細資訊，請參閱 [寫入規則](rule-editor.md#p-write-rules-p).

### [!UICONTROL 时间] {#whenruletype}

此 **[!UICONTROL 時間]** 規則型別會遵循 **condition-action-alternate action** 規則結構，或有時僅 **condition-action** 建構。 在此規則型別中，您先指定評估條件，接著指定在條件符合時觸發的動作( `True`)。 使用When規則型別時，您可以使用多個AND和OR運運算元來建立 [巢狀運算式](#nestedexpressions).

使用When規則型別，您可以評估表單物件的條件，並對一個或多個物件執行動作。

簡單地說，典型的When規則結構如下：

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

物件B上的動作2；以及物件C上的動作3；

_

當您有多值元件（例如選項按鈕或清單）時，為該元件建立規則時，會自動擷取選項，並讓規則建立者可以使用這些選項。 您不需要再次輸入選項值。

例如，清單有四個選項：紅色、藍色、綠色和黃色。 建立規則時，會自動擷取選項（選項按鈕），以供規則建立者使用，如下所示：

![多值顯示選項](assets/multivaluefcdisplaysoptions.png)

撰寫When規則時，您可以觸發Clear Value Of動作。 清除值動作會清除指定物件的值。 在When陳述式中將的清除值作為選項可讓您建立具有多個欄位的複雜條件。

![清除值](assets/clearvalueof.png)

**[!UICONTROL 隱藏]** 隱藏指定的物件。

**[!UICONTROL 顯示]** 顯示指定的物件。

**[!UICONTROL 啟用]** 啟用指定的物件。

**[!UICONTROL 停用]** 停用指定的物件。

**[!UICONTROL 啟動服務]** 叫用表單資料模型中設定的服務。 選擇「啟動服務」作業時，會出現一個欄位。 點選欄位時，它會顯示您在上的所有表單資料模型中設定的所有服務 [!DNL Experience Manager] 執行個體。 選擇「表單資料模型」服務時，會出現更多欄位，您可以在其中使用指定服務的輸入和輸出引數對應表單物件。 請參閱呼叫表單資料模型服務的範例規則。

除了表單資料模型服務之外，您還可以指定直接的WSDL URL來叫用Web服務。 不過，表單資料模型服務有許多優點，且建議叫用服務的方法。

如需在表單資料模型中設定服務的詳細資訊，請參閱 [[!DNL Experience Manager Forms] 資料整合](data-integration.md).

**[!UICONTROL 設定值]** 計算並設定指定物件的值。 您可以將物件值設定為字串、其他物件的值、使用數學運算式或函式的計算值、物件屬性的值，或來自已設定表單資料模型服務的輸出值。 當您選擇Web服務選項時，它會在您的頁面上顯示所有表單資料模型中設定的所有服務 [!DNL Experience Manager] 執行個體。 選擇「表單資料模型」服務時，會出現更多欄位，您可以在其中使用指定服務的輸入和輸出引數對應表單物件。

如需在表單資料模型中設定服務的詳細資訊，請參閱 [[!DNL Experience Manager Forms] 資料整合](data-integration.md).

此 **[!UICONTROL 設定屬性]** 規則型別可讓您根據條件動作來設定指定物件的屬性值。

它可讓您定義規則，以動態地將核取方塊新增至最適化表單。 您可以使用自訂函式、表單物件或物件屬性來定義規則。

![设置属性](assets/set_property_rule_new.png)

若要根據自訂函式定義規則，請選取 **[!UICONTROL 函式輸出]** ，然後從「 」拖放自訂函式 **[!UICONTROL 函式]** 標籤。 如果符合條件動作，則自訂函式中定義的核取方塊數會新增至最適化表單。

若要根據表單物件定義規則，請選取 **[!UICONTROL 表單物件]** 從下拉式清單中，將表單物件從 **[!UICONTROL 表單物件]** 標籤。 如果符合條件動作，則表單物件中定義的核取方塊數會新增至調適型表單。

根據物件屬性的Set Property規則可讓您根據最適化表單中包含的其他物件屬性，新增最適化表單中的核取方塊數量。

下圖是根據最適化表單中的下拉式清單數目，以動態方式新增核取方塊的範例：

![对象属性](assets/object_property_set_property_new.png)

**[!UICONTROL 清除值]** 清除指定物件的值。

**[!UICONTROL 設定焦點]** 設定焦點在指定的物件。

**[!UICONTROL 儲存表單]** 儲存表單。

**[!UICONTROL 提交Forms]** 提交表單。

**[!UICONTROL 重設表單]** 重設表單。

**[!UICONTROL 驗證表單]** 驗證表單。

**[!UICONTROL 新增例項]** 新增指定之可重複面板或表格列的例項。

**[!UICONTROL 移除例項]** 移除指定之可重複面板或表格列的例項。

**[!UICONTROL 導覽至]** 導覽至其他 <!--Interactive Communications,--> 最適化Forms、影像或檔案片段等其他資產，或外部URL。 <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

### [!UICONTROL 设置值] {#set-value-of}

此 **[!UICONTROL 設定值]** 規則型別可讓您根據是否滿足指定的條件來設定表單物件的值。 值可以設定為另一個物件的值、常值字串、衍生自數學運算式或函式的值、另一個物件的屬性值，或Form Data Model服務的輸出。 同樣地，您可以檢查元件、字串、屬性或衍生自函式或數學運算式的值的條件。

此 **設定值** 規則型別不適用於所有表單物件，例如面板和工具列按鈕。 標準「設定值」規則具有以下結構：

將物件A的值設為：

（字串ABC） OR （物件C的物件屬性X） OR （函式的值） OR （數學運算式的值） OR （資料模型服務或Web服務的輸出值）；

時間（選擇性）：

（條件1和條件2和條件3）為TRUE；

以下範例將值帶入 `dependentid` 欄位作為輸入，並設定 `Relation` 欄位至輸出 `Relation` 的引數 `getDependent` 表單資料模型服務。

![Set-value-web-service](assets/set-value-web-service.png)

使用表單資料模型服務的設定值規則範例

>[!NOTE]
>
>此外，您可以使用規則的「設定值」，從表單資料模型服務或Web服務的輸出，填入下拉式清單元件中的所有值。 不過，請確定您選擇的輸出引數屬於陣列型別。 陣列中傳回的所有值都可在指定的下拉式清單中使用。

### [!UICONTROL 显示] {#show}

使用 **[!UICONTROL 顯示]** 規則型別，您可以根據是否滿足條件來編寫顯示或隱藏表單物件的規則。 Show rule型別也會在條件不滿足或傳回時觸發Hide動作 `False`.

典型的Show規則結構如下：

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

### [!UICONTROL 隐藏] {#hide}

與顯示規則型別類似，您可以使用 **[!UICONTROL 隱藏]** 規則型別，根據是否滿足條件來顯示或隱藏表單物件。 若條件不滿足或傳回，隱藏規則型別也會觸發「顯示」動作 `False`.

典型的「隱藏」規則的結構如下：

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

### [!UICONTROL 启用] {#enable}

此 **[!UICONTROL 啟用]** 規則型別可讓您根據是否滿足條件來啟用或停用表單物件。 Enable規則型別也會在條件未滿足或傳回時觸發Disable動作 `False`.

典型的Enable規則結構如下：

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

### [!UICONTROL 禁用] {#disable}

與啟用規則型別類似， **[!UICONTROL 停用]** 規則型別可讓您根據是否滿足條件來啟用或停用表單物件。 Disable規則型別也會在條件不滿足或傳回時觸發Enable動作 `False`.

典型的「停用」規則的結構如下：

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### [!UICONTROL 验证] {#validate}

此 **[!UICONTROL 驗證]** 規則型別會使用運算式來驗證欄位中的值。 例如，您可以編寫運算式來檢查指定名稱的文字方塊是否不包含特殊字元或數字。

典型的驗證規則結構如下：

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>如果指定的值不符合驗證規則，您可以向使用者顯示驗證訊息。 您可以在 **[!UICONTROL 指令碼驗證訊息]** 欄中元件屬性的欄位。

![指令碼驗證](assets/script-validation.png)

### [!UICONTROL 設定選項] {#setoptionsof}

此 **[!UICONTROL 設定選項]** 規則型別可讓您定義規則，以動態地將核取方塊新增至最適化表單。 您可以使用表單資料模型或自訂函式來定義規則。

若要根據自訂函式定義規則，請選取 **[!UICONTROL 函式輸出]** ，然後從「 」拖放自訂函式 **[!UICONTROL 函式]** 標籤。 自訂函式中定義的核取方塊數會新增至最適化表單。

![自訂函式](assets/custom_functions_set_options_new.png)

若要建立自訂函式，請參閱 [規則編輯器中的自訂函式](#custom-functions).

若要根據表單資料模型定義規則：

1. 選取 **[!UICONTROL 服務輸出]** 下拉式清單中的。
1. 選取資料模型物件。
1. 從中選擇資料模型物件屬性 **[!UICONTROL 顯示值]** 下拉式清單。 最適化表單中的核取方塊數目是從資料庫中為該屬性定義的例項數目衍生而來。
1. 從中選擇資料模型物件屬性 **[!UICONTROL 儲存值]** 下拉式清單。

![FDM設定選項](assets/fdm_set_options_new.png)

## 瞭解規則編輯器使用者介面 {#understanding-the-rule-editor-user-interface}

規則編輯器提供完整但簡單的使用者介面，用於撰寫和管理規則。 您可以在製作模式下，從最適化表單中啟動規則編輯器使用者介面。

若要啟動規則編輯器使用者介面：

1. 在製作模式中開啟最適化表單。
1. 點選您要為其寫入規則的表單物件，然後在「元件工具列」中點選 ![edit-rules](assets/edit-rules-icon.svg). 規則編輯器使用者介面隨即顯示。

   ![create-rules](assets/create-rules.png)

   此檢視中會列出所選表單物件上的任何現有規則。 如需有關管理現有規則的資訊，請參閱 [管理規則](rule-editor.md#p-manage-rules-p).

1. 點選 **[!UICONTROL 建立]** 以撰寫新規則。 第一次啟動規則編輯器時，預設會開啟規則編輯器使用者介面的視覺化編輯器。

   ![規則編輯器UI](assets/rule-editor-ui.png)

讓我們來詳細瞭解規則編輯器UI的每個元件。

### A.元件規則顯示 {#a-component-rule-display}

顯示啟動規則編輯器所使用的最適化表單物件的標題，以及目前選取的規則型別。 在上述範例中，規則編輯器是從名為Salary的最適化表單物件啟動，而選取的規則型別是When。

### B.表單物件和函式 {#b-form-objects-and-functions-br}

規則編輯器使用者介面左側的窗格包含兩個標籤 —  **[!UICONTROL Forms物件]** 和 **[!UICONTROL 函式]**.

「表單物件」標籤會顯示最適化表單中包含之所有物件的階層檢視。 它會顯示物件的標題和型別。 在撰寫規則時，您可以將表單物件拖放至規則編輯器上。 將物件或函式拖放至預留位置時，在建立或編輯規則時，預留位置會自動採用適當的值型別。

已套用一或多個有效規則的表單物件會以綠色圓點標示。 如果套用至表單物件的任何規則無效，則表單物件會標示為黃色點。

「函式」標籤包含一組內建函式，例如「總和」、「最小值」、「最大值」、「平均值」、「數目」和「驗證表單」。 您可以使用這些函式計算可重複面板和表格列中的值，並在寫入規則時在動作和條件陳述式中使用它們。 不過，您可以建立 [自訂函式](#custom-functions) 也是。

![函式標籤](assets/functions.png)

>[!NOTE]
>
>您可以在Forms「物件」和「函式」標籤中對物件和函式名稱及標題執行文字搜尋。

在表單物件的左側樹狀結構中，您可以點選表單物件以顯示套用至每個物件的規則。 您不僅可以導覽各種表單物件的規則，還可以複製並貼上表單物件之間的規則。 如需詳細資訊，請參閱 [複製貼上規則](rule-editor.md#p-copy-paste-rules-p).

### C.表單物件和函式切換 {#c-form-objects-and-functions-toggle-br}

點選切換按鈕時，會切換表單物件和函式窗格。

### D.視覺規則編輯器 {#visual-rule-editor}

視覺化規則編輯器是規則編輯器使用者介面的視覺化編輯器模式中寫入規則的區域。 它可讓您選取規則型別，並據此定義條件和動作。 在規則中定義條件和動作時，您可以從「表單物件和函式」窗格拖放表單物件和函式。

如需使用視覺化規則編輯器的詳細資訊，請參閱 [寫入規則](rule-editor.md#p-write-rules-p).
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and vice versa, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E.完成和取消按鈕 {#done-and-cancel-buttons}

此 **[!UICONTROL 完成]** 按鈕可用來儲存規則。 您可以儲存不完整的規則。 但是，不完整內容無效，且不會執行。 當您下次從相同表單物件啟動規則編輯器時，會列出表單物件上已儲存的規則。 您可以在該檢視中管理現有規則。 如需詳細資訊，請參閱 [管理規則](rule-editor.md#p-manage-rules-p).

此 **[!UICONTROL 取消]** 按鈕會捨棄您對規則所做的任何變更並關閉規則編輯器。

## 寫入規則 {#write-rules}

您可以使用視覺規則編輯器來撰寫規則 &lt;!> — 或程式碼編輯器>。 第一次啟動規則編輯器時，它會在視覺化編輯器模式下開啟。 您可以切換到程式碼編輯器模式並編寫規則。 不過，如果您在程式碼編輯器中撰寫或修改規則，則必須清除程式碼編輯器，才能切換至該規則的視覺化編輯器。 當您下次啟動規則編輯器時，它會在您上次用來建立規則的模式中開啟。

讓我們先來看看如何使用視覺化編輯器來撰寫規則。

### 使用視覺化編輯器 {#using-visual-editor}

讓我們瞭解如何使用下列範例表單在視覺化編輯器中建立規則。

![Create-rule-example](assets/create-rule-example.png)

範例貸款申請表單中的「貸款需求」區段會要求申請人指定其婚姻狀況、薪資，如果已婚，則需指定其配偶的薪資。 規則會根據使用者輸入來計算貸款資格金額，並顯示在「貸款資格」欄位中。 套用下列規則以實施情境：

* 配偶的「薪資」欄位僅在「婚姻狀況」為「已婚」時顯示。
* 貸款資格金額為總薪資的50%。

若要寫入規則，請執行下列步驟：

1. 首先，根據使用者為「婚姻狀況」選項按鈕選取的選項，撰寫規則以控制「配偶薪資」欄位的可見度。

   以撰寫模式開啟貸款申請表單。 點選 **[!UICONTROL 婚姻狀況]** 元件並點選 ![edit-rules](assets/edit-rules-icon.svg). 下一步，點選 **[!UICONTROL 建立]** 以啟動規則編輯器。

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   啟動規則編輯器時，預設會選取When規則。 此外，您啟動規則編輯器的表單物件（在此例中為「婚姻狀況」）也會在When陳述式中指定。

   雖然您無法變更或修改選取的物件，但您可以使用規則下拉式清單（如下所示）來選取其他規則型別。 如果您想在另一個物件上建立規則，請點選「取消」以退出規則編輯器，然後從所需的表單物件再次啟動它。

1. 點選 **[!UICONTROL 選取狀態]** 下拉式清單並選取 **[!UICONTROL 等於]**. 此 **[!UICONTROL 輸入字串]** 欄位隨即顯示。

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   在「婚姻狀況」選項按鈕中， **[!UICONTROL 已婚]** 和 **[!UICONTROL 單一]** 已指派選項 **0** 和 **1** 個值。 您可以在「編輯」選項按鈕對話方塊的「標題」標籤中驗證指派的值，如下所示。

   ![規則編輯器的選項按鈕值](assets/radio-button-values.png)

1. 在 **[!UICONTROL 輸入字串]** 欄位，請指定 **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   您已將條件定義為 `When Marital Status is equal to Married`. 接下來，定義此條件為True時要執行的動作。

1. 在Then陳述式中，選取 **[!UICONTROL 顯示]** 從 **[!UICONTROL 選取動作]** 下拉式清單。

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. 拖放 **[!UICONTROL 配偶薪資]** 欄位。 **[!UICONTROL 拖放物件或在這裡選取]** 欄位。 或者，點選 **[!UICONTROL 拖放物件或在這裡選取]** 欄位並選取 **[!UICONTROL 配偶薪資]** 欄位，其中列出表單中的所有表單物件。

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   規則在規則編輯器中會顯示如下。

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

1. 點選 **[!UICONTROL 完成]** 以儲存規則。

1. 重複步驟1到5，定義另一個規則，以隱藏「配偶薪資」欄位（若婚姻狀況為「單身」）。 規則在規則編輯器中會顯示如下。

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >或者，您可以在「配偶薪資」欄位上撰寫一個「顯示」規則，而不是「婚姻狀況」欄位上撰寫兩個「當規則」，以實施相同的行為。

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. 接下來，撰寫規則以計算貸款資格金額（為薪資總額的50%），並在「貸款資格」欄位中顯示該金額。 若要獲得此結果，請建立 **[!UICONTROL 設定值]** 「貸款資格」欄位的規則。

   在製作模式中，點選 **[!UICONTROL 貸款資格]** 欄位並點選 ![edit-rules](assets/edit-rules-icon.svg). 下一步，點選 **[!UICONTROL 建立]** 以啟動規則編輯器。

1. 選取 **[!UICONTROL 設定值]** 規則下拉式清單中的規則。

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. 點選 **[!UICONTROL 選取選項]** 並選取 **[!UICONTROL 數學運算式]**. 用於寫入數學運算式的欄位隨即開啟。

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. 在運算式欄位中：

   * 從「Forms物件」標籤中選取或拖放 **[!UICONTROL 薪資]** 第一個欄位 **[!UICONTROL 拖放物件或在這裡選取]** 欄位。

   * 選取 **[!UICONTROL 加號]** 從 **[!UICONTROL 選取運運算元]** 欄位。

   * 從「Forms物件」標籤中選取或拖放 **[!UICONTROL 配偶薪資]** 其他欄位 **[!UICONTROL 拖放物件或在這裡選取]** 欄位。

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. 接下來，在運算式欄位周圍反白顯示的區域中點選，然後點選 **[!UICONTROL 延伸運算式]**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   在延伸運算式欄位中，選取 **[!UICONTROL 除以]** 從 **[!UICONTROL 選取運運算元]** 欄位和 **[!UICONTROL 數字]** 從 **[!UICONTROL 選取選項]** 欄位。 然後，指定 **[!UICONTROL 2]** 在數字欄位中。

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >您可以從「選取選項」欄位使用元件、函式、數學運算式和屬性值來建立複雜運算式。

   接著，建立條件，當傳回True時，執行運算式。

1. 點選 **[!UICONTROL 新增條件]** 新增When陳述式。

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   在When陳述式中：

   * 從「Forms物件」標籤中選取或拖放 **[!UICONTROL 婚姻狀況]** 第一個欄位 **[!UICONTROL 拖放物件或在這裡選取]** 欄位。

   * 選取 **[!UICONTROL 等於]** 從 **[!UICONTROL 選取運運算元]** 欄位。

   * 選取其他中的字串 **[!UICONTROL 拖放物件或在這裡選取]** 欄位並指定 **[!UICONTROL 已婚]** 在 **[!UICONTROL 輸入字串]** 欄位。

   規則編輯器中的規則最後會如下所示。  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

1. 點選 **[!UICONTROL 完成]**. 這會儲存規則。

1. 重複步驟7到14，定義另一個規則，以計算婚姻狀況為「單身」時的貸款資格。 規則在規則編輯器中會顯示如下。

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>或者，您可以使用「設定值」規則，在您建立用來顯示 — 隱藏「配偶薪資」欄位的「時間」規則中計算貸款資格。 當「婚姻狀況」為「單一」時，產生的合併規則會顯示在規則編輯器中，如下所示。
>
>同樣地，您可以撰寫合併規則來控制「配偶薪資」欄位的可見度，並在「婚姻狀況」為「已婚」時計算貸款資格。

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

<!-- ### Using code editor {#using-code-editor}

Users added to the forms-power-users group can use code editor. The rule editor auto generates the JavaScript code for any rule you create using visual editor. You can switch from visual editor to the code editor to view the generated code. However, if you modify the rule code in the code editor, you cannot switch back to the visual editor. If you prefer writing rules in code editor rather than visual editor, you can write rules afresh in the code editor. The visual-code editors switcher helps you switch between the two modes.

The code editor JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. These expressions return values of certain types. For the complete list of Adaptive Forms classes, events, objects, and public APIs, see [JavaScript Library API reference for Adaptive Forms](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

For more information about guidelines to write rules in the code editor, see [Adaptive Form Expressions](adaptive-form-expressions.md).

While writing JavaScript code in the rule editor, the following visual cues help you with the structure and syntax:

* Syntax highlights

* Auto Indentation

* Hints and suggestions for Form objects, functions, and their properties

* Auto completion of form component names and common JavaScript functions

![javascriptruleeditor](assets/javascriptruleeditor.png)
-->

#### 規則編輯器中的自訂函式 {#custom-functions}

除了開箱即用的功能，例如 *總和* 「函式輸出」下列出的函式，您可以編寫經常需要的自訂函式。 請確定您撰寫的函式附有 `jsdoc` 在其上方。

隨附 `jsdoc` 必填：

* 如果您想要自訂設定和說明
* 因為有多種方式可以在中宣告函式 `JavaScript,` 和註解可讓您追蹤函式。

規則編輯器支援指令碼和自訂函式的JavaScript ES2015語法。
如需詳細資訊，請參閱 [jsdoc.app](https://jsdoc.app/).

支援 `jsdoc` 標籤：

* **私人**
語法：私用函式不會作為自訂函式納入。`@private`
私有函式不會包含為自訂函式。

* **名稱**
語法：或者 `@name funcName <Function Name>`
或者 `,` 您可以使用： `@function funcName <Function Name>` **或** `@func` `funcName <Function Name>`.
   `funcName` 是函式的名稱（不允許空格）。
   `<Function Name>` 是函式的顯示名稱。

* **會員**
語法：將名稱空間附加至函式。`@memberof namespace`
將名稱空間附加至函式。

* **引數**
語法：或者，您可以使用： `@param {type} name <Parameter Description>`
或者，您可以使用： `@argument` `{type} name <Parameter Description>` **或** `@arg` `{type}` `name <Parameter Description>`.
顯示函式使用的引數。 函式可以有多個引數標籤，每個引數會依發生順序各一個標籤。
   `{type}` 代表引數型別。 允許的引數型別包括：

   1. 字符串
   1. 数字
   1. 布尔型
   1. 範圍

   範圍是指最適化表單的欄位。 表單使用延遲載入時，您可以使用 `scope` 以存取其欄位。 您可以在載入欄位時存取欄位，或者如果欄位標示為全域。

   所有引數型別都歸類於上述其中一種。 不支援無。 請確定您選取上述其中一種型別。 型別不區分大小寫。 引數中不允許有空格 `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **傳回型別**
語法：或者，您可以使用 `@return {type}`
或者，您可以使用 `@returns {type}`.
新增函式的相關資訊，例如其目標。
{type}代表函式的傳回型別。 允許的傳回型別包括：

   1. 字符串
   1. 数字
   1. 布尔型

   所有其他回訪型別則歸類到上述任一型別之下。 不支援無。 請確定您選取上述其中一種型別。 傳回型別不區分大小寫。

   * **此**
語法： 
`@this currentComponent`
   使用@this可參照寫入規則的最適化表單元件。

   以下範例是根據欄位值。 在以下範例中，規則會隱藏表單中的欄位。 此 `this` 部分 `this.value` 指寫入規則的基礎調適型表單元件。

   ```
      /**
      * @function myTestFunction
      * @this currentComponent
      * @param {scope} scope in which code inside function will be executed.
      */
      myTestFunction = function (scope) {
         if(this.value == "O"){
               scope.age.visible = true;
         } else {
            scope.age.visible = false;
         }
      }
   ```

   >[!NOTE]
   >
   >摘要使用自訂函式之前的註解。 摘要可延伸至多行，直到遇到標籤為止。 將大小限製為單一，以在規則產生器中提供簡要說明。

**新增自訂函式**

例如，您想要新增計算正方形區域的自訂函式。 Side length是自訂函式的使用者輸入，可使用表單中的數值方塊來接受。 計算的輸出會顯示在表單的另一個數值方塊中。 若要新增自訂函式，您必須先建立使用者端資料庫，然後將其新增到CRX存放庫。

若要建立使用者端程式庫並將其新增至CRX存放庫，請執行以下步驟：

1. 建立使用者端對程式庫執行下列步驟。 如需詳細資訊，請參閱 [使用使用者端資料庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).
1. 在CRXDE中，新增屬性 `categories`字串型別值為 `customfunction` 至 `clientlib` 資料夾。

   >[!NOTE]
   >
   >`customfunction`是範例類別。 您可以為在中建立的類別選擇任何名稱 `clientlib`資料夾。

在CRX存放庫中新增使用者端程式庫後，請將其用於最適化表單。 它可讓您使用自訂函式作為表單中的規則。 若要在最適化表單中新增使用者端程式庫，請執行下列步驟：

1. 在編輯模式下開啟您的表單。
若要以編輯模式開啟表單，請選取表單並點選 **[!UICONTROL 開啟]**.
1. 在編輯模式中，選取元件，然後點選 ![欄位層級](assets/select_parent_icon.svg) > **[!UICONTROL 最適化表單容器]**，然後點選 ![cmppr](assets/configure-icon.svg).
1. 在側邊欄中的「使用者端資料庫名稱」下方，新增使用者端資料庫。 ( `customfunction` 在此範例中。)

   ![新增自訂函式使用者端程式庫](assets/clientlib.png)

1. 選取輸入數字方塊，然後點選 ![edit-rules](assets/edit-rules-icon.svg) 以開啟規則編輯器。
1. 點選 **[!UICONTROL 建立規則]**. 使用下列選項，建立規則以將輸入的平方值儲存在表單的「輸出」欄位中。

   [![使用自訂函式建立規則](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)

1. 點選 **[!UICONTROL 完成]**. 您的自訂函式已新增。

#### 函式宣告支援的型別 {#function-declaration-supported-types}

**函式陳述式**

```javascript
function area(len) {
    return len*len;
}
```

此函式包含但不包含 `jsdoc` 評論。

**函式運算式**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**函式運算式和陳述式**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**函式宣告為變數**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

限制：自訂函式只會從變數清單中挑選第一個函式宣告（如果同時挑選）。 您可以對每個宣告的函式使用函式運算式。

**函式宣告為物件**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>確保您使用 `jsdoc` 每個自訂函式。 雖然 `jsdoc`建議使用註解，包括空白 `jsdoc`備註以將您的函式標示為自訂函式。 它會啟用自訂函式的預設處理。

## 管理規則 {#manage-rules}

當您點選物件並點選時，會列出表單物件上任何現有的規則 ![edit-rules1](assets/edit-rules-icon.svg). 您可以檢視標題並預覽規則摘要。 此外，UI可讓您展開並檢視完整的規則摘要、變更規則的順序、編輯規則以及刪除規則。

![List-rules](assets/list-rules.png)

您可以對規則執行下列動作：

* **展開/收合**：規則清單中的「內容」欄會顯示規則內容。 如果整個規則內容在預設檢視中不可見，請點選 ![expand-rule-content](assets/Smock_ChevronDown.svg) 以將其展開。

* **重新排序**：您建立的任何新規則都會棧疊在規則清單底部。 規則會從上到下執行。 頂端的規則會先執行，接著執行相同型別的其他規則。 例如，如果您分別從頂端開始，在第一、第二、第三和第四個位置有When、Show、Enable和When規則，則頂端的When規則會先執行，接著在第四個位置有When規則。 接著會執行「顯示」和「啟用」規則。
您可以點選以變更規則的順序 ![sort-rules](assets/sort-rules.svg) 或將其拖放至清單中所需的順序。

* **編輯**：若要編輯規則，請選取規則標題旁的核取方塊。 隨即顯示編輯和刪除規則的選項。 點選 **[!UICONTROL 編輯]** 在規則編輯器中開啟選取的規則 <!-- in visual  or code editor mode depending on the mode used to create the rule -->.

* **刪除**：若要刪除規則，請選取規則並點選 **[!UICONTROL 刪除]**.

* **啟用/停用**：您必須暫時暫停使用規則時，可以選取一或多個規則並點選 **[!UICONTROL 停用]** 以停用動作。 如果規則已停用，則不會在執行階段執行。 若要啟用已停用的規則，您可以選取該規則，然後點選動作工具列中的「啟用」。 規則的狀態列顯示規則是啟用還是停用。

![停用規則](assets/disablerule.png)

## 複製貼上規則 {#copy-paste-rules}

您可以將規則從一個欄位複製並貼上到其他類似欄位，以節省時間。

若要複製貼上規則，請執行下列動作：

1. 點選您要從中複製規則的表單物件，然後在元件工具列點選 ![編輯規則](assets/edit-rules-icon.svg). 規則編輯器使用者介面隨即出現，並選取表單物件，而現有規則隨即出現。

   ![複製規則](assets/copyrule.png)

   如需有關管理現有規則的資訊，請參閱 [管理規則](rule-editor.md#p-manage-rules-p).

1. 選取規則標題旁的核取方塊，管理規則的選項就會顯示。 点按&#x200B;**[!UICONTROL 复制]**。

   ![copyrule2](assets/copyrule2.png)

1. 選取您要貼上規則的其他表單物件，然後點選 **[!UICONTROL 貼上]**. 此外，您可以編輯規則以對其進行變更。

   >[!NOTE]
   >
   >只有在表單物件支援複製的規則事件時，您才能將規則貼到另一個表單物件。 例如，按鈕支援點選事件。 您可以將含有點按事件的規則貼到按鈕上，但不可貼到核取方塊上。

1. 點選 **[!UICONTROL 完成]** 以儲存規則。

## 巢狀運算式 {#nestedexpressions}

規則編輯器可讓您使用多個AND和OR運運算元來建立巢狀規則。 您可以在規則中混合使用多個AND和OR運運算元。

以下是巢狀規則的範例，會在符合必要條件時，向使用者顯示有關兒童監護權的資格的訊息。

![複雜運算式](assets/complexexpression.png)

您也可以拖放規則中的條件以進行編輯。 點選並將滑鼠懸停在控點上( ![控制代碼](assets/drag-handle.svg))之前填入。 指標變成如下所示的手形符號後，請將條件拖放至規則內的任何位置。 規則結構會變更。

![拖放](assets/drag-and-drop.png)

## 日期運算式條件 {#dateexpression}

規則編輯器可讓您使用日期比較來建立條件。

以下是一個範例條件，會在房屋已抵押時顯示靜態文字物件，使用者需填入日期欄位來表示該條件。

當使用者填寫的屬性按揭日期為過去時，最適化表單會顯示有關收入計算的附註。 下列規則會比較使用者填寫的日期與目前日期，如果使用者填寫的日期早於目前日期，則表單會顯示文字訊息（名為Income）。

![日期運算式條件](assets/dateexpressioncondition.png)

當填寫日期早於目前日期時，表單會顯示文字訊息（收入）如下：

![符合日期運算式條件](assets/dateexpressionconditionmet.png)

## 數字比較條件 {#number-comparison-conditions}

規則編輯器可讓您建立可比較兩個數字的條件。

以下範例條件會在應徵者停留在目前地址的月數少於36時顯示靜態文字物件。

![數字比較條件](assets/numbercomparisoncondition.png)

當使用者表示在目前的居住地址生活不到36個月時，表單會顯示通知，指出可要求更多居住證明。

![已要求更多校訂](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

## 規則範例 {#example}

### 啟動表單資料模型服務 {#invoke}

考慮Web服務 `GetInterestRates` 以貸款金額、保有權和申請者的信用評分作為輸入，並傳回包含EMI金額和利率的貸款計畫。 您可以使用Web服務作為資料來源來建立表單資料模型。 您新增資料模型物件和 `get` 表單模型的服務。 此服務會出現在表單資料模型的「服務」標籤中。 然後，建立包含資料模型物件欄位的最適化表單，以擷取使用者對貸款金額、保有權和信用評分的輸入。 新增觸發Web服務擷取計畫詳細資料的按鈕。 輸出會填入適當的欄位中。

下列規則顯示如何設定叫用服務動作以完成範例情境。

![Example-invoke-services](assets/example-invoke-services.png)

使用最適化表單規則叫用表單資料模型服務

### 使用When規則觸發多個動作 {#triggering-multiple-actions-using-the-when-rule}

在貸款申請表單中，您想要擷取貸款申請人是否為現有客戶。 根據使用者提供的資訊，客戶ID欄位應顯示或隱藏。 此外，如果使用者是現有客戶，您想要將焦點設定在客戶ID欄位。 貸款申請表單包含下列元件：

* 選項按鈕， **[!UICONTROL 您是Geometrixx的現有客戶嗎？]**，可提供 [!UICONTROL 是] 和 [!UICONTROL 否] 選項。 「是」的值為 **0** 而否為 **1**.

* 文字欄位， **[!UICONTROL Geometrixx客戶ID]**，以指定客戶ID。

當您在選項按鈕上撰寫When規則來實作此行為時，該規則在視覺規則編輯器中會顯示如下。

![When-rule-example](assets/when-rule-example.png)

視覺化編輯器中的規則

在範例規則中，When區段中的陳述式是條件，當傳回True時，會執行Then區段中指定的動作。

<!-- The rule appears as follows in the code editor.

![when-rule-example-code](assets/when-rule-example-code.png) 

Rule in the code editor -->

### 在規則中使用函式輸出 {#using-a-function-output-in-a-rule}

在採購單表單中，您有下表，使用者可在其中填寫其訂單。 在此表格中：

* 第一列是可重複的，因此使用者可以訂購多個產品並指定不同的數量。 其元素名稱為 `Row1`.
* 重複資料列之「產品數量」欄中的儲存格標題為「數量」。 此儲存格的元素名稱為 `productquantity`.
* 表格中的第二列是不可重複的，且此列中「產品數量」欄中的儲存格標題為「總數量」。

![Example-function-table](assets/example-function-table.png)

**答：** Row1 **B.** 數量 **C.** 總數量

現在，您要在所有產品的「產品數量」欄中新增指定數量，並在「總數量」儲存格中顯示總和。 您可以在「總數量」儲存格上撰寫「設定值」規則，以達到此總和，如下所示。

![Example-function-output](assets/example-function-output.png)

視覺化編輯器中的規則

<!-- he rule appears as follows in the code editor.

![example-function-output-code](assets/example-function-output-code.png)

Rule in the code editor -->

### 使用運算式驗證欄位值 {#validating-a-field-value-using-expression}

在上一個範例中說明的採購單表單中，您想要限制使用者訂購超過一個數量的任何訂價超過10000個數量的產品。 若要執行此驗證，您可以編寫驗證規則，如下所示。

![Example-validate](assets/example-validate.png)

視覺化編輯器中的規則

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->
