---
title: 如何將內嵌樣式套用至最適化表單元件？
description: 您可以在最適化表單上套用自訂樣式，也可以在最適化表單的個別元件上套用內嵌CSS屬性。 瞭解如何將內嵌樣式套用至最適化表單元件。 使用將內嵌樣式套用至文字欄位元件的範例深入瞭解。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 25adabfb-ff19-4cb2-aef5-0a8086d2e552
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# 最適化表單元件的內嵌樣式 {#inline-styling-of-adaptive-form-components}

您可以透過以下方式指定樣式，定義最適化表單的整體外觀和樣式： [主題編輯器](themes.md). 此外，您也可以將內嵌CSS樣式套用至個別的最適化表單元件，並即時預覽變更。 內嵌樣式會覆寫主題中提供的樣式。

## 套用內嵌CSS屬性 {#apply-inline-css-properties}

若要將內嵌樣式新增至元件：

1. 在表單編輯器中開啟您的表單，然後將模式變更為樣式模式。 若要將模式變更為樣式模式，請在頁面工具列中，點選 ![畫佈下拉式清單](assets/Smock_ChevronDown.svg) > **[!UICONTROL 樣式]**.
1. 在頁面中選取元件，然後點選「編輯」按鈕 ![編輯按鈕](assets/edit.svg). 在側欄中開啟樣式屬性。

   您也可以從側欄中的表單階層樹狀結構中選取元件。 表單階層樹狀結構在側邊欄中可作為表單物件使用。

   在 [!UICONTROL 樣式] 模式，您會看到列在「表單物件」下的元件。 不過，側邊欄中的「表單物件」清單會列出欄位和面板等元件。 欄位和面板是可包含文字方塊和選項按鈕等元件的通用元件。

   從側欄選取元件時，您會看到列出所有子元件和所選元件的屬性。 您可以選取特定的子元件並設定其樣式。

1. 按一下側邊欄中的索引標籤以指定CSS屬性。 您可以指定屬性，例如：

   * [!UICONTROL Dimension與位置] （顯示設定、邊框間距、高度、寬度、邊界、位置、z索引、浮點數、清除、溢位）
   * [!UICONTROL 文字] （字型系列、粗細、顏色、大小、行高和對齊）
   * [!UICONTROL 背景] （影像和漸層，背景顏色）
   * [!UICONTROL 邊框] （寬度、樣式、顏色、半徑）
   * [!UICONTROL 效果] （陰影、不透明度）
   * [!UICONTROL 進階] （可讓您為元件編寫自訂CSS）

1. 同樣地，您也可以為元件的其他部分套用樣式，例如 [!UICONTROL Widget]， [!UICONTROL 註解]、和 [!UICONTROL 說明].
1. 點選 **[!UICONTROL 完成]** 確認變更或 **[!UICONTROL 取消]** 以捨棄變更。

## 範例：欄位元件的內嵌樣式 {#example-inline-styles-for-a-field-component}

下列影像說明套用內嵌樣式之前和之後的文字欄位。

![套用內嵌樣式之前的文字方塊元件](assets/no-style.png)

套用內嵌樣式屬性前的文字方塊元件

請注意套用下列CSS屬性後，文字方塊樣式所發生的變更，如下圖所示。

<table>
 <tbody>
  <tr>
   <td><p>选择器</p> </td>
   <td><p>CSS屬性</p> </td>
   <td><p>价值</p> </td>
   <td><p>效果</p> </td>
  </tr>
  <tr>
   <td><p>字段</p> </td>
   <td><p>邊框</p> </td>
   <td><p>邊框寬度=2px</p> <p>邊框樣式=實線</p> <p>邊框顏色=#1111</p> </td>
   <td><p>在欄位周圍建立黑色2px寬邊框</p> </td>
  </tr>
  <tr>
   <td><p>文本框</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>將背景顏色變更為CornflowerBlue (#6495ED)</p> <p>注意：您可以在值欄位中指定顏色名稱或其十六進位代碼。</p> </td>
  </tr>
  <tr>
   <td><p>标签</p> </td>
   <td><p>Dimension與位置&gt;寬度</p> </td>
   <td><p>100px</p> </td>
   <td><p>將標籤的寬度修正為100px</p> </td>
  </tr>
  <tr>
   <td>字段帮助图标</td>
   <td>文字&gt;字型色彩</td>
   <td>#2ECC40</td>
   <td>變更說明圖示面部的色彩。</td>
  </tr>
  <tr>
   <td><p>詳細說明</p> </td>
   <td><p>text-align</p> </td>
   <td><p>居中</p> </td>
   <td><p>將說明的詳細描述對齊中心</p> </td>
  </tr>
 </tbody>
</table>

![套用內嵌樣式後的文字方塊樣式](assets/applied-style.png)

套用內嵌樣式屬性後的文字方塊元件

依照上述步驟，您可以選取其他元件並設定其樣式，例如面板、提交按鈕和選項按鈕。

>[!NOTE]
>
>樣式屬性會因您選取的元件而異。

## 複製並貼上樣式 {#copy-paste-styles}

您也可以在最適化表單中，將樣式從一個元件複製並貼到另一個元件。 在 **[!UICONTROL 樣式]** 模式，點選元件並點選「複製」圖示 ![複製](assets/property-copy-icon.svg).

點選相同型別的其他元件，然後點選「貼上」圖示 ![複製](assets/Smock_Paste_18_N.svg) 貼上複製的樣式。 您也可以點選「清除樣式」圖示 ![複製](assets/clear-style-icon.svg) 以清除套用的樣式。

## 為元件的不同狀態設定樣式 {#set-styles-for-states}

您可以為元件型別的不同狀態設定樣式。 不同的狀態包括： [!UICONTROL 焦點]， [!UICONTROL 已停用]， [!UICONTROL 暫留]， [!UICONTROL 錯誤]， [!UICONTROL 成功]、和 [!UICONTROL 強制].

若要定義元件狀態的樣式：

1. 在 **[!UICONTROL 樣式]** 模式，點選元件並點選「編輯」圖示 ![編輯](assets/Smock_Edit_18_N.svg).

1. 使用選取元件的狀態 **[!UICONTROL 州]** 下拉式清單。

   ![選取狀態](assets/select-state.png)

1. 定義元件所選狀態的樣式，然後點選 ![儲存](assets/save_icon.svg) 以儲存屬性。

您也可以模擬成功和錯誤狀態。 點選「展開」圖示以檢視 **[!UICONTROL 模擬成功]** 和 **[!UICONTROL 模擬錯誤]** 選項。

![模擬狀態](assets/simulate-states.png)
