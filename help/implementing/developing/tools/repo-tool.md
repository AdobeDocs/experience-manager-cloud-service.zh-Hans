---
title: AEM Repo 工具
description: AEM Repo Tool是一種簡單的解決方案，可透過類似FTP的命令列，在本機檔案系統和AEM伺服器之間傳輸JCR內容。
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 2%

---

# AEM Repo 工具 {#aem-repo-tool}

AEM Repo Tool是一種簡單的解決方案，可透過類似FTP的命令列，在本機檔案系統和AEM伺服器之間傳輸JCR內容。 AEM Repo工具類似於 [Jackrabbit FileVault Maven外掛程式](https://jackrabbit.apache.org/filevault-package-maven-plugin)，但速度更快、相依性最低，且為簡單的bash指令碼。

此工具可簡化開發人員檔案的傳輸，並可整合至Eclipse和IntelliJ，讓開發更有效率。

## 概述 {#overview}

針對內的指定路徑 `jcr_root` 檔案系統上的FileVault結構，「AEM存放庫工具」會為整個子樹狀結構建立包含單一篩選器的套件，並將其推送到伺服器（類似FTP） `put`)，會從伺服器擷取( `get`)或比較兩者之間的差異( `status` 和 `diff`)。

此工具不支援多個篩選路徑或FileVault的 `filter.xml`.

>[!CAUTION]
>
>請注意，AEM Repo Tool一律會覆寫指定的整個檔案或目錄。

## 下載和檔案 {#download-and-documentation}

此 [AEM Repo Tool可透過此連結在GitHub上取得](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) 以及詳細的安裝和使用說明。

如果您想要下載AEM Repo工具的來源，請參閱下方連結的GitHub專案。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟工具專案](https://github.com/Adobe-Marketing-Cloud/tools)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
