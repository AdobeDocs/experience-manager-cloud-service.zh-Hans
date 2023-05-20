---
title: XDP型最適化Forms中的XFA支援
seo-title: XFA support in XDP-based Adaptive Forms
description: 列出Adaptive Forms中支援的XFA事件、屬性、指令碼和驗證。
seo-description: Lists supported XFA events, properties, scripts, and validation in Adaptive Forms.
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 5%

---


# XDP型最適化Forms中的XFA支援{#xfa-support-in-xdp-based-adaptive-forms}

## 简介 {#introduction}

Adaptive Forms可支援XDP檔案中定義的多種XFA事件、屬性、指令碼和驗證，包括：

* 執行在XDP檔案中的事件上定義的指令碼。
* 擷取XDP檔案中欄位的預設值和行為屬性。
* 執行XDP檔案中定義的驗證指令碼。

根據XDP檔案建立最適化表單時，屬性、事件和驗證會自動填入表單編寫UI中。 不過，表單作者可以覆寫其中某些元素來建立替代體驗。

本文列出Adaptive Forms中支援的XFA事件、屬性和遵循的驗證，並說明如何在Adaptive Forms中覆寫這些事件、屬性和驗證。

## 最適化Forms中支援的XFA元素及其對應 {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### 字段 {#fields}

使用XDP檔案建立調適型表單時，您可以將XFA欄位拖放至調適型表單上。 下表列出XFA欄位如何對應至最適化表單欄位。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA欄位或容器</strong></p> </td>
   <td><p><strong>對應的最適化表單元件</strong></p> </td>
  </tr>
  <tr>
   <td><p>按钮 </p> </td>
   <td><p>按钮</p> </td>
  </tr>
  <tr>
   <td><p>复选框 </p> </td>
   <td><p>复选框</p> </td>
  </tr>
  <tr>
   <td><p>清單方塊 </p> </td>
   <td><p>下拉列表</p> </td>
  </tr>
  <tr>
   <td><p>日期/時間欄位 </p> </td>
   <td><p>日期选取器</p> </td>
  </tr>
  <tr>
   <td><p>手寫簽名</p> </td>
   <td><p>潦草签名</p> </td>
  </tr>
  <tr>
   <td><p>數值欄位 </p> </td>
   <td><p>数值框</p> </td>
  </tr>
  <tr>
   <td><p>小數欄位</p> </td>
   <td><p>数值框</p> </td>
  </tr>
  <tr>
   <td><p>文本字段 </p> </td>
   <td><p>文本框</p> </td>
  </tr>
  <tr>
   <td><p>密码字段 </p> </td>
   <td><p>密码框</p> </td>
  </tr>
  <tr>
   <td><p>图像</p> </td>
   <td><p>图像</p> </td>
  </tr>
  <tr>
   <td><p>文本</p> </td>
   <td><p>文本</p> </td>
  </tr>
  <tr>
   <td><p>子表單 </p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>區域（群組）</p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>子表單集 </p> </td>
   <td><p>面板</p> </td>
  </tr>
 </tbody>
</table>

### 属性 {#properties}

下表擷取XDP檔案中定義的各種XFA指令碼在Adaptive Forms中的行為。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA元件屬性</strong></p> </td>
   <td><p><strong>Adaptive Forms中的對應行為</strong></p> </td>
  </tr>
  <tr>
   <td><p>somexpression </p> </td>
   <td><p>對應至最適化表單中的繫結參考(bindRef)屬性。</p> </td>
  </tr>
  <tr>
   <td><p>是否存在 </p> </td>
   <td><p>對應至最適化表單中的可見屬性。 您可以使用「可見性」運算式來覆寫它。</p> </td>
  </tr>
  <tr>
   <td><p>存取 </p> </td>
   <td><p>對應至最適化表單中已啟用的屬性。 您可以使用Access運算式來覆寫它。</p> </td>
  </tr>
  <tr>
   <td><p>協助工具：角色 </p> </td>
   <td><p>對應至最適化表單中的角色屬性。</p> </td>
  </tr>
  <tr>
   <td><p>協助工具： speakPriority </p> </td>
   <td><p>對應至最適化表單中的speakPriority屬性。</p> </td>
  </tr>
  <tr>
   <td><p>協助工具： speakText</p> </td>
   <td><p>對應至最適化表單中的自訂協助工具文字。</p> </td>
  </tr>
  <tr>
   <td><p>協助工具：工具提示 </p> </td>
   <td><p>對應至最適化表單中的簡短說明屬性。</p> </td>
  </tr>
  <tr>
   <td><p>註解<em> （所有欄位型別）</em></p> </td>
   <td><p>對應至最適化表單中的Title屬性。</p> </td>
  </tr>
  <tr>
   <td><p>displayformat<em> （所有欄位型別）</em></p> </td>
   <td><p>對應至最適化表單的顯示模式。</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> （所有欄位型別）</em></p> </td>
   <td><p>對應至最適化表單中的值屬性。</p> </td>
  </tr>
  <tr>
   <td><p>個專案<em> （清單方塊、核取方塊）</em></p> </td>
   <td><p>對應至最適化表單中的options屬性。 您可以使用「選項」運算式來覆寫它。</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> （文字欄位）</em></p> </td>
   <td><p>對應至最適化表單中允許的最大字元數屬性。</p> </td>
  </tr>
  <tr>
   <td><p>多行<em> （文字欄位）</em></p> </td>
   <td><p>對應至最適化表單中的允許多行屬性。</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> （數值欄位，小數欄位）</em></p> </td>
   <td><p>對應至最適化表單中的Frac數字屬性。</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> （數值欄位，小數欄位）</em></p> </td>
   <td><p>對應至最適化表單中的前導位數屬性。</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> （清單方塊）</em></p> </td>
   <td><p>對應至允許最適化表單中的多選屬性。</p> </td>
  </tr>
 </tbody>
</table>

### 脚本 {#scripts}

下表擷取XDP檔案中定義的各種XFA指令碼在Adaptive Forms中的行為。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA指令碼事件</strong></p> </td>
   <td><p><strong>Adaptive Forms中的對應行為</strong></p> </td>
  </tr>
  <tr>
   <td><p>初始化 </p> </td>
   <td><p>此指令碼在執行階段執行，且無法在最適化表單中覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>計算</p> </td>
   <td><p>對應至最適化表單中的計算運算式。</p> </td>
  </tr>
  <tr>
   <td><p>驗證 </p> </td>
   <td><p>對應至最適化表單中的驗證運算式。</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>此指令碼在執行階段執行，且無法在最適化表單中覆寫。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>退出 </p> </td>
   <td><p>此指令碼在執行階段執行，且無法在最適化表單中覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>按一下（按鈕欄位）</p> </td>
   <td><p>對應至按鈕的Click運算式。</p> </td>
  </tr>
  <tr>
   <td><p>支援伺服器端指令碼</p> </td>
   <td><p>此指令碼在執行階段執行，且無法在最適化表單中覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>支援網站服務</p> </td>
   <td><p>此指令碼在執行階段執行，且無法在最適化表單中覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>變更（塗鴉欄位、選項按鈕、核取方塊）</p> </td>
   <td><p>此指令碼在執行階段執行，且無法在最適化表單中覆寫。</p> </td>
  </tr>
 </tbody>
</table>

### 驗證 {#validations}

下表擷取XFA驗證如何對應到Adaptive Forms中的驗證。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA驗證</strong></p> </td>
   <td><p><strong>最適化表單中的對應驗證</strong></p> </td>
  </tr>
  <tr>
   <td><p>驗證模式(formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>驗證模式訊息(formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>必要(nullTest )</p> </td>
   <td><p>強制 </p> </td>
  </tr>
  <tr>
   <td><p>空訊息(nullTestMessage) </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>驗證指令碼(scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>驗證指令碼訊息(scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您無法覆寫與XFA核取按鈕繫結的最適化表單選項按鈕和核取方塊群組的強制屬性。

