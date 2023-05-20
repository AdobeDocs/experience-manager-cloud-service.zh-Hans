---
title: 回應式設計
description: 透過回應式設計，能以多種方向在多種裝置上有效顯示相同的體驗
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# 回應式設計 {#responsive-design}

設計您的體驗，以使其適應顯示體驗的使用者端檢視區。 透過回應式設計，相同的頁面可雙向有效顯示在多個裝置上。 下圖示範頁面可回應檢視區大小變更的一些方式：

* 版面：對較小的檢視區使用單欄版面，對較大的檢視區使用多欄版面。
* 文字大小：在較大的檢視區中使用較大的文字大小（如標題）。
* 內容：在較小裝置上顯示時，僅包含最重要的內容。
* 導覽：提供裝置特定工具來存取其他頁面。
* 影像：根據視窗尺寸提供適合使用者端檢視區的影像轉譯。

![回應式設計範例](assets/responsive-example.png)

開發可產生HTML5的Adobe Experience Manager (AEM)應用程式，以調整多個視窗大小和方向。 例如，下列檢視區寬度範圍會與各種裝置型別和方向相對應

* 最大寬度480畫素（手機、縱向）
* 最大寬度767畫素（手機、橫向）
* 介於768畫素和979畫素之間的寬度（平板電腦，縱向）
* 寬度介於980畫素和1199畫素之間（平板電腦、橫向）
* 寬度1200px或更高（桌上型電腦）

如需實作回應式設計行為的相關資訊，請參閱下列主題：

* [媒體查詢](#using-media-queries)
* [流動格線](#developing-a-fluid-grid)
* [最適化影像](#using-adaptive-images)

在設計時，請使用 **模擬器** 工具列，以預覽各種熒幕大小的頁面。

## 開發之前 {#before-you-develop}

在開發支援網頁的AEM應用程式之前，您應該先做出數個設計決定。 例如，您需要具備下列資訊：

* 您定位的裝置
* 目標檢視區大小
* 每個目標檢視區大小的頁面配置

### 應用程式結構 {#application-structure}

典型的AEM應用程式結構支援所有回應式設計實作：

* 頁面元件位於下方 `/apps/<application_name>/components`
* 範本位於下方 `/apps/<application_name>/templates`

## 使用媒體查詢 {#using-media-queries}

媒體查詢可選擇性使用CSS樣式來轉譯頁面。 AEM開發工具和功能可讓您在應用程式中有效率地實作媒體查詢。

W3C群組提供 [媒體查詢](https://www.w3.org/TR/css3-mediaqueries/) 說明此CSS3功能和語法的建議。

### 建立CSS檔案 {#creating-the-css-file}

在CSS檔案中，根據您鎖定目標的裝置屬性定義媒體查詢。 下列實作策略可有效管理每個媒體查詢的樣式：

* 使用 [使用者端資料庫資料夾](clientlibs.md) 以定義在轉譯頁面時組裝的CSS。
* 在不同的CSS檔案中定義每個媒體查詢和相關聯的樣式。 使用代表媒體查詢之裝置功能的檔案名稱會很有用。
* 定義個別CSS檔案中所有裝置通用的樣式。
* 在Client Library資料夾的css.txt檔案中，依照組合的CSS檔案中的要求，對CSS檔案清單進行排序。

此 [wknd教學課程](develop-wknd-tutorial.md) 使用此策略來定義網站設計中的樣式。 WKND使用的CSS檔案位於 `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.
