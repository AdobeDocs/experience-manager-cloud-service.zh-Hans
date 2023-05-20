---
title: Screens as a Cloud Service 常见问题解答
description: 本頁說明Screensas a Cloud Service常見問答。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 02c9cbff56399ea2ca1baad7d2289d5d4c17c1c5
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 2%

---

# Screens as a Cloud Service 常见问题解答 {#screens-cloud-faqs}

以下章節提供與Screensas a Cloud Service專案相關的常見問題(FAQ)解答。

## 如果AEM Screens Player指向Screensas a Cloud Service時沒有挑選具有/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css格式的自訂clientlibs，怎麼辦？

AEMas a Cloud Service會在每次部署時變更長快取金鑰。 AEM Screens會在修改內容時產生離線快取，而不是在Cloud Manager執行部署時產生。 資訊清單中的這些長快取金鑰無效，因此播放器無法下載這些金鑰 *clientlibs*.

使用 `longCacheKey="none"` 在您的 `clientlib` 資料夾會完全移除這些專案的長快取金鑰 *clientlibs*.


## 如果離線資訊清單未依預期包含所有資源，我們該怎麼做？ {#offline-manifest}

離線快取產生方式： **bulk-offline-update-screens-service** 服務使用者。 某些路徑，無法由存取 `bulk-offline-update-screens-service`，導致離線資訊清單中缺少內容。

在您的程式碼中， `ui.config or ui.apps`，在設定資料夾中建立OSGi設定，包含以下內容，並將檔案名稱命名為 `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## 在AEM Screensas a Cloud Service頻道中無縫轉譯影像時，建議使用哪些影像格式？{#screens-cloud-image-format}

建議在格式中使用影像 `.png` 和 `.jpeg` 在AEM Screensas a Cloud Service頻道中，獲得最佳的數位看板體驗。
格式的影像 `*.tif` （標籤影像檔案格式）在AEM Screensas a Cloud Service中不受支援。 如果管道有此格式的影像，那麼在播放器端，將不會轉譯影像。

## 如果處於開發人員模式（線上）的管道未在AEM Screens Player上呈現，怎麼辦？{#screens-cloud-online-channel-blank-iframe}

建議您運用AEM Screens快取功能，但如果您需要在開發人員模式下執行頻道，而AEM Screens Player顯示空白畫面，請檢查您的Player開發人員工具，並尋找 `X-Frame-Options` 或 `frame-ancestors` 錯誤。 解決方法是將Dispatcher設定為允許內容在iFrame中執行。 通常以下設定將可運作：

```
Header set Content-Security-Policy "frame-ancestors ‘self’ file: localhost:*;"
```

## 註冊代碼限制的用法為何？

依據最佳做法的要求，您可以限制註冊代碼的使用方式。 如果註冊碼遭到破壞，但限製為100個註冊，則攻擊者最多只能註冊該數字，但不能註冊更多。 建立註冊代碼並註冊部分客戶播放器後，您隨時都可以更新使用量限制。 如果客戶觀察到特定註冊代碼的不尋常註冊活動，他們可以在調查時即時降低限制，如果這是誤報，還可以增加數字，而不會影響已註冊的玩家。
