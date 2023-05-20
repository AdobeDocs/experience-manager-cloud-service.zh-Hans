---
title: 在 Dynamic Media 中激活热链接保护
description: 瞭解如何在Dynamic Media中啟用直接連結保護。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%

---

# 在 Dynamic Media 中激活热链接保护 {#activating-hotlink-protection-in-dynamic-media}

熱連結是指第三方網站使用HTML程式碼顯示您網站中的影像時。 每次要求圖片時，他們都會使用您的頻寬，因為訪客的瀏覽器會直接從您的伺服器存取圖片。 直接連結 *保護* 是防止其他網站直接連結至您網頁上的圖片、CSS或JavaScript的方法。 這種遮蔽有助於減少Dynamic Media帳戶下不必要的頻寬使用量。

[Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=Experience+Manager#home) 可以在CDN層級設定反向連結篩選器。 這麼做可確保Dynamic Media內容僅供網域許可網站清單上的網站使用。

>[!NOTE]
>
>此功能需要您使用Adobe Experience Manager Dynamic Media隨附的現成可用CDN。 此功能不支援任何其他自訂CDN。 若要啟用快速連結保護，管理員必須建立支援票證以請求對您的Dynamic Media帳戶進行設定變更。 啟用熱連結保護不需額外付費。
