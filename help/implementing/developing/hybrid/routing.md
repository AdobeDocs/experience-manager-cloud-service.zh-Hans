---
title: SPA模型製程
description: 若為AEM中的單頁應用程式，則由應用程式負責路由。 本檔案說明路由機制、合約及可用的選項。
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# SPA模型製程{#spa-model-routing}

若為AEM中的單頁應用程式，則由應用程式負責路由。 本檔案說明路由機制、合約及可用的選項。

## 專案路由 {#project-routing}

應用程式擁有路由，然後由專案前端開發人員實作。 本檔案說明AEM伺服器傳回之模型的特定路由。 頁面模型資料結構會顯示基礎資源的URL。 前端專案可以使用任何提供路由功能的自訂或第三方資料庫。 一旦路由預期了模型的片段，就會呼叫 `PageModelManager.getData()` 可以建立函式。 當模型路由變更時，必須觸發事件，以警告聆聽程式庫（例如頁面編輯器）。

## 架构 {#architecture}

如需詳細說明，請參閱 [PageModelManager](blueprint.md#pagemodelmanager) SPA Blueprint檔案的區段。

## 模型路由器 {#modelrouter}

此 `ModelRouter`  — 啟用時 — 封裝HTML5 History API函式 `pushState` 和 `replaceState` 以確保預先擷取並存取模型的指定片段。 然後通知註冊的前端元件模型已被修改。

## 手動與自動模型製程 {#manual-vs-automatic-model-routing}

此 `ModelRouter` 自動擷取模型的片段。 但就像任何自動化工具一樣，它也有侷限性。 需要時 `ModelRouter` 可停用或設定為使用中繼屬性略過路徑(請參閱 [SPA頁面元件](page-component.md) 檔案)。 前端開發人員可透過請求 `PageModelManager` 若要使用載入模型的任何指定片段 `getData()` 函式。

>[!CAUTION]
>
>目前版本的 `ModelRouter` 僅支援使用指向Sling模型進入點的實際資源路徑的URL。 不支援使用虛名URL或別名。

## 路由合約 {#routing-contract}

目前的實作是根據SPA專案使用HTML5 History API路由傳送至不同應用程式頁面的假設。

### 配置 {#configuration}

此 `ModelRouter` 支援模型路由的概念，因為它會偵聽 `pushState` 和 `replaceState` 對預先擷取模型片段的呼叫。 在內部，它會觸發 `PageModelManager` 載入與指定URL對應的模型並觸發 `cq-pagemodel-route-changed` 其他模組可以監聽的事件。

依預設，此行為會自動啟用。 若要停用，SPA應呈現以下中繼屬性：

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

請注意，SPA的每個路由都應對應至AEM中可存取的資源(例如，「 `/content/mysite/mypage"`)從以下日期開始： `PageModelManager` 選取路由後，將自動嘗試載入對應的頁面模型。 不過，如有需要，SPA也可以定義路由的「封鎖清單」，該清單應被 `PageModelManager`：

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
