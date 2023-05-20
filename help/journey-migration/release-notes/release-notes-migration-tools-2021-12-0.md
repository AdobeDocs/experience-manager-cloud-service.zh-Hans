---
title: AEMas a Cloud Service2021.12.0版中移轉工具的發行說明
description: AEMas a Cloud Service2021.12.0版中移轉工具的發行說明
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 46%

---

# AEMas a Cloud Service2021.12.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2021.12.0中移轉工具發行說明。

>[!NOTE]
>要查看 Adobe Experience Manager as a Cloud Service 的当前发行说明，请单击[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=zh-Hans)。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.22 的发布日期是 2021 年 12 月 1 日。

### 新增功能 {#what-is-new-bpa}

* 能够检测和报告所使用的 ACS Commons 版本。
* 能够检测和报告一个组中用户和子组的数量。
* 能够检测和报告 MongoDB 中超过 16MB 的节点属性值。

### 错误修复 {#bug-fixes-bpa}

* 已改进对 Foundation 组件的检测来减少误报。
* 对于 AEM Forms 客户，已修复有关 `EMAIL_PDF_SUBMIT_ACTION` 在 AEM as a Cloud Service 中不可用的 BPA 消息。


## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

內容轉移工具v1.7.10的發行日期為2021年12月8日。

### 新增功能 {#what-is-new-ctt}

* 切換新增到內容轉移工具中的擷取階段，以允許使用者停用 [預先複製](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 在內嵌期間。 為獲得最佳擷取速度，小型移轉集或在上次擷取後僅新增幾個blob時，應停用擷取期間的預先複製。
* 使用者對應已更新，使用改良的使用者管理API，一次可取得2000名使用者，大幅改善效能。
