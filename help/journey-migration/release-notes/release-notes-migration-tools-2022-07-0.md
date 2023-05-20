---
title: AEMas a Cloud Service2022.7.0版中移轉工具的發行說明
description: AEMas a Cloud Service2022.7.0版中移轉工具的發行說明
feature: Release Information
exl-id: bc8f1a80-867e-423a-9c03-4a53b1ebc57c
source-git-commit: cc52dfac1e7495d6a792bc7525720695022db8eb
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 9%

---

# AEMas a Cloud Service2022.7.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2022.7.0中移轉工具發行說明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.30的發行日期為2022年7月27日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可以偵測和報告總計可移轉Lucene索引大小，也就是不包括Lucene索引總計 `/oak:index/lucene` 和 `/oak:index/damAssetLucene`.
* BPA中新增的新模式，可偵測及報告自訂i18n字典的使用情況。 AEMas a Cloud Service中不提供Translator.html，而自訂i18n字典需要透過Cloud Manager CI/CD管道從Git部署。

### 错误修复 {#bug-fixes-bpa}

* BPA報告缺少內容片段的原始轉譯。 由於內容片段沒有轉譯，因此現在會略過內容片段的這項檢查。
* BPA UI中缺少篩選ACS Commons發現的選項。 此问题已得到修复。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

內容轉移工具v2.0.12的發行日期為2022年7月19日。

### 新增功能 {#what-is-new-ctt}

* 透過LDAP登入的使用者現在可以在CTT中執行「檢查大小」和「使用者對應」功能。
* 為了協助在擷取期間偵錯SSL/TLS連線問題，使用者現在可以啟用SSL記錄。
* 為協助偵錯來源連線問題，現在當與Azure的連線失敗時，子網域名稱會列印在記錄中。
* 為協助偵錯預先複製期間的問題，現在會在預先複製失敗時，將AzCopy記錄檔附加至擷取記錄檔。
* 為避免過時的「檢查大小」結果，使用者只能在先前「檢查大小」完成後重新執行「檢查大小」。

### 错误修复 {#bug-fixes-ctt}

* 刪除並重新建立移轉集後出現先前的擷取記錄。 此问题已得到修复。
* 「檢視進度」動作按鈕不適用於狀態為「已停止」的移轉集。 此问题已得到修复。
* 具有過期擷取金鑰的移轉集無法使用刪除動作按鈕。 此问题已得到修复。
* 已修正多個UI錯誤。

## Cloud Acceleration Manager {#cam-release}

### 发布日期 {#release-date-cam}

Cloud Acceleration Manager的發行日期為2022年7月15日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在可讓使用者手動擷取移轉權杖，以便在自動擷取失敗時開始內嵌。 如果客戶已設定封鎖CAM的IP允許清單，或如果非管理員使用者嘗試開始內嵌，則自動擷取可能會失敗。 請參閱 [疑難排除](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) 以取得詳細資訊。
* 「移轉複雜性」頁面上的長表格現在可以摺疊，以方便使用。
