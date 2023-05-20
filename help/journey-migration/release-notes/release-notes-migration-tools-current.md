---
title: AEMas a Cloud Service2023.03.0版中移轉工具的發行說明
description: AEMas a Cloud Service2022.03.0版中移轉工具的發行說明
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: b2681113f5565e4f63c76abeaf46d5f4b1a8a8ea
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 10%

---

# AEMas a Cloud Service2023.03.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2022.03.0中移轉工具發行說明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.40 的发布日期是 2023 年 3 月 03 日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可以偵測並報告衝突的節點 — 具有相同的節點 `jcr:uuid`. 這類發現會被標籤為嚴重，因為在將內容移至AEMas a Cloud Service時，可能會導致內容擷取失敗。
* BPA現在可以偵測及報告事件接聽程式的使用情況。 建議在移至AEMas a Cloud Service時，將此型別的事件處理機制重構為Sling工作。

### 错误修复 {#bug-fixes-bpa}

* BPA回報的誤報為 `grouprendercondition`. 此问题已得到修复。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

內容轉移工具v2.0.16的發行日期為2022年3月8日。

### 新增功能 {#what-is-new-ctt}

* 使用者對應已經過簡化，並整合至內容擷取步驟。 不需要任何設定，預設情況下，當使用者起始內容擷取時，會自動完成使用者對應。 使用者可以選擇視需要停用使用者對應。 瞭解更多 [此處。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html?lang=en#user-mapping-detail)
* 使用進行的預先複製步驟 [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 已與內容轉移工具整合，以大幅加快內容擷取速度。 安裝此版本的CTT時，會自動設定並安裝Precopy。 根據預設，在開始提取時，將會對大於200GB的移轉集自動執行預先複製。 使用者可以選擇視需要將其停用。 瞭解更多 [此處。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)
* CTT現在可用於Windows伺服器。

### 错误修复 {#bug-fixes-ctt}

* 多項錯誤修正，以改善內容擷取恢復能力。
