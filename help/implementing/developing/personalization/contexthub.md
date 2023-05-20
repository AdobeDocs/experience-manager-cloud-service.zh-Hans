---
title: ContextHub
description: ContextHub是一種用於儲存、操控和呈現內容資料的架構
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub是一種用於儲存、操控和呈現內容資料的架構。 其主要功能是提供 [在模擬和切換各種角色時檢視內容資料。](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub允許您：

* [呈現、檢視、切換角色和模擬使用者體驗](#presentation) 使用內容資料製作頁面時。
* [保留內容資料](#persistence) 以資料層呈現方式在您的網站上。
* [管理區段](#segmentation) 所選前後關聯的。

使用者端Javascript API可讓您存取個人化內容的資料。

## 演示文稿 {#presentation}

此 [contexthub工具列](/help/sites-cloud/authoring/personalization/contexthub.md) 可讓行銷人員和作者檢視並操控存放區資料，以便在編寫頁面時模擬使用者體驗。 工具列由提供存取許可權的UI模組群組組成 [ContextHub存放區，](#persistence) 會將ContextHub資料儲存在使用者端上。

每個ContextHub UI模組都是預先定義模組型別的例項：

* ContextHub提供數種 [範例模組型別](sample-modules.md).
* 使用AEM主控台 [新增使用者介面模組](configuring-contexthub.md#adding-a-ui-module)，並至 [在UI模式下將其分組](configuring-contexthub.md#adding-a-ui-mode).
* 開發人員可以 [建立自訂模組型別](extending-contexthub.md#creating-contexthub-ui-module-types).

開發人員需要 [將ContextHub元件新增至頁面](configuring-contexthub.md).

## 持續性 {#persistence}

ContextHub會儲存持續存在於使用者端上的內容資料。 ContextHub Javascript API可讓您存取存放區，以視需要建立、更新和刪除資料。 因此，ContextHub代表頁面上的資料層。

每個ContextHub存放區都是預先定義存放區型別的例項：

* ContextHub提供數種 [範例存放區型別](sample-stores.md).
* 使用AEM主控台 [建立存放區](configuring-contexthub.md#creating-a-contexthub-store).
* 開發人員可以 [建立自訂商店型別](extending-contexthub.md#creating-custom-store-candidates).
* 開發人員可以 [存取存放區資料](adding-contexthub.md#interacting-with-contexthub-stores) 透過Javascript。

## 分段 {#segmentation}

ContextHub包含區段引擎，可管理區段並決定針對目前內容解析哪些區段。 已定義數個區段。 您可以使用Javascript API來 [決定已解析的區段](adding-contexthub.md#determining-resolved-contexthub-segments).
