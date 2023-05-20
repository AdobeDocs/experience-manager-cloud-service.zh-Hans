---
title: AEMas a Cloud Service2022.9.0版中移轉工具的發行說明
description: AEMas a Cloud Service2022.9.0版中移轉工具的發行說明
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
source-git-commit: dd4515bdbba81dcec0868c3058c7745775cc80ff
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 10%

---

# AEMas a Cloud Service2022.9.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2022.9.0中移轉工具發行說明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.34的發行日期為2022年9月12日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可以偵測和報告客戶是否已新增自訂記錄器設定。 AEMas a Cloud Service不支援自訂記錄檔。 所有記錄檔都需要管道傳輸至 `error.log`
* BPA現在可以報告存在於客戶存放庫中的不同二進位MIME型別以及與其相關的計數。

### 错误修复 {#bug-fixes-bpa}

* 在單一模式下顯示大量發現時，BPA UI出現轉譯問題。 此问题已得到修复。
* BPA錯誤地報告了一些發現為與嚴重嚴重性不相容的變更。 此问题已得到修复。
