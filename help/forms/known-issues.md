---
title: 已知問題和限制
description: 的已知問題和限制  [!DNL AEM Forms] as a Cloud Service環境
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 94825e3b60d970fec5bf696d932ca66bb83fd2f3
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 11%

---

# 已知問題和限制 {#known-issues-and-limitations}

開始使用之前 [!DNL AEM Forms] as a Cloud Service，請檢閱下列已知問題和限制：

## 已知问题 {#known-issues}

* 在進一步通知之前，請勿新增和執行從發佈執行個體提交最適化表單的測試至在作者執行個體上執行的AEM Workflow。

* 匯入使用範本的最適化表單時，該範本包含 **[!UICONTROL 儲存]** 按鈕， **[!UICONTROL 儲存]** 即使按鈕從對應的範本中移除，按鈕仍會繼續顯示在調適型表單中。 移除 **[!UICONTROL 儲存]** 最適化Forms中的按鈕。 請留意發行說明，瞭解Forms入口網站的可用性並儲存為草稿功能，以還原和使用按鈕。

* 此 **[!UICONTROL 設定變數]** AEM工作流程步驟不支援型別陣列清單的變數。 您可以使用程式步驟來設定型別陣列清單的變數。

* 當您從Apple iOS裝置提交包含標準HTML上傳欄位的最適化表單時，不會傳送檔案內容，而在另一端會收到0位元組檔案。 此問題間歇性地發生，且只會在使用同步提交時發生。 這是 [已知問題](https://feedbackassistant.apple.com/feedback/9117687) 在Apple iOS中。

* 從Apple iOS裝置提交包含標準HTML上傳欄位的表單時，有時不會傳送檔案內容，而在另一端會收到0位元組檔案。 這是Apple iOS中的已知問題。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* AEM Formsas a Cloud Service不會為XDP和JSON結構描述檔案產生縮圖。 此服務會顯示預設圖示來取代縮圖。

   ![Forms縮圖已知問題](/help/forms/assets/forms-tumbnail-known-issue.png)


## 限制 {#limitations}

* 对基于 XFA 的自适应表单的支持并非现成可用。如果您需要使用基于 XFA 的自适应表单，请联系 Adobe 支持部门并提供您用例的详细信息和具体要求。

