---
title: 如何設定重新導向頁面？
description: 瞭解如何將使用者重新導向至表單作者可在建立表單時設定的網頁。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 設定重新導向頁面 {#configuring-redirect-page}

表單作者可為每個表單設定一個頁面，表單使用者在提交表單後即重新導向至該頁面。

1. 在編輯模式中，選取元件，然後按一下 ![欄位層級](assets/select_parent_icon.svg) > **[!UICONTROL 最適化表單容器]**，然後按一下 ![cmppr](assets/configure-icon.svg).

1. 在側邊欄中，按一下 **[!UICONTROL 提交]**.

1. 在下方提供重新導向頁面的URL **[!UICONTROL 重新導向URL/路徑]** 在 **[!UICONTROL 提交]** 區段。
1. 或者，您可以在「送出動作」下，針對「送出至REST端點」動作，設定要傳遞至重新導向頁面的引數。

   ![重新導向頁面設定](assets/redirect-url.png)

   重新導向頁面設定

表單作者可以使用以下傳遞至感謝頁面的引數。 針對所有可用的「提交」動作， `status` 和 `owner` 引數已傳遞。 除了這兩個引數外，系統還會為下列「提交動作」傳遞其他引數：

* **[!UICONTROL 提交至REST端點]**：傳遞為欄位內與引數對應新增的引數。 `status` 和 `owner` 此提交動作中未傳遞引數。 如需詳細資訊，請參閱 [設定提交至REST端點提交動作](configuring-submit-actions.md).
