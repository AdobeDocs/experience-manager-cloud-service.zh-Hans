---
title: 发布 Dynamic Media 资源
description: 瞭解如何發佈Dynamic Media資產。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---

# 发布 Dynamic Media 资源 {#publishing-dynamic-media-assets}

您可以選取已上傳的資產，然後選取「 」，發佈Dynamic Media資產 **[!UICONTROL 發佈]** 或 **[!UICONTROL 快速發佈]**. 發佈Dynamic Media資產後，您就可以透過URL或透過在頁面上內嵌程式碼的方式將其納入網頁中。

您也可以立即發佈您上傳的資產，無需任何使用者介入。 或者，您可以選擇發佈這些資產。 另請參閱 [設定Dynamic Media](config-dm.md). 或者，您可以選擇將資產發佈到Dynamic Media或Adobe Experience Manager，兩者互相排斥，使用 **[!UICONTROL 選擇性發佈]** 在資料夾層級。 另請參閱 [在Dynamic Media中使用選擇性發佈](/help/assets/dynamic-media/selective-publishing.md).

在 **[!UICONTROL 卡片檢視]**，資產名稱的正下方及日期和時間左側會出現一個小地球圖示，指出資產已發佈。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

>[!NOTE]
>
>如果資產已發佈，然後您將資產移動到另一個資料夾，並從其新位置重新發佈，則仍然可以使用原始已發佈的資產位置，以及新重新發佈的資產。 然而，原始發佈的資產會被「遺失」給Experience Manager，且無法取消發佈。 因此，最佳做法是先取消發佈資產，然後再將其移至其他資料夾。

如果您打算在編碼視訊資產後立即發佈，請務必完成編碼。 當視訊編碼時，系統會告知您視訊處理工作流程正在進行中。 視訊編碼完成後，您可以預覽視訊轉譯。 到那時，您可以安全地發佈影片，而不會發生任何發佈錯誤。

另請參閱 [將URL連結至您的網頁應用程式](linking-urls-to-yourwebapplication.md).

另請參閱 [將Dynamic Media視訊檢視器或影像檢視器內嵌在網頁上](embed-code.md).

>[!NOTE]
>
>* 必須發佈資產才能使用URL。 如果資產未發佈，將無法將URL複製並貼到網頁瀏覽器。
>* 影像預設集和檢視器預設集必須啟動並發佈，才能即時傳送。
>


如需發佈集合或資產的詳細資訊，請參閱 [發佈資產](/help/assets/manage-digital-assets.md).

## Dynamic Media資產的HTTP/2傳送 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援透過HTTP/2傳送所有Dynamic Media內容（影像和視訊）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可整合至任何接受託管資產的應用程式。 然後會透過HTTP/2通訊協定傳遞該已發佈的資產。 此傳遞方法可改善瀏覽器和伺服器的通訊方式，讓您的所有Dynamic Media資產獲得更好的回應和載入時間。

另請參閱 [HTTP/2內容傳送常見問題](/help/assets/dynamic-media/http2faq.md).

<!--this md file used to reside under sites-administering-->
